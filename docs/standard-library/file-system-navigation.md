---
title: 文件系统导航
description: 如何使用 c + + 标准库文件系统 Api 在文件系统中导航。
ms.date: 04/13/2020
ms.assetid: f7cc5f5e-a541-4e00-87c7-a3769ef6096d
ms.openlocfilehash: f5f85eaf5e665ea4374e71c5eab7434b9c3d34e4
ms.sourcegitcommit: a89eac9acdbd54a181e3bd5d5bc71a3ef3c1abca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "106506086"
---
# <a name="file-system-navigation"></a>文件系统导航

`<filesystem>`标头实现 c + + 文件系统技术规范 ISO/IEC TS 18822:2015 (最终草案： [ISO/iec JTC 1/SC 22/WG 21 N4100](https://wg21.link/n4100)) ，并具有可用于编写与平台无关的代码来导航文件系统的类型和函数。 因为它是跨平台的，所以它包含与 Windows 系统不相关的 Api。 例如， `is_fifo(const path&)` **`false`** 在 Windows 上始终返回。

## <a name="overview"></a>概述

将 `<filesystem>` api 用于以下任务：

- 循环访问指定路径下的文件和目录

- 获取有关包含创建时间、大小、扩展名和根目录的文件的信息

- 编写、分解和比较路径

- 创建、复制和删除目录

- 复制和删除文件

有关使用标准库的文件 IO 的详细信息，请参阅 [iostream 编程](../standard-library/iostream-programming.md)。

## <a name="paths"></a>路径

### <a name="constructing-and-composing-paths"></a>构造和编写路径

Windows（自 XP 起）中的路径以 Unicode 格式进行本机存储。 [`path`](../standard-library/path-class.md)类自动执行所有必需的字符串转换。 它同时接受宽字符数组和窄字符数组的参数， `std::string` 以及 `std::wstring` 格式化为 UTF8 或 UTF16 的和类型。 `path` 类还自动标准化路径分隔符。 可在构造函数参数中将单个正斜杠用作目录分隔符。 此分隔符使你可以使用相同的字符串在 Windows 和 UNIX 环境中存储路径：

```cpp
path pathToDisplay(L"/FileSystemTest/SubDir3");     // OK!
path pathToDisplay2(L"\\FileSystemTest\\SubDir3");  // Still OK as always
path pathToDisplay3(LR"(\FileSystemTest\SubDir3)"); // Raw string literals are OK, too.
```

若要连接两个路径，可使用重载的 `/` 和 `/=` 运算符，它们类似于 `+` 和 `+=` 上的 `std::string` 和 `std::wstring`运算符。 `path`如果不是，对象可方便地提供分隔符。

```cpp
path myRoot("C:/FileSystemTest");  // no trailing separator, no problem!
myRoot /= path("SubDirRoot");      // C:/FileSystemTest/SubDirRoot
```

### <a name="examining-paths"></a>检查路径

Path 类具有多个方法，这些方法可返回有关路径本身各个部分的信息。 此信息不同于其可能引用的文件系统实体的相关信息。 可以获取根、相对路径、文件名、文件扩展名及更多内容。 可循环访问路径对象以检查层次结构中的所有文件夹。 下面的示例演示如何循环访问路径对象。 以及如何检索有关其部件的信息。

```cpp
// filesystem_path_example.cpp
// compile by using: /EHsc /W4 /permissive- /std:c++17 (or /std:c++latest)
#include <string>
#include <iostream>
#include <sstream>
#include <filesystem>

using namespace std;
using namespace std::filesystem;

wstring DisplayPathInfo()
{
    // This path may or may not refer to an existing file. We are
    // examining this path string, not file system objects.
    path pathToDisplay(L"C:/FileSystemTest/SubDir3/SubDirLevel2/File2.txt ");

    wostringstream wos;
    int i = 0;
    wos << L"Displaying path info for: " << pathToDisplay << endl;
    for (path::iterator itr = pathToDisplay.begin(); itr != pathToDisplay.end(); ++itr)
    {
        wos << L"path part: " << i++ << L" = " << *itr << endl;
    }

    wos << L"root_name() = " << pathToDisplay.root_name() << endl
        << L"root_path() = " << pathToDisplay.root_path() << endl
        << L"relative_path() = " << pathToDisplay.relative_path() << endl
        << L"parent_path() = " << pathToDisplay.parent_path() << endl
        << L"filename() = " << pathToDisplay.filename() << endl
        << L"stem() = " << pathToDisplay.stem() << endl
        << L"extension() = " << pathToDisplay.extension() << endl;

    return wos.str();
}

int main()
{
    wcout << DisplayPathInfo() << endl;
    // wcout << ComparePaths() << endl; // see following example
    wcout << endl << L"Press Enter to exit" << endl;
    wstring input;
    getline(wcin, input);
}
```

此代码产生以下输出：

```Output
Displaying path info for: C:\FileSystemTest\SubDir3\SubDirLevel2\File2.txt
path part: 0 = C:
path part: 1 = \
path part: 2 = FileSystemTest
path part: 3 = SubDir3
path part: 4 = SubDirLevel2
path part: 5 = File2.txt
root_name() = C:
root_path() = C:\
relative_path() = FileSystemTest\SubDir3\SubDirLevel2\File2.txt
parent_path() = C:\FileSystemTest\SubDir3\SubDirLevel2
filename() = File2.txt
stem() = File2
extension() = .txt
```

### <a name="comparing-paths"></a>比较路径

`path` 类会重载与 `std::string` 和 `std::wstring`相同的比较运算符。 比较两个路径时，将在已规范化分隔符后进行字符串比较。 如果缺少尾部斜杠 (或反斜杠) ，则它不会被添加，并会影响比较。 下面的示例演示如何比较路径值：

```cpp
wstring ComparePaths()
{
    path p0(L"C:/Documents");                 // no trailing separator
    path p1(L"C:/Documents/");                // p0 < p1
    path p2(L"C:/Documents/2013/");           // p1 < p2
    path p3(L"C:/Documents/2013/Reports/");   // p2 < p3
    path p4(L"C:/Documents/2014/");           // p3 < p4
    path p5(L"D:/Documents/2013/Reports/");   // p4 < p5

    wostringstream wos;
    wos << boolalpha <<
        p0.wstring() << L" < " << p1.wstring() << L": " << (p0 < p1) << endl <<
        p1.wstring() << L" < " << p2.wstring() << L": " << (p1 < p2) << endl <<
        p2.wstring() << L" < " << p3.wstring() << L": " << (p2 < p3) << endl <<
        p3.wstring() << L" < " << p4.wstring() << L": " << (p3 < p4) << endl <<
        p4.wstring() << L" < " << p5.wstring() << L": " << (p4 < p5) << endl;
    return wos.str();
}
```

```Output
C:\Documents < C:\Documents\: true
C:\Documents\ < C:\Documents\2013\: true
C:\Documents\2013\ < C:\Documents\2013\Reports\: true
C:\Documents\2013\Reports\ < C:\Documents\2014\: true
C:\Documents\2014\ < D:\Documents\2013\Reports\: true
```

若要运行此代码，请将其粘贴到上述完整示例中的 `main` 前，并取消注释在 main 中调用它的行。

### <a name="converting-between-path-and-string-types"></a>在路径和字符串类型之间进行转换

`path` 对象可隐式转换为 `std::wstring` 或 `std::string`。 这意味着可以将路径传递给函数（如 [`wofstream::open`](../standard-library/basic-ofstream-class.md#open) ），如以下示例中所示：

```cpp
// filesystem_path_conversion.cpp
// compile by using: /EHsc /W4 /permissive- /std:c++17 (or /std:c++latest)
#include <string>
#include <iostream>
#include <fstream>
#include <filesystem>

using namespace std;
using namespace std::filesystem;

int main()
{
    const wchar_t* p{ L"C:/Users/Public/Documents" };
    path filePath(p);

    filePath /= L"NewFile.txt";

    // Open, write to, and close the file.
    wofstream writeFile(filePath, ios::out);  // implicit conversion
    writeFile << L"Lorem ipsum\nDolor sit amet";
    writeFile.close();

    // Open, read, and close the file.
    wifstream readFile;
    wstring line;
    readFile.open(filePath);  // implicit conversions
    wcout << L"File " << filePath << L" contains:" << endl;
    while (readFile.good())
    {
        getline(readFile, line);
        wcout << line << endl;
    }
    readFile.close();

    wcout << endl << L"Press Enter to exit" << endl;
    wstring input;
    getline(wcin, input);
}
```

```Output
File C:\Users\Public\Documents\NewFile.txt contains:
Lorem ipsum
Dolor sit amet

Press Enter to exit
```

## <a name="iterating-directories-and-files"></a>循环访问目录和文件

`<filesystem>`标头提供 [`directory_iterator`](../standard-library/directory-iterator-class.md) 类型以循环访问单个目录，并提供 [`recursive_directory_iterator`](../standard-library/recursive-directory-iterator-class.md) 类以递归方式循环访问目录及其子目录。 通过向迭代器传递一个 `path` 对象来构造该迭代器之后，该迭代器指向路径中的第一个 directory_entry。 通过调用默认构造函数创建结尾迭代器。

循环访问目录时，可能会发现几种类型的项。 这些项包括目录、文件、符号链接和套接字文件等。 将 `directory_iterator` 其项作为 [`directory_entry`](../standard-library/directory-entry-class.md) 对象返回。
