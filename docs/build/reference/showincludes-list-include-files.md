---
description: '了解详细信息：/showIncludes (列表包括文件) '
title: /showIncludes（列出包含文件）
ms.date: 04/15/2021
f1_keywords:
- VC.Project.VCCLWCECompilerTool.ShowIncludes
- VC.Project.VCCLCompilerTool.ShowIncludes
- /showincludes
helpviewer_keywords:
- include files
- /showIncludes compiler option [C++]
- include files, displaying in compilation
- -showIncludes compiler option [C++]
- showIncludes compiler option [C++]
ms.openlocfilehash: 3c960b7b88b9d96cde54f535bffbaf67dd3f67b6
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539261"
---
# <a name="showincludes-list-include-files"></a>`/showIncludes` (列表包括文件) 

使编译器输出包含文件的列表。 选项还显示嵌套的包含文件，即包含的文件所包含的文件。

## <a name="syntax"></a>语法

> **`/showIncludes`**

## <a name="remarks"></a>备注

如果编译器在编译过程中进入包含文件，则会输出消息，如以下示例中所示：

```cmd
Note: including file: d:\MyDir\include\stdio.h
```

嵌套的包含文件通过缩进来表示，每个嵌套级别有一个空间，如下例所示：

```cmd
Note: including file: d:\temp\1.h
Note: including file:  d:\temp\2.h
```

在这种情况下， *`2.h`* 从内包含 *`1.h`* ，导致缩进。

**`/showIncludes`** 选项将发出到 `stderr` ，而不是 `stdout` 。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 选择 "**配置属性**" "  >  **c/c + +**  >  **高级**" 属性页。

1. 修改 " **显示包含** " 属性。

### <a name="to-set-this-compiler-option-programmatically"></a>以编程方式设置此编译器选项

- 请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.ShowIncludes%2A>。

## <a name="see-also"></a>另请参阅

[MSVC 编译器选项](compiler-options.md)\
[MSVC 编译器命令行语法](compiler-command-line-syntax.md)
