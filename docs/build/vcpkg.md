---
title: vcpkg：用于 Windows、Linux 和 macOS 的 C++ 包管理器
description: vcpkg 是一种命令行包管理器，可极大简化 Windows、macOS 和 Linux 上开源 C++ 库的购置与安装。
ms.custom: contperf-fy21q2
ms.date: 12/11/2020
ms.topic: overview
ms.technology: cpp-ide
ms.openlocfilehash: 23ad9b34a04791181b83bcae3d413d6dfe0eed00
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099594"
---
# <a name="vcpkg-a-c-package-manager-for-windows-linux-and-macos"></a>vcpkg：用于 Windows、Linux 和 macOS 的 C++ 包管理器

Vcpkg 是适用于 C 和 C++ 库的跨平台命令行包管理器。 它简化了 Windows、Linux 和 macOS 上第三方库的购置与安装。 如果项目要使用第三方库，建议通过 vcpkg 来安装它们。 vcpkg 同时支持开源和专有库。 已测试 vcpkg Windows 目录中所有库与 Visual Studio 2015、Visual Studio 2017 及 Visual Studio 2019 的兼容性。 在 Windows 和 Linux/macOS 目录之间，vcpkg 现已支持数千个库。 C++ 社区会不断向两个目录添加更多的库。

## <a name="how-to-get-and-use-vcpkg"></a>如何获取和使用 vcpkg

可通过从 vcpkg GitHub 存储库创建本地克隆来安装 vcpkg[https://github.com/Microsoft/vcpkg](https://github.com/Microsoft/vcpkg)。 然后运行 vcpkg-bootstrapper 脚本对其进行设置。 有关详细的安装说明，请参阅[安装 vcpkg](install-vcpkg.md)。 若要将 vcpkg 与 Visual Studio 或 Visual Studio Code 开发环境集成，请参阅[集成 vcpkg](integrate-vcpkg.md)。 若要使用 vcpkg 来安装或更新库，请参阅[使用 vcpkg 管理库](manage-libraries-with-vcpkg.md)。 有关 vcpkg 命令的详细信息，请参阅 [vcpkg 命令行参考](vcpkg-command-line-reference.md)。

## <a name="how-vcpkg-works"></a>Vcpkg 的工作原理

Vcpkg 是 GitHub 上提供的开放源代码项目。 Vcpkg 存储库的克隆或本地副本包含 vcpkg 可执行文件和目录，这是描述库及其选项的包的列表 。 每个包都包含一个或多个端口，还包括有关如何从源获取和生成库的信息，或为特定目标环境下载二进制版本的信息。 使用 vcpkg 安装库时，它会使用包和端口信息在 vcpkg 目录的子目录中下载并生成库的本地副本，供你使用。

当库可用于源表单时，vcpkg 会下载源而不是二进制文件。 它使用最新版 C 或 C++ 编译器和可以找到的工具编译这些源代码。 在 C++ ABI 兼容性方面，有一点至关重要，即你的应用程序代码以及你所使用的任何库都应由同一编译器的相同版本进行编译。 通过 vcpkg 可以消除或最大程度减少不匹配二进制文件的存在风险及它可能造成的问题。 对于使用特定编译器版本的标准化团队而言，可让一位成员使用 vcpkg 下载源并编译一组二进制文件。 让团队中的每位成员都下载和生成公用库是一种效率较低的做法。 可让一位团队成员使用 `vcpkg export` 命令来创建二进制文件和标头的通用 zip 文件，或者创建一个 NuGet 包。 然后，可以轻松地将它与其他团队成员共享。

## <a name="customize-vcpkg-instances-for-different-targets"></a>为不同的目标自定义 vcpkg 实例

可以在计算机上克隆 vcpkg 的多个副本或实例，并针对特定用途自定义每个副本或实例。 例如，除了在公共目录中找到的内容外，还可以安装不同的库或不同版本的库。 可使用首选的编译器选项设置每个实例，以生成自定义库集合。 每个实例都是一个自包含的环境，它自身的 vcpkg.exe 副本仅可在自己的层次结构中运行。 vcpkg 不会被添加到任何环境变量中，并且在 Windows 注册表或 Visual Studio 上也没有依赖项。

你还可以创建一个包含端口集合中的专用库的 vcpkg 克隆。 可添加一个可下载预生成的二进制文件和标头的端口。 然后，编写一个仅将这些文件复制到首选位置的 portfile.cmake 文件。

## <a name="the-vcpkg-folder-hierarchy"></a>vcpkg 文件夹层次结构

所有 vcpkg 功能和数据都自包含在实例的单独目录层次结构中。 没有注册表设置或环境变量。 可以在一台计算机上设置任意数量的 vcpkg 实例，它们彼此互不干扰。

vcpkg 实例的内容如下：

- `buildtrees` - 包含从中生成每个库的源的子文件夹。
- `docs` - 文档和示例。
- `downloads` - 所有已下载的工具或源的缓存副本。 运行安装命令时，vcpkg 会首先搜索此处。
- `installed` - 包含每个已安装库的标头和二进制文件。 与 Visual Studio 集成时，实质上是相当于告知它将此文件夹添加到其搜索路径。
- `packages` - 在不同的安装之间用于暂存的内部文件夹。
- `ports` - 用于描述每个库的目录、版本和下载位置的文件。 如有需要，可添加自己的端口。
- `scripts` - 由 vcpkg 使用的脚本（CMake、PowerShell）。
- `toolsrc` - vcpkg 和相关组件的 C++ 源代码。
- `triplets` - 包含每个受支持目标平台（如 x86-windows 或 x64-uwp）的设置。

## <a name="telemetry"></a>遥测技术

Vcpkg 收集使用数据，以帮助我们改进你的体验。 Microsoft 收集的数据是匿名的。 通过使用 `-disableMetrics` 选项重新运行 `bootstrap-vcpkg.bat` 或 `bootstrap-vcpkg.sh` 脚本，可以选择退出遥测  。 或者，将 `--disable-metrics` 选项传递到命令行上的 vcpkg。 还可通过设置 `VCPKG_DISABLE_METRICS` 环境变量来禁用指标。

## <a name="send-feedback-about-vcpkg"></a>发送关于 vcpkg 的反馈

使用 `vcpkg contact --survey` 命令向 Microsoft 发送有关 vcpkg 的反馈，包括 Bug 报告和功能建议。 有关详细信息，请参阅 [vcpkg 命令行参考](vcpkg-command-line-reference.md)。

## <a name="see-also"></a>另请参阅

[GitHub 上的 vcpkg](https://github.com/Microsoft/vcpkg)\
[安装 vcpkg](install-vcpkg.md)\
[集成 vcpkg](integrate-vcpkg.md)\
[使用 vcpkg 管理库](manage-libraries-with-vcpkg.md)\
[vcpkg 命令行参考](vcpkg-command-line-reference.md)\
[快速入门](https://github.com/microsoft/vcpkg/blob/master/docs/README.md)\
[常见问题解答](https://github.com/microsoft/vcpkg/blob/master/docs/about/faq.md)
