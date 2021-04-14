---
title: /translateInclude（将 include 指令转换为 import 指令）
description: '使用/translateInclude 编译器选项可在可导入标头单位可用时将 #include 指令视为导入语句。'
ms.date: 4/13/2021
author: tylermsft
ms.author: twhitney
f1_keywords:
- /translateInclude
helpviewer_keywords:
- /translateInclude
- Translate include directives into import directives
ms.openlocfilehash: e700e79c64be466e33e0ee698114c85eba1f7e18
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381294"
---
# <a name="translateinclude-translate-include-directives-into-import-directives"></a>`/translateInclude`（将 include 指令转换为 import 指令）

指示编译器将 `#include` `import` () 文件中预构建为标头单元的标头视为 `.ifc` 。

## <a name="syntax"></a>语法

> **`/translateInclude`**

## <a name="remarks"></a>备注

**`/translateInclude`** 编译器选项要求启用 [/std： c + + 最新](std-specify-language-standard-version.md)选项。 `/translateInclude` 从 Visual Studio 2019 版本 16.10 Preview 2 开始提供。

此 **`/translateInclude`** 选项将有效地进行以下转换，其中示例 `<vector>` 已预建为可导入标头单元：

```cpp
#include <vector>
```

编译器将此指令替换为：

```cpp
import <vector>;
```

在 MSVC 中，可通过选项使用可用的标头单位 **`/headerUnit`** ，这会将标头文件映射到相应的预生成的可导入标头单元。 有关详细信息，请参阅[ `/headerUnit` (指定在何处查找页眉单元文件 (`.ifc` 指定标头的) ) ](headerunit.md)。

### <a name="examples"></a>示例

假设某个项目引用了此表中列出的两个头文件及其标题单元：

| 头文件 | IFC 文件 |
|--|--|
| *`C:\utils\util.h`* | *`C:\util.h.ifc`* |
| *`C:\app\app.h`* | *`C:\app.h.ifc`* |

和 *`.cpp`* 包含标头的源文件

```cpp
#include "utils/util.h"
#include "app/app.h"

int main() { }
```

**`/translateInclude`** 选项允许编译器将 `#include` 作为 `import` 具有对应的已编译标头单元文件 (*`.ifc`*) 并通过开关在命令行上指定的的标头文件 `/headerUnit` 。

如果 `#include` 遇到没有通过开关指定的相应标头单元的情况 `/headerUnit` ，则预处理器会将其作为常规指令进行处理 `#include` 。

 下面是一个示例命令行，用于转换和的 include 指令以 *`util.h`* *`app.h`* 导入标题单元的导入：

```CMD
cl /IC:\ /translateInclude /headerUnit C:\utils\util.h=C:\util.h.ifc /headerUnit C:\app\app.h=C:\app.h.ifc
```

## <a name="to-set-this-compiler-option-in-visual-studio"></a>在 Visual Studio 中设置此编译器选项

若要启用 `/translateInclude` ，请在项目属性中设置 " **翻译包含到导入** " 选项：

1. 在项目属性页的左窗格中，选择 "**配置属性**" "  >  **c/c + +**  >  **常规**"
1. 更改 **转换包含以** 将下拉列表导入到 **"是** 
 ![ 项目属性" 对话框集转换包含到导入](../media/vs2019-translate-includes-option.png)


## <a name="see-also"></a>请参阅

[ `/headerUnit` (使用标题单元 IFC) ](headerunit.md)。
[`/exportHeader` (创建标题单元) ](module-exportheader.md)\
[`/reference`（使用命名模块 IFC）](module-reference.md)
