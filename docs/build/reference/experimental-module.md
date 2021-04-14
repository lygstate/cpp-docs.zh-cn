---
title: '/experimental： module (启用模块支持) '
description: 使用/experimental： module 编译器选项对命名模块启用实验编译器支持。
ms.date: 04/13/2021
f1_keywords:
- module
- /experimental:module
helpviewer_keywords:
- module
- /experimental:module
- Enable module support
ms.openlocfilehash: dd9d3c9f571b50b328dbb52ee4e7561d5684de1f
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381163"
---
# <a name="experimentalmodule-enable-module-support"></a>/experimental： module (启用模块支持) 

为标准模板库命名模块启用实验编译器支持。

## <a name="syntax"></a>语法

> **/experimental： module**[ **-** ]

## <a name="remarks"></a>备注

可以通过将 **`/experimental:module`** 编译器选项与 [/std： c + + 最新](std-specify-language-standard-version.md) 选项一起使用来启用实验性模块支持。 使用 **`/experimental:module-`** 显式禁用模块支持。

从 Visual Studio 2015 Update 1 开始提供此选项。 在 Visual Studio 2019 版本16.2 中，在 Microsoft c + + 编译器中没有完全实现 c + + 20 标准模块草案。 你可以使用模块功能创建单分区模块，并导入 Microsoft 提供的标准库模块。 模块和使用它的代码必须使用相同的编译器选项编译。

有关模块以及如何使用和创建模块的详细信息，请参阅 [c + + 中的模块概述](../../cpp/modules-cpp.md)。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 将 **配置** 下拉箭头设置为 " **所有配置**"。

1. 选择 "**配置属性**" "  >  **c/c + +**  >  **语言**" 属性页。

1. 修改 " **启用 c + + 模块 (试验性)** " 属性，然后选择 **"确定"**。

## <a name="see-also"></a>请参阅

[`/headerUnit` (使用标题单元 IFC) ](headerunit.md)\
[`/exportHeader` (创建标题单元) ](module-exportheader.md)\
[`/reference` (使用命名模块 IFC) ](module-reference.md)\
[`/translateInclude` (将 include 指令转换为导入指令) ](translateinclude.md)\
[`/Zc` (一致性) ](zc-conformance.md)
