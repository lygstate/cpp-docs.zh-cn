---
title: float_control pragma
description: 描述 float_control 指令的用法和效果 pragma 。 Float_control 指令在运行时控制浮点精确语义和异常语义的状态。
ms.date: 04/15/2021
f1_keywords:
- vc-pragma.float_control
- float_control_CPP
helpviewer_keywords:
- float_control pragma
- pragma, float_control
no-loc:
- pragma
ms.openlocfilehash: b7a02acf729d04527300454fed6e74e7d06bbfe9
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539769"
---
# <a name="float_control-pragma"></a>`float_control` pragma

指定函数的浮点行为。

## <a name="syntax"></a>语法

> **`#pragma float_control`**\
> **`#pragma float_control( precise,`** { **`on`** &vert; **`off`** } [ **`, push`** ] **`)`**\
> **`#pragma float_control( except,`** { **`on`** &vert; **`off`** } [ **`, push`** ] **`)`**\
> **`#pragma float_control(`** { **`push`** &vert; **`pop`** } **`)`**

## <a name="options"></a>选项

**`precise`**, **`on`** | **`off`**, **`push`**\
指定是启用 (**`on`**) 还是禁用 (**`off`**) 精确的浮点语义。 有关与编译器选项的差异的信息 **`/fp:precise`** ，请参阅 "备注" 部分。 可选 **`push`** 令牌为 **`float_control`** 内部编译器堆栈推送当前设置。

**`except`**, **`on`** | **`off`**, **`push`**\
指定是启用 (**`on`**) 还是禁用 (**`off`**) 浮点异常语义。 可选 **`push`** 令牌为 **`float_control`** 内部编译器堆栈推送当前设置。

**`except`****`on`** 如果 **`precise`** 也设置为，则只能将设置为 **`on`** 。

**`push`**\
将的当前 **`float_control`** 设置推送到内部编译器堆栈上。

**`pop`**\
**`float_control`** 从内部编译器堆栈的顶部移除设置，并使其成为新的 **`float_control`** 设置。

## <a name="remarks"></a>注解

的 **`float_control`** pragma 行为与编译器选项的行为不同 [`/fp`](../build/reference/fp-specify-floating-point-behavior.md) 。 **`float_control`** pragma 仅控制浮点行为的部分。 它必须与和指令组合在一起， [`fp_contract`](../preprocessor/fp-contract.md) [`fenv_access`](../preprocessor/fenv-access.md) pragma 才能重新创建 **`/fp`** 编译器选项。 下表显示了 pragma 每个编译器选项的等效设置：

| 选项 | `float_control(precise, *)` | `float_control(except, *)` | `fp_contract(*)` | `fenv_access(*)` |
|-|-|-|-|-|
| `/fp:strict`             | `on`  | `on`  | `off` | `on`  |
| `/fp:precise`            | `on`  | `off` | `on`  | `off` |
| `/fp:fast`               | `off` | `off` | `on`  | `off` |

换句话说，你可能需要结合使用多个 pragma 指令来模拟 **`/fp:fast`** 、 **`/fp:precise`** 和 **`/fp:strict`** 命令行选项。

**`float_control`** 结合使用和 **`fenv_access`** 浮点指令的方式有一些限制 pragma ：

- **`float_control`** **`except`** **`on`** 如果启用了精确语义，则只能使用将设置为。 可以通过或 **`float_control`** pragma 使用 **`/fp:precise`** 或 **`/fp:strict`** 编译器选项来启用精确语义。

- **`float_control`** **`precise`** 启用异常语义时，无论是通过 **`float_control`** pragma 还是 **`/fp:except`** 编译器选项，都不能使用来关闭。

- **`fenv_access`** 除非启用了精确语义，否则不能启用，无论是通过 **`float_control`** pragma 还是编译器选项启用。

- 启用后，不能使用 **`float_control`** 来关闭 **`precise`** **`fenv_access`** 。

这些限制意味着某些浮点指令的顺序 pragma 非常重要。 若要使用指令从快速模型转为严格模型 pragma ，请使用以下代码：

```cpp
#pragma float_control(precise, on)  // enable precise semantics
#pragma fenv_access(on)             // enable environment sensitivity
#pragma float_control(except, on)   // enable exception semantics
#pragma fp_contract(off)            // disable contractions
```

若要使用从严格模型转为快速模型 **`float_control`** pragma ，请使用以下代码：

```cpp
#pragma float_control(except, off)  // disable exception semantics
#pragma fenv_access(off)            // disable environment sensitivity
#pragma float_control(precise, off) // disable precise semantics
#pragma fp_contract(on)             // enable contractions
```

如果未指定任何选项，则 **`float_control`** 不起作用。

## <a name="example"></a>示例

下面的示例演示如何使用捕获溢出浮点异常 pragma **`float_control`** 。

```cpp
// pragma_directive_float_control.cpp
// compile with: /EHa
#include <stdio.h>
#include <float.h>

double func( ) {
   return 1.1e75;
}

#pragma float_control (except, on)

int main( ) {
   float u[1];
   unsigned int currentControl;
   errno_t err;

   err = _controlfp_s(&currentControl, ~_EM_OVERFLOW, _MCW_EM);
   if (err != 0)
      printf_s("_controlfp_s failed!\n");

   try  {
      u[0] = func();
      printf_s ("Fail");
      return(1);
   }

   catch (...)  {
      printf_s ("Pass");
      return(0);
   }
}
```

```Output
Pass
```

## <a name="see-also"></a>另请参阅

[杂注指令和 `__pragma` 和 `_Pragma` 关键字](./pragma-directives-and-the-pragma-keyword.md)\
[`fenv_access` pragma](../preprocessor/fenv-access.md)\
[`fp_contract` pragma](../preprocessor/fp-contract.md)
