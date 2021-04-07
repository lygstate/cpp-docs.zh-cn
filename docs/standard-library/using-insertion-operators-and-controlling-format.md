---
description: 了解详细信息：使用插入运算符和控制格式
title: 使用插入运算符并控制格式
ms.date: 11/04/2016
helpviewer_keywords:
- insertion operators
ms.assetid: cdefe986-6548-4cd1-8a67-b431d7d36a1c
ms.openlocfilehash: 1e5098beb7ff3c83439780c2dc3f908f7fec946a
ms.sourcegitcommit: a89eac9acdbd54a181e3bd5d5bc71a3ef3c1abca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "106505995"
---
# <a name="using-insertion-operators-and-controlling-format"></a>使用插入运算符并控制格式

本主题演示如何控制格式以及如何为你自己的类创建插入运算符。 插入 (**`<<`**) 运算符（适用于所有标准 c + + 数据类型的预先编程）将字节发送到输出流对象。 插入运算符使用预定义的“操控器”，操控器是更改整数自变量的默认格式的元素。

你可以使用以下选项控制格式：

- [输出宽度](#vclrfoutputwidthanchor3)

- [对齐方式](#vclrfalignmentanchor4)

- [精度](#vclrfprecisionanchor5)

- [基数](#vclrfradixanchor6)

## <a name="output-width"></a><a name="vclrfoutputwidthanchor3"></a>输出宽度

若要对齐输出，可通过 `setw` 将操控器放置在流中或通过调用成员函数来指定每个项的输出宽度 `width` 。 此示例右对齐至少为 10 个字符宽的列中的值：

```cpp
// output_width.cpp
// compile with: /EHsc
#include <iostream>
using namespace std;

int main( )
{
   double values[] = { 1.23, 35.36, 653.7, 4358.24 };
   for( int i = 0; i < 4; i++ )
   {
      cout.width(10);
      cout << values[i] << '\n';
   }
}
```

```Output
      1.23
     35.36
     653.7
   4358.24
```

前导空白被添加到任何少于 10 个字符宽的值。

若要填充某个字段，请使用 `fill` 成员函数，该函数将为具有指定宽度的字段设置填充字符的值。 默认值为空白。 若要用星号填充数字列，请按如下所示修改上一个 **`for`** 循环：

```cpp
for (int i = 0; i <4; i++)
{
    cout.width(10);
    cout.fill('*');
    cout << values[i] << endl;
}
```

`endl` 操控器取代了换行字符 (`'\n'`)。 输出如下所示：

```Output
******1.23
*****35.36
*****653.7
***4358.24
```

若要在同一行中指定数据元素的宽度，请使用 `setw` 操控器：

```cpp
// setw.cpp
// compile with: /EHsc
#include <iostream>
#include <iomanip>
using namespace std;

int main( )
{
   double values[] = { 1.23, 35.36, 653.7, 4358.24 };
   char *names[] = { "Zoot", "Jimmy", "Al", "Stan" };
   for( int i = 0; i < 4; i++ )
      cout << setw( 7 )  << names[i]
           << setw( 10 ) << values[i] << endl;
}
```

`width`成员函数在中声明 `<iostream>` 。 如果使用 `setw` 或任何其他带参数的操控器，则必须包含 `<iomanip>` 。 在输出中，在宽度为 6 的字段中打印字符串，在宽度为 10 的字段中打印整数：

```Output
   Zoot      1.23
  Jimmy     35.36
     Al     653.7
   Stan   4358.24
```

和均不 `setw` `width` 截断值。 如果格式化输出超出宽度，则整个值受流的精度设置的约束进行打印。 `setw`和 `width` 仅影响以下字段。 已打印一个字段之后，字段宽度将恢复为其默认行为（必要宽度）。 但是，在更改之前，其他流格式选项保持有效。

## <a name="alignment"></a><a name="vclrfalignmentanchor4"></a> 关联

输出流默认为右对齐的文本。 若要左对齐上一示例中的名称并右对齐数字，请将循环替换 **`for`** 为以下内容：

```cpp
for (int i = 0; i <4; i++)
    cout << setiosflags(ios::left)
         << setw(6) << names[i]
         << resetiosflags(ios::left)
         << setw(10) << values[i] << endl;
```

输出如下所示：

```Output
Zoot        1.23
Jimmy      35.36
Al         653.7
Stan     4358.24
```

左对齐标志通过对 [`setiosflags`](../standard-library/iomanip-functions.md#setiosflags) 枚举器使用操控器来设置 `left` 。 此枚举器在类中定义 [`ios`](../standard-library/basic-ios-class.md) ，因此它的引用必须包含 **`ios::`** 前缀。 [`resetiosflags`](../standard-library/iomanip-functions.md#resetiosflags)操控器关闭左对齐标志。 与 `width` 和不同 `setw` ，和的 `setiosflags` 效果 `resetiosflags` 是永久性的。

## <a name="precision"></a><a name="vclrfprecisionanchor5"></a> Precision

浮点精度的默认值为六。 例如，数字 3466.9768 打印为 3466.98。 若要更改此值的打印方式，请使用 [`setprecision`](../standard-library/iomanip-functions.md#setprecision) 操控器。 操控器具有两个标志： [`fixed`](../standard-library/ios-functions.md#fixed) 和 [`scientific`](../standard-library/ios-functions.md#scientific) 。 如果 [`fixed`](../standard-library/ios-functions.md#fixed) 设置了，则数字将打印为3466.976800。 如果 `scientific` 已设置，则它将打印为 3.4669773 + 003。

若要显示与一个有效数字 [对齐](#vclrfalignmentanchor4) 显示的浮点数，请按如下所示替换 **`for`** 循环：

```cpp
for (int i = 0; i <4; i++)
    cout << setiosflags(ios::left)
         << setw(6)
         << names[i]
         << resetiosflags(ios::left)
         << setw(10)
         << setprecision(1)
         << values[i]
         << endl;
```

该程序将打印此列表：

```Output
Zoot          1
Jimmy     4e+01
Al        7e+02
Stan      4e+03
```

若要消除科学记数法，请在循环之前插入此语句 **`for`** ：

```cpp
cout << setiosflags(ios::fixed);
```

使用固定记数法，该程序在小数点之后使用一位数字打印。

```Output
Zoot         1.2
Jimmy       35.4
Al         653.7
Stan      4358.2
```

如果将标志更改 `ios::fixed` 为 `ios::scientific` ，则程序将打印以下内容：

```cpp
Zoot    1.2e+00
Jimmy   3.5e+01
Al      6.5e+02
Stan    4.4e+03
```

程序会再次在小数点之后打印一位数字。 如果 `ios::fixed` `ios::scientific` 设置了或，则精度值将确定小数点后的位数。 如果两个标志均未设定，则精度值将确定有效位数的总数。 `resetiosflags` 操控器清除这些标志。

## <a name="radix"></a><a name="vclrfradixanchor6"></a> 基数

`dec`、 `oct` 和操控器 `hex` 设置输入和输出的默认基数。 例如，如果将操控器插入 `hex` 到输出流中，则对象会将整数的内部数据表示形式正确地转换为十六进制输出格式。 如果默认)  (清楚标志，则以小写形式显示数字 a 到 f [`uppercase`](../standard-library/ios-functions.md#uppercase) ; 否则，将以大写形式显示。 默认基数 `dec` (decimal) 。

## <a name="quoted-strings-c14"></a>引用字符串 (C++14)

将字符串插入到流时，可以通过调用成员函数轻松地检索相同的字符串 `stringstream::str()` 。 但是，如果你想要使用提取运算符在以后将流插入新字符串，可能会收到意外结果，因为 `>>` 默认情况下，运算符在遇到第一个空格字符时将停止。

```cpp
std::stringstream ss;
std::string inserted = "This is a sentence.";
std::string extracted;

ss << inserted;
ss >> extracted;

std::cout << inserted;     //  This is a sentence.
std::cout << extracted;    //  This
```

可以手动克服这种行为，但为了使字符串往返过程更方便，C++14 在 `<iomanip>` 中添加了 `std::quoted` 流操控器。 插入时， `quoted()` 使用一个分隔符（默认情况下为双引号 ' " '）包围字符串，且在提取时，操作流以提取所有字符直到遇到最后一个分隔符。 任何嵌入的引号都使用转义符进行转义（默认为“\\\\”）。

分隔符仅存在于流对象中;它们不存在于提取的字符串中，但它们存在于返回的字符串中 [`basic_stringstream::str`](../standard-library/basic-stringstream-class.md#str) 。

插入和提取操作的空格行为不依赖于字符串在代码中的表示方式，因此，无论输入的字符串是原始字符串文本还是规则的字符串，带引号的运算符都很有用。 输入字符串，无论其格式是什么，都可以有嵌入的引号、换行符、制表符等等，操控程序将保留所有这些内容 `quoted()` 。

有关详细信息和完整代码示例，请参阅 [`quoted`](../standard-library/iomanip-functions.md#quoted) 。

## <a name="see-also"></a>另请参阅

[输出流](../standard-library/output-streams.md)
