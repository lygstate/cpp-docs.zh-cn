---
title: 在 Visual Studio 中安装 C11 和 C17 支持
description: 在 Visual Studio 中安装对 C11 和 C17 的 Windows SDK 和 CRT 支持
ms.date: 09/11/2020
helpviewer_keywords:
- Install preview Windows SDK
ms.assetid: 45138d70-719d-42dc-90d7-1d0ca31a2f54
ms.openlocfilehash: 84e3e17c7d65fc129e789634e6cf0b442565e26b
ms.sourcegitcommit: bf6d8a220f6392f1f19c0c0605d1467d0221ef6c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105551743"
---
# <a name="install-c11-and-c17-support-in-visual-studio"></a>在 Visual Studio 中安装 C11 和 C17 支持

::: moniker range="<=msvc-150"

支持 C11 和 C17 标准需要 Visual Studio 2019 16.8 或更高版本。 若要查看此版本对应的文档，请将本文的 Visual Studio“版本”选择器控件设置为“Visual Studio 2019”。 它位于此页面上目录表的顶部。

::: moniker-end

::: moniker range="msvc-160"

从 Visual Studio 2019 版本 16.8 开始，提供对 C11 和 C17 的支持。 支持需要更新的通用 C 运行时 (UCRT) 和最新的 Windows SDK 更新，才能正确地使用一致的预处理器 ([`/Zc:preprocessor`](../build/reference/zc-preprocessor.md))。

Windows SDK 版本与 Windows OS 版本相对应。 由于 Windows 版本未进行这些更改，因此需要 *Insider Preview Windows SDK*。 这是 Windows SDK 的预览版本，它与当前由 Windows Insider 外部测试的 Windows 版本相对应。 安装 Insider Preview Windows 10 SDK 后，配置为使用最新的 Windows SDK 的 Visual Studio 项目将使用 Insider Preview。

## <a name="prerequisites"></a>先决条件

- Visual Studio 2019 版本 16.8 或更高版本已安装并正在你的计算机上运行。 在安装中，包括“使用 C++ 的桌面开发”工作负载。 可以从 [Visual Studio 预览版](https://visualstudio.microsoft.com/vs/preview/)页中下载最新预览版。 如果尚未安装 Visual Studio，请参阅[在 Visual Studio 中安装 C++ 支持](../build/vscpp-step-0-installation.md)以获取安装说明。

## <a name="step-1-sign-in-by-using-an-insider-microsoft-account"></a>步骤 1：使用 Insider Microsoft 帐户登录

任何人都可以创建免费的 [Microsoft 帐户](https://signup.live.com/)，然后选择加入 Insider 计划。 转到[面向开发人员的 Windows Insider 计划](https://insider.windows.com/for-developers)页，选择“注册”，然后登录。

注册后，会向你提供开始外部测试 Windows 的 Insider 版本的选项。 此步骤不是下载和使用 Insider Windows 10 SDK 所必需的。 注册 Windows Insider 后，不会自动选择加入计算机来下载新的 Windows 外部测试。

转到“欢迎使用 Windows Insider 计划”页后，无需选择“立即外部测试”。 继续执行下一步以下载 Insider Preview Windows 10 SDK。

## <a name="step-2-download-the-insider-preview-windows-10-sdk"></a>步骤 2：下载 Insider Preview Windows 10 SDK

可以从 [Windows Insider Preview 下载](https://www.microsoft.com/software-download/windowsinsiderpreviewSDK)页安装 Insider Preview Windows SDK。 如果看到一条消息指出“你需要成为 Windows Insider 计划的成员”，请确保你已登录。 使用用于 Insider 计划的同一 Microsoft 帐户。 如果看到一条消息指出“很抱歉，找不到你请求的页面”，请尝试将 URL 中的区域设置更改为“en-us”。

Insider 页面声明需要使用 Windows 10 Insider Preview OS。 它仅适用于 Windows SDK 中包含的某些内容。 该内容可能依赖于 Windows 旧版本中不存在的新 API。 但是，Windows 和通用 C 运行时标头可以在没有 Insider OS 的情况下安装和使用。

选择“获取 SDK Insider Preview - 内部版本 20211”（或更高版本）开始下载。 Windows SDK 的更高版本也可行。

## <a name="step-3-install-the-insider-preview-windows-10-sdk"></a>步骤 3：安装 Insider Preview Windows 10 SDK

Insider Preview Windows SDK 下载为 `.iso` 文件。 在文件资源管理器中打开包含已下载文件的文件夹。 装载 `.iso` 文件，然后运行 `WinSDKSetup.exe` 以开始安装。

在“指定位置”页上，选择“将 Windows 软件开发工具包 - \<version> 安装到此计算机中”，然后选择“下一步”。 在“Windows 工具包隐私”页上，选择是否允许 Microsoft 收集 Windows 10 工具包的见解，然后选择“下一步”。 选择“接受”以接受许可协议。 在“选择要安装的功能”页上，仅选择以下功能：  

- 适用于桌面应用的 Windows SDK 签名工具

- 适用于 UWP 托管应用的 Windows SDK

- 适用于 UWP C++ 应用的 Windows SDK

- 适用于桌面 C++ X86 应用的 Windows SDK（如果计划针对 x86 生成）

- 适用于桌面 C++ amd64 应用的 Windows SDK（如果计划针对 amd64 生成）

- 适用于桌面 C++ arm 应用的 Windows SDK（如果计划针对 arm 生成）

- 适用于桌面 C++ arm64 应用的 Windows SDK（如果计划针对 arm64 生成）

![Windows SDK 安装程序的屏幕截图，其中显示为安装选择的组件](media/c11-7-windows-sdk-installer-select-features.png)

选择“安装”以安装所选的 SDK 组件。 SDK 需要几分钟时间才能完成安装。 完成后，打开 Visual Studio。

## <a name="step-4-configuring-c11-or-c17-mode-in-visual-studio"></a>步骤 4：在 Visual Studio 中配置 C11 或 C17 模式

在 Visual Studio 中，打开新的或现有的 C 项目，然后打开项目的“属性页”对话框。

将项目设置为使用 Insider Preview Windows 10 SDK。 在“配置属性” > “常规”页上，将“Windows SDK 版本”属性设置为 10.0（最新安装的版本），或设置为你安装的特定预览版本。

你还将看到一个新选项：C 语言标准。 将此属性设置为“ISO C11 标准(`/std:c11`)”或“ISO C17 (2018)标准(`/std:c17`)”。  

![“配置属性”的“常规”页上的“属性页”对话框的屏幕截图，其中显示 C 语言标准属性下拉选项，如 ISO C 17](media/c11-9-project-property-page-c-language-standard.png)

语言为 C++ 时使用 C++ 语言标准。 当文件扩展名为 *`.cpp`* 时，这是默认设置。 语言为 C 时使用 C 语言标准版本。当文件扩展名为 *`.c`* 时，这是默认设置。 若要使用 C11 或 C17 生成，请将源代码放在 `.c` 文件中，或将代码设置为“编译为 C”。可以在“配置属性” > “C/C++” > “高级”页上设置项目的此属性。 将“编译为”属性设置为“编译为 C 代码(/TC)”。

恭喜，你已完成在 Visual Studio 中生成 C11 和 C17 代码所需的所有设置！

## <a name="see-also"></a>请参阅

[`/std`（指定语言标准版本）](../build/reference/std-specify-language-standard-version.md)

::: moniker-end
