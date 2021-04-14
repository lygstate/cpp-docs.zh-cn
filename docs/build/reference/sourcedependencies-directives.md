---
title: '/sourceDependencies： (列出模块和标头单元依赖关系的指令) '
description: Microsoft c + + 中/sourceDependencies：指令编译器选项的参考指南。
ms.date: 04/13/2020
author: tylermsft
ms.author: twhitney
f1_keywords:
- /sourceDependencies:directives
helpviewer_keywords:
- /sourceDependencies:directives compiler option
- /sourceDependencies:directives
ms.openlocfilehash: ecc2b107eae6a4f2a331084d7fe9813f34277915
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381711"
---
# <a name="sourcedependenciesdirectives-list-module-and-header-unit-dependencies"></a>`/sourceDependencies:directives` (List) 模块和标头单元依赖关系

此命令行开关生成一个 JSON 文件，其中列出了模块和标头单元依赖关系。

它标识了在编译使用它们的项目之前需要编译的模块和标头单元。 例如，它将列出 `import <library>;` 或 `import "library";` 作为标题单元依赖项，并 `import name;` 作为模块依赖项列出。

此命令行选项类似于 [`/sourceDependencies`](sourcedependencies.md) ，但在以下方面有所不同：

- 编译器不会生成编译的输出。 相反，将扫描文件中的模块指令。 不生成编译的代码、模块或标头单元。
- 输出 JSON 文件不会列出导入的模块和导入的标头单元 (*`.ifc`* 文件) 因为此开关对项目文件进行扫描，而不是进行编译。 因此没有要列出的生成模块或标头单元。
- 仅列出直接导入的模块或标头单元。 它不会列出导入的模块或标题单元本身的依赖项。
- 标头文件依赖项未列出。 `#include <file>` `#include "file"` 未列出或依赖项。
- `/sourceDependencies:directives`应在生成文件之前使用 *`.ifc`* 。

## <a name="syntax"></a>语法

> **`/sourceDependencies:directives`** -\
> **`/sourceDependencies:directives`***filename*\
> **`/sourceDependencies:directives`***目录*\

## <a name="arguments"></a>参数

*`-`*\
如果提供了单破折号，则编译器会将源依赖项 JSON 发出到 `stdout` ，或将编译器输出重定向到的位置。

*`filename`*\
编译器会将源依赖项输出写入指定的文件名，其中可能包括相对或绝对路径。

*`directory`*\
如果参数是一个目录，则编译器将在指定的目录中生成源依赖项文件。 输出文件的名称基于输入文件的全名，附加了 *`.json`* 扩展名。 例如，如果为编译器提供的文件是，则 *`main.cpp`* 生成的输出文件名为 *`main.cpp.json`* 。

## <a name="remarks"></a>备注

**`/sourceDependencies:directives`** 从 Visual Studio 2019 版本 16.10 Preview 2 开始提供。 默认情况下不启用它。

指定 **`/MP`** 编译器选项时，我们建议你使用 **`/sourceDependencies`** with directory 参数。 如果提供单个 filename 参数，则两个编译器实例可能尝试同时打开输出文件并导致错误。 有关的详细信息 **`/MP`** ，请参阅 [ `/MP`)  (具有多个进程的生成](mp-build-with-multiple-processes.md)。

发生非致命编译器错误时，依赖关系信息仍会写入到输出文件中。

所有文件路径在输出中都显示为绝对路径。

### <a name="examples"></a>示例

给定下面的示例代码：

```cpp
//main.cpp:
#include <vector>

import m;
import std.core;

import <utility>;

import "t.h";

int main() {}
```

> `cl /std:c++latest /sourceDependencies:directives output.json main.cpp`

此命令行生成一个 JSON 文件 *`output.json`* ，其中包含类似于以下内容的内容：

```JSON
{
   "Version":"1.1",
   "Data":{
      "Source":"C:\\a\\b\\main.cpp",
      "ProvidedModule":"",
      "ImportedModules":[
         "m",
         "std.core"
      ],
      "ImportedHeaderUnits":[
         "C:\\...\\utility",
         "C:\\a\\b\\t.h"
      ]
   }
}
```

我们已使用 `...` 来缩写报告的路径。 该报表将包含绝对路径。 报告的路径取决于编译器查找依赖项的位置。 如果结果不是预期的，则可能需要检查项目的 "包含路径" 设置。

`ProvidedModule` 列出导出的模块或模块分区名称。

*`.ifc`* 输出中未列出任何文件，因为它们未生成。 与不同的 `/sourceDependencies` 是，在指定时，编译器不会生成编译的输出 `/sourceDependencies:directives` ，因此不会生成任何已编译的模块或标头单元以进行导入。

## <a name="to-set-this-compiler-option-in-visual-studio"></a>在 Visual Studio 中设置此编译器选项

通常不应在 Visual Studio 开发环境中自行设置此项。 它是由生成系统设置的。

## <a name="see-also"></a>请参阅

[MSVC 编译器选项](compiler-options.md)\
[MSVC 编译器命令行语法](compiler-command-line-syntax.md)