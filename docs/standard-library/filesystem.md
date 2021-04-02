---
title: '&lt;filesystem&gt;'
description: 描述 filesystem 标准 c + + 库标头中的类、函数和类型。
ms.date: 01/15/2021
f1_keywords:
- <filesystem>
- filesystem/std::filesystem
- std::filesystem
- std::experimental::filesystem
no-loc:
- filesystem
- experimental
- char
- wchar_t
- char16_t
- char32_t
ms.openlocfilehash: 4af9e0a5d5f2839de564f25c976e018e8f1565e7
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099347"
---
# `filesystem`

包括标头 `<filesystem>` 以访问用于操作和检索有关路径、文件和目录的信息的类和函数。

## <a name="syntax"></a>语法

```cpp
#include <filesystem> // C++17 standard header file name
#include <experimental/filesystem> // Header file for pre-standard implementation
using namespace std::experimental::filesystem::v1;
```

> [!IMPORTANT]
> 在 Visual Studio 2017 版本中， `<filesystem>` 标头尚不是 c + + 标准。 Visual Studio 2017 RTW 中的 c + + 实现了最终草案标准，可在 [ISO/IEC JTC 1/SC 22/WG 21 N4100](https://wg21.link/n4100)中找到。 Visual Studio 2017 版本15.7 及更高版本支持新的 c + + 17 `<filesystem>` 标准版。
> 这是一个全新的实现，与以前的版本不兼容 `std::experimental` 。 这是必要的，如符号支持、bug 修复和标准要求的行为更改。 目前，包括 `<filesystem>` 提供新的 `std::filesystem` 和上一个 `std::experimental::filesystem` 。 包括 `<experimental/filesystem>` 仅提供旧 experimental 实现。 experimental将在下一次 ABI 中断版本的库中删除该实现。

此标头支持两大类主机操作系统（Microsoft Windows 和 POSIX）之一的文件系统。

虽然这两种操作系统的大多数功能均相同，但本文档将介绍它们之间存在的差异。 例如：

- Windows 支持多个根名称，例如 `c:` 或 `\\network_name` 。 文件系统由一个树林组成，每个树都有其自己的根目录（如 `c:\` 或 `\\network_name\` ），并且每个树都有其自己的当前目录，用于完成不是绝对路径名)  (相对路径名。

- POSIX 支持单个树，无根名称、单个根目录 `/` 和一个当前目录。

另一个重要差异是路径名的本机表示方式：

- Windows 使用以 null 结尾的序列 **`wchar_t`** ，编码为 utf-16 (每个 acter) 一个或多个元素 char 。

- POSIX 使用以 null 结尾的序列 **`char`** ，编码为 utf-8 (每个 acter) 的一个或多个元素 char 。

- 类的对象 `path` 以本机形式存储路径名，但支持在此存储的窗体和多个外部窗体之间轻松转换：

  - 以 null 值结束的序列 **`char`** ，编码为操作系统所优先的。

  - 以 null 结尾的序列 **`char`** ，编码为 utf-8。

  - 以 null 值结束的序列 **`wchar_t`** ，编码为操作系统所优先的。

  - 以 null 结尾的序列 **`char16_t`** ，编码为 utf-16。

  - 以 null 结尾的序列 **`char32_t`** ，编码为32。

  通过使用一个或多个 `codecvt` facet，按需调节这些表示形式之间的相互转换。 如果未指定特定的区域设置对象，则将从全局区域设置获取这些 facet。

另一个差别是每个操作系统允许你用于指定文件或目录访问权限的详细信息：

- Windows 记录文件是只读还是可写，这对于目录没有意义。

- 如果目录) ，POSIX 记录是否可以读取、写入或执行 (扫描的文件。 和，无论是允许所有者、所有者组还是每个人操作，还有其他一些权限。

两个系统的共同点是通过根名称后施加于路径名的结构。 对于 pathname `c:/abc/xyz/def.ext` ：

- 根名称是 `c:` 。

- 根目录为 `/` 。

- 根路径为 `c:/` 。

- 相对路径为 `abc/xyz/def.ext` 。

- 父路径为 `c:/abc/xyz` 。

- 文件名为 `def.ext`。

- 主体是 `def` 。

- 扩展为 `.ext` 。

一个次要差别是路径名中目录序列之间的首选分隔符。 这两个操作系统都允许写入正斜杠 `/` ，但在某些上下文中，Windows 更倾向于使用反斜杠 `\` 。 实现将其首选分隔符存储在的数据成员 `preferred_separator` 中 `path` 。

最后， `path` 对象具有一项重要功能：在标头中定义的类中需要 filename 参数时，可以使用它们 [`<fstream>`](fstream.md) 。

有关详细信息和代码示例，请参阅 [文件系统导航 (c + +) ](../standard-library/file-system-navigation.md)。

## <a name="members"></a>成员

### <a name="classes"></a>类

|“属性”|说明|
|-|-|
|[`directory_entry` 类](../standard-library/directory-entry-class.md)|描述由 `directory_iterator` 或返回 `recursive_directory_iterator` 并包含的对象 `path` 。|
|[`directory_iterator` 类](../standard-library/directory-iterator-class.md)|描述通过文件系统目录中的文件名排序的输入迭代器。|
|[`filesystem_error` 类](../standard-library/filesystem-error-class.md)|所引发以报告低级系统溢出的异常的基类。|
|[`path` 类](../standard-library/path-class.md)|定义一个类，该类存储适合用作文件名的模板类型 `String` 的对象。|
|[`recursive_directory_iterator` 类](../standard-library/recursive-directory-iterator-class.md)|描述通过文件系统目录中的文件名排序的输入迭代器。 迭代器还可以降到子目录中。|
|[`file_status` 类](../standard-library/file-status-class.md)|包装 `file_type`。|

### <a name="structs"></a>结构

|名称|说明|
|-|-|
|[`space_info` 构造](../standard-library/space-info-structure.md)|保存有关卷的信息。|

## <a name="functions"></a>函数

[`<filesystem>` 函数](../standard-library/filesystem-functions.md)

## <a name="operators"></a>运算符

[`<filesystem>` 运算符](../standard-library/filesystem-operators.md)

## <a name="enumerations"></a>枚举

|名称|说明|
|-|-|
|[`copy_options`](../standard-library/filesystem-enumerations.md#copy_options)|如果目标文件已存在，则与 [copy_file](../standard-library/filesystem-functions.md#copy_file) 一起使用的枚举将决定行为。|
|[`directory_options`](../standard-library/filesystem-enumerations.md#directory_options)|为目录迭代器指定选项的枚举。|
|[`file_type`](../standard-library/filesystem-enumerations.md#file_type)|文件类型的枚举。|
|[`perm_options`](../standard-library/filesystem-enumerations.md#perm_options)| 枚举函数的选项 `permissions` 。 |
|[`perms`](../standard-library/filesystem-enumerations.md#perms)|用于传达权限和权限选项的位掩码类型|

## <a name="see-also"></a>另请参阅

[标头文件引用](../standard-library/cpp-standard-library-header-files.md)
