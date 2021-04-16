---
description: '详细了解：/D (预处理器定义) '
title: /D（预处理器定义）
ms.date: 09/18/2019
f1_keywords:
- VC.Project.VCNMakeTool.PreprocessorDefinitions
- VC.Project.VCCLCompilerTool.PreprocessorDefinitions
- /d
helpviewer_keywords:
- preprocessor definition symbols
- constants, defining
- macros, compiling
- /D compiler option [C++]
- -D compiler option [C++]
- D compiler option [C++]
ms.assetid: b53fdda7-8da1-474f-8811-ba7cdcc66dba
ms.openlocfilehash: 2e94c28c094f6ea03eacdb04c452785511fb3a3f
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539656"
---
# <a name="d-preprocessor-definitions"></a>/D（预处理器定义）

定义源文件的预处理符号。

## <a name="syntax"></a>语法

> **`/D`**\[]_name_ \[ `=` &vert; `#` \[ { *string* &vert; *number* }]] \
> **`/D`**\[] `"` _name_ \[ `=` &vert; `#` \[ { *string* &vert; *number* }]]`"`

## <a name="remarks"></a>注解

可以将此符号与 `#if` 或 `#ifdef` 一起使用，以便有条件地编译源代码。 符号定义在代码中重新定义之前有效，或在代码中由 `#undef` 指令定义。

**`/D`** 与源代码文件开头的指令具有相同的效果 `#define` 。 不同之处在于 **`/D`** ，命令行上有带引号的引号， `#define` 指令会将其保留。 和符号之间可以有空格 **`/D`** 。 符号和等号之间不能存在空格，或者在等号和分配的任何值之间不能存在空格。

默认情况下，与符号关联的值为 1。 例如，`/D name` 等效于 `/D name=1`。 在本文末尾的示例中，显示的定义 `TEST` 是 "打印" `1` 。

使用进行编译将 `/D name=` 导致符号 *名称* 没有关联值。 尽管该符号仍可用于有条件地编译代码，但它不会计算出任何结果。 在此示例中，如果使用进行编译 `/DTEST=` ，则会发生错误。 此行为类似于带或不带值使用 `#define`。

**`/D`** 选项不支持类似于函数的宏定义。 若要插入不能在命令行上定义的定义，请考虑[ `/FI` (名称强制包含文件) ](fi-name-forced-include-file.md)编译器选项。

您可以 **`/D`** 在命令行上多次使用来定义更多符号。 如果多次定义同一符号，则使用最后一个定义。

此命令在 TEST.c 中定义符号 DEBUG：

```cmd
CL /DDEBUG TEST.C
```

此命令删除在 test.txt 中出现的所有关键字 **`__far`** ：

```cmd
CL /D __far= TEST.C
```

**CL** 环境变量不能设置为包含等号的字符串。 若要 **`/D`** 与 **`CL`** 环境变量一起使用，必须指定数字符号 (`#`) 而不是等号：

```cmd
SET CL=/DTEST#0
```

在命令提示符处定义预处理符号时，应同时考虑编译器分析规则和 shell 分析规则。 例如，若要在程序中定义一个百分号预处理符号 (`%`) ，请在 `%%` 命令提示符下 () 指定两个百分号字符。 如果仅指定一个分析错误，则会发出分析错误。

```cmd
CL /DTEST=%% TEST.C
```

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

1. 打开项目“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 选择 "**配置属性**" "  >  **c/c + +**  >  **预处理器**" 属性页。

1. 打开 " **预处理器定义** " 属性的下拉菜单，然后选择 " **编辑**"。

1. 在 " **预处理器定义** " 对话框中，添加、修改或删除一个或多个定义，每行一个或多个定义。 选择“确定”以保存更改  。

   不需要在此处指定的定义上包含 "/D" 选项前缀。 在属性页中，定义由分号分隔 (`;`) 。

### <a name="to-set-this-compiler-option-programmatically"></a>以编程方式设置此编译器选项

- 请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.PreprocessorDefinitions%2A>。

## <a name="example"></a>示例

```cpp
// cpp_D_compiler_option.cpp
// compile with: cl /EHsc /DTEST cpp_D_compiler_option.cpp
#include <stdio.h>

int main( )
{
#ifdef TEST
    printf_s("TEST defined %d\n", TEST);
#else
    printf_s("TEST not defined\n");
#endif
}
```

```Output
TEST defined 1
```

## <a name="see-also"></a>另请参阅

[MSVC 编译器选项](compiler-options.md)\
[MSVC 编译器命令行语法](compiler-command-line-syntax.md)\
[`/FI` (名称强制包含文件) ](fi-name-forced-include-file.md)\
[`/U`， `/u` (取消定义符号) ](u-u-undefine-symbols.md)\
[`#undef` 指令 (C/c + +) ](../../preprocessor/hash-undef-directive-c-cpp.md)\
[`#define` 指令 (C/c + +) ](../../preprocessor/hash-define-directive-c-cpp.md)
