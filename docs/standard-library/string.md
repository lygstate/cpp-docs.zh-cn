---
description: 了解更多： &lt; 字符串&gt;
title: '&lt;字符串&gt;'
ms.date: 11/04/2016
f1_keywords:
- <string>
helpviewer_keywords:
- string header
ms.assetid: a2fb9d00-d7ae-4170-bfea-2dc337aa37cf
ms.openlocfilehash: d8b89bf1a9621e863f6608e46557d374cd8e6245
ms.sourcegitcommit: a89eac9acdbd54a181e3bd5d5bc71a3ef3c1abca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "106506112"
---
# `<string>`

定义容器类模板 `basic_string` 和各种支持模板。

有关的详细信息 `basic_string` ，请参阅[ `basic_string` 类](../standard-library/basic-string-class.md)

## <a name="syntax"></a>语法

```cpp
#include <string>
```

## <a name="remarks"></a>备注

C++ 语言和 C++ 标准库支持两种类型的字符串：

- 以 null 结尾的字符数组通常作为 C 字符串被引用。

- 类模板对象（类型为 `basic_string` ），它处理 **`char`** 类似于的所有模板参数。

### <a name="typedefs"></a>Typedef

|类型名称|描述|
|-|-|
|[`string`](../standard-library/string-typedefs.md#string)|一种类型，它使用类型为的元素来描述类模板的专用化 `basic_string` **`char`** `string` 。|
|[`wstring`](../standard-library/string-typedefs.md#wstring)|一种类型，它使用类型为的元素来描述类模板的专用化 `basic_string` **`wchar_t`** `wstring` 。|
|[`u16string`](../standard-library/string-typedefs.md#u16string)|一种类型，它基于类型的元素描述类模板的专用化 `basic_string` **`char16_t`** 。|
|[`u32string`](../standard-library/string-typedefs.md#u32string)|一种类型，它基于类型的元素描述类模板的专用化 `basic_string` **`char32_t`** 。|

### <a name="operators"></a>运算符

|运算符|说明|
|-|-|
|[`operator+`](../standard-library/string-operators.md#op_add)|连接两个字符串对象。|
|[`operator!=`](../standard-library/string-operators.md#op_neq)|测试运算符左侧的字符串对象是否不等于右侧的字符串对象。|
|[`operator==`](../standard-library/string-operators.md#op_eq_eq)|测试运算符左侧的字符串对象是否等于右侧的字符串对象。|
|[`operator<`](../standard-library/string-operators.md#op_lt)|测试运算符左侧的字符串对象是否小于右侧的字符串对象。|
|[`operator<=`](../standard-library/string-operators.md#op_lt_eq)|测试运算符左侧的字符串对象是否小于或等于右侧的字符串对象。|
|[`operator<<`](../standard-library/string-operators.md#op_lt_lt)|一个模板函数，用于向输出流插入字符串。|
|[`operator>`](../standard-library/string-operators.md#op_gt)|测试运算符左侧的字符串对象是否大于右侧的字符串对象。|
|[`operator>=`](../standard-library/string-operators.md#op_gt_eq)|测试运算符左侧的字符串对象是否大于或等于右侧的字符串对象。|
|[`operator>>`](../standard-library/string-operators.md#op_gt_gt)|一个模板函数，用于从输入流提取字符串。|

### <a name="specialized-template-functions"></a>专用化模板函数

|名称|说明|
|-|-|
|`hash`|生成字符串的哈希。|
|[`swap`](../standard-library/string-functions.md#swap)|交换两个字符串的字符数组。|
|[`stod`](../standard-library/string-functions.md#stod)|将字符序列转换为 **`double`** 。|
|[`stof`](../standard-library/string-functions.md#stof)|将字符序列转换为 **`float`** 。|
|[`stoi`](../standard-library/string-functions.md#stoi)|将字符序列转换为 **`int`** 。|
|[`stold`](../standard-library/string-functions.md#stold)|将字符序列转换为 **`long double`** 。|
|[`stoll`](../standard-library/string-functions.md#stoll)|将字符序列转换为 **`long long`** 。|
|[`stoul`](../standard-library/string-functions.md#stoul)|将字符序列转换为 **`unsigned long`** 。|
|[`stoull`](../standard-library/string-functions.md#stoull)|将字符序列转换为 **`unsigned long long`** 。|
|[`to_string`](../standard-library/string-functions.md#to_string)|将一个值转换为 `string`。|
|[`to_wstring`](../standard-library/string-functions.md#to_wstring)|将一个值转换为宽字符串。|

### <a name="functions"></a>函数

|函数|说明|
|-|-|
|[`getline` 模版](../standard-library/string-functions.md#getline)|`string`从输入流中按行提取。|

### <a name="classes"></a>类

|类|说明|
|-|-|
|[`basic_string` 班级](../standard-library/basic-string-class.md)|一个类模板，用于描述可存储任意类似于字符的对象序列的对象。|
|[`char_traits` 结构](../standard-library/char-traits-struct.md)|一个类模板，用于描述与类型的字符关联的特性。 `CharType`|

### <a name="specializations"></a>专用化

|名称|说明|
|-|-|
|[`char_traits<char>` 结构](../standard-library/char-traits-char-struct.md)|一个结构，它是模板结构 `char_traits<CharType>` 对类型的元素的专用化 **`char`** 。|
|[`char_traits<wchar_t>` 结构](../standard-library/char-traits-wchar-t-struct.md)|一个结构，它是模板结构 `char_traits<CharType>` 对类型的元素的专用化 **`wchar_t`** 。|
|[`char_traits<char16_t>` 结构](../standard-library/char-traits-char16-t-struct.md)|一个结构，它是模板结构 `char_traits<CharType>` 对类型的元素的专用化 **`char16_t`** 。|
|[`char_traits<char32_t>` 结构](../standard-library/char-traits-char32-t-struct.md)|一个结构，它是模板结构 `char_traits<CharType>` 对类型的元素的专用化 **`char32_t`** 。|

## <a name="requirements"></a>要求

- **标头：**`<string>`

- **命名空间:** std

## <a name="see-also"></a>另请参阅

[标头文件引用](../standard-library/cpp-standard-library-header-files.md)\
[C + + 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)
