---
description: 了解详细信息：使用 WRL 和媒体基础创建 UWP 应用
title: 演练：使用 WRL 和媒体基础创建 UWP 应用
ms.date: 04/15/2021
ms.topic: reference
ms.openlocfilehash: 823d5d53da5d67f79cb4f79e24560d6d581772c3
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539285"
---
# <a name="walkthrough-creating-a-uwp-app-using-wrl-and-media-foundation"></a>演练：使用 WRL 和媒体基础创建 UWP 应用

> [!NOTE]
> 对于新的 UWP 应用和组件，我们建议你使用 [c + +/WinRT](/windows/uwp/cpp-and-winrt-apis/)，这是一个新的标准 c + + 17 语言投影，适用于 Windows 运行时 api。 C++/WinRT 从版本 1803 起在 Windows 10 SDK 中提供。 C++/WinRT 完全在头文件中实现，旨在提供对新式 Windows API 的优先访问权限。

在本教程中，你将了解如何使用 Windows 运行时 c + + 模板库 (WRL) 创建使用 [ (](/windows/win32/medfound/microsoft-media-foundation-sdk)的通用 WINDOWS 平台) UWP Microsoft 媒体基础应用。

此示例将创建一个自定义媒体基础转换。 它将灰度效果应用于从网络摄像机中捕获的图像。 该应用利用 C++ 定义自定义转换，并利用 C# 将该组件用于转换捕捉的图像。

> [!NOTE]
> 除了 C#，你也可以利用 JavaScript、Visual Basic 或 C++ 来使用自定义转换组件。

通常可以使用 c + +/CX 创建 Windows 运行时组件。 但是，有时您必须使用 WRL。 例如，在为 Microsoft 媒体基础创建媒体扩展时，必须创建同时实现 COM 和 Windows 运行时接口的组件。 由于 c + +/CX 只能创建 Windows 运行时对象，若要创建媒体扩展，必须使用 WRL。 这是因为它可以实现 COM 接口和 Windows 运行时接口。

> [!NOTE]
> 尽管此代码示例很长，但它演示了创建有用的媒体基础转换所需的最低要求。 你可以将它作为自己的自定义转换的起点。 此示例与 [media extensions 示例](https://github.com/Microsoft/VCSamples/tree/master/VC2012Samples/Windows%208%20samples/C%2B%2B/Windows%208%20app%20samples)进行了调整，该示例使用媒体扩展将效果应用于视频和解码视频，并创建生成媒体流的方案处理程序。

## <a name="prerequisites"></a>先决条件

- 在 Visual Studio 2017 和更高版本中，UWP 支持是一个可选组件。 若要安装它，请从 Windows "开始" 菜单打开 Visual Studio 安装程序，并找到你的 Visual Studio 版本。 选择 " **修改** "，然后确保选中 " **通用 Windows 平台开发** " 磁贴。 在 " **可选组件** " 下，查看 **适用于 uwp 的 c + + 工具 (** 用于 visual studio 2017 的 V141) ，或 visual studio 2019 的 **c + + 工具 (v142)** 。 然后检查要使用的 Windows SDK 的版本。

- [Windows 运行时](/uwp/api/)的经验。

- 熟悉 COM。

- 网络摄像机。

## <a name="key-points"></a>要点

- 要创建自定义媒体基础组件，请使用 Microsoft 接口定义语言 (MIDL) 定义文件定义一个接口，实现该接口，然后使其可从其他组件激活。

- `namespace`和 `runtimeclass` 特性以及 `NTDDI_WIN8` [version](/windows/win32/Midl/version)特性值是使用 WRL 的媒体基础组件的 MIDL 定义的重要部分。

- [`Microsoft::WRL::RuntimeClass`](runtimeclass-class.md) 自定义媒体基础组件的基类。 [ `Microsoft::WRL::RuntimeClassType::WinRtClassicComMix]` (runtimeclasstype-enumeration.md) 枚举值作为模板参数提供，用于将类标记为用作 Windows 运行时类和经典 COM 运行时类。

- [`InspectableClass`](inspectableclass-macro.md)宏实现基本 COM 功能，如引用计数和 `QueryInterface` 方法，并设置运行时类名称和信任级别。

- 使用 [`Microsoft::WRL::Module`](module-class.md) 类实现 DLL 入口点函数 [`DllGetActivationFactory`](/windows/win32/winrt/functions) ，例如、 [`DllCanUnloadNow`](/windows/win32/api/combaseapi/nf-combaseapi-dllcanunloadnow) 和 [`DllGetClassObject`](/windows/win32/api/combaseapi/nf-combaseapi-dllgetclassobject) 。

- 将组件 DLL 链接到 *`runtimeobject.lib`* 。 还 [`/WINMD`](../../cppcx/compiler-and-linker-options-c-cx.md) 在链接器行上指定生成 Windows 元数据。

- 使用项目引用可使 WRL 组件可用于 UWP 应用。

### <a name="to-use-the-wrl-to-create-the-media-foundation-grayscale-transform-component"></a>使用 WRL 创建媒体基础灰度转换组件

1. 在 Visual Studio 中，创建一个 **空白解决方案** 项目。 为该项目命名，例如， *MediaCapture*。

1. 将 **(通用 Windows)** 项目中的 DLL 添加到解决方案。 为该项目命名，例如， *GrayscaleTransform*。

1. 将 **MIDL 文件 ( .idl)** 文件添加到项目。 为文件命名，例如 *`GrayscaleTransform.idl`* 。

1. 将以下代码添加到 GrayscaleTransform：

   [!code-cpp[wrl-media-capture#1](../codesnippet/CPP/walkthrough-creating-a-windows-store-app-using-wrl-and-media-foundation_1.idl)]

1. 使用以下代码替换的内容 *`pch.h`* ：

   [!code-cpp[wrl-media-capture#2](../codesnippet/CPP/walkthrough-creating-a-windows-store-app-using-wrl-and-media-foundation_2.h)]

1. 向项目中添加一个新的头文件，将其命名为 *`BufferLock.h`* ，然后将内容替换为以下代码：

   [!code-cpp[wrl-media-capture#3](../codesnippet/CPP/walkthrough-creating-a-windows-store-app-using-wrl-and-media-foundation_3.h)]

1. *`GrayscaleTransform.h`* 在此示例中未使用。 如有需要，可以将其从项目中删除。

1. 使用以下代码替换的内容 *`GrayscaleTransform.cpp`* ：

   [!code-cpp[wrl-media-capture#4](../codesnippet/CPP/walkthrough-creating-a-windows-store-app-using-wrl-and-media-foundation_4.cpp)]

1. 向项目中添加一个新的模块定义文件，将其命名为 *`GrayscaleTransform.def`* ，然后添加以下代码：

   ```idl
   EXPORTS
       DllCanUnloadNow                     PRIVATE
       DllGetActivationFactory             PRIVATE
       DllGetClassObject                   PRIVATE
   ```

1. 使用以下代码替换的内容 `dllmain.cpp` ：

   [!code-cpp[wrl-media-capture#6](../codesnippet/CPP/walkthrough-creating-a-windows-store-app-using-wrl-and-media-foundation_6.cpp)]

1. 在项目的 " **属性页** " 对话框中，设置以下 **链接器** 属性。

   1. 在 " **输入**" 下，为 **模块定义文件** 指定 `GrayScaleTransform.def` 。

   1. 此外，在 " **输入**" 下，将 `runtimeobject.lib` 、 `mfuuid.lib` 和添加 `mfplat.lib` 到 " **其他依赖项** " 属性。

   1. 在 " **Windows 元数据**" 下，将 "**生成 Windows 元数据**" 设置为 **"是 (/WINMD)**

### <a name="to-use-the-wrl-the-custom-media-foundation-component-from-a-c-app"></a>在 c # 应用中使用 WRL 自定义媒体基础组件

1. 将新的 **c # 空白应用 (通用 Windows)** 项目添加到 `MediaCapture` 解决方案。 为该项目命名，例如， *MediaCapture*。

1. 在 **MediaCapture** 项目中，添加对项目的引用 `GrayscaleTransform` 。 若要了解如何操作，请参阅 [如何：使用引用管理器添加或删除引用](/visualstudio/ide/how-to-add-or-remove-references-by-using-the-reference-manager)。

1. 在 *`Package.appxmanifest`* 的 " **功能** " 选项卡上，选择 " **麦克风** 和 **网络摄像机**"。 从网络摄像头中捕捉照片时需要这两项功能。

1. 在中 *`MainPage.xaml`* ，将以下代码添加到根 [`Grid`](/uwp/api/windows.ui.xaml.controls.grid) 元素：

   [!code-xml[wrl-media-capture#7](../codesnippet/Xaml/walkthrough-creating-a-windows-store-app-using-wrl-and-media-foundation_7.xaml)]

1. 使用以下代码替换的内容 `MainPage.xaml.cs` ：

   [!code-cs[wrl-media-capture#8](../codesnippet/CSharp/walkthrough-creating-a-windows-store-app-using-wrl-and-media-foundation_8.cs)]

下图显示了 `MediaCapture app` 。

![捕获照片的 MediaCapture 应用程序的屏幕截图。](../media/wrl_media_capture.png "WRL_Media_Capture")

## <a name="next-steps"></a>后续步骤

该示例演示如何从默认网络摄像头逐张捕捉照片。 [媒体扩展示例](https://github.com/Microsoft/VCSamples/tree/master/VC2012Samples/Windows%208%20samples/C%2B%2B/Windows%208%20app%20samples)执行的功能更多。 它演示如何枚举网络摄像机设备并使用本地方案处理程序。 该示例还演示了对单独的照片和视频流使用的其他媒体效果。

## <a name="see-also"></a>另请参阅

[Windows 运行时 c + + 模板库 (WRL) ](windows-runtime-cpp-template-library-wrl.md)\
[Microsoft 媒体基础](/windows/win32/medfound/microsoft-media-foundation-sdk)
