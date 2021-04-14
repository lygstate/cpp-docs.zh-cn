---
title: /sourceDependencies（报告源级别依赖项）
description: 介绍了 Microsoft c + + 中的/sourceDependencies 编译器选项。
ms.date: 04/13/2020
author: tylermsft
ms.author: twhitney
f1_keywords:
- /sourceDependencies
helpviewer_keywords:
- /sourceDependencies compiler option
- /sourceDependencies
ms.openlocfilehash: cf76d6e31abc7328b82b877bf6f3e2545efc7878
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381345"
---
# <a name="sourcedependencies-list-all-source-level-dependencies"></a>`/sourceDependencies` (列出所有源级别的依赖项) 

此命令行开关生成一个 JSON 文件，该文件详细说明在编译期间使用的源级依赖项。 JSON 文件包含源依赖项的列表，其中包括：

- 标头文件。 这两者都是直接包括的，以及这些标头中包含的标头列表。
- 如果) 指定，则使用的 PCH (**`/Yu`** 。
- 导入的模块的名称
- 导入的标头单元的文件路径和名称。 直接导入，由这些模块和标头单元导入的。

这会提供按正确的依赖项顺序生成模块和标头单元所需的信息。

## <a name="syntax"></a>语法

> **`/sourceDependencies`** -\
> **`/sourceDependencies`***filename*\
> **`/sourceDependencies`***目录*

## <a name="arguments"></a>参数

*`-`*\
如果提供了单破折号，则编译器会将源依赖项 JSON 发出到 `stdout` ，或将编译器输出重定向到的位置。

*`filename`*\
编译器会将源依赖项输出写入指定的文件名，其中可能包括相对或绝对路径。

*`directory`*\
如果参数是一个目录，则编译器将在指定的目录中生成源依赖项文件。 输出文件的名称基于输入文件的全名，附加了 *`.json`* 扩展名。 例如，如果为编译器提供的文件是，则 *`main.cpp`* 生成的输出文件名为 *`main.cpp.json`* 。

## <a name="remarks"></a>备注

**`/sourceDependencies`** 编译器选项在 Visual Studio 2019 版本16.7 中开始提供。 默认情况下不启用它。

指定 **`/MP`** 编译器选项时，我们建议你使用 **`/sourceDependencies`** with directory 参数。 如果提供单个 filename 参数，则两个编译器实例可能尝试同时打开输出文件并导致错误。 有关的详细信息 **`/MP`** ，请参阅 [ `/MP`)  (具有多个进程的生成](mp-build-with-multiple-processes.md)。

发生非致命编译器错误时，依赖关系信息仍会写入到输出文件中。

所有文件路径在输出中都显示为绝对路径。

### <a name="examples"></a>示例

给定下面的示例代码：

```cpp
// ModuleE.ixx:
export module ModuleE;
import ModuleC;
import ModuleD;
import <iostream>;
```

你可以将 **`/sourceDependencies`** 与其他编译器选项一起使用：

> `cl ... /sourceDependencies output.json ... main.cpp`

其中 `...` 表示其他编译器选项。 此命令行生成一个 JSON 文件 *`output.json`* ，其中包含类似于以下内容的内容：

```JSON
{
    "Version": "1.1",
    "Data": {
        "Source": "F:\\Sample\\myproject\\modulee.ixx",
        "ProvidedModule": "ModuleE",
        "Includes": [],
        "ImportedModules": [
            {
                "Name": "ModuleC",
                "BMI": "F:\\Sample\\Outputs\\Intermediate\\MyProject\\x64\\Debug\\ModuleC.ixx.ifc"
            },
            {
                "Name": "ModuleB",
                "BMI": "F:\\Sample\\Outputs\\Intermediate\\ModuleB\\x64\\Debug\\ModuleB.ixx.ifc"
            },
            {
                "Name": "ModuleD",
                "BMI": "F:\\Sample\\Outputs\\Intermediate\\MyProject\\x64\\Debug\\ModuleD.cppm.ifc"
            }
        ],
        "ImportedHeaderUnits": [
            {
                "Header": "f:\\visual studio 16 main\\vc\\tools\\msvc\\14.29.30030\\include\\iostream",
                "BMI": "F:\\Sample\\Outputs\\Intermediate\\HeaderUnits\\x64\\Debug\\iostream_W4L4JYGFJ3GL8OG9.ifc"
            },
            {
                "Header": "f:\\visual studio 16 main\\vc\\tools\\msvc\\14.29.30030\\include\\yvals_core.h",
                "BMI": "F:\\Sample\\Outputs\\Intermediate\\HeaderUnits\\x64\\Debug\\yvals_core.h.ifc"
            }
        ]
    }
}
```

我们已使用 `...` 来缩写报告的路径。 该报表将包含绝对路径。 报告的路径取决于编译器查找依赖项的位置。 如果结果不是预期的，则可能需要检查项目的 "包含路径" 设置。

`ProvidedModule` 列出导出的模块或模块分区名称。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

通常不应在 Visual Studio 开发环境中自行设置此项。 它是由生成系统设置的。

## <a name="see-also"></a>请参阅

[MSVC 编译器选项](compiler-options.md)<br/>
[MSVC 编译器命令行语法](compiler-command-line-syntax.md)<br/>
