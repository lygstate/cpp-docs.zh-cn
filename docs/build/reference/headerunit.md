---
title: /headerUnit（使用标头单位 IFC）
description: 使用/headerUnit 编译器选项，将标头文件与要导入的标头单元关联。
ms.date: 04/13/2021
f1_keywords:
- /headerUnit
helpviewer_keywords:
- /headerUnit
- Use header unit IFC
author: tylermsft
ms.author: twhitney
ms.openlocfilehash: 205809e25644f4beaa0105a2611c7eaa4e6b7b02
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381371"
---
# <a name="headerunit-use-header-unit-ifc"></a>`/headerUnit` （使用标头单元 IFC）

用于导入标题单元。 告诉编译器在何处查找 *`.ifc`* 指定标头的标头单元) 的二进制表示形式的文件 (。

## <a name="syntax"></a>语法

> **`/headerUnit`** *`header-filename`*=*`ifc-filename`*\
> **`/headerUnit:quote`** \[*`header-filename`*=*`ifc-filename`*\]\
> **`/headerUnit:angle`** \[*`header-filename`*=*`ifc-filename`*\]

### <a name="arguments"></a>参数

*`header-filename`*\
在编译器中，将 `import header-name;` 解析 `header-name` 为磁盘上的文件。 用于 *`header-filename`* 指定该文件。 一旦匹配，编译器将打开名为的对应 IFC *`ifc-filename`* 以进行导入。

*`ifc-filename`*\
包含已编译的标头单元信息的文件的名称。 若要导入多个标头单位，请 **`/headerUnit`** 为每个文件添加一个单独的选项。

## <a name="remarks"></a>备注

**`/headerUnit`** 编译器选项需要 [/std： c + + 最新](std-specify-language-standard-version.md)选项。

**`/headerUnit`** 从 Visual Studio 2019 版本 16.10 preview 2 开始提供了编译器选项。

当编译器跨越或时 `import "file";` `import <file>;` ，此编译器开关有助于编译器查找 *`.ifc`* 指定标头文件 () 的已编译标头单元。 可以通过三种方式表示该文件的路径：

**`/headerUnit`** 查找当前目录中的已编译标头单元，或在中指定的位置 *`ifc-filename`* 。

**`/headerUnit:quote`** 使用与相同的规则查找已编译的标头单元文件 `#include "file"` 。

**`/headerUnit:angle`** 使用与相同的规则查找已编译的标头单元文件 `#include <file>` 。

编译器无法将单个文件映射 *`header-name`* 到多个 *`.ifc`* 文件。 虽然可以将多个 *`header-name`* 自变量映射到单个参数 *`.ifc`* ，但我们不建议这样做。 导入的内容将 *`.ifc`* 导入，就好像它只是由指定的标头 *`header-name`* 。

使用此开关时，编译器将隐式启用新的预处理器。 也就是说， [`/Zc:preprocessor`](zc-preprocessor.md) 如果 `/headerUnit` 在命令行上指定了任何形式的，编译器会将它添加到命令行。 若要选择退出隐式 `/Zc:preprocessor` ，请指定： `/Zc:preprocessor-`

如果禁用新的预处理器，但编译的文件会导入标题单元，则编译器将报告错误。

### <a name="examples"></a>示例

假设某个项目引用了此表中列出的两个头文件及其标题单元：

| 头文件 | IFC 文件 |
|--|--|
| *`C:\utils\util.h`* | *`C:\util.h.ifc`* |
| *`C:\app\app.h`* | *`C:\app\app.h.ifc`* |

用于引用这些特定标头文件的标头单元的编译器选项如下所示：

```CMD
cl ... /std:c++latest /headerUnit C:\utils\util.h=C:\util.h.ifc /headerUnit:quote app.h=app.h.ifc
```

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

通常不应在 Visual Studio 开发环境中设置此项。 它是由生成系统设置的。

## <a name="see-also"></a>请参阅

[`/exportHeader` (创建标题单元) ](module-exportheader.md)\
[`/headerName` (从指定的标头创建标题单元) ](headername.md)\
[`/reference`（使用命名模块 IFC）](module-reference.md)
