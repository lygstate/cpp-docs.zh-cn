---
title: 使用 vcpkg 管理库
description: 了解如何在 Windows、macOS 和 Linux 上使用 vcpkg 管理库。
ms.date: 12/11/2020
ms.technology: cpp-ide
ms.openlocfilehash: 5e5fc0e9cb1616155bfe8268f2c55afcee4c4a94
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099243"
---
# <a name="manage-libraries-with-vcpkg"></a>使用 vcpkg 管理库

[安装 vcpkg](install-vcpkg.md)之后，可以使用它在本地计算机上获取并生成库。

## <a name="search-the-list-of-available-libraries"></a>搜索可用库列表

### <a name="windows"></a>Windows

要查看哪些包可用，请在命令提示符中键入 `vcpkg search`。

此命令会枚举 `vcpkg/ports` 子文件夹中的控件文件。 将出现如下的文件列表：

```cmd
ace       6.4.3   The ADAPTIVE Communication Environment
anax      2.1.0-1 An open source C++ entity system. \<https://github...
antlr4    4.6-1   ANother Tool for Language Recognition
apr       1.5.2   The Apache Portable Runtime (APR) is a C library ...
asio      1.10.8  Asio is a cross-platform C++ library for network ...
assimp    3.3.1   The Open Asset import library
atk       2.24.0  GNOME Accessibility Toolkit
...
```

可根据模式进行筛选，例如 `vcpkg search ta`：

```cmd
botan       2.0.1      A cryptography library written in C++11
portaudio   19.0.6.00  PortAudio Portable Cross-platform Audio I/O API P...
taglib      1.11.1-2   TagLib Audio Meta-Data Library
```

### <a name="install-a-library-on-your-local-machine"></a>在本地计算机上安装库

在使用 `vcpkg search` 获取库的名称后，可使用 `vcpkg install` 下载库并对其进行编译 。 vcpkg 在端口目录中使用库的端口文件。 如果未指定三元组，vcpkg 将针对目标平台的默认三元组进行安装和编译：x86-windows、x64-linux.cmake 或 x64-osx.cmake。

对于 Linux 库，vcpkg 取决于本地计算机上安装的 GCC。 在 macOS 上，vcpkg 使用 Clang。

当端口文件指定了依赖项时，vcpkg 也会下载并安装这些依赖项。 下载后，vcpkg 将使用库所使用的同一生成系统生成库。 首选 CMake 和 MSBuild（Windows 上）项目，但同时还支持 MAKE 以及其他任何生成系统。 如果 vcpkg 在本地计算机上找不到指定的生成系统，它会下载并安装一个。

```cmd
> vcpkg install boost:x86-windows

The following packages will be built and installed:
    boost:x86-windows
  * bzip2:x86-windows
  * zlib:x86-windows
Additional packages (*) will be installed to complete this operation.
```

对于 CMake 项目，通过 `CMAKE_TOOLCHAIN_FILE` 来配合使用库和 `find_package()`。 例如，在 Linux 或 macOS 上：

```cmd
cmake .. -DCMAKE_TOOLCHAIN_FILE=vcpkg/scripts/buildsystems/vcpkg.cmake
```

在 Windows 上：

```cmd
cmake .. -DCMAKE_TOOLCHAIN_FILE=vcpkg\scripts\buildsystems\vcpkg.cmake
```

某些库包括可安装选项。 例如，在搜索 curl 库时，还将看到用方括号括起的受支持的选项的列表：

```cmd
> vcpkg search curl
curl                 7.68.0-3         A library for transferring data with URLs
curl[tool]                            Builds curl executable
curl[non-http]                        Enables protocols beyond HTTP/HTTPS/HTTP2
curl[http2]                           HTTP2 support
curl[ssl]                             Default SSL backend
curl[ssh]                             SSH support via libssh2
curl[openssl]                         SSL support (OpenSSL)
curl[winssl]                          SSL support (Secure Channel / "WinSSL")
curl[mbedtls]                         SSL support (mbedTLS)
curl[sectransp]                       SSL support (sectransp)
curl[c-ares]                          c-ares support
curl[sspi]                            SSPI support
curl[brotli]                          brotli support (brotli)
curlpp               2018-06-15-3     C++ wrapper around libcURL
```

在这种情况下，方括号 `[` 和 `]` 是文本，不是元字符 。

可在命令行上指定要安装的特定选项。 例如，若要使用 Windows 的默认 SSL 后端安装 curl 库，请使用 `vcpkg install curl[ssl]:x86-windows` 命令。 如果需要，该命令将安装所有必备项（包括核心库）：

```cmd
> vcpkg list
curl:x86-windows            7.68.0-3   A library for transferring data with URLs
curl[non-http]:x86-windows             Enables protocols beyond HTTP/HTTPS/HTTP2
curl[ssl]:x86-windows                  Default SSL backend
curl[sspi]:x86-windows                 SSPI support
curl[winssl]:x86-windows               SSL support (Secure Channel / "WinSSL")
zlib:x86-windows            1.2.11-6   A compression library
```

### <a name="macos"></a>[macOS](#tab/macos)

若要查看哪些包可用，请更改为 vcpkg 根目录，然后在“终端”中输入 `./vcpkg search`。

此命令会枚举 `vcpkg/ports` 子文件夹中的控件文件。 将出现如下的文件列表：

```Terminal
ace       6.4.3   The ADAPTIVE Communication Environment
anax      2.1.0-1 An open source C++ entity system. \<https://github...
antlr4    4.6-1   ANother Tool for Language Recognition
apr       1.5.2   The Apache Portable Runtime (APR) is a C library ...
asio      1.10.8  Asio is a cross-platform C++ library for network ...
assimp    3.3.1   The Open Asset import library
atk       2.24.0  GNOME Accessibility Toolkit
...
```

可根据模式进行筛选，例如 `vcpkg search ta`：

```Terminal
botan       2.0.1      A cryptography library written in C++11
portaudio   19.0.6.00  PortAudio Portable Cross-platform Audio I/O API P...
taglib      1.11.1-2   TagLib Audio Meta-Data Library
```

### <a name="install-a-library-on-your-computer"></a>在你的计算机上安装库

在使用 `vcpkg search` 获取库的名称后，可使用 `vcpkg install` 下载库并对其进行编译 。 vcpkg 在端口目录中使用库的端口文件。 如果未指定三元组，vcpkg 将针对目标平台的默认三元组进行安装和编译：x86-windows、x64-linux.cmake 或 x64-osx.cmake。

对于 Linux 库，vcpkg 取决于本地计算机上安装的 GCC。 在 macOS 上，vcpkg 使用 Clang。

当端口文件指定了依赖项时，vcpkg 也会下载并安装这些依赖项。 下载后，vcpkg 将使用库所使用的同一生成系统生成库。 首选 CMake 和 MSBuild（Windows 上）项目，但同时还支持 MAKE 以及其他任何生成系统。 如果 vcpkg 在本地计算机上找不到指定的生成系统，它会下载并安装一个。

```Terminal
$ ./vcpkg install boost

The following packages will be built and installed:
    boost:x86-macos
  * bzip2:x86-macos
  * zlib:x86-macos
Additional packages (*) will be installed to complete this operation.
```

对于 CMake 项目，通过 `CMAKE_TOOLCHAIN_FILE` 来配合使用库和 `find_package()`。 例如：

```Terminal
cmake .. -DCMAKE_TOOLCHAIN_FILE=./vcpkg/scripts/buildsystems/vcpkg.cmake
```

某些库包括可安装选项。 例如，在搜索 curl 库时，还将看到用方括号括起的受支持的选项的列表：

```cmd
> vcpkg search curl
curl                 7.68.0-3         A library for transferring data with URLs
curl[tool]                            Builds curl executable
curl[non-http]                        Enables protocols beyond HTTP/HTTPS/HTTP2
curl[http2]                           HTTP2 support
curl[ssl]                             Default SSL backend
curl[ssh]                             SSH support via libssh2
curl[openssl]                         SSL support (OpenSSL)
curl[winssl]                          SSL support (Secure Channel / "WinSSL")
curl[mbedtls]                         SSL support (mbedTLS)
curl[sectransp]                       SSL support (sectransp)
curl[c-ares]                          c-ares support
curl[sspi]                            SSPI support
curl[brotli]                          brotli support (brotli)
curlpp               2018-06-15-3     C++ wrapper around libcURL
```

在这种情况下，方括号 `[` 和 `]` 是文本，不是元字符 。

可在命令行上指定要安装的特定选项。 例如，若要使用默认 SSL 后端安装 curl 库，请使用 `./vcpkg install curl[ssl]` 命令。 如果需要，该命令将安装所有必备项（包括核心库）。

### <a name="linux"></a>[Linux](#tab/linux)

若要查看哪些包可用，请在 shell 中切换到 vcpkg 根目录，然后输入 `./vcpkg search`。

此命令会枚举 `vcpkg/ports` 子文件夹中的控件文件。 将出现如下的文件列表：

```shell
ace       6.4.3   The ADAPTIVE Communication Environment
anax      2.1.0-1 An open source C++ entity system. \<https://github...
antlr4    4.6-1   ANother Tool for Language Recognition
apr       1.5.2   The Apache Portable Runtime (APR) is a C library ...
asio      1.10.8  Asio is a cross-platform C++ library for network ...
assimp    3.3.1   The Open Asset import library
atk       2.24.0  GNOME Accessibility Toolkit
...
```

可根据模式进行筛选，例如 `./vcpkg search ta`：

```shell
botan       2.0.1      A cryptography library written in C++11
portaudio   19.0.6.00  PortAudio Portable Cross-platform Audio I/O API P...
taglib      1.11.1-2   TagLib Audio Meta-Data Library
```

### <a name="install-a-library-on-your-linux-machine"></a>在 Linux 计算机上安装库

在使用 `./vcpkg search` 获取库的名称后，可使用 `/vcpkg install` 下载库并对其进行编译 。 Vcpkg 在 `ports` 目录中使用库的端口文件。 如果未指定三元组，vcpkg 将针对目标平台（例如 x64-linux.cmake）的默认三元组进行安装和编译。

对于 Linux 库，vcpkg 取决于本地计算机上安装的 GCC。

当端口文件指定了依赖项时，vcpkg 也会下载并安装这些依赖项。 下载后，vcpkg 将使用库所使用的同一生成系统生成库。 首选 CMake 项目，但同时还支持 MAKE 以及其他任何生成系统。 如果 vcpkg 在本地计算机上找不到指定的生成系统，它会下载并安装一个。

```shell
$ ./vcpkg install boost:x64-linux

The following packages will be built and installed:
    boost:x64-linux
  * bzip2:x64-linux
  * zlib:x64-linux
Additional packages (*) will be installed to complete this operation.
```

对于 CMake 项目，通过 `CMAKE_TOOLCHAIN_FILE` 来配合使用库和 `find_package()`。 例如：

```shell
cmake .. -DCMAKE_TOOLCHAIN_FILE=./vcpkg/scripts/buildsystems/vcpkg.cmake
```

某些库包括可安装选项。 例如，在搜索 curl 库时，还将看到用方括号括起的受支持的选项的列表：

```cmd
> vcpkg search curl
curl                 7.68.0-3         A library for transferring data with URLs
curl[tool]                            Builds curl executable
curl[non-http]                        Enables protocols beyond HTTP/HTTPS/HTTP2
curl[http2]                           HTTP2 support
curl[ssl]                             Default SSL backend
curl[ssh]                             SSH support via libssh2
curl[openssl]                         SSL support (OpenSSL)
curl[winssl]                          SSL support (Secure Channel / "WinSSL")
curl[mbedtls]                         SSL support (mbedTLS)
curl[sectransp]                       SSL support (sectransp)
curl[c-ares]                          c-ares support
curl[sspi]                            SSPI support
curl[brotli]                          brotli support (brotli)
curlpp               2018-06-15-3     C++ wrapper around libcURL
```

在这种情况下，方括号 `[` 和 `]` 是文本，不是元字符 。

可在命令行上指定要安装的特定选项。 例如，若要使用默认 SSL 后端安装 curl 库，请使用 `./vcpkg install curl[ssl]` 命令。 如果需要，该命令将安装所有必备项（包括核心库）。

---

## <a name="list-the-libraries-already-installed"></a>列出已安装的库

安装某些库后，可使用 Windows 上的 `vcpkg list` 命令来查看你具有的内容。 Linux 和 macOS 命令类似。

```cmd
> vcpkg list

boost:x86-windows       1.64-3   Peer-reviewed portable C++ source libraries
bzip2:x86-windows       1.0.6-1  High-quality data compressor.
cpprestsdk:x86-windows  2.9.0-2  C++11 JSON, REST, and OAuth library The C++ REST ...
openssl:x86-windows     1.0.2k-2 OpenSSL is an open source project that provides a...
websocketpp:x86-windows 0.7.0    Library that implements RFC6455 The WebSocket Pro...
zlib:x86-windows        1.2.11   A compression library
```

## <a name="target-linux-from-windows-via-wsl"></a>通过 WSL 从 Windows 指向 Linux

可使用适用于 Linux 的 Windows 子系统（也称为 WSL）在 Windows 计算机上生成 Linux 二进制文件。 按照[在 Windows 10 上安装 WSL](/windows/wsl/install-win10) 的说明操作。 然后，使用[适用于 Linux 的 Visual Studio 扩展](https://devblogs.microsoft.com/cppblog/targeting-windows-subsystem-for-linux-from-visual-studio/)对其进行配置。 可以将所有针对 Windows 和 Linux 生成的库放入同一文件夹中。 可以从 Windows 和 WSL 访问它们。

## <a name="export-compiled-binaries-and-headers"></a><a name="export_binaries_per_project"></a>导出已编译的二进制文件和标头

让团队中的每位成员都下载和生成公用库是一种效率较低的做法。 可让一位团队成员使用 `vcpkg export` 命令来创建二进制文件和标头的通用 zip 文件，或者创建一个 NuGet 包。 然后，可以轻松地将它与其他团队成员共享。

## <a name="updateupgrade-installed-libraries"></a>更新/升级已安装的库

公共目录始终与最新版本的库保持一致。 要判断哪个本地库已过期，请使用 `vcpkg update`。 准备好将端口集合更新到最新版本的公共目录后，请运行 `vcpkg upgrade` 命令。 它会自动下载并重新生成已过期的任意或所有已安装的库。

默认情况下，`vcpkg upgrade` 命令仅列出过期库，不对它们进行升级。 若要真正升级这些库，请使用 `--no-dry-run` 选项。

```cmd
> vcpkg upgrade --no-dry-run
```

### <a name="upgrade-options"></a>升级选项

- `--no-dry-run`：执行升级；若未指定，该命令将仅列出过期的包。
- `--keep-going`：继续安装包（即使某项失败）。
- `--triplet <t>`：为非限定的包设置默认的三元组。
- `--vcpkg-root <path>`：指定要使用的 vcpkg 目录，而不是使用当前目录或工具目录。

### <a name="upgrade-example"></a>升级示例

下面的示例演示如何在 Windows 上只升级指定的库。 Linux 和 macOS 命令类似。 必要时 vcpkg 会自动拉取依赖项。

```cmd
c:\users\username\vcpkg> vcpkg upgrade tiny-dnn:x86-windows zlib
The following packages are up-to-date:
   tiny-dnn:x86-windows

The following packages will be rebuilt:
    * libpng[core]:x86-windows
    * tiff[core]:x86-windows
      zlib[core]:x86-windows
Additional packages (*) will be modified to complete this operation.
If you are sure you want to rebuild the above packages, run this command with the --no-dry-run option.
```

## <a name="contribute-new-libraries"></a>发布新库

可以在自己的专用端口集合中添加任意库。 要建议适合公共目录的新库，请在 [GitHub vcpkg 问题页](https://github.com/Microsoft/vcpkg/issues)上打开一个问题。

## <a name="remove-a-library"></a>删除库

键入 `vcpkg remove` 可删除已安装的库。 如果有其他库依赖它，系统会提示你使用 `--recurse` 重新运行命令；重新运行会导致下游的所有库都被删除。

## <a name="see-also"></a>另请参阅

[vcpkg：用于 Windows、Linux 和 MacOS 的 C++ 包管理器](./vcpkg.md)\
[GitHub 上的 vcpkg](https://github.com/Microsoft/vcpkg)\
[安装 vcpkg](install-vcpkg.md)\
[集成 vcpkg](integrate-vcpkg.md)\
[vcpkg 命令行参考](vcpkg-command-line-reference.md)\
[快速入门](https://github.com/microsoft/vcpkg/blob/master/docs/README.md)\
[常见问题解答](https://github.com/microsoft/vcpkg/blob/master/docs/about/faq.md)\
[安装和使用包示例：SQLite](https://github.com/microsoft/vcpkg/blob/master/docs/examples/installing-and-using-packages.md)
