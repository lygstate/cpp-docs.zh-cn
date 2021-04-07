---
title: 演练：在命令行上编译本机 C++ 程序
description: 在命令提示符下使用 Microsoft C++ 编译器。
ms.custom: conceptual
ms.date: 03/25/2021
helpviewer_keywords:
- native code [C++]
- Visual C++, native code
- compiling programs [C++]
- command-line applications [C++], native
ms.assetid: b200cfd1-0440-498f-90ee-7ecf92492dc0
ms.openlocfilehash: 35d78f7c8fdaca6b32847dce4ba2c9c3dd914549
ms.sourcegitcommit: f7bfb6dffa410008cf1bc01f70aae5c27e464f72
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2021
ms.locfileid: "105613703"
---
# <a name="walkthrough-compiling-a-native-c-program-on-the-command-line"></a>演练：在命令行上编译本机 C++ 程序

Visual Studio 包含命令行 C 和 C++ 编译器。 可以使用它创建从基本控制台应用到通用 Windows 平台应用、桌面应用、设备驱动程序和 .NET 组件的所有内容。

在此演练中，你将使用文本编辑器创建一个基本的“Hello, World”程序，然后在命令行上对其进行编译。 如果想尝试使用 Visual Studio IDE 而不是使用命令行，请参阅[演练：使用项目和解决方案 (C++)](../ide/walkthrough-working-with-projects-and-solutions-cpp.md) 或[使用 Visual Studio IDE 进行 C++ 桌面开发](../ide/using-the-visual-studio-ide-for-cpp-desktop-development.md)。

在本演练中，你可以使用自己的 C++ 程序而不是键入显示的程序。 也可以使用另一个帮助文章中的 C++ 代码示例。

## <a name="prerequisites"></a>先决条件

要完成此演练，必须安装 Visual Studio 和可选的“使用 C++ 进行桌面开发”工作负载，或 Visual Studio 的命令行生成工具。

Visual Studio 是一个集成开发环境 (IDE)。 它支持多种语言和平台的功能完备的编辑器、资源管理器、调试器和编译器。 可用版本包括免费的 Visual Studio Community 版本，且所有版本都支持 C 和 C++ 开发。 有关如何下载和安装 Visual Studio 的信息，请参阅[在 Visual Studio 中安装 C++ 支持](vscpp-step-0-installation.md)。

Visual Studio 生成工具只安装生成 C 和 C++ 程序所需的命令行编译器、工具和库。 它非常适合生成实验室或课堂练习，安装速度也相对较快。 如果只安装命令行工具，请在 [Visual Studio 下载](https://visualstudio.microsoft.com/downloads/#build-tools-for-visual-studio-2019)页面上查找 Visual Studio 生成工具。

在命令行上生成 C 或 C++ 程序之前，请验证是否安装了这些工具，并且是否可以从命令行访问它们。 Visual C++ 对用于查找其使用的工具、标头和库的命令行环境有复杂的要求。 如果没有事先准备，在普通的命令提示窗口中不能使用 Visual C++。 幸运的是，Visual C++ 为你安装了快捷方式来启动开发人员命令提示，该命令提示符为命令行生成设置了环境。 遗憾的是，开发人员命令提示快捷方式的名称和它们所在的位置在几乎所有版本的 Visual C++ 和不同版本的 Windows 中都是不同的。 你的第一个演练任务是找到要使用的正确的命令提示符。

> [!NOTE]
> 开发人员命令提示快捷方式自动为编译器和工具以及所有必需的标头和库设置正确的路径。 如果使用常规的命令提示窗口，则必须自己设置这些环境值。 有关详细信息，请参阅 [为命令行生成设置路径和环境变量](setting-the-path-and-environment-variables-for-command-line-builds.md)。 建议使用开发人员命令提示快捷方式，而不是构建自己的快捷方式。

### <a name="open-a-developer-command-prompt"></a>打开“开发人员命令提示”

1. 如果在 Windows 10 上安装了 Visual Studio 2017 或更高版本，请打开“开始”菜单并选择“所有应用”。 向下滚动并打开“Visual Studio”文件夹（不是 Visual Studio 应用程序）。 选择“VS 开发人员命令提示”以打开命令提示窗口。

   如果在 Windows 10 上安装了 Microsoft Visual C++ 生成工具 2015，请打开“开始”菜单并选择“所有应用” 。 向下滚动并打开“Visual C++ 生成工具”文件夹。 选择“Visual C++ 2015 x86 本机工具命令提示”，打开命令提示窗口  。

   还可以使用 Windows 搜索功能搜索“开发人员命令提示”，然后选择与安装的 Visual Studio 版本匹配的命令提示。 使用快捷方式打开命令提示窗口。

1. 接下来，验证 Visual C++ 开发人员命令提示是否设置正确。 在命令提示窗口中，输入 `cl`，并验证输出是否如下所示：

   ```Output
   C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise>cl
   Microsoft (R) C/C++ Optimizing Compiler Version 19.10.25017 for x86
   Copyright (C) Microsoft Corporation.  All rights reserved.

   usage: cl [ option... ] filename... [ /link linkoption... ]
   ```

   当前目录或版本号可能存在差异。 这些值取决于 Visual C++ 的版本和安装的任何更新。 如果上述输出与所看到的类似，则可以在命令行中生成 C 或 C++ 程序。

   > [!NOTE]
   > 当你运行 `cl` 命令时，如果遇到错误，例如“CL 无法识别为内部或外部命令、可操作的程序或批处理文件”、错误 C1034 或错误 LNK1104，则说明你没有使用开发人员命令提示，或者安装 Visual C++ 时出现了错误。 必须先解决此问题，然后才能继续。

   如果找不到开发人员命令提示快捷方式，或在输入 `cl` 时收到错误消息，则说明 Visual C++ 安装可能有问题。 尝试在 Visual Studio 中重新安装 Visual C++ 组件，或重新安装 Microsoft Visual C++ 生成工具。 除非 `cl` 命令运行，否则不要继续下一节。 有关 Visual C++ 的安装和故障排除的更多信息，请参阅[安装 Visual Studio](/visualstudio/install/install-visual-studio)。

   > [!NOTE]
   > 根据计算机上的 Windows 版本和系统安全配置，可能必须右键单击以打开“开发人员命令提示”快捷方式的快捷菜单，然后选择“以管理员身份运行”，才能成功生成和运行通过本演练创建的程序。

### <a name="create-a-visual-c-source-file-and-compile-it-on-the-command-line"></a>创建 Visual C++ 源文件并在命令行上对其进行编译

1. 在“开发人员命令提示”窗口中，输入 `md c:\hello` 以创建目录，然后输入 `cd c:\hello` 更改为该目录。 此目录是创建源文件和编译程序的位置。

1. 在命令提示窗口中输入 `notepad hello.cpp`。

   当记事本提示你创建新文件时，选择“是”。 此步骤将打开一个空白记事本窗口，你可以在名为 hello.cpp 的文件中输入代码。

1. 在记事本中，输入以下代码行：

   ```cpp
   #include <iostream>
   using namespace std;
   int main()
   {
       cout << "Hello, world, from Visual C++!" << endl;
   }
   ```

   此代码是一个非常简单的程序，会在屏幕上写入一行文本，然后退出。 为了尽量减少错误，请将此代码复制并粘贴到记事本中。

1. 保存所有内容！ 在记事本中，在“文件”  菜单上选择“保存” 。

   恭喜，你已经创建了一个 C++ 源文件 Helo.cp，可以进行编译。

1. 切换回开发人员命令提示窗口。 在命令提示符下输入 `dir` 以列出 c:\hello 目录的内容。 目录列表中应显示源文件 hello.cpp，如下所示：

   ```Output
   c:\hello>dir
    Volume in drive C has no label.
    Volume Serial Number is CC62-6545

    Directory of c:\hello

   05/24/2016  05:36 PM    <DIR>          .
   05/24/2016  05:36 PM    <DIR>          ..
   05/24/2016  05:37 PM               115 hello.cpp
                  1 File(s)            115 bytes
                  2 Dir(s)  571,343,446,016 bytes free

   ```

   日期和其他详细信息在你的计算机上会有所不同。
   
   > [!NOTE]
   > 如果看不到源代码文件 `hello.cpp`，请确保命令提示符中的当前工作目录是你创建的 `C:\hello` 目录。 此外，请确保这是保存源文件的目录。 另请确保保存的源代码扩展名为 `.cpp`，而不是 `.txt` 。 如果在命令提示符下使用 `notepad hello.cpp` 命令打开记事本，则源文件会以 `.cpp` 文件的形式自动保存在当前目录中。 如果以另一种方式打开记事本，则其行为会有所不同：默认情况下，保存时记事本，它会向新文件追加 `.txt` 扩展。 它还默认将文件保存在“文档”目录中。 若要使用记事本保存带有 `.cpp` 扩展名的文件，请选择“文件” > “另存为”。 在“另存为”对话框中，导航到目录树视图控件中的 `C:\hello` 文件夹。 然后，使用“另存为类型”下拉控件选择“所有文件( \*.\*)”。 在“文件名”编辑控件中输入 `hello.cpp` ，然后选择“保存”以保存该文件。

1. 在开发人员命令提示下，输入 `cl /EHsc hello.cpp` 来编译程序。

   cl.exe 编译器会生成包含已编译代码的 .obj 文件，然后运行链接器来创建名为 basic.exe 的可执行程序。 此名称会显示在编译器显示的多行输出信息中。 编译器的输出应如下所示：

   ```Output
   c:\hello>cl /EHsc hello.cpp
   Microsoft (R) C/C++ Optimizing Compiler Version 19.10.25017 for x86
   Copyright (C) Microsoft Corporation.  All rights reserved.

   hello.cpp
   Microsoft (R) Incremental Linker Version 14.10.25017.0
   Copyright (C) Microsoft Corporation.  All rights reserved.

   /out:hello.exe
   hello.obj
   ```

   > [!NOTE]
   > 如果遇到错误（例如“‘cl’无法识别为内部或外部命令、可操作的程序或批处理文件”、错误 C1034 或错误 LNK1104），则说明未正确设置开发人员命令提示。 有关如何解决此问题的信息，请返回“打开开发人员命令提示”部分。

   > [!NOTE]
   > 如果收到其他编译器或链接器错误或警告，请检查源代码以更正任何错误，然后保存它并再次运行编译器。 有关特定错误的信息，请使用搜索框查找错误号。

1. 若要运行 hello.exe 程序，请在命令提示处输入 `hello`。

   该程序显示以下文本并退出：

   ```Output
   Hello, world, from Visual C++!
   ```

   恭喜，你已通过命令行工具编译并运行了 C++ 程序。

## <a name="next-steps"></a>后续步骤

此“Hello, World”示例与 C++ 程序一样简单。 现实世界中的程序通常有头文件、更多源文件和指向库的链接。

你可以使用本演练中的步骤来创建自己的 C++ 代码，而不是键入所示的示例代码。 还可通过这些步骤生成你在其他位置看到的许多 C++ 代码示例程序。 你可以在任何可写目录放置源代码并生成应用。 默认情况下，Visual Studio IDE 在用户文件夹的“source\\repos”子文件夹中创建项目。 旧版本可能会将项目放入 Documents\\Visual Studio \<version>\\Projects* 文件夹中。

若要编译包含其他源代码文件的程序，请在命令行上将它们全部输入，例如：

`cl /EHsc file1.cpp file2.cpp file3.cpp`

`/EHsc` 命令行选项指示编译器启用标准 C++ 异常处理行为。 如果没有它，则引发的异常可能导致未受损对象和资源泄漏。 有关详细信息，请参阅 [/EH（异常处理模型）](reference/eh-exception-handling-model.md)。

提供其他源文件时，编译器会使用第一个输入文件创建程序名。 在本例中，编译器输出一个名为 file1.exe 的程序。 若要将名称更改为 program1.exe，请添加 [/out](reference/out-output-file-name.md) 链接器选项：

`cl /EHsc file1.cpp file2.cpp file3.cpp /link /out:program1.exe`

若要自动捕获更多编程错误，我们建议使用 [/W3](reference/compiler-option-warning-level.md) 或 [/W4](reference/compiler-option-warning-level.md) 警告级别选项进行编译：

`cl /W4 /EHsc file1.cpp file2.cpp file3.cpp /link /out:program1.exe`

编译器 cl.exe 还有很多选项。 可以应用这些选项来生成、优化、调试和分析你的代码。 如需快速列表，请在开发人员命令提示下输入 `cl /?`。 你还可以单独编译和链接，并在更复杂的生成方案中应用链接器选项。 有关编译器和链接器选项及用法的详细信息，请参阅 [C/C++ 生成参考](reference/c-cpp-building-reference.md)。

可以使用 NMAKE 和生成文件、MSBuild 和项目文件或 CMake 在命令行上配置和生成更复杂的项目。 有关使用这些工具的详细信息，请参阅 [NMAKE 参考](reference/nmake-reference.md)、[MSBuild](msbuild-visual-cpp.md) 和 [Visual Studio 中的 CMake 项目](cmake-projects-in-visual-studio.md)。

C 和 C++ 语言相似，但并不相同。 MSVC 编译器使用一个简单的规则来确定在编译代码时使用哪种语言。 默认情况下，MSVC 编译器将以 `.c` 结尾的文件视为 C 源代码，将以 `.cpp` 结尾的所有文件视为 C++ 源代码 。 要强制编译器将所有文件视为独立于文件扩展名的 C++，请使用 [/TP](reference/tc-tp-tc-tp-specify-source-file-type.md) 编译器选项。

MSVC 编译器包括符合 ISO C99 标准的 C 运行时库 (CRT)，只有几个较小例外。 可移植代码通常按预期方式进行编译和运行。 MSVC 编译器弃用了某些过时的库函数和多个 POSIX 函数名。 这些函数仍然受支持，但首选名称已更改。 有关详细信息，请参阅 [CRT 中的安全功能](../c-runtime-library/security-features-in-the-crt.md)和[编译器警告（级别 3）C4996](../error-messages/compiler-warnings/compiler-warning-level-3-c4996.md)。

## <a name="see-also"></a>请参阅

[C++ 语言参考](../cpp/cpp-language-reference.md)<br/>
[项目和生成系统](projects-and-build-systems-cpp.md)<br/>
[MSVC 编译器选项](reference/compiler-options.md)
