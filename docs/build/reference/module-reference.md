---
title: '/reference (使用 named module IFC) '
description: 使用/reference 编译器选项可为指定的标头名称或包含文件创建模块标头单元。
ms.date: 04/13/2020
f1_keywords:
- /reference
helpviewer_keywords:
- /reference
- Use named module IFC
ms.openlocfilehash: 00b8938e270ff6e6cd0fc29580b0e8b278888eaa
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381319"
---
# <a name="reference-use-named-module-ifc"></a>`/reference`（使用命名模块 IFC）

通知编译器使用现有的 IFC (*`.ifc`*) 用于当前编译。

## <a name="syntax"></a>语法

> **`/reference`** *`module-name=filename`*\
> **`/reference`** *`filename`*

### <a name="arguments"></a>参数

*`filename`*\
包含 *IFC 数据* 的文件的名称，它是预生成的模块信息。 若要导入多个模块，请 **`/reference`** 为每个文件包含单独的选项。

*`module-name`*\
导出的主模块接口单位名称或完整模块分区名称的有效名称。

## <a name="remarks"></a>备注

在大多数情况下，无需指定此开关，因为项目系统会在解决方案中自动发现模块依赖项。

**`/reference`** 编译器选项要求启用 [/std： c + + 最新](std-specify-language-standard-version.md)选项。 **`/reference`** 从 Visual Studio 2019 版本 16.10 Preview 2 开始提供选项。

如果 **`/reference`** 参数不是 *`filename`* ，则在 *`module-name`* 运行时将打开该文件，以验证 *`filename`* 参数是否命名了特定的导入。 在具有许多参数的情况下，它可能会导致运行时性能较慢 **`/reference`** 。

*`module-name`* 必须是有效的主模块接口单元名称或完整的模块分区名称。 主模块接口名称的示例包括：

- `M`
- `M.N.O`
- `MyModule`
- `my_module`

完整模块分区名称的示例包括：

- `M:P`
- `M.N.O:P.Q`
- `MyModule:Algorithms`
- `my_module:algorithms`

如果使用创建模块引用，则在 *`module-name`* 编译器遇到此名称的导入时，命令行上的其他模块不会得到搜索。 例如，给定以下命令行：

```cmd
cl ... /std:c++latest /reference m.ifc /reference m=n.ifc
```

在上述情况下，如果编译器发现， `import m;` 则 *`m.ifc`* 不会搜索。

### <a name="examples"></a>示例

此表中列出了三个模块：

| 模块 | IFC 文件 |
|--|--|
| *`M`* | *`m.ifc`* |
| *`M:Part1`* | *`m-part1.ifc`* |
| *`Core.Networking`* | *`Networking.ifc`* |

使用参数的引用选项 *`filename`* 如下所示：

```cmd
cl ... /std:c++latest /reference m.ifc /reference m-part.ifc /reference Networking.ifc
```

使用的引用选项 *`module-name=filename`* 如下所示：

```cmd
cl ... /std:c++latest /reference m=m.ifc /reference M:Part1=m-part.ifc /reference Core.Networking=Networking.ifc
```

## <a name="see-also"></a>请参阅

[`/sourceDependencies:directives` (List) 模块和标头单元依赖关系 ](sourcedependencies-directives.md)\
[`/headerUnit` (使用标题单元 IFC) ](headerunit.md)\
[`/exportHeader`（创建标头单元）](module-exportheader.md)
