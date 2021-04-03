---
description: '了解详细信息：/openmp (Enable OpenMP 支持) '
title: '/openmp (启用 OpenMP 支持) '
ms.date: 04/01/2021
f1_keywords:
- /openmp
- /openmp:experimental
- /openmp:llvm
- VC.Project.VCCLCompilerTool.OpenMP
helpviewer_keywords:
- /openmp compiler option [C++]
- /openmp:experimental compiler option [C++]
- /openmp:llvm compiler option [C++]
- -openmp compiler option [C++]
ms.openlocfilehash: d8363b253136c7e962ef62ecb29f0e2f13cc453e
ms.sourcegitcommit: be9a1af0b9d3f1d6c2987d8744392170b8dccab0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106232317"
---
# <a name="openmp-enable-openmp-support"></a>`/openmp` (启用 OpenMP 支持) 

导致编译器处理 [`#pragma omp`](../../preprocessor/omp.md) OpenMP 支持的指令。

## <a name="syntax"></a>语法

::: moniker range=">= msvc-160"

> **`/openmp`**\
> **`/openmp:experimental`**\
> **`/openmp:llvm`**

::: moniker-end

::: moniker range="<= msvc-150"

> **`/openmp`**

::: moniker-end

## <a name="remarks"></a>备注

`#pragma omp` 用于指定 [指令](../../parallel/openmp/reference/openmp-directives.md) 和 [子句](../../parallel/openmp/reference/openmp-clauses.md)。 如果 **`/openmp`** 编译中未指定，编译器将忽略 OpenMP 子句和指令。 即使未指定，也会由编译器处理 [OpenMP 函数](../../parallel/openmp/reference/openmp-functions.md)调用 **`/openmp`** 。

::: moniker range=">= msvc-160"

C + + 编译器当前支持 OpenMP 2.0 标准。 但是，Visual Studio 2019 现在还提供 SIMD 功能。 若要使用 SIMD，请使用 **`/openmp:experimental`** 选项编译。 使用此选项可在使用开关时启用常见 OpenMP 功能和 OpenMP SIMD 功能 **`/openmp`** 。

从 Visual Studio 2019 版本16.9 开始，你可以使用实验 **`/openmp:llvm`** 选项而不是 **`/openmp`** 来以 LLVM OpenMP 运行时为目标。 当前支持不能用于生产代码，因为所需的 libomp Dll 是不可再发行的。 选项支持与相同的 OpenMP 2.0 指令 **`/openmp`** 。 而且，它支持选项支持的所有 SIMD 指令 **`/openmp:experimental`** 。 它还支持按 OpenMP 3.0 标准为循环并行提供无符号整数索引。 有关详细信息，请参阅 [Visual Studio 中对 c + + 的 OpenMP 支持](https://devblogs.microsoft.com/cppblog/improved-openmp-support-for-cpp-in-visual-studio/)。

目前， **`/openmp:llvm`** 选项仅适用于 x64 体系结构。 选项与或不兼容 **`/clr`** **`/ZW`** 。

::: moniker-end

使用和编译的应用 **`/openmp`** 程序 **`/clr`** 只能在单个应用程序域进程中运行。 不支持多个应用程序域。 也就是说，当模块构造函数 (`.cctor`) 运行时，它会检测是否使用编译了该进程 **`/openmp`** ，以及该应用程序是否已加载到非默认运行时。 有关详细信息，请 [`appdomain`](../../cpp/appdomain.md) 参阅[ `/clr` (公共语言运行时编译) ](clr-common-language-runtime-compilation.md)和[混合程序集的初始化](../../dotnet/initialization-of-mixed-assemblies.md)。

如果尝试将使用和 * 编译的应用加载 **`/openmp`** *`/clr*`* 到非默认应用程序域中，则会在 <xref:System.TypeInitializationException> 调试器外部引发异常，并且 `OpenMPWithMultipleAppdomainsException` 调试器中会引发异常。

在下列情况下，也可能会引发这些异常：

- 如果你的应用程序是使用而不是使用进行编译的 **`/clr`** **`/openmp`** ，并且加载到非默认应用程序域中，则该过程包含使用编译的应用 **`/openmp`** 。

- 如果将应用程序传递 **`/clr`** 到 [regasm.exe](/dotnet/framework/tools/regasm-exe-assembly-registration-tool)，则会将其目标程序集加载到非默认应用程序域中。

公共语言运行时的代码访问安全性不适用于 OpenMP 区域。 如果在并行区域外部应用 CLR 代码访问安全性属性，则该属性在并行区域中不起作用。

Microsoft 不建议你编写 **`/openmp`** 允许部分受信任的调用方的应用程序。 不要使用 <xref:System.Security.AllowPartiallyTrustedCallersAttribute> 或任何 CLR 代码访问安全性属性。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 展开 "**配置属性**" "  >  **c/c + +**  >  **语言**" 属性页。

1. 修改 **OpenMP 支持** 属性。

### <a name="to-set-this-compiler-option-programmatically"></a>以编程方式设置此编译器选项

- 请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.OpenMP%2A>。

## <a name="example"></a>示例

下面的示例显示了在启动线程池后使用线程池的某些影响。 假设有一个 x64、单核、双处理器，线程池需要大约16毫秒的时间启动。 在此之后，线程池的开销较低。

使用进行编译时 **`/openmp`** ，对 test2 的第二次调用的运行时间不会超过使用进行编译的时间 **`/openmp-`** ，因为不会启动线程池。 在一百万次迭代时， **`/openmp`** 版本比 **`/openmp-`** 第二次调用 test2 的版本更快。 25次迭代时， **`/openmp-`** 和的 **`/openmp`** 版本寄存器小于时钟粒度。

如果你的应用程序中仅有一个循环，并且该循环在不到15毫秒的时间内运行 (则会在计算机) 的大致开销内调整，这 **`/openmp`** 可能不适合。 如果较高，则可能需要考虑使用 **`/openmp`** 。

```cpp
// cpp_compiler_options_openmp.cpp
#include <omp.h>
#include <stdio.h>
#include <stdlib.h>
#include <windows.h>

volatile DWORD dwStart;
volatile int global = 0;

double test2(int num_steps) {
   int i;
   global++;
   double x, pi, sum = 0.0, step;

   step = 1.0 / (double) num_steps;

   #pragma omp parallel for reduction(+:sum) private(x)
   for (i = 1; i <= num_steps; i++) {
      x = (i - 0.5) * step;
      sum = sum + 4.0 / (1.0 + x*x);
   }

   pi = step * sum;
   return pi;
}

int main(int argc, char* argv[]) {
   double   d;
   int n = 1000000;

   if (argc > 1)
      n = atoi(argv[1]);

   dwStart = GetTickCount();
   d = test2(n);
   printf_s("For %d steps, pi = %.15f, %d milliseconds\n", n, d, GetTickCount() - dwStart);

   dwStart = GetTickCount();
   d = test2(n);
   printf_s("For %d steps, pi = %.15f, %d milliseconds\n", n, d, GetTickCount() - dwStart);
}
```

## <a name="see-also"></a>另请参阅

[MSVC 编译器选项](compiler-options.md) \
[MSVC 编译器命令行语法](compiler-command-line-syntax.md) \
[MSVC 中的 OpenMP](../../parallel/openmp/openmp-in-visual-cpp.md)
