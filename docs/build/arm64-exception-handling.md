---
title: ARM64 异常处理
description: 描述 ARM64 上的 Windows 使用的异常处理约定和数据。
ms.date: 11/19/2018
ms.openlocfilehash: b1137e4e46e1127ea5452e93e1d8d9452ba0ea4d
ms.sourcegitcommit: dc77cf3b5b644d8e2adf595540b98194ab95c6e1
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377263"
---
# <a name="arm64-exception-handling"></a>ARM64 异常处理

针对异步硬件生成的异常和同步软件生成的异常，ARM64 上的 Windows 将使用相同的结构化异常处理机制。 将通过使用语言帮助器函数，基于 Windows 结构化异常处理来生成特定于语言的异常处理程序。 本文档描述了 ARM64 上的 Windows 中的异常处理以及由 Microsoft ARM 汇编程序和 MSVC 编译器生成的代码所使用的语言帮助程序。

## <a name="goals-and-motivation"></a>目标和动机

异常展开数据约定和此描述旨在：

1. 提供足够的描述以允许在所有情况下都可进行展开而无需代码探测。

   - 分析代码需要对代码进行分页。 这可在某些十分有用的情况下（跟踪、采样、调试）阻止展开。

   - 分析代码非常复杂；编译器必须小心，仅生成展开器可以解码的指令。

   - 如果无法使用展开代码来完整描述展开，则在某些情况下，必须回退到指令解码。 这会增加总体复杂性，理想情况下应避免。

1. 支持在 prolog 中间和 epilog 中间展开。

   - 展开在 Windows 中不仅用于异常处理。 至关重要的是，即使是在 prolog 或 epilog 代码序列中间，代码也可以准确地展开。

1. 占用最少量的空间。

   - 展开代码不得进行聚合以显著增加二进制文件大小。

   - 由于展开代码可能会在内存中锁定，因此，较小的内存占用可确保每个加载的二进制文件的开销最小。

## <a name="assumptions"></a>假设

在异常处理描述中进行了以下假设：

1. Prolog 和 epilog 往往互为镜像。 利用这种常见特性，描述展开所需的元数据大小可以大幅降低。 在函数主体中，无论是撤销 prolog 操作，还是以前进的方式执行 epilog 操作都不重要。 这两种操作应产生完全相同的结果。

1. 总体上，函数往往相对较小。 多个空间优化依赖于此事实来实现最高效的数据打包。

1. epilog 中没有条件代码。

1. 专用帧指针寄存器：如果 sp 在 prolog 中保存在另一个寄存器 (x29) 中，则该寄存器会在整个函数中保持不变。 这意味着，可以随时恢复原始 sp。

1. 除非 sp 保存在另一个寄存器中，否则堆栈指针的所有操作都必须严格在 prolog 和 epilog 内执行。

1. 堆栈帧布局按下一部分所述方式进行组织。

## <a name="arm64-stack-frame-layout"></a>ARM64 堆栈帧布局

![堆栈帧布局](media/arm64-exception-handling-stack-frame.png "堆栈帧布局")

对于帧链接函数，fp 和 lr 对可以保存在局部变量区域中的任意位置保存，具体取决于优化注意事项。 目标是最大程度地提高单个指令基于帧指针 (x29) 或堆栈指针 (sp) 可以访问的局部变量数。 但是，对于 `alloca` 函数，它必须进行链接，并且 x29 必须指向堆栈底部。 为了实现更好的寄存器对寻址模式覆盖范围，非易失性寄存器保存区位于本地区域堆栈顶部。 以下示例演示几个最高效的 prolog 序列。 为清楚起见和实现更好的缓存区域，在所有规范 prolog 中存储被调用方保存的寄存器的顺序都是“递增”顺序。 下面的 `#framesz` 表示整个堆栈的大小（不包括 alloca 区域）。 `#localsz` 和 `#outsz` 分别表示本地区域大小（包括 \<x29, lr> 对的保存区域）和传出参数大小。

1. 链式，#localsz \<= 512

    ```asm
        stp    x19,x20,[sp,#-96]!        // pre-indexed, save in 1st FP/INT pair
        stp    d8,d9,[sp,#16]            // save in FP regs (optional)
        stp    x0,x1,[sp,#32]            // home params (optional)
        stp    x2,x3,[sp,#48]
        stp    x4,x5,[sp,#64]
        stp    x6,x7,[sp,#72]
        stp    x29,lr,[sp,#-localsz]!   // save <x29,lr> at bottom of local area
        mov    x29,sp                   // x29 points to bottom of local
        sub    sp,sp,#outsz             // (optional for #outsz != 0)
    ```

1. 链式，#localsz > 512

    ```asm
        stp    x19,x20,[sp,#-96]!        // pre-indexed, save in 1st FP/INT pair
        stp    d8,d9,[sp,#16]            // save in FP regs (optional)
        stp    x0,x1,[sp,#32]            // home params (optional)
        stp    x2,x3,[sp,#48]
        stp    x4,x5,[sp,#64]
        stp    x6,x7,[sp,#72]
        sub    sp,sp,#(localsz+outsz)   // allocate remaining frame
        stp    x29,lr,[sp,#outsz]       // save <x29,lr> at bottom of local area
        add    x29,sp,#outsz            // setup x29 points to bottom of local area
    ```

1. 非链式，叶函数（lr 未保存）

    ```asm
        stp    x19,x20,[sp,#-80]!       // pre-indexed, save in 1st FP/INT reg-pair
        stp    x21,x22,[sp,#16]
        str    x23,[sp,#32]
        stp    d8,d9,[sp,#40]           // save FP regs (optional)
        stp    d10,d11,[sp,#56]
        sub    sp,sp,#(framesz-80)      // allocate the remaining local area
    ```

   所有局部变量都基于 SP 进行访问。 \<x29,lr> 指向前一帧。 对于帧大小 \<= 512，如果寄存器保存的区域移动到堆栈底部，则可以优化掉“sub sp, ...”。 缺点是它与上面的其他布局不一致，并且保存的寄存器会占用对寄存器以及索引前和索引后偏移寻址模式的范围。

1. 非链式，非叶函数（lr 保存在 Int 保存区域中）

    ```asm
        stp    x19,x20,[sp,#-80]!       // pre-indexed, save in 1st FP/INT reg-pair
        stp    x21,x22,[sp,#16]         // ...
        stp    x23,lr,[sp,#32]          // save last Int reg and lr
        stp    d8,d9,[sp,#48]           // save FP reg-pair (optional)
        stp    d10,d11,[sp,#64]         // ...
        sub    sp,sp,#(framesz-80)      // allocate the remaining local area
    ```

   或者，对于偶数个已保存 Int 寄存器，

    ```asm
        stp    x19,x20,[sp,#-80]!       // pre-indexed, save in 1st FP/INT reg-pair
        stp    x21,x22,[sp,#16]         // ...
        str    lr,[sp,#32]              // save lr
        stp    d8,d9,[sp,#40]           // save FP reg-pair (optional)
        stp    d10,d11,[sp,#56]         // ...
        sub    sp,sp,#(framesz-80)      // allocate the remaining local area
    ```

   仅保存 x19：

    ```asm
        sub    sp,sp,#16                // reg save area allocation*
        stp    x19,lr,[sp]              // save x19, lr
        sub    sp,sp,#(framesz-16)      // allocate the remaining local area
    ```

   \* 寄存器保存区域分配不会折叠到 stp 中，因为索引前寄存器 lr stp 无法使用展开代码进行表示。

   所有局部变量都基于 SP 进行访问。 \<x29> 指向前一帧。

1. 链式，#framesz \<= 512，#outsz = 0

    ```asm
        stp    x29,lr,[sp,#-framesz]!       // pre-indexed, save <x29,lr>
        mov    x29,sp                       // x29 points to bottom of stack
        stp    x19,x20,[sp,#(framesz-32)]   // save INT pair
        stp    d8,d9,[sp,#(framesz-16)]     // save FP pair
    ```

   与上面的第一个 prolog 示例相比，此处的优点是所有寄存器保存指令都在仅一个堆栈分配指令之后即可执行。 这意味着对 sp 不会有阻止指令级并行的任何反依赖关系。

1. 链式，帧大小 > 512（对于不带 alloca 的函数是可选的）

    ```asm
        stp    x29,lr,[sp,#-80]!            // pre-indexed, save <x29,lr>
        stp    x19,x20,[sp,#16]             // save in INT regs
        stp    x21,x22,[sp,#32]             // ...
        stp    d8,d9,[sp,#48]               // save in FP regs
        stp    d10,d11,[sp,#64]
        mov    x29,sp                       // x29 points to top of local area
        sub    sp,sp,#(framesz-80)          // allocate the remaining local area
    ```

   出于优化目的，x29 可以置于本地区域中的任意位置，以便为“寄存器对”和索引前/索引后偏移寻址模式提供更好的覆盖范围。 帧指针下的局部变量可以基于 SP 进行访问。

1. 链式，帧大小 > 4K，带有或没有 alloca()，

    ```asm
        stp    x29,lr,[sp,#-80]!            // pre-indexed, save <x29,lr>
        stp    x19,x20,[sp,#16]             // save in INT regs
        stp    x21,x22,[sp,#32]             // ...
        stp    d8,d9,[sp,#48]               // save in FP regs
        stp    d10,d11,[sp,#64]
        mov    x29,sp                       // x29 points to top of local area
        mov    x15,#(framesz/16)
        bl     __chkstk
        sub    sp,sp,x15,lsl#4              // allocate remaining frame
                                            // end of prolog
        ...
        sub    sp,sp,#alloca                // more alloca() in body
        ...
                                            // beginning of epilog
        mov    sp,x29                       // sp points to top of local area
        ldp    d10,d11,[sp,#64]
        ...
        ldp    x29,lr,[sp],#80              // post-indexed, reload <x29,lr>
    ```

## <a name="arm64-exception-handling-information"></a>ARM64 异常处理信息

### <a name="pdata-records"></a>.pdata 记录

.pdata 记录是由固定长度项组成的有序数组，这些项描述了 PE 二进制文件中每个堆栈操作函数。 短语“堆栈操作”非常重要：无需任何本地存储、无需保存/还原非易失性寄存器、无需 .pdata 记录的叶函数。 应显式省略这些记录以节省空间。 从这些函数之一进行展开可能会直接从 LR 获取返回地址，以向上移动到调用方。

ARM64 的每个 .pdata 记录的长度是 8 字节。 每个记录的一般格式是将函数起始位置的 32 位 RVA 放置在第一个字中，后跟第二个字，该字包含指向长度可变的 .xdata 块的指针，或包含描述规范函数展开序列的已打包字。

![.pdata 记录布局](media/arm64-exception-handling-pdata-record.png ".pdata 记录布局")

字段如下所示：

- 函数起始 RVA  为函数起始位置的 32 位 RVA。

- 标志  是指示如何解释第二个 .pdata 字的剩余 30 位的一个 2 位字段。 如果标志为 0，则剩余的位将形成异常信息 RVA（最低两位隐式为 0）。 如果标志  非零，则剩余的位将形成已打包的展开数据  结构。

- 异常信息 RVA  是 .xdata 部分中存储的长度可变的异常信息结构的地址。 此数据必须是对齐的 4 字节。

- 已打包的展开数据是对从函数展开时所需操作的概括说明，采用规范格式。 在这种情况下，不需要任何 .xdata 记录。

### <a name="xdata-records"></a>.xdata 记录

当已打包的展开格式不足以描述函数的展开时，必须创建长度可变的 .xdata 记录。 该记录的地址存储在 .pdata 记录的第二个字中。 .xdata 的格式是已打包的长度可变的字集：

![.xdata 记录布局](media/arm64-exception-handling-xdata-record.png ".xdata 记录布局")

此数据分为四个部分：

1. 1 个字或 2 个字的标头，描述结构的总大小并提供密钥函数数据。 第二个字仅在 Epilog 计数和代码字字段同时设置为 0 时存在。 标头包含以下位域：

   a. 函数长度是一个 18 位字段。 它指示以字节为单位的函数总长度除以 4 的值。 如果函数的大小大于 1M，则必须使用多个 .pdata 和 .xdata 记录来描述函数。 有关详细信息，请参阅[大函数](#large-functions)部分。

   b. Vers 是一个 2 位字段。 它描述剩余 .xdata 的版本。 当前仅定义了版本 0，因此不允许使用值 1-3。

   c. X 是一个 1 位字段。 它指示存在 (1) 或不存在 (0) 异常数据。

   d. E 是一个 1 位字段。 它指示描述单个 epilog 的信息已打包到标头 (1) 而非以后需要其他范围字 (0)。

   e. Epilog 计数是一个 5 位字段，它具有两种含义，具体取决于 E 位的状态：

      1. 如果 E 为 0，则它指定第 2 部分中所述 epilog 范围的总数的计数。 如果超过 31 个范围存在于此函数中，则代码字字段必须设置为 0，以指示需要一个扩展字。

      2. 如果 E 为 1，则此字段将指示仅描述一个唯一 epilog 的第一个展开代码的索引。

   f. 代码字是一个 5 位字段，它指示包含第 3 部分中所有展开代码所需的 32 位字的数目。 如果需要超过 31 个字（即，如果有超过 124 个展开代码字节），则此字段必须为 0，以指示需要一个扩展字。

   g. 扩展 Epilog 计数和扩展代码字分别为 16 位和 8 位字段。 它们提供更多空间来编码极大量的 epilog 或极大量的展开代码字。 包含这些字段的扩展字仅在第一个标头字中的 Epilog 计数和代码字字段都为 0 时才存在。

1. 如果 Epilog 计数 不为零，则有关 epilog 范围的信息的列表（一个范围打包到一个字中）会在标头和可选扩展标头后出现。 它们按增加起始偏移的顺序存储。 每个范围都包含以下位：

   a. Epilog 起始偏移是一个 18 位字段，它具有 epilog 相对于函数起始位置的偏移（以字节为单位）除以 4 的值。

   b. Res 是为将来扩展保留的一个 4 位字段。 其值必须为 0。

   c. Epilog 起始索引是一个 10 位字段（比扩展代码字多 2 位）。 它指示描述此 epilog 的第一个展开代码的字节索引。

1. epilog 范围列表之后是包含展开代码的字节数组（在后面部分中进行了详细介绍）。 在最接近的全字边界的末尾处填充此数组。 展开代码会写入此数组。 它们从最接近函数主体的一个开始，然后向前移动到函数的边缘。 每个展开代码的字节以 big-endian 顺序存储，因此可以从最高有效字节开始直接提取，该字节标识代码的操作和其余部分的长度。

1. 最后，如果标头中的 X 位设置为 1，则展开代码字节后跟异常处理程序信息。 它包含单个异常处理程序 RVA，用于提供异常处理程序本身的地址。 其后紧跟异常处理程序所需的长度可变的数据量。

.xdata 记录的设计目的是为了能够提取前 8 个字节并使用它们计算该记录的完整大小，减去它后面的大小可变的异常数据的长度。 以下代码段将计算记录大小：

```cpp
ULONG ComputeXdataSize(PULONG Xdata)
{
    ULONG Size;
    ULONG EpilogScopes;
    ULONG UnwindWords;

    if ((Xdata[0] >> 22) != 0) {
        Size = 4;
        EpilogScopes = (Xdata[0] >> 22) & 0x1f;
        UnwindWords = (Xdata[0] >> 27) & 0x1f;
    } else {
        Size = 8;
        EpilogScopes = Xdata[1] & 0xffff;
        UnwindWords = (Xdata[1] >> 16) & 0xff;
    }

    if (!(Xdata[0] & (1 << 21))) {
        Size += 4 * EpilogScopes;
    }

    Size += 4 * UnwindWords;

    if (Xdata[0] & (1 << 20)) {
        Size += 4;  // Exception handler RVA
    }

    return Size;
}
```

虽然 prolog 和每个 epilog 都具有自己的指向展开代码的索引，但此表对它们而言是通用的。 它们共享相同代码是完全可能的（而且并不罕见）。 （有关示例，请参阅[示例](#examples)部分中的示例 2。）特别是编译器编写器应针对此情况进行优化，因为可指定的最大索引为 255，这限制了特定函数的展开代码的总数。

### <a name="unwind-codes"></a>展开代码

展开代码的数组是准确描述如何撤消 prolog 效果的序列的池，这些序列按照需要撤消操作的相同顺序进行存储。 展开代码可以视为编码为字节字符串的小型指令集。 执行完成后，调用函数的返回地址处于 lr 寄存器中。 并且非易失性寄存器将还原为调用函数时它们的值。

如果可保证异常仅出现在函数主体内部，并且始终不会出现在 prolog 或任何 epilog 内部，则仅需要一个序列。 但是，Windows 展开模式需要可以从部分执行的 prolog 或 epilog 中进行展开。 为了满足此需求，已谨慎地将展开代码设计为对 prolog 和 epilog 中的每个相关操作码进行明确的 1:1 映射。 此设计具有几方面的含义：

1. 可通过计算展开代码的数量来计算 prolog 和 epilog 的长度。

1. 通过计算超出某个 epilog 范围起始位置的指令数，可以跳过相等数量的展开代码。 然后，可以执行序列的其余部分以完成由 epilog 进行的部分执行展开。

1. 通过计算 prolog 结尾之前的指令数，可以跳过相等数量的展开代码。 然后可以执行序列的其余部分，以仅撤消 prolog 中已完成执行的那些部分。

展开代码按下表进行编码。 所有展开代码都是单字节/双字节，除了分配大型堆栈的代码。 总共有 21 个展开代码。 每个展开代码只映射 prolog/epilog 中的一个指令，以便可以对部分执行的 prolog 和 epilog 进行展开。

|展开代码|位和解释|
|-|-|
|`alloc_s`|000xxxxx：分配小型堆栈，大小为 \< 512 (2^5 * 16)。|
|`save_r19r20_x`|    001zzzzz：将 \<x19,x20> 对保存在 `[sp-#Z*8]!`，索引前偏移 >= -248 |
|`save_fplr`|        01zzzzzz：将 \<x29,lr> 对保存在 `[sp+#Z*8]`，偏移 \<= 504。 |
|`save_fplr_x`|        10zzzzzz：将 \<x29,lr> 对保存在 `[sp-(#Z+1)*8]!`，索引前偏移 >= -512 |
|`alloc_m`|        11000xxx'xxxxxxxx：分配大型堆栈，大小为 \< 16k (2^11 * 16)。 |
|`save_regp`|        110010xx'xxzzzzzz：将 x(19+#X) 对保存在 `[sp+#Z*8]`，偏移 \<= 504 |
|`save_regp_x`|        110011xx'xxzzzzzz：将 x(19+#X) 对保存在 `[sp-(#Z+1)*8]!`，索引前偏移 >= -512 |
|`save_reg`|        110100xx'xxzzzzzz：将 reg x(19+#X) 保存在 `[sp+#Z*8]`，偏移 \<= 504 |
|`save_reg_x`|        1101010x'xxxzzzzz：将 reg x(19+#X) 保存在 `[sp-(#Z+1)*8]!`，索引前偏移 >= -256 |
|`save_lrpair`|         1101011x'xxzzzzzz：将 \<x(19+2*#X),lr> 对保存在 `[sp+#Z*8]`，偏移 \<= 504 |
|`save_fregp`|        1101100x'xxzzzzzz：将 d(8+#X) 对保存在 `[sp+#Z*8]`，偏移 \<= 504 |
|`save_fregp_x`|        1101101x'xxzzzzzz：将 d(8+#X) 对保存在 `[sp-(#Z+1)*8]!`，索引前偏移 >= -512 |
|`save_freg`|        1101110x'xxzzzzzz：将 reg d(8+#X) 保存在 `[sp+#Z*8]`，偏移 \<= 504 |
|`save_freg_x`|        11011110'xxxzzzzz：将 reg d(8+#X) 保存在 `[sp-(#Z+1)*8]!`，索引前偏移 >= -256 |
|`alloc_l`|         11100000'xxxxxxxx'xxxxxxxx'xxxxxxxx：分配大型堆栈，大小为 \< 256M (2^24 *16) |
|`set_fp`|        11100001：使用 `mov x29,sp` 设置 x29 |
|`add_fp`|        11100010'xxxxxxxx：使用 `add x29,sp,#x*8` 设置 x29 |
|`nop`|            11100011：不需要任何展开操作。 |
|`end`|            11100100：展开代码结尾。 在 epilog 中隐含 ret。 |
|`end_c`|        11100101：当前链式范围中的展开代码结尾。 |
|`save_next`|        11100110：保存下一个非易失性 Int 或 FP 寄存器对。 |
| |            11100111：已预留 |
| |              11101xxx：为以下自定义堆栈情况保留，仅为 asm 例程生成 |
| |              11101000：MSFT_OP_TRAP_FRAME 的自定义堆栈 |
| |              11101001：MSFT_OP_MACHINE_FRAME 的自定义堆栈 |
| |              11101010：MSFT_OP_CONTEXT 的自定义堆栈 |
| |              11101100：MSFT_OP_CLEAR_UNWOUND_TO_CALL 的自定义堆栈 |
| |              1111xxxx：保留 |

在具有涵盖多个字节的较大值的指令中，将首先存储最高有效位。 此设计使你可以通过只查找代码的第一个字节来获得展开代码的总大小（以字节为单位）。 由于每个展开代码都精确映射到 prolog 或 epilog 中的一个指令，因此可以计算 prolog 或 epilog 的大小。 可以从序列的开头审核到结尾，然后使用查找表或类似设备来确定相应操作码的长度。

prolog 中不允许使用索引后偏移寻址。 所有偏移范围 (#Z) 都匹配 STP/STR 寻址的编码，`save_r19r20_x` 除外，在这种情况下，248 足以用于所有保存区域（10 个 Int 寄存器 + 8 个 FP 寄存器 + 8 个输入寄存器）。

`save_next` 必须遵循 Int 或 FP 易失性寄存器对的保存：`save_regp`、`save_regp_x`、`save_fregp`、`save_fregp_x`、`save_r19r20_x` 或其他 `save_next`。 它会按“递增”顺序将下一个寄存器对保存在下一个 16 字节槽。 当 `save_next` 跟在 表示最后一个 Int 寄存器对的 `save-next` 后时，指第一个 FP 寄存器对。

由于常规返回和跳转指令的大小相同，因此不需要对尾调用方案使用分隔的 `end` 展开代码。

`end_c` 旨在处理非连续函数片段，以实现优化。 一个 `end_c`，指示当前范围中的展开代码结尾必须后跟以真实 `end` 结尾的另一个展开代码序列。 `end_c` 和 `end` 之间的展开代码表示父区域中的 prolog 操作（“虚拟”prolog）。  下面一节介绍了更多详细信息和示例。

### <a name="packed-unwind-data"></a>已打包的展开数据

对于 prolog 和 epilog 遵循如下所述的规范格式的函数，可以使用已打包的展开数据。 这类数据完全无需 .xdata 记录，并且可以显著减少提供展开数据所需的成本。 规范 prolog 和 epilog 旨在满足简单函数的常见要求：不需要异常处理程序，以及以标准顺序执行其安装和停止操作的函数。

具有已打包展开数据的 .pdata 记录的格式如下所示：

![具有已打包展开数据的 .pdata 记录](media/arm64-exception-handling-packed-unwind-data.png "具有已打包展开数据的 .pdata 记录")

字段如下所示：

- 函数起始 RVA  为函数起始位置的 32 位 RVA。
- 标志是如上所述的一个 2 位字段，具有以下含义：
  - 00 = 未使用的已打包展开数据；剩余的位指向 .xdata 记录
  - 01 = 已打包展开数据在范围开头和结尾与单个 prolog 和 epilog 一起使用
  - 10 = 已打包展开数据用于没有任何 prolog 和 epilog 的代码。 用于描述分隔函数段
  - 11 = 保留。
- 函数长度是一个 11 位字段，提供以字节为单位的整个函数的长度除以 4 的值。 如果函数的大小大于 8k，则必须改用一个完整的 .xdata 记录。
- 帧大小是一个 9 位字段，指示为此函数分配的堆栈的字节数除以 16 的值。 分配大于 (8k-16) 字节的堆栈的函数必须使用完整的 .xdata 记录。 它包括局部变量区域、传出参数区域、被调用方保存的 Int 和 FP 区域以及寻址参数区域，但不包括动态分配区域。
- CR 是 2 位标志，它指示函数是否包含用于设置帧链和返回链接的额外指令：
  - 00 = 非链式函数，\<x29,lr> 对不保存在堆栈中。
  - 01 = 非链式函数，\<lr> 保存在堆栈中
  - 10 = 保留；
  - 11 = 链式函数，在 prolog/epilog \<x29,lr> 中使用存储/加载对指令
- H 是 1 位标志，它指示函数是否通过在其开始位置存储整数参数寄存器 (x0-x7) 来对它们进行寻址。 （0=不会对寄存器进行寻址，1=对寄存器进行寻址）。
- RegI 是一个 4 位字段，它指示在规范堆栈位置中保存的非易失性 INT 寄存器 (x19-x28) 数量。
- RegF 是一个 3 位字段，它指示在规范堆栈位置中保存的非易失性 FP 寄存器 (d8-d15) 数量。 （RegF=0：未保存任何 FP 寄存器；RegF>0：保存了 RegF+1 个 FP 寄存器）。 已打包展开数据不能用于仅保存一个 FP 寄存器的函数。

属于上一部分中的类别 1、2（无传出参数区域）、3 和 4 的规范 prolog 可以使用已打包展开格式进行表示。  规范函数的 epilog 遵循类似形式，但 H 不起作用，省略了 `set_fp` 指令，并且步骤的顺序和每个步骤中的指令在 epilog 中会反转。 已打包 .xdata 的算法遵循下表中详细介绍的步骤：

步骤 0：预先计算每个区域的大小。

步骤 1：保存被调用方保存的 Int 寄存器。

步骤 2：此步骤特定于前面部分中的类型 4。 lr 保存在 Int 区域结尾。

步骤 3：保存被调用方保存的 FP 寄存器。

步骤 4：在寻址参数区域保存输入参数。

步骤 5：分配剩余堆栈，包括本地区域、\<x29,lr> 对和传出参数区域。 5a 对应于规范类型 1。 5b 和 5c 适用于规范类型 2。 5d 和 5e 适用于类型 3 和类型 4。

步骤编号|标志值|指令数|操作码|展开代码
-|-|-|-|-
0|||`#intsz = RegI * 8;`<br/>`if (CR==01) #intsz += 8; // lr`<br/>`#fpsz = RegF * 8;`<br/>`if(RegF) #fpsz += 8;`<br/>`#savsz=((#intsz+#fpsz+8*8*H)+0xf)&~0xf)`<br/>`#locsz = #famsz - #savsz`|
1|0 < RegI <= 10|RegI / 2 + RegI % 2|`stp x19,x20,[sp,#savsz]!`<br/>`stp x21,x22,[sp,#16]`<br/>`...`|`save_regp_x`<br/>`save_regp`<br/>`...`
2|CR==01*|1|`str lr,[sp,#(intsz-8)]`\*|`save_reg`
3|0 < RegF <=7|(RegF + 1) / 2 +<br/>(RegF + 1) % 2)|`stp d8,d9,[sp,#intsz]`\*\*<br/>`stp d10,d11,[sp,#(intsz+16)]`<br/>`...`<br/>`str d(8+RegF),[sp,#(intsz+fpsz-8)]`|`save_fregp`<br/>`...`<br/>`save_freg`
4|H == 1|4|`stp x0,x1,[sp,#(intsz+fpsz)]`<br/>`stp x2,x3,[sp,#(intsz+fpsz+16)]`<br/>`stp x4,x5,[sp,#(intsz+fpsz+32)]`<br/>`stp x6,x7,[sp,#(intsz+fpsz+48)]`|`nop`<br/>`nop`<br/>`nop`<br/>`nop`
5a|CR == 11 && #locsz<br/> <= 512|2|`stp x29,lr,[sp,#-locsz]!`<br/>`mov x29,sp`\*\*\*|`save_fplr_x`<br/>`set_fp`
5b|CR == 11 &&<br/>512 < #locsz <= 4080|3|`sub sp,sp,#locsz`<br/>`stp x29,lr,[sp,0]`<br/>`add x29,sp,0`|`alloc_m`<br/>`save_fplr`<br/>`set_fp`
5c|CR == 11 && #locsz > 4080|4|`sub sp,sp,4080`<br/>`sub sp,sp,#(locsz-4080)`<br/>`stp x29,lr,[sp,0]`<br/>`add x29,sp,0`|`alloc_m`<br/>`alloc_s`/`alloc_m`<br/>`save_fplr`<br/>`set_fp`
5d|(CR == 00 \|\| CR==01) && <br/>#locsz <= 4080|1|`sub sp,sp,#locsz`|`alloc_s`/`alloc_m`
5e|(CR == 00 \|\| CR==01) && <br/>#locsz > 4080|2|`sub sp,sp,4080`<br/>`sub sp,sp,#(locsz-4080)`|`alloc_m`<br/>`alloc_s`/`alloc_m`

\* 如果 CR == 01 且 RegI 为奇数，则步骤 2 和步骤 1 中的最后一个 save_rep 会合并为一个 save_regp。

\*\* 如果 RegI == CR == 0，且 RegF != 0，则浮点的第一个 stp 会执行前递减。

\*\*\* epilog 中不存在与 `mov x29,sp` 对应的指令。 如果函数需要从 x29 还原 sp，则无法使用已打包展开数据。

### <a name="unwinding-partial-prologs-and-epilogs"></a>展开部分 prolog 和 epilog

最常见的展开情况是，异常或调用在函数主体中出现，远离 prolog 和所有 epilog。 在这种情况下，展开十分简单：展开器只需从索引 0 处开始执行展开数组中的代码，并且在检测到结束操作码之前将一直持续该操作。

如果在执行 prolog 或 epilog 时发生异常或中断，则更难以正确展开。 在这些情况下，堆栈帧只会进行部分构造。 问题在于精确确定已执行的操作，以正确撤消。

例如，采用以下 prolog 和 epilog 序列：

```asm
0000:    stp    x29,lr,[sp,#-256]!          // save_fplr_x  256 (pre-indexed store)
0004:    stp    d8,d9,[sp,#224]             // save_fregp 0, 224
0008:    stp    x19,x20,[sp,#240]           // save_regp 0, 240
000c:    mov    x29,sp                      // set_fp
         ...
0100:    mov    sp,x29                      // set_fp
0104:    ldp    x19,x20,[sp,#240]           // save_regp 0, 240
0108:    ldp    d8,d9,[sp,224]              // save_fregp 0, 224
010c:    ldp    x29,lr,[sp],#256            // save_fplr_x  256 (post-indexed load)
0110:    ret    lr                          // end
```

每个操作码旁是相应的展开代码，用于描述此操作。 可以看到，prolog 展开代码序列如何是 epilog 展开代码的精确镜像（不计入 epilog 的最终指令）。 这是一种常见情况，并且是始终将 prolog 的展开代码假设为以与 prolog 执行顺序相反的顺序进行存储的原因。

因此，对于 prolog 和 epilog，我们剩下一组通用的展开代码：

`set_fp`, `save_regp 0,240`, `save_fregp,0,224`, `save_fplr_x_256`, `end`

epilog 情况非常简单，因为它按正常顺序进行。 从 epilog 中的偏移 0 开始（这会从函数中的偏移 0x100 开始），我们希望执行完整展开序列，因为尚未进行任何清理。 如果我们自己在其中找到一个指令（epilog 中的偏移 2 处），则可以通过跳过第一个展开代码来成功展开。 我们可以一般化这种情况，并假设操作码与展开代码之间存在 1:1 映射。 然后，若要从 epilog 中的指令 n 开始展开，应跳过前 n 个展开代码，并从该处开始执行。

事实证明，类似逻辑适用于 prolog，不过顺序相反。 如果要从 prolog 中的偏移 0 开始展开，则无需执行任何操作。 如果从偏移 2（一个指令在其中）展开，则我们要从结尾开始执行展开序列的一个展开代码。 （请记住，代码按相反顺序存储。）在这里也可以进行一般化：如果从 prolog 中的指令 n 开始展开，则应从代码列表结尾开始执行 n 个展开代码。

prolog 和 epilog 代码并非总是完全匹配。 这便是为何展开数组可能需要包含几个代码序列。 若要确定开始处理代码的偏移，请使用以下逻辑：

1. 如果从函数主体内部展开，请在索引 0 处开始执行展开代码，并且继续该操作，直到命中“结束”操作码。

1. 如果从 epilog 内部展开，请使用由 epilog 范围提供的特定于 epilog 的起始索引作为起始点。 计算相关电脑从 epilog 开始位置读取的字节数。 然后在展开代码中快进，跳过展开代码，直到处理完所有已执行的指令。 然后从该点开始执行。

1. 如果从 prolog 内部展开，请使用索引 0 作为起始点。 计算序列中的 prolog 代码的长度，然后计算相关电脑从 prolog 结束位置读取的字节数。 然后在展开代码中快进，跳过展开代码，直到处理完所有未执行的指令。 然后从该点开始执行。

这些规则意味着 prolog 的展开代码必须始终位于数组的最前面。 而且在从主体内部展开的一般情况下，prolog 的展开代码也是用于展开的代码。 特定于 epilog 的任何代码序列应紧随其后。

### <a name="function-fragments"></a>函数片段

出于代码优化目的和其他原因，最好将函数拆分为分隔片段（也称为区域）。 完成拆分后，生成的每个函数片段都需要各自单独的 .pdata（并且可能需要 .xdata）记录。

对于具有自己的 prolog 的每个分隔辅助片段，其 prolog 中不应进行任何堆栈调整。 辅助区域所需的所有堆栈空间都必须由其父区域（或称为主机区域）预先分配。 这会将堆栈指针操作严格保留在函数原始 prolog 中。

函数片段的典型情况是“代码分隔”，因为编译器可能会将代码区域移出其主机函数。 代码分隔可能会导致三种异常情况。

#### <a name="example"></a>示例

- （区域 1：开头）

    ```asm
        stp     x29,lr,[sp,#-256]!      // save_fplr_x  256 (pre-indexed store)
        stp     x19,x20,[sp,#240]       // save_regp 0, 240
        mov     x29,sp                  // set_fp
        ...
    ```

- （区域 1：结尾）

- （区域 3：开头）

    ```asm
        ...
    ```

- （区域 3：结尾）

- （区域 2：开头）

    ```asm
        ...
        mov     sp,x29                  // set_fp
        ldp     x19,x20,[sp,#240]       // save_regp 0, 240
        ldp     x29,lr,[sp],#256        // save_fplr_x  256 (post-indexed load)
        ret     lr                      // end
    ```

- （区域 2：结尾）

1. 仅 Prolog（区域 1：所有 epilog 都在分隔区域中）：

   仅仅必须描述 prolog。 这不能以紧凑 .pdata 格式进行表示。 对于完整 .xdata，它可以通过设置 Epilog 计数 = 0 来表示。 请参阅上面示例中的区域 1。

   展开代码：`set_fp`、`save_regp 0,240`、`save_fplr_x_256`、`end`。

1. 仅 Epilog（区域 2：prolog 在主机区域中）

   假设到控制跳转到此区域中时，已执行了所有 prolog 代码。 部分展开可以按照与正常函数中相同的方式在 epilog 中进行。 此类型的区域不能由紧凑 .pdata 进行表示。 对于完整 .xdata 记录，它可以使用“虚拟”prolog 进行编码，由 `end_c` 和 `end` 展开代码对括起来。  前导 `end_c` 指示 prolog 的大小为零。 单个 epilog 的 epilog 起始索引指向 `set_fp`。

   区域 2 的展开代码：`end_c`、`set_fp`、`save_regp 0,240`、`save_fplr_x_256`、`end`。

1. 没有 prolog 或 epilog（区域3：prolog 和所有 epilog 都在其他片段中）：

   可以通过设置标志 = 10 来应用紧凑 .pdata 格式。 对于完整 .xdata 记录，Epilog 计数 = 1。 展开代码与上面区域 2 的代码相同，但是 Epilog 起始索引也指向 `end_c`。 部分展开从不会发生在此代码区域中进行。

函数片段的另一种更复杂的情况是“紧缩套装”。 编译器可能会选择延迟保存某些被调用方保存的寄存器，直到位于函数入口 prolog 之外。

- （区域 1：开头）

    ```asm
        stp     x29,lr,[sp,#-256]!      // save_fplr_x  256 (pre-indexed store)
        stp     x19,x20,[sp,#240]       // save_regp 0, 240
        mov     x29,sp                  // set_fp
        ...
    ```

- （区域 2：开头）

    ```asm
        stp     x21,x22,[sp,#224]       // save_regp 2, 224
        ...
        ldp     x21,x22,[sp,#224]       // save_regp 2, 224
    ```

- （区域 2：结尾）

    ```asm
        ...
        mov     sp,x29                  // set_fp
        ldp     x19,x20,[sp,#240]       // save_regp 0, 240
        ldp     x29,lr,[sp],#256        // save_fplr_x  256 (post-indexed load)
        ret     lr                      // end
    ```

- （区域 1：结尾）

在区域 1 的 prolog 中，预先分配了堆栈空间。 可以看到，区域 2 将具有相同的展开代码，即使它已移出其主机函数。

区域1：`set_fp`、`save_regp 0,240`、`save_fplr_x_256`、`end`，其 Epilog 起始索引与平常一样指向 `set_fp`。

区域2：`save_regp 2, 224`、`end_c`、`set_fp`、`save_regp 0,240`、`save_fplr_x_256`、`end`。 Epilog 起始索引指向第一个展开代码 `save_regp 2, 224`。

### <a name="large-functions"></a>大函数

片段可用于描述大小超过 .xdata 标头中位字段施加的 1M 限制的函数。 若要描述类似于这样的非常大的函数，需要将它分解为小于 1M 的片段。 应当调整每个片段，以便它不会将 epilog 拆分为多个部分。

仅函数的第一个片段包含 prolog；所有其他片段都被标记为不包含 prolog。 根据 epilog 的数目，每个片段可能包含零个或多个 epilog。 请记住，片段中的每个 epilog 范围指定相对于该片段开头处（而非函数的开始位置）的起始偏移。

如果片段没有 prolog 和 epilog，则它仍然需要自己的 .pdata（并且可能需要 .xdata）记录，以描述如何从函数主体内部展开。

## <a name="examples"></a>示例

### <a name="example-1-frame-chained-compact-form"></a>示例 1：帧链式，紧凑形式

```asm
|Foo|     PROC
|$LN19|
    str     x19,[sp,#-0x10]!        // save_reg_x
    sub     sp,sp,#0x810            // alloc_m
    stp     fp,lr,[sp]              // save_fplr
    mov     fp,sp                   // set_fp
                                    //  end of prolog
    ...

|$pdata$Foo|
    DCD     imagerel     |$LN19|
    DCD     0x416101ed
    ;Flags[SingleProEpi] functionLength[492] RegF[0] RegI[1] H[0] frameChainReturn[Chained] frameSize[2080]
```

### <a name="example-2-frame-chained-full-form-with-mirror-prolog--epilog"></a>示例 2：帧链式，具有镜像 Prolog 和 Epilog 的完整形式

```asm
|Bar|     PROC
|$LN19|
    stp     x19,x20,[sp,#-0x10]!    // save_regp_x
    stp     fp,lr,[sp,#-0x90]!      // save_fplr_x
    mov     fp,sp                   // set_fp
                                    // end of prolog
    ...
                                    // begin of epilog, a mirror sequence of Prolog
    mov     sp,fp
    ldp     fp,lr,[sp],#0x90
    ldp     x19,x20,[sp],#0x10
    ret     lr

|$pdata$Bar|
    DCD     imagerel     |$LN19|
    DCD     imagerel     |$unwind$cse2|
|$unwind$Bar|
    DCD     0x1040003d
    DCD     0x1000038
    DCD     0xe42291e1
    DCD     0xe42291e1
    ;Code Words[2], Epilog Count[1], E[0], X[0], Function Length[6660]
    ;Epilog Start Index[0], Epilog Start Offset[56]
    ;set_fp
    ;save_fplr_x
    ;save_r19r20_x
    ;end
```

Epilog 起始索引 [0] 指向相同的 Prolog 展开代码序列。

### <a name="example-3-variadic-unchained-function"></a>示例 3：可变参数非链式函数

```asm
|Delegate| PROC
|$LN4|
    sub     sp,sp,#0x50
    stp     x19,lr,[sp]
    stp     x0,x1,[sp,#0x10]        // save incoming register to home area
    stp     x2,x3,[sp,#0x20]        // ...
    stp     x4,x5,[sp,#0x30]
    stp     x6,x7,[sp,#0x40]        // end of prolog
    ...
    ldp     x19,lr,[sp]             // beginning of epilog
    add     sp,sp,#0x50
    ret     lr

    AREA    |.pdata|, PDATA
|$pdata$Delegate|
    DCD     imagerel |$LN4|
    DCD     imagerel |$unwind$Delegate|

    AREA    |.xdata|, DATA
|$unwind$Delegate|
    DCD     0x18400012
    DCD     0x200000f
    DCD     0xe3e3e3e3
    DCD     0xe40500d6
    DCD     0xe40500d6
    ;Code Words[3], Epilog Count[1], E[0], X[0], Function Length[18]
    ;Epilog Start Index[4], Epilog Start Offset[15]
    ;nop        // nop for saving in home area
    ;nop        // ditto
    ;nop        // ditto
    ;nop        // ditto
    ;save_lrpair
    ;alloc_s
    ;end
```

Epilog 起始索引 [4] 指向 Prolog 展开代码的中间（部分重用展开数组）。

## <a name="see-also"></a>请参阅

[ARM64 ABI 约定概述](arm64-windows-abi-conventions.md)<br/>
[ARM 异常处理](arm-exception-handling.md)
