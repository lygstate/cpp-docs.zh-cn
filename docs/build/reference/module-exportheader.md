---
title: '/exportHeader (创建标题单元) '
description: 使用/exportHeader 编译器选项可为指定的标头名称或包含文件创建模块标头单元。
ms.date: 04/13/2020
author: tylermsft
ms.author: twhitney
f1_keywords:
- /exportHeader
helpviewer_keywords:
- /exportHeader
- Create header units
ms.openlocfilehash: c116b3786b17f0a4574acff01b661a212767aa68
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381332"
---
# <a name="exportheader-create-header-units"></a>`/exportHeader`（创建标头单元）

指示编译器创建由输入参数指定的标头单元。 编译器将标题单元生成为 IFC (*`.ifc`*) 文件。

## <a name="syntax"></a>语法

> **`/exportHeader /headerName:angle`** *`header-name`*
> **`/exportHeader /headerName:quote`** *`header-name`*
> **`/exportHeader`** *`full path to header file`*

### <a name="arguments"></a>参数

的参数 `/exportHeader` 是一个 `/headerName` 命令行选项，该选项指定  *`header-name`* 要导出的标头文件的名称。  

## <a name="remarks"></a>备注

**`/exportHeader`** 从 Visual Studio 2019 版本 16.10 Preview 2 开始提供。

**`/exportHeader`** 编译器选项要求启用 [/std： c + + 最新](std-specify-language-standard-version.md)选项。 

一个 **`/exportHeader`** 编译器选项可以指定您的生成所需的标头名称参数数量。 不需要单独指定它们。

使用此开关时，编译器将隐式启用新的预处理器。 也就是说， [`/Zc:preprocessor`](zc-preprocessor.md) 如果 `/exportHeader` 在命令行上使用任何形式的，编译器会将它添加到命令行。 若要选择退出隐式 `/Zc:preprocessor` ，请使用： `/Zc:preprocessor-`

默认情况下，编译标题单元时，编译器不会生成对象文件。 若要生成对象文件，请指定 **`/Fo`** 编译器选项。 有关详细信息，请参阅[ `/Fo` (对象文件名) ](fo-object-file-name.md)。

你可能会发现，使用互补选项非常有用 **`/showResolvedHeader`** 。 **`/showResolvedHeader`** 选项打印 *`header-name`* 自变量解析到的文件的绝对路径。

**`/exportHeader`** 可以一次处理多个输入，即使在下也是如此 **`/MP`** 。 建议使用 **`/ifcOutput  <directory>`** 为每个编译创建一个单独的 *`.ifc`* 文件。

### <a name="examples"></a>示例

若要生成标题单元，如 `<vector>` ：

```cmd
cl … /std:c++latest /exportHeader /headerName:angle vector
```

生成本地项目标题，如 `"utils/util.h"` ：

```cmd
cl … /std:c++latest /exportHeader /headerName:quote util/util.h
```

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

通常不应在 Visual Studio 开发环境中设置此项。 它是由生成系统设置的。

## <a name="see-also"></a>请参阅

[`/headerUnit` (使用标题单元 IFC) ](headerunit.md)\
[`/reference` (使用命名模块 IFC) ](module-reference.md)\
[`/translateInclude`（将 include 指令转换为 import 指令）](translateinclude.md)
