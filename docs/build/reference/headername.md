---
title: '/headerName (从指定的标头生成标题单元) '
description: 使用/headerName 编译器选项可以在标头文件和要生成的标头单元之间建立映射。
ms.date: 04/13/2021
author: tylermsft
ms.author: twhitney
f1_keywords:
- /headerName
helpviewer_keywords:
- /headerName
- Use header unit IFC
ms.openlocfilehash: cb2b5f6e5a85eb3e14ab3b0139d79fc22b080c37
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381712"
---
# <a name="headername-build-a-header-unit-from-the-specified-header"></a>`/headerName` (从指定的标头生成标题单元) 

将指定的标头文件生成到标题单元中 (*`.ifc`* 文件) 。

## <a name="syntax"></a>语法

> **`/headerName:quote`** `header-filename`\
> **`/headerName:angle`** `header-filename`

### <a name="arguments"></a>参数

*`header-filename`*\
编译器应编译为标题单元 (文件) 的标头文件的名称 *`.ifc`* 。

## <a name="remarks"></a>备注

**`/headerName`** 从 Visual Studio 2019 版本 16.10 preview 2 开始提供了编译器选项。

**`/headerName`** 编译器选项在其所有窗体中都需要 [/std： c + + 最新](std-specify-language-standard-version.md)选项。
如果指定 **`/headerName:{quote,angle}`** ，则还必须指定 [`/exportHeader`](module-exportheader.md) 。

**`/headerName:quote`** 查找 *`header-filename`* 使用与相同的规则 `#include "header-name"` ，并将其生成为标题单元 (*`.ifc`* 文件) 。
**`/headerName:angle`** 查找 *`header-filename`* 使用与相同的规则 `#include <header-name>` ，并将其生成为标题单元 (*`.ifc`* 文件) 。

### <a name="examples"></a>示例

如果某个项目引用了它定义的标头文件 `m.h` ，则将其编译为标题单元的编译器选项如下所示：

```Bash
$ cl /std:c++latest /exportHeader /headerName:quote m.h /Fom.h.obj
```

`/headerName:{quote,angle}`开关的行为类似于标志，并且不显式需要自变量。 下面的示例是有效的：

```Bash
$ cl /std:c++latest /exportHeader /headerName:angle /MP /Fo.\ vector iostream algorithm
$ cl /std:c++latest /exportHeader /headerName:quote /MP /Fo.\ my-utilities.h a/b/my-core.h
```

您可以 `/headerName` 在同一命令行上指定多个开关，该开关之后的每个参数都将用指定的 *`header-filename`* 查找规则进行处理。 下面的示例以相同的方式处理前面两个命令行示例的所有标头。 它使用应用的查找规则查找标头，就好像它们已指定为： `#include <vector>` 、 `#include "my-utilties.h"` 和 `#include "a/b/my-core.h"` ：

```bash
$ cl /std:c++latest /exportHeader /headerName:angle /MP /Fo.\ vector iostream algorithm /headerName:quote my-utilities.h a/b/my-core.h
```

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

> [!NOTE]
> 用户通常不会设置此命令行开关。 它是由生成系统设置的。

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 将 **配置** 下拉箭头设置为 " **所有配置**"。

1. 选择 "**配置属性**" "  >  **c/c + +**  >  **命令行**" 属性页。

1. 修改 " **附加选项** " 属性以添加 *`/headerName`* 选项和参数。 然后，选择 **"确定" 或 "** **应用** " 保存所做的更改。

## <a name="see-also"></a>请参阅

[`/exportHeader` (创建标题单元) ](module-exportheader.md)\
[`/headerUnit` (创建标题单元) ](headerunit.md)\
[`/reference` (使用命名模块 IFC) ](module-reference.md)\
[`/translateInclude`（将 include 指令转换为 import 指令）](translateinclude.md)
