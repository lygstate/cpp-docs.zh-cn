---
description: '了解有关以下方面的详细信息：/Zc:threadSafeInit (线程安全的本地静态初始化) '
title: '/Zc:threadSafeInit (线程安全的本地静态初始化) '
ms.date: 03/14/2018
f1_keywords:
- threadSafeInit
- /Zc:threadSafeInit
helpviewer_keywords:
- -Zc compiler options (C++)
- threadSafeInit
- Thread-safe Local Static Initialization
- /Zc compiler options (C++)
- Zc compiler options (C++)
ms.assetid: a0fc4b34-2cf0-45a7-a642-b8afc4ca19f2
ms.openlocfilehash: ac14e7979d2adab0b21229f426e00a489c14f38f
ms.sourcegitcommit: d6af41e42699628c3e2e6063ec7b03931a49a098
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2020
ms.locfileid: "97271208"
---
# <a name="zcthreadsafeinit-thread-safe-local-static-initialization"></a>/Zc:threadSafeInit (线程安全的本地静态初始化) 

**/Zc:threadSafeInit** 编译器选项告知编译器在线程安全的方式下初始化静态本地 (函数范围) 变量，从而无需手动同步。 只有初始化是线程安全的。 使用和修改多个线程的静态局部变量仍必须手动同步。 从 Visual Studio 2015 开始，可以使用此选项。 默认情况下，Visual Studio 会启用此选项。

## <a name="syntax"></a>语法

> **/Zc:threadSafeInit**[ **-** ]

## <a name="remarks"></a>备注

在 c + + 11 标准中，具有静态或线程存储持续时间的块范围变量必须在进行任何其他初始化之前都为零初始化。 当控件第一次通过变量的声明时发生初始化。 如果在初始化过程中引发了异常，则该变量将被视为未初始化，并将在下一次控件通过声明时重新尝试初始化。 如果控件同时与初始化一起进入声明，则在初始化完成时并发执行将被阻止。 如果控件在初始化过程中以递归方式重新输入声明，则行为是不确定的。 默认情况下，visual studio 在 Visual Studio 2015 中启动将实现此标准行为。 此行为可以通过设置 **/zc： threadSafeInit** 编译器选项显式指定。

默认情况下， **/Zc:threadSafeInit** 编译器选项处于启用状态。 [/Permissive-](permissive-standards-conformance.md)选项不影响 **/Zc:threadSafeInit**。

静态局部变量的线程安全初始化依赖于通用 C 运行时库中实现的代码 (UCRT) 。 若要避免依赖于 UCRT，或为保留在 Visual Studio 2015 之前 Visual Studio 版本的非线程安全初始化行为，请使用 **/Zc:threadSafeInit-**。 如果你知道不需要线程安全，则使用此选项可以更快地生成有关静态局部声明的代码。

线程安全的静态局部变量将内部 (TLS) 使用线程本地存储，以便在静态已初始化时提供高效执行。 此功能的实现依赖于 Windows Vista 和更高版本操作系统中的 Windows 操作系统支持功能。 Windows XP、Windows Server 2003 和更早版本的操作系统不支持此支持，因此它们不会获得更高的效率优势。 这些操作系统还限制了可加载的 TLS 部分数量。 超过 TLS 部分限制可能导致崩溃。 如果这是代码中的问题，尤其是在必须在较早版本的操作系统上运行的代码中，请使用 **/Zc:threadSafeInit-** 禁用线程安全的初始化代码。

有关 Visual C++ 中一致性问题的详细信息，请参阅 [Nonstandard Behavior](../../cpp/nonstandard-behavior.md)。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 从 " **配置** " 下拉菜单中，选择 " **所有配置**"。

1. 选择 "**配置属性**" "  >  **c/c + +**  >  **命令行**" 属性页。

1. 修改 " **附加选项** " 属性以包括 **/Zc:threadSafeInit** 或 **/Zc:ThreadSafeInit-** ，然后选择 **"确定"**。

## <a name="see-also"></a>请参阅

[MSVC 编译器选项](compiler-options.md)<br/>
[MSVC 编译器 Command-Line 语法](compiler-command-line-syntax.md)<br/>
[/Zc（一致性）](zc-conformance.md)<br/>
