---
title: 将 vcpkg 与 Visual Studio 或 Visual Studio Code 集成
description: 了解如何将 vcpkg 与 Windows 上的 Visual Studio 或者与 macOS 和 Linux 上的 Visual Studio Code 集成。
ms.date: 12/11/2020
ms.technology: cpp-ide
ms.openlocfilehash: a08820ad65781a89ec6bc59a62d615cae2798b4b
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099373"
---
# <a name="integrate-vcpkg-with-visual-studio-or-visual-studio-code"></a>将 vcpkg 与 Visual Studio 或 Visual Studio Code 集成

Vcpkg 是适用于 C 和 C++ 库的跨平台命令行包管理器。 可以将其与 Windows 上的 Visual Studio 或者与 Linux 和 macOS 上的 Visual Studio Code 集成。

## <a name="integrate-with-visual-studio-on-windows"></a>与 Windows 上的 Visual Studio 集成

### <a name="integrate-per-user"></a>按用户集成

从 vcpkg 根目录，运行 `vcpkg integrate install` 来配置 Visual Studio，以便按用户找到所有 vcpkg 头文件和二进制文件。 无需在 Visual Studio 中编辑 VC + + 目录路径。 如果有多个 vcpkg 克隆，则你从中运行此命令的克隆将成为新的默认位置。

现在，只需键入文件夹/标头名称即可轻松加入标头，并且自动完成功能将帮助你完成这一切。 无需执行任何额外的步骤即可链接到库或添加项目引用。 下图演示了 Visual Studio 查找 `azure-storage-cpp` 标头的方法。 Vcpkg 将其标头置于 `/installed` 子文件夹中，由目标平台予以分区。 下图显示库的 `/was` 子文件夹中包含文件的列表：

![Visual Studio 编辑器中的“IntelliSense 自动完成”弹出窗口](media/vcpkg-intellisense.png "vcpkg 和 IntelliSense")

### <a name="integrate-per-project"></a>按项目集成

如果需要使用的库的版本与活动 vcpkg 实例中的版本不同，请按以下步骤操作：

1. 新建 vcpkg 克隆。 有关详细信息，请参阅[安装 vcpkg](install-vcpkg.md)。

1. 更改为新的 vcpkg 根目录。

1. 修改库的端口文件以获取所需版本。

1. 运行 `vcpkg install <library>`。 有关详细信息，请参阅[使用 vcpkg 管理库](manage-libraries-with-vcpkg.md)。

1. 使用 `vcpkg integrate project` 创建 NuGet 包，它会按项目来引用该库。

## <a name="integrate-with-visual-studio-code-on-linux-or-macos"></a>与 Linux 或 macOS 上的 Visual Studio Code 集成

在 shell 或“终端”窗口中，将目录更改为 vcpkg 根目录。 然后运行 `./vcpkg integrate install`，在 Linux 或 macOS 上配置 Visual Studio Code。 此命令将设置 vcpkg 工具和库的位置，并对源文件启用 IntelliSense。

## <a name="remove-vcpkg-integration"></a>删除 vcpkg 集成

如果已使用 `integrate` 选项，则应在删除 vcpkg 实例之前删除该集成。 若要删除和清理该集成，请将目录更改为 vcpkg 根目录。 在 Windows 上，运行 `vcpkg integrate remove`，确保清除该集成。 在 Linux 或 macOS 上，运行 `./vcpkg integrate remove` 命令。

## <a name="see-also"></a>另请参阅

[vcpkg：用于 Windows、Linux 和 MacOS 的 C++ 包管理器](./vcpkg.md)\
[GitHub 上的 vcpkg](https://github.com/Microsoft/vcpkg)\
[安装 vcpkg](install-vcpkg.md)\
[使用 vcpkg 管理库](manage-libraries-with-vcpkg.md)\
[vcpkg 命令行参考](vcpkg-command-line-reference.md)\
[快速入门](https://github.com/microsoft/vcpkg/blob/master/docs/README.md)\
[常见问题解答](https://github.com/microsoft/vcpkg/blob/master/docs/about/faq.md)
