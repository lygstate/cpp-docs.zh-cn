---
description: 详细了解：操作说明：修改目标框架和平台工具集
title: 如何：修改目标框架和平台工具集
ms.custom: contperf-fy21q3
ms.date: 03/31/2021
helpviewer_keywords:
- 'msbuild (c++), howto: modify target framework and platform toolset'
ms.openlocfilehash: 3242b79f2b939d2b668a9bcd7d13ea80c424d2fe
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099321"
---
# <a name="how-to-modify-the-target-framework-and-platform-toolset"></a>如何：修改目标框架和平台工具集

可以编辑 Visual Studio C++ 项目文件以面向不同版本的 C++ 平台工具集。 使用的 Windows SDK 和 .NET Framework 也是可编辑的。 （.NET Framework 仅适用于 C++/CLI 项目）。 新项目使用默认 .NET Framework 和你用于创建项目的 Visual Studio 版本的工具集。 如果在 .vcxproj 文件中修改所有这些值，可以对每个编译目标使用相同的代码库。

## <a name="platform-toolset"></a>平台工具集

平台工具集包含 C++ 编译器 (cl.exe) 和链接器 (link.exe) 以及 C/C++ 标准库。 Visual Studio 2015、Visual Studio 2017 和 Visual Studio 2019 是二进制兼容的。 这由工具集的主版本（仍为 14）显示。 在 Visual Studio 2019 或 Visual Studio 2017 中编译的项目与 2017 和 2015 项目 ABI 后向兼容。 自 Visual Studio 2015 以来，次版本对于每个版本都按 1 更新：

- Visual Studio 2015：v140
- Visual Studio 2017：v141
- Visual Studio 2019：v142

这些工具集支持 .NET Framework 4.5 及更高版本。

Visual Studio 还对 C++ 项目支持多定向。 可以使用最新 Visual Studio IDE 编辑和生成使用较旧版本的 Visual Studio 创建的项目。 无需将项目升级为使用新版工具集。 需要在计算机上安装旧版工具集。 有关详细信息，请参阅[如何在 Visual Studio 中使用本机多定向](../porting/use-native-multi-targeting.md)。 例如，在 Visual Studio 2015 中，可以面向 .NET Framework 2.0，但必须使用支持它的早期工具集。

## <a name="target-framework-ccli-project-only"></a>目标框架（仅限 C++/CLI 项目）

在更改目标 Framework 时，也要将平台工具集更改为支持该 Framework 的版本。 例如，要面向 .NET Framework 4.5，必须使用兼容的平台工具集。 这些工具集包括 Visual Studio 2015 (v140)、Visual Studio 2013 (v120) 和 Visual Studio 2012 (v110)。 可以使用 [Windows 7.1 SDK](https://www.microsoft.com/download/details.aspx?id=8279) 面向 .NET Framework 2.0、3.0、3.5 和 4。

可以通过创建自定义平台工具集来扩展目标平台。 有关详细信息，请参见 Visual C++ 博客上的 [C++ 本机多目标](https://devblogs.microsoft.com/cppblog/c-native-multi-targeting/) 。

### <a name="to-change-the-target-framework"></a>更改目标框架

1. 在 Visual Studio 中，在“解决方案资源管理器”  中，选择你的项目。 在菜单栏上，打开“项目”  菜单并选择“卸载项目”  。 此命令将为你的项目卸载项目文件 (.vcxproj)。

   > [!NOTE]
   >  在 Visual Studio 中编辑项目文件时不能加载 C++ 项目。 但是，当项目加载到 Visual Studio 中时，你可以使用另一个编辑器（如记事本）来修改项目文件。 Visual Studio 会检测到项目文件的更改并提示你重新加载项目。

1. 在菜单栏上，依次选择 **“文件”** 、 **“打开”** 、 **“文件”** 。 在 **“打开文件”** 对话框中，导航到项目文件夹，然后打开项目文件 (.vcxproj)。

1. 在项目文件中，找到目标 Framework 版本的条目。 例如，如果你的项目设计为使用 .NET Framework 4.5，请在 `<TargetFrameworkVersion>v4.5</TargetFrameworkVersion>` 元素的 `<PropertyGroup Label="Globals">` 元素中找到 `<Project>` 。 如果 `<TargetFrameworkVersion>` 元素不存在，你的项目不使用 .NET Framework，也无需进行更改。

1. 将值更改为需要的 Framework 版本，例如 v3.5 或 v4.6。

1. 保存更改并关闭编辑器。

1. 在 **“解决方案资源管理器”** 中，打开项目的快捷菜单，然后选择 **“重新加载项目”** 。

1. 若要验证更改，请在菜单栏上选择“项目” >  “属性”以打开项目“属性页”对话框。 在该对话框中，选择“配置属性” > “常规”属性页。 验证“.NET 目标 Framework 版本”  是否显示了新的 Framework 版本。

### <a name="to-change-the-platform-toolset"></a>更改平台工具集

1. 在 Visual Studio 中，在菜单栏上选择“项目” >  “属性”以打开项目“属性页”对话框。

1. 在“属性页”对话框顶部，打开“配置”下拉列表，然后选择“所有配置”。  

1. 在该对话框中，选择“配置属性” > “常规”属性页。

1. 在属性页中，选择“平台工具集”，然后从下拉列表中选择需要的工具集。 例如，如果已安装了 Visual Studio 2010 工具集，请选择“Visual Studio 2010 (v100)”以用于项目。

1. 选择“确定”按钮以保存更改。

## <a name="next-steps"></a>后续步骤

[演练：使用项目和解决方案 (C++)](../ide/walkthrough-working-with-projects-and-solutions-cpp.md)

## <a name="see-also"></a>请参阅

[命令行上的 MSBuild - C++](msbuild-visual-cpp.md)
