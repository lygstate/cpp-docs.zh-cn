---
description: 了解详细信息：将项目从混合模式转换为纯中间语言
title: 将项目从混合模式转换为纯中间语言项目
ms.date: 04/15/2021
helpviewer_keywords:
- intermediate language, mixed-mode applications
- mixed-mode applications
- mixed-mode applications, intermediate language
- projects [C++], converting to intermediate language
ms.openlocfilehash: af16c9f179aa9bb6cc88ba3e47debbcdcc63cb04
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539225"
---
# <a name="converting-projects-from-mixed-mode-to-pure-intermediate-language"></a>将项目从混合模式转换为纯中间语言项目

默认情况下，所有 Visual C++ CLR 项目都链接到 C 运行时库。 因此，这些项目归类为 *混合模式* 应用程序，因为它们将本机代码与面向公共语言运行时的代码组合 (托管代码) 。 编译时，它们将被编译成中间语言 (IL) ，也称为 Microsoft 中间语言 (MSIL) 。

> [!IMPORTANT]
> Visual Studio 2015 已弃用，Visual Studio 2017 不再支持为 **`/clr:pure`** **`/clr:safe`** CLR 应用程序创建或代码。 如果需要纯程序集或安全程序集，建议将应用程序转换为 c #。

如果你使用的是早期版本的支持或的 Microsoft c + + 编译器工具集 **`/clr:pure`** **`/clr:safe`** ，则可以使用此过程将代码转换为纯 MSIL：

### <a name="to-convert-your-mixed-mode-application-into-pure-intermediate-language"></a>将混合模式应用程序转换为纯中间语言

1. 删除 (CRT) 的 [C 运行时库](../c-runtime-library/crt-library-features.md) 的链接：

   1. 在定义应用程序的入口点的 .cpp 文件中，将入口点更改为 `Main()` 。 使用 `Main()` 指示你的项目不链接到 CRT。

   1. 在解决方案资源管理器中，右键单击项目，然后在快捷菜单上选择 " **属性** " 以打开应用程序的属性页。

   1. 在 **链接器** 的 "**高级** 项目" 属性页中，选择 **入口点**，然后在此字段中输入 **Main** 。

   1. 对于控制台应用程序，在 **链接器** 的 "**系统** 项目" 属性页中，选择 "**子系统**" 字段并将其更改为 **`Console (/SUBSYSTEM:CONSOLE)`** 。

      > [!NOTE]
      > 不必为 Windows 窗体应用程序设置此属性，因为默认情况下 **子系统** 字段设置为 **`Windows (/SUBSYSTEM:WINDOWS)`** 。

   1. 在中 *`stdafx.h`* ，注释掉所有 `#include` 语句。 例如，在控制台应用程序中：

      ```cpp
      // #include <iostream>
      // #include <tchar.h>
      ```

       -或-

       例如，在 Windows 窗体应用程序中：

      ```cpp
      // #include <stdlib.h>
      // #include <malloc.h>
      // #include <memory.h>
      // #include <tchar.h>
      ```

   1. 对于 Windows 窗体的应用程序，请在中 *`Form1.cpp`* 注释掉 `#include` 引用的语句 *`windows.h`* 。 例如：

      ```cpp
      // #include <windows.h>
      ```

1. 将以下代码添加到 *`stdafx.h`* ：

   ```cpp
   #ifndef __FLTUSED__
   #define __FLTUSED__
      extern "C" __declspec(selectany) int _fltused=1;
   #endif
   ```

1. 删除所有非托管类型：

   在适当的位置，将非托管类型替换为命名空间中的结构 [`System`](/dotnet/api/system) 。 下表列出了常见的托管类型：

   |结构|说明|
   |---------------|-----------------|
   |[`Boolean`](/dotnet/api/system.boolean)|表示布尔值。|
   |[`Byte`](/dotnet/api/system.byte)|表示一个 8 位无符号整数。|
   |[`Char`](/dotnet/api/system.char)|表示一个 Unicode 字符。|
   |[`DateTime`](/dotnet/api/system.datetime)|表示时间上的一刻，通常以日期和当天的时间表示。|
   |[`Decimal`](/dotnet/api/system.decimal)|表示十进制数。|
   |[`Double`](/dotnet/api/system.double)|表示一个双精度浮点数。|
   |[`Guid`](/dotnet/api/system.guid)|表示全局唯一标识符 (GUID)。|
   |[`Int16`](/dotnet/api/system.int16)|表示 16 位有符号整数。|
   |[`Int32`](/dotnet/api/system.int32)|表示 32 位带符号整数。|
   |[`Int64`](/dotnet/api/system.int64)|表示 64 位有符号整数。|
   |[`IntPtr`](/dotnet/api/system.intptr)|用于表示指针或句柄的平台特定类型。|
   |[`SByte`](/dotnet/api/system.byte)|表示 8 位有符号整数。|
   |[`Single`](/dotnet/api/system.single)|表示一个单精度浮点数。|
   |[`TimeSpan`](/dotnet/api/system.timespan)|表示一个时间间隔。|
   |[`UInt16`](/dotnet/api/system.uint16)|表示 16 位无符号整数。|
   |[`UInt32`](/dotnet/api/system.uint32)|表示 32 位无符号整数。|
   |[`UInt64`](/dotnet/api/system.uint64)|表示 64 位无符号整数。|
   |[`UIntPtr`](/dotnet/api/system.uintptr)|用于表示指针或句柄的平台特定类型。|
   |[`Void`](/dotnet/api/system.void)|指示未返回值的方法;也就是说，该方法具有 `void` 返回类型。|
