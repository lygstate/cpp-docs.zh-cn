---
title: Vcpkg 命令行参考
description: 了解如何在 Windows、macOS 和 Linux 上使用 vcpkg 的命令行选项。
ms.date: 12/17/2020
ms.topic: reference
ms.technology: cpp-ide
ms.openlocfilehash: 22210f3ee80050890d0b71fcc26461372e77e11e
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099620"
---
# <a name="vcpkg-command-line-reference"></a>Vcpkg 命令行参考

Vcpkg 中提供的命令的快速参考。

## <a name="commands"></a>命令

| 命令 | 描述 |
|--|--|
| **`vcpkg search [pat]`** | 搜索可安装的包 |
| **`vcpkg install <pkg>...`** | 安装包 |
| **`vcpkg remove <pkg>...`** | 卸载包 |
| **`vcpkg remove --outdated`** | 卸载所有过期包 |
| **`vcpkg list`** | 列出已安装的包 |
| **`vcpkg update`** | 显示用于更新的包列表 |
| **`vcpkg upgrade`** | 重新生成所有过期包 |
| **`vcpkg hash <file> [alg]`** | 通过特定算法对文件执行哈希操作，默认为 SHA512 |
| **`vcpkg integrate install`** | 使已安装包在用户范围内可用。 首次使用时需要管理权限 |
| **`vcpkg integrate remove`** | 删除用户范围的集成 |
| **`vcpkg integrate project`** | 为使用单个 VS 项目生成引用 NuGet 包 |
| **`vcpkg export <pkg>... [opt]...`** | 导出包 |
| **`vcpkg edit <pkg>`** | 打开端口进行编辑（使用 %EDITOR%，默认为“code”） |
| **`vcpkg create <pkg> <url> [archivename]`** | 创建新程序包 |
| **`vcpkg cache`** | 列出缓存的已编译包 |
| **`vcpkg version`** | 显示版本信息 |
| **`vcpkg contact --survey`** | 显示联系信息，以便发送反馈。 |

## <a name="options"></a>选项

| 选项 | 描述 |
|--|--|
| **`--triplet <t>`** | 指定目标体系结构三元组。 （默认：`%VCPKG_DEFAULT_TRIPLET%`，另请参阅 `vcpkg help triplet`） |
| **`--vcpkg-root <path>`** | 指定 vcpkg 根目录（默认：`%VCPKG_ROOT%`） |

## <a name="see-also"></a>另请参阅

[vcpkg：用于 Windows、Linux 和 MacOS 的 C++ 包管理器](./vcpkg.md)\
[GitHub 上的 vcpkg](https://github.com/Microsoft/vcpkg)\
[安装 vcpkg](install-vcpkg.md)\
[集成 vcpkg](integrate-vcpkg.md)\
[使用 vcpkg 管理库](manage-libraries-with-vcpkg.md)\
[快速入门](https://github.com/microsoft/vcpkg/blob/master/docs/README.md)\
[常见问题解答](https://github.com/microsoft/vcpkg/blob/master/docs/about/faq.md)
