---
description: '了解详细信息：数组类 (c + + 标准库) '
title: array 类（C++ 标准库）| Microsoft 文档
ms.date: 11/13/2019
f1_keywords:
- array/std::array
- array/std::array::const_iterator
- array/std::array::const_pointer
- array/std::array::const_reference
- array/std::array::const_reverse_iterator
- array/std::array::difference_type
- array/std::array::iterator
- array/std::array::pointer
- array/std::array::reference
- array/std::array::reverse_iterator
- array/std::array::size_type
- array/std::array::value_type
- array/std::array::assign
- array/std::array::at
- array/std::array::back
- array/std::array::begin
- array/std::array::cbegin
- array/std::array::cend
- array/std::array::crbegin
- array/std::array::crend
- array/std::array::data
- array/std::array::empty
- array/std::array::end
- array/std::array::fill
- array/std::array::front
- array/std::array::max_size
- array/std::array::rbegin
- array/std::array::rend
- array/std::array::size
- array/std::array::swap
- array/std::array::operator=
- array/std::array::operator[]
helpviewer_keywords:
- std::array [C++]
- std::array [C++], const_iterator
- std::array [C++], const_pointer
- std::array [C++], const_reference
- std::array [C++], const_reverse_iterator
- std::array [C++], difference_type
- std::array [C++], iterator
- std::array [C++], pointer
- std::array [C++], reference
- std::array [C++], reverse_iterator
- std::array [C++], size_type
- std::array [C++], value_type
- std::array [C++], assign
- std::array [C++], at
- std::array [C++], back
- std::array [C++], begin
- std::array [C++], cbegin
- std::array [C++], cend
- std::array [C++], crbegin
- std::array [C++], crend
- std::array [C++], data
- std::array [C++], empty
- std::array [C++], end
- std::array [C++], fill
- std::array [C++], front
- std::array [C++], max_size
- std::array [C++], rbegin
- std::array [C++], rend
- std::array [C++], size
- std::array [C++], swap
- ', '
- std::array [C++], const_iterator
- std::array [C++], const_pointer
- std::array [C++], const_reference
- std::array [C++], const_reverse_iterator
- std::array [C++], difference_type
- std::array [C++], iterator
- std::array [C++], pointer
- std::array [C++], reference
- std::array [C++], reverse_iterator
- std::array [C++], size_type
- std::array [C++], value_type
- std::array [C++], assign
- std::array [C++], at
- std::array [C++], back
- std::array [C++], begin
- std::array [C++], cbegin
- std::array [C++], cend
- std::array [C++], crbegin
- std::array [C++], crend
- std::array [C++], data
- std::array [C++], empty
- std::array [C++], end
- std::array [C++], fill
- std::array [C++], front
- std::array [C++], max_size
- std::array [C++], rbegin
- std::array [C++], rend
- std::array [C++], size
- std::array [C++], swap
ms.assetid: fdfd43a5-b2b5-4b9e-991f-93bf10fb4293
ms.openlocfilehash: ba5fe51420d2f81bfd2ba90b02fe530ba5441d3d
ms.sourcegitcommit: a89eac9acdbd54a181e3bd5d5bc71a3ef3c1abca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "106506008"
---
# <a name="array-class-c-standard-library"></a>`array` 类 (c + + 标准库) 

描述了一个对象，此对象控制类型 `Ty` 的元素的长度序列 `N`。 此序列存储为 `Ty` 的数组，包含在 `array<Ty, N>` 对象中。

## <a name="syntax"></a>语法

```cpp
template <class Ty, std::size_t N>
class array;
```

### <a name="parameters"></a>参数

`Ty`\
元素的类型。

`N`\
元素数量。

## <a name="members"></a>成员

|类型定义|说明|
|-|-|
|[`const_iterator`](#const_iterator)|受控序列的常量迭代器的类型。|
|[`const_pointer`](#const_pointer)|元素的常量指针的类型。|
|[`const_reference`](#const_reference)|元素的常量引用的类型。|
|[`const_reverse_iterator`](#const_reverse_iterator)|受控序列的常量反向迭代器的类型。|
|[`difference_type`](#difference_type)|两个元素间的带符号距离的类型。|
|[`iterator`](#iterator)|受控序列的迭代器的类型。|
|[`pointer`](#pointer)|指向元素的指针的类型。|
|[`reference`](#reference)|元素的引用的类型。|
|[`reverse_iterator`](#reverse_iterator)|受控序列的反向迭代器的类型。|
|[`size_type`](#size_type)|两个元素间的无符号距离的类型。|
|[`value_type`](#value_type)|元素的类型。|

|成员函数|说明|
|-|-|
|[`array`](#array)|构造一个数组对象。|
|[`assign`](#assign)| (已过时。 使用 `fill` 。 ) 替换所有元素。|
|[`at`](#at)|访问指定位置处的元素。|
|[`back`](#back)|访问最后一个元素。|
|[`begin`](#begin)|指定受控序列的开头。|
|[`cbegin`](#cbegin)|返回一个随机访问常量迭代器，它指向数组中的第一个元素。|
|[`cend`](#cend)|返回一个随机访问常量迭代器，它指向刚超过数组末尾的位置。|
|[`crbegin`](#crbegin)|返回一个指向反向数据中第一个元素的常量迭代器。|
|[`crend`](#crend)|返回一个指向反向数组末尾的常量迭代器。|
|[`data`](#data)|获取第一个元素的地址。|
|[`empty`](#empty)|测试元素是否存在。|
|[`end`](#end)|指定受控序列的末尾。|
|[`fill`](#fill)|将所有元素替换为指定值。|
|[`front`](#front)|访问第一个元素。|
|[`max_size`](#max_size)|对元素数进行计数。|
|[`rbegin`](#rbegin)|指定反向受控序列的开头。|
|[`rend`](#rend)|指定反向受控序列的末尾。|
|[`size`](#size)|对元素数进行计数。|
|[`swap`](#swap)|交换两个容器的内容。|

|运算符|说明|
|-|-|
|[`array::operator=`](#op_eq)|替换受控序列。|
|[`array::operator[]`](#op_at)|访问指定位置处的元素。|

## <a name="remarks"></a>备注

此类型具有默认的构造函数 `array()` 和默认的赋值运算符 `operator=`，并且满足 `aggregate` 的要求。 因此，可使用聚合初始化表达式来初始化类型 `array<Ty, N>` 的对象。 例如，

```cpp
array<int, 4> ai = { 1, 2, 3 };
```

创建包含四个整数值的对象 `ai`，分别将前三个元素初始化为值 1、2 和 3，并将第四个元素初始化为 0。

## <a name="requirements"></a>要求

**标头：**`<array>`

**命名空间：** `std`

## <a name="arrayarray"></a><a name="array"></a> `array::array`

构造一个数组对象。

```cpp
array();

array(const array& right);
```

### <a name="parameters"></a>参数

*`right`*\
要插入的对象或范围。

### <a name="remarks"></a>备注

默认构造函数 `array()` 将受控序列保留为未初始化（或默认已初始化）。 使用它来指定未初始化的控制序列。

复制构造函数 `array(const array& right)` 用序列 [*right* `.begin()` ， *right*) 初始化受控序列 `.end()` 。 用于指定初始受控序列，该序列是由数组对象控制的序列的副本 *`right`* 。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    typedef std::array<int, 4> Myarray;

    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    Myarray c1(c0);

    // display contents " 0 1 2 3"
    for (const auto& it : c1)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0 1 2 3
```

## <a name="arrayassign"></a><a name="assign"></a> `array::assign`

在 c + + 11 中已过时，替换为 [`fill`](#fill) 。 替换所有元素。

## <a name="arrayat"></a><a name="at"></a> `array::at`

访问指定位置处的元素。

```cpp
reference at(size_type off);

constexpr const_reference at(size_type off) const;
```

### <a name="parameters"></a>参数

*`off`*\
要访问的元素的位置。

### <a name="remarks"></a>备注

成员函数返回对受控序列中位置处的元素的引用 *`off`* 。 如果该位置无效，则该函数将引发 `out_of_range` 类的对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display odd elements " 1 3"
    std::cout << " " << c0.at(1);
    std::cout << " " << c0.at(3);
    std::cout << std::endl;

    return (0);
}
```

## <a name="arrayback"></a><a name="back"></a> `array::back`

访问最后一个元素。

```cpp
reference back();

constexpr const_reference back() const;
```

### <a name="remarks"></a>备注

成员函数返回对受控序列的最后一个元素的引用，受控序列必须为非空。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display last element " 3"
    std::cout << " " << c0.back();
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
3
```

## <a name="arraybegin"></a><a name="begin"></a> `array::begin`

指定受控序列的开头。

```cpp
iterator begin() noexcept;
const_iterator begin() const noexcept;
```

### <a name="remarks"></a>备注

该成员函数返回一个随机访问迭代器，指向序列的第一个元素（或刚超出空序列末尾的位置）。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display first element " 0"
    Myarray::iterator it2 = c0.begin();
    std::cout << " " << *it2;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0
```

## <a name="arraycbegin"></a><a name="cbegin"></a> `array::cbegin`

返回一个 **`const`** 迭代器，该迭代器用于寻址范围内的第一个元素。

```cpp
const_iterator cbegin() const noexcept;
```

### <a name="return-value"></a>返回值

一个 **`const`** 随机访问迭代器，指向范围的第一个元素，或刚超出空范围末尾 (空范围) 的位置 `cbegin() == cend()` 。

### <a name="remarks"></a>备注

由于使用 `cbegin` 的返回值，因此不能修改范围中的元素。

可以使用此成员函数替代 `begin()` 成员函数，以保证返回值为 `const_iterator`。 通常，它与 [`auto`](../cpp/auto-cpp.md) 类型推导关键字一起使用，如下面的示例中所示。 在此示例中，将视为 `Container` 支持和的任何类型的可修改 (非 **`const`**) 容器 `begin()` `cbegin()` 。

```cpp
auto i1 = Container.begin();
// i1 is Container<T>::iterator
auto i2 = Container.cbegin();

// i2 is Container<T>::const_iterator
```

## <a name="arraycend"></a><a name="cend"></a> `array::cend`

返回一个 **`const`** 迭代器，该迭代器用于寻址范围内最后一个元素之外的位置。

```cpp
const_iterator cend() const noexcept;
```

### <a name="return-value"></a>返回值

指向刚超出范围末尾的位置的随机访问迭代器。

### <a name="remarks"></a>备注

`cend` 用于测试迭代器是否超过了其范围的末尾。

可以使用此成员函数替代 `end()` 成员函数，以保证返回值为 `const_iterator`。 通常，它与 [`auto`](../cpp/auto-cpp.md) 类型推导关键字一起使用，如下面的示例中所示。 在此示例中，将视为 `Container` 支持和的任何类型的可修改 (非 **`const`**) 容器 `end()` `cend()` 。

```cpp
auto i1 = Container.end();
// i1 is Container<T>::iterator
auto i2 = Container.cend();

// i2 is Container<T>::const_iterator
```

不应对 `cend` 返回的值取消引用。

## <a name="arrayconst_iterator"></a><a name="const_iterator"></a> `array::const_iterator`

受控序列的常量迭代器的类型。

```cpp
typedef implementation-defined const_iterator;
```

### <a name="remarks"></a>备注

该类型描述可用作受控序列的常量随机访问迭代器的对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> MyArray;

int main()
{
    MyArray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    std::cout << "it1:";
    for (MyArray::const_iterator it1 = c0.begin();
        it1 != c0.end();
        ++it1) {
        std::cout << " " << *it1;
    }
    std::cout << std::endl;

    // display first element " 0"
    MyArray::const_iterator it2 = c0.begin();
    std::cout << "it2:";
    std::cout << " " << *it2;
    std::cout << std::endl;

    return (0);
}
```

```Output
it1: 0 1 2 3
it2: 0
```

## <a name="arrayconst_pointer"></a><a name="const_pointer"></a> `array::const_pointer`

元素的常量指针的类型。

```cpp
typedef const Ty *const_pointer;
```

### <a name="remarks"></a>备注

该类型描述了可用作指向序列中元素的常量指针的对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display first element " 0"
    Myarray::const_pointer ptr = &*c0.begin();
    std::cout << " " << *ptr;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0
```

## <a name="arrayconst_reference"></a><a name="const_reference"></a> `array::const_reference`

元素的常量引用的类型。

```cpp
typedef const Ty& const_reference;
```

### <a name="remarks"></a>备注

该类型将可作为常量引用的对象描述为受控序列中的元素。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display first element " 0"
    Myarray::const_reference ref = *c0.begin();
    std::cout << " " << ref;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0
```

## <a name="arrayconst_reverse_iterator"></a><a name="const_reverse_iterator"></a> `array::const_reverse_iterator`

受控序列的常量反向迭代器的类型。

```cpp
typedef std::reverse_iterator<const_iterator> const_reverse_iterator;
```

### <a name="remarks"></a>备注

该类型描述为可用作受控序列的常量反向迭代器的对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display last element " 3"
    Myarray::const_reverse_iterator it2 = c0.rbegin();
    std::cout << " " << *it2;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
3
```

## <a name="arraycrbegin"></a><a name="crbegin"></a> `array::crbegin`

返回一个指向反向数据中第一个元素的常量迭代器。

```cpp
const_reverse_iterator crbegin() const;
```

### <a name="return-value"></a>返回值

发现反向数组中的第一个元素或发现曾是非反向数组中的最后一个元素的元素的常量反向随机访问迭代器。

### <a name="remarks"></a>备注

返回值为 `crbegin` 时，无法修改数组对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

int main( )
{
   using namespace std;
   array<int, 2> v1 = {1, 2};
   array<int, 2>::iterator v1_Iter;
   array<int, 2>::const_reverse_iterator v1_rIter;

   v1_Iter = v1.begin( );
   cout << "The first element of array is "
        << *v1_Iter << "." << endl;

   v1_rIter = v1.crbegin( );
   cout << "The first element of the reversed array is "
        << *v1_rIter << "." << endl;
}
```

```Output
The first element of array is 1.
The first element of the reversed array is 2.
```

## <a name="arraycrend"></a><a name="crend"></a> `array::crend`

返回用于寻址反向数组中最后一个元素之后的位置的常量迭代器。

```cpp
const_reverse_iterator crend() const noexcept;
```

### <a name="return-value"></a>返回值

用于寻址反向数组中最后一个元素之后的位置（非反向数组中第一个元素之前的位置）的常量反向随机存取迭代器。

### <a name="remarks"></a>备注

`crend` 与反向数组一起使用，就像 [`array::cend`](#cend) 与数组一起使用一样。

如果返回值为 `crend`（适当递减），则不能修改数组对象。

`crend` 可用于测试反向迭代器是否已到达其数组末尾。

不应对 `crend` 返回的值取消引用。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

int main( )
{
   using namespace std;
   array<int, 2> v1 = {1, 2};
   array<int, 2>::const_reverse_iterator v1_rIter;

   for ( v1_rIter = v1.rbegin( ) ; v1_rIter != v1.rend( ) ; v1_rIter++ )
      cout << *v1_rIter << endl;
}
```

```Output
2
1
```

## <a name="arraydata"></a><a name="data"></a> `array::data`

获取第一个元素的地址。

```cpp
Ty *data();

const Ty *data() const;
```

### <a name="remarks"></a>备注

成员函数返回受控序列中的第一个元素的地址。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display first element " 0"
    Myarray::pointer ptr = c0.data();
    std::cout << " " << *ptr;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0
```

## <a name="arraydifference_type"></a><a name="difference_type"></a> `array::difference_type`

两个元素间的带符号距离的类型。

```cpp
typedef std::ptrdiff_t difference_type;
```

### <a name="remarks"></a>备注

带符号的整数类型描述一个可表示受控序列中任意两个元素的地址之间的差异的对象。 它是类型 `std::ptrdiff_t`的同义词。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display distance first-last " -4"
    Myarray::difference_type diff = c0.begin() - c0.end();
    std::cout << " " << diff;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
-4
```

## <a name="arrayempty"></a><a name="empty"></a> `array::empty`

测试元素是否存在。

```cpp
constexpr bool empty() const;
```

### <a name="remarks"></a>备注

仅当 `N == 0` 时，此成员函数才返回 true。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display whether c0 is empty " false"
    std::cout << std::boolalpha << " " << c0.empty();
    std::cout << std::endl;

    std::array<int, 0> c1;

    // display whether c1 is empty " true"
    std::cout << std::boolalpha << " " << c1.empty();
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
false
true
```

## <a name="arrayend"></a><a name="end"></a> `array::end`

指定受控序列的末尾。

```cpp
reference end();

const_reference end() const;
```

### <a name="remarks"></a>备注

成员函数返回一个随机访问迭代器，它指向刚超出序列末尾的位置。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display last element " 3"
    Myarray::iterator it2 = c0.end();
    std::cout << " " << *--it2;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
3
```

## <a name="arrayfill"></a><a name="fill"></a> `array::fill`

清除数组并将指定的元素复制到该空数组。

```cpp
void fill(const Type& val);
```

### <a name="parameters"></a>参数

*`val`*\
要插入到数组中的元素的值。

### <a name="remarks"></a>备注

`fill` 将数组的每个元素替换为指定的值。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

int main()
{
    using namespace std;
    array<int, 2> v1 = { 1, 2 };

    cout << "v1 = ";
    for (const auto& it : v1)
    {
        std::cout << " " << it;
    }
    cout << endl;

    v1.fill(3);
    cout << "v1 = ";
    for (const auto& it : v1)
    {
        std::cout << " " << it;
    }
    cout << endl;
}
```

## <a name="arrayfront"></a><a name="front"></a> `array::front`

访问第一个元素。

```cpp
reference front();

constexpr const_reference front() const;
```

### <a name="remarks"></a>备注

成员函数返回对受控序列的第一个元素的引用，该元素必须为非空。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display first element " 0"
    std::cout << " " << c0.front();
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0
```

## <a name="arrayiterator"></a><a name="iterator"></a> `array::iterator`

受控序列的迭代器的类型。

```cpp
typedef implementation-defined iterator;
```

### <a name="remarks"></a>备注

该类型描述可用作受控序列的随机访问迭代器的对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> MyArray;

int main()
{
    MyArray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    std::cout << "it1:";
    for (MyArray::iterator it1 = c0.begin();
        it1 != c0.end();
        ++it1) {
        std::cout << " " << *it1;
    }
    std::cout << std::endl;

    // display first element " 0"
    MyArray::iterator it2 = c0.begin();
    std::cout << "it2:";
    std::cout << " " << *it2;
    std::cout << std::endl;

    return (0);
}
```

```Output
it1: 0 1 2 3

it2: 0
```

## <a name="arraymax_size"></a><a name="max_size"></a> `array::max_size`

对元素数进行计数。

```cpp
constexpr size_type max_size() const;
```

### <a name="remarks"></a>备注

成员函数返回 `N`。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display (maximum) size " 4"
    std::cout << " " << c0.max_size();
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
4
```

## <a name="arrayoperator"></a><a name="op_at"></a> `array::operator[]`

访问指定位置处的元素。

```cpp
reference operator[](size_type off);

constexpr const_reference operator[](size_type off) const;
```

### <a name="parameters"></a>参数

*`off`*\
要访问的元素的位置。

### <a name="remarks"></a>备注

成员函数返回对受控序列中位置处的元素的引用 *`off`* 。 如果该位置无效，则该行为未定义。

还有一个 [`get`](array-functions.md#get) 可用于获取对的元素的引用的非成员函数 **`array`** 。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display odd elements " 1 3"
    std::cout << " " << c0[1];
    std::cout << " " << c0[3];
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
1 3
```

## <a name="arrayoperator"></a><a name="op_eq"></a> `array::operator=`

替换受控序列。

```cpp
array<Value> operator=(array<Value> right);
```

### <a name="parameters"></a>参数

*`right`*\
用于复制的容器。

### <a name="remarks"></a>备注

成员运算符将的每个元素分配 *`right`* 给受控序列的相应元素，然后返回 **`*this`** 。 用于将受控序列替换为中受控序列的副本 *`right`* 。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    Myarray c1;
    c1 = c0;

    // display copied contents " 0 1 2 3"
        // display contents " 0 1 2 3"
    for (auto it : c1)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0 1 2 3
```

## <a name="arraypointer"></a><a name="pointer"></a> `array::pointer`

指向元素的指针的类型。

```cpp
typedef Ty *pointer;
```

### <a name="remarks"></a>备注

该类型描述了可用作指向序列中元素的指针的对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display first element " 0"
    Myarray::pointer ptr = &*c0.begin();
    std::cout << " " << *ptr;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0
```

## <a name="arrayrbegin"></a><a name="rbegin"></a> `array::rbegin`

指定反向受控序列的开头。

```cpp
reverse_iterator rbegin()noexcept;
const_reverse_iterator rbegin() const noexcept;
```

### <a name="remarks"></a>备注

成员函数返回一个反向迭代器，它指向刚超出受控序列末尾的位置。 因此，它指定反向序列的开头。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display last element " 3"
    Myarray::const_reverse_iterator it2 = c0.rbegin();
    std::cout << " " << *it2;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
3
```

## <a name="arrayreference"></a><a name="reference"></a> `array::reference`

元素的引用的类型。

```cpp
typedef Ty& reference;
```

### <a name="remarks"></a>备注

该类型描述了可用作对受控序列中元素的引用的对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display first element " 0"
    Myarray::reference ref = *c0.begin();
    std::cout << " " << ref;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0
```

## <a name="arrayrend"></a><a name="rend"></a> `array::rend`

指定反向受控序列的末尾。

```cpp
reverse_iterator rend()noexcept;
const_reverse_iterator rend() const noexcept;
```

### <a name="remarks"></a>备注

该成员函数返回一个反向迭代器，指向序列的第一个元素（或刚超出空序列末尾的位置）。 因此，它指定反向序列的末尾。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display first element " 0"
    Myarray::const_reverse_iterator it2 = c0.rend();
    std::cout << " " << *--it2;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0
```

## <a name="arrayreverse_iterator"></a><a name="reverse_iterator"></a> `array::reverse_iterator`

受控序列的反向迭代器的类型。

```cpp
typedef std::reverse_iterator<iterator> reverse_iterator;
```

### <a name="remarks"></a>备注

此类型描述为可用作受控序列的反向迭代器的对象。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display last element " 3"
    Myarray::reverse_iterator it2 = c0.rbegin();
    std::cout << " " << *it2;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
3
```

## <a name="arraysize"></a><a name="size"></a> `array::size`

对元素数进行计数。

```cpp
constexpr size_type size() const;
```

### <a name="remarks"></a>备注

成员函数返回 `N`。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display size " 4"
    std::cout << " " << c0.size();
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
4
```

## <a name="arraysize_type"></a><a name="size_type"></a> `array::size_type`

两个元素间的无符号距离的类型。

```cpp
typedef std::size_t size_type;
```

### <a name="remarks"></a>备注

无符号的整数类型描述可表示任何受控序列长度的对象。 它是类型 `std::size_t`的同义词。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display distance last-first " 4"
    Myarray::size_type diff = c0.end() - c0.begin();
    std::cout << " " << diff;
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
4
```

## <a name="arrayswap"></a><a name="swap"></a> `array::swap`

将此数组的内容交换到另一个数组。

```cpp
void swap(array& right);
```

### <a name="parameters"></a>参数

*`right`*\
要与其交换内容的数组。

### <a name="remarks"></a>备注

成员函数交换和右之间的受控 **`*this`** 序列。 它执行与 `N` 成正比的多个元素分配和构造函数调用。

还有一个 [`swap`](array-functions.md#swap) 可用于交换两个实例的非成员函数 **`array`** 。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    Myarray c1 = { 4, 5, 6, 7 };
    c0.swap(c1);

    // display swapped contents " 4 5 6 7"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    swap(c0, c1);

    // display swapped contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
4 5 6 7
0 1 2 3
```

## <a name="arrayvalue_type"></a><a name="value_type"></a> `array::value_type`

元素的类型。

```cpp
typedef Ty value_type;
```

### <a name="remarks"></a>备注

类型是模板参数 `Ty` 的同义词。

### <a name="example"></a>示例

```cpp
#include <array>
#include <iostream>

typedef std::array<int, 4> Myarray;
int main()
{
    Myarray c0 = { 0, 1, 2, 3 };

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        std::cout << " " << it;
    }
    std::cout << std::endl;

    // display contents " 0 1 2 3"
    for (const auto& it : c0)
    {
        Myarray::value_type val = it;
        std::cout << " " << val;
    }
    std::cout << std::endl;

    return (0);
}
```

```Output
0 1 2 3
0 1 2 3
```

## <a name="see-also"></a>另请参阅

[`<array>`](../standard-library/array.md)
