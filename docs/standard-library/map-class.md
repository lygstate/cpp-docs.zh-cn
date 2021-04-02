---
title: map 类
description: C + + 标准模板库的 API 参考 (STL) `map` 类，可用于存储和检索集合中的数据，其中每个元素都是具有数据值和排序键的对。
ms.date: 9/10/2020
f1_keywords:
- map/std::map
- map/std::map::allocator_type
- map/std::map::const_iterator
- map/std::map::const_pointer
- map/std::map::const_reference
- map/std::map::const_reverse_iterator
- map/std::map::difference_type
- map/std::map::iterator
- map/std::map::key_compare
- map/std::map::key_type
- map/std::map::mapped_type
- map/std::map::pointer
- map/std::map::reference
- map/std::map::reverse_iterator
- map/std::map::size_type
- map/std::map::value_type
- map/std::map::at
- map/std::map::begin
- map/std::map::cbegin
- map/std::map::cend
- map/std::map::clear
- map/std::map::count
- map/std::map::contains
- map/std::map::crbegin
- map/std::map::crend
- map/std::map::emplace
- map/std::map::emplace_hint
- map/std::map::empty
- map/std::map::end
- map/std::map::equal_range
- map/std::map::erase
- map/std::map::find
- map/std::map::get_allocator
- map/std::map::insert
- map/std::map::key_comp
- map/std::map::lower_bound
- map/std::map::max_size
- map/std::map::rbegin
- map/std::map::rend
- map/std::map::size
- map/std::map::swap
- map/std::map::upper_bound
- map/std::map::value_comp
helpviewer_keywords:
- std::map [C++]
- std::map [C++], allocator_type
- std::map [C++], const_iterator
- std::map [C++], const_pointer
- std::map [C++], const_reference
- std::map [C++], const_reverse_iterator
- std::map [C++], difference_type
- std::map [C++], iterator
- std::map [C++], key_compare
- std::map [C++], key_type
- std::map [C++], mapped_type
- std::map [C++], pointer
- std::map [C++], reference
- std::map [C++], reverse_iterator
- std::map [C++], size_type
- std::map [C++], value_type
- std::map [C++], at
- std::map [C++], begin
- std::map [C++], cbegin
- std::map [C++], cend
- std::map [C++], clear
- std::map [C++], count
- std::map [C++], contains
- std::map [C++], crbegin
- std::map [C++], crend
- std::map [C++], emplace
- std::map [C++], emplace_hint
- std::map [C++], empty
- std::map [C++], end
- std::map [C++], equal_range
- std::map [C++], erase
- std::map [C++], find
- std::map [C++], get_allocator
- std::map [C++], insert
- std::map [C++], key_comp
- std::map [C++], lower_bound
- std::map [C++], max_size
- std::map [C++], rbegin
- std::map [C++], rend
- std::map [C++], size
- std::map [C++], swap
- std::map [C++], upper_bound
- std::map [C++], value_comp
ms.openlocfilehash: 7d8e4c674e525f1b67f000403791c7ccdb2f9673
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099737"
---
# <a name="map-class"></a>`map` 类

用于存储和检索集合中的数据，此集合中的每个元素均为包含数据值和排序键的元素对。 键的值是唯一的，用于自动排序数据。

可以直接更改映射中的元素值。 键值是常量，不能更改。 必须先删除与旧元素关联的键值，才能为新元素插入新键值。

## <a name="syntax"></a>语法

```cpp
template <class Key,
    class Type,
    class Traits = less<Key>,
    class Allocator=allocator<pair <const Key, Type>>>
class map;
```

### <a name="parameters"></a>参数

*`Key`*\
要存储在中的键数据类型 `map` 。

*`Type`*\
要在 `map` 中存储的元素数据类型。

*`Traits`*\
提供一个函数对象的类型，该函数对象可将两个元素值作为排序键进行比较，以确定它们在中的相对顺序 `map` 。 此参数为可选自变量，默认值是二元谓词 `less<Key>`。

在 c + + 14 中，可以通过指定没有类型参数的谓词来启用异类查找 `std::less<>` 。 有关详细信息，请参阅 [关联容器中的异类查找](../standard-library/stl-containers.md#sequence_containers) 。

*`Allocator`*\
一种表示存储的分配器对象的类型，该分配器对象封装有关映射的内存分配和解除分配的详细信息。 此参数为可选参数，默认值为 `allocator<pair<const Key, Type> >`。

## <a name="remarks"></a>注解

C++ 标准库 map 类为：

- 大小可变的关联容器，基于关联键值高效检索元素值。

- 可逆，因为它提供双向迭代器来访问其元素。

- 有序，因为它的元素根据指定的比较函数按键值排序。

- 唯一。 因为它的每个元素必须具有唯一键。

- 关联容器对，因为它的元素数据值与其键值不同。

- 类模板，因为它提供的功能是泛型的，独立于元素或键类型。 用于元素和键的数据类型作为类模板以及比较函数和分配器中的参数指定。

映射类提供的迭代器是双向迭代器，但 [`insert`](#insert) 和 [`map`](#map) 类成员函数具有将较弱输入迭代器作为模板参数的版本，较弱输入迭代器的功能要求少于双向迭代器类保证的功能要求。 不同的迭代器概念通过它们的功能优化相关联。 每个迭代器概念有它自己的一套要求，使用这些概念的算法必须受这些要求的限制。 输入迭代器可取消引用以引用某个对象，并可递增到序列中的下一迭代器。

建议你根据应用程序需要的搜索和插入类型选择容器类型。 关联容器针对查找、插入和移除操作进行了优化。 显式支持这些操作的成员函数在最差的情况下执行这些操作，这与容器中元素数的对数成正比。 插入元素不会使迭代器失效，移除元素仅会使专门指向已移除元素的迭代器失效。

建议你在应用程序满足将值与键关联的条件时，选择映射作为关联容器。 此类结构的模型是关键字排序列表，这些关键字只出现一次，并具有提供定义的关联字符串值。 如果一个词有多个正确的定义，而该密钥不是唯一的，则多重映射将成为所选容器。 如果仅存储关键字列表，则应使用集作为适当容器。 如果允许关键字多次出现，则多重集合为适当容器。

该映射通过调用存储的类型的函数对象，对它控制的元素进行排序 [`key_compare`](#key_compare) 。 此存储的对象是比较函数，可通过调用方法来访问 [`key_comp`](#key_comp) 。 通常，将比较任意两个给定的元素，以确定其中一个元素是否小于另一个元素或它们是否等效。 比较所有元素后，将创建非等效元素的排序序列。

> [!NOTE]
> 比较函数是一个二元谓词，在标准数学的意义上引发严格弱排序。 二元谓词 f (x，y) 是具有两个参数对象（x 和 y）和一个返回值（或）的函数对象 **`true`** **`false`** 。 如果二元谓词是具有自反、对称性和可传递的，则对集进行的排序将为严格弱排序，如果等效可传递，其中两个对象 x 和 y 定义为在 f (x、y) 和 f (y，x) 都是等效的 **`false`** 。 如果键之间的更强相等条件取代了等效性，则排序将为总排序（即所有元素彼此排序），并且匹配的键将难以彼此辨别。
>
> 在 c + + 14 中，可以通过指定 `std::less<>` 没有类型参数的或谓词来启用异类查找 `std::greater<>` 。 有关详细信息，请参阅 [关联容器中的异类查找](../standard-library/stl-containers.md#sequence_containers) 。

## <a name="members"></a>成员

### <a name="constructors"></a>构造函数

|名称|说明|
|-|-|
|[`map`](#map)|构造特定大小的列表、包含具有特定值的元素的列表、包含特定 `allocator` 的列表或作为其他某个映射的副本的列表。|

### <a name="typedefs"></a>Typedef

|名称|说明|
|-|-|
|[`allocator_type`](#allocator_type)|映射对象的 `allocator` 类的 typedef。|
|[`const_iterator`](#const_iterator)|可读取中的元素的双向迭代器的 typedef **`const`** `map` 。|
|[`const_pointer`](#const_pointer)|指向映射中的元素的指针的 typedef **`const`** 。|
|[`const_reference`](#const_reference)|对 **`const`** 存储在映射中以读取和执行操作的元素的引用的 typedef **`const`** 。|
|[`const_reverse_iterator`](#const_reverse_iterator)|一种类型，它提供可读取中的任何元素的双向迭代器 **`const`** `map` 。|
|[`difference_type`](#difference_type)|映射中迭代器指向的元素间范围内元素数量的有符号整数 typedef。|
|[`iterator`](#iterator)|可读取或修改映射中任何元素的双向迭代器的 typedef。|
|[`key_compare`](#key_compare)|可比较两个排序键以确定 `map` 中两个元素的相对顺序的函数对象的 typedef。|
|[`key_type`](#key_type)|存储在映射内每个元素中的排序键的 typedef。|
|[`mapped_type`](#mapped_type)|存储在映射内每个元素中的数据的 typedef。|
|[`pointer`](#pointer)|指向映射中的元素的指针的 typedef **`const`** 。|
|[`reference`](#reference)|对映射中存储的元素的引用的 typedef。|
|[`reverse_iterator`](#reverse_iterator)|可读取或修改反向映射中的元素的双向迭代器的 typedef。|
|[`size_type`](#size_type)|映射中元素数量的无符号整数 typedef。|
|[`value_type`](#value_type)|作为元素存储在映射中的对象类型的 typedef。|

### <a name="member-functions"></a>成员函数

|成员函数|说明|
|-|-|
|[`at`](#at)|查找具有指定键值的元素。|
|[`begin`](#begin)|返回一个迭代器，此迭代器指向 `map` 中的第一个元素。|
|[`cbegin`](#cbegin)|返回一个常量迭代器，该迭代器指向中的第一个元素 `map` 。|
|[`cend`](#cend)|返回一个超过末尾常量迭代器。|
|[`clear`](#clear)|清除 `map` 的所有元素。|
|[`contains`](#contains)<sup>C + + 20</sup>|检查中是否存在具有指定键的元素 `map` 。|
|[`count`](#count)|返回映射中其键与参数中指定的键匹配的元素数量。|
|[`crbegin`](#crbegin)|返回一个常量迭代器，该迭代器指向反向中的第一个元素 `map` 。|
|[`crend`](#crend)|返回一个常量迭代器，该迭代器指向反向中最后一个元素之后的位置 `map` 。|
|[`emplace`](#emplace)|将就地构造的元素插入到中 `map` 。|
|[`emplace_hint`](#emplace_hint)|使用位置提示将就地构造的元素插入到中 `map` 。|
|[`empty`](#empty)|**`true`** 如果为空，则返回 `map` 。|
|[`end`](#end)|返回超过末尾迭代器。|
|[`equal_range`](#equal_range)|返回一对迭代器。 此迭代器对中的第一个迭代器指向 `map` 中其键大于指定键的第一个元素。 此迭代器对中的第二个迭代器指向 `map` 中其键等于或大于指定键的第一个元素。|
|[`erase`](#erase)|从指定位置移除映射中的元素或元素范围。|
|[`find`](#find)|返回一个迭代器，该迭代器指向中其 `map` 键与指定键相等的元素的位置。|
|[`get_allocator`](#get_allocator)|返回用于构造 `allocator` 的 `map` 对象的副本。|
|[`insert`](#insert)|将一个或一系列元素插入到 `map` 中的指定位置。|
|[`key_comp`](#key_comp)|返回用于对中的键进行排序的比较对象的副本 `map` 。|
|[`lower_bound`](#lower_bound)|返回一个迭代器，该迭代器指向中其 `map` 键值等于或大于指定键的键值的第一个元素。|
|[`max_size`](#max_size)|返回 `map` 的最大长度。|
|[`rbegin`](#rbegin)|返回一个迭代器，此迭代器指向反向 `map` 中的第一个元素。|
|[`rend`](#rend)|返回一个迭代器，该迭代器指向反向中最后一个元素之后的位置 `map` 。|
|[`size`](#size)|返回 `map` 中的元素数量。|
|[`swap`](#swap)|交换两个映射的元素。|
|[`upper_bound`](#upper_bound)|返回一个迭代器，该迭代器指向中其 `map` 键值大于指定键的键值的第一个元素。|
|[`value_comp`](#value_comp)|检索用于对 `map` 中的元素值进行排序的比较对象副本。|

### <a name="operators"></a>运算符

|名称|说明|
|-|-|
|[`operator[]`](#op_at)|将元素插入到具有指定键值的映射。|
|[`operator=`](#op_eq)|将一个映射中的元素替换为另一映射副本。|

## <a name="allocator_type"></a><a name="allocator_type"></a> `allocator_type`

一个类型，代表映射对象分配器类。

```cpp
typedef Allocator allocator_type;
```

### <a name="example"></a>示例

[`get_allocator`](#get_allocator)有关使用的示例，请参阅示例 `allocator_type` 。

## <a name="at"></a><a name="at"></a> `at`

查找具有指定键值的元素。

```cpp
Type& at(const Key& key);

const Type& at(const Key& key) const;
```

### <a name="parameters"></a>参数

*`key`*\
要查找的键值。

### <a name="return-value"></a>返回值

对找到的元素数据值的引用。

### <a name="remarks"></a>注解

如果未找到参数键值，则函数将[ `out_of_range` 引发类的对象。](../standard-library/out-of-range-class.md)

### <a name="example"></a>示例

```cpp
// map_at.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

typedef std::map<char, int> Mymap;
int main()
    {
    Mymap c1;

    c1.insert(Mymap::value_type('a', 1));
    c1.insert(Mymap::value_type('b', 2));
    c1.insert(Mymap::value_type('c', 3));

// find and show elements
    std::cout << "c1.at('a') == " << c1.at('a') << std::endl;
    std::cout << "c1.at('b') == " << c1.at('b') << std::endl;
    std::cout << "c1.at('c') == " << c1.at('c') << std::endl;

    return (0);
    }
```

## <a name="begin"></a><a name="begin"></a> `begin`

返回一个迭代器，此迭代器用于发现 `map` 中的第一个元素。

```cpp
const_iterator begin() const;

iterator begin();
```

### <a name="return-value"></a>返回值

一个双向迭代器，用于寻址中的第一个元素 `map` 或空映射之后的位置。

### <a name="example"></a>示例

```cpp
// map_begin.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;

   map <int, int> :: iterator m1_Iter;
   map <int, int> :: const_iterator m1_cIter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 0, 0 ) );
   m1.insert ( Int_Pair ( 1, 1 ) );
   m1.insert ( Int_Pair ( 2, 4 ) );

   m1_cIter = m1.begin ( );
   cout << "The first element of m1 is " << m1_cIter -> first << endl;

   m1_Iter = m1.begin ( );
   m1.erase ( m1_Iter );

   // The following 2 lines would err because the iterator is const
   // m1_cIter = m1.begin ( );
   // m1.erase ( m1_cIter );

   m1_cIter = m1.begin( );
   cout << "The first element of m1 is now " << m1_cIter -> first << endl;
}
```

```Output
The first element of m1 is 0
The first element of m1 is now 1
```

## <a name="cbegin"></a><a name="cbegin"></a> `cbegin`

返回一个 **`const`** 迭代器，该迭代器用于寻址范围内最后一个元素之外的位置。

```cpp
const_iterator cbegin() const;
```

### <a name="return-value"></a>返回值

一个 **`const`** 双向迭代器，用于寻址范围内的第一个元素，或刚超出空范围 (空范围) 的位置 `cbegin() == cend()` 。

### <a name="remarks"></a>注解

如果返回值为 `cbegin` ，则不能修改范围中的元素。

可以使用此成员函数替代 `begin()` 成员函数，以保证返回值为 `const_iterator`。 通常，它与 [`auto`](../cpp/auto-cpp.md) 类型推导关键字一起使用，如下面的示例中所示。 在此示例中，将视为 `Container` 支持和的任何类型的可修改 (非 **`const`**) 容器 `begin()` `cbegin()` 。

```cpp
auto i1 = Container.begin();
// i1 is Container<T>::iterator
auto i2 = Container.cbegin();

// i2 is Container<T>::const_iterator
```

## <a name="cend"></a>` cend`

返回一个 **`const`** 迭代器，该迭代器用于寻址范围内最后一个元素之外的位置。

```cpp
const_iterator cend() const;
```

### <a name="return-value"></a>返回值

**`const`** 双向访问迭代器，它指向刚超出范围末尾的位置。

### <a name="remarks"></a>注解

`cend` 用于测试迭代器是否超过了其范围的末尾。

可以使用此成员函数替代 `end()` 成员函数，以保证返回值为 `const_iterator`。 通常，它与 [`auto`](../cpp/auto-cpp.md) 类型推导关键字一起使用，如下面的示例中所示。 在此示例中，将视为 `Container` 支持和的任何类型的可修改 (非 **`const`**) 容器 `end()` `cend()` 。

```cpp
auto i1 = Container.end();
// i1 is Container<T>::iterator
auto i2 = Container.cend();

// i2 is Container<T>::const_iterator
```

不应对 `cend` 返回的值取消引用。

## <a name="clear"></a><a name="clear"></a> `clear`

清除映射的所有元素。

```cpp
void clear();
```

### <a name="example"></a>示例

下面的示例演示成员函数的用法 `map::clear` 。

```cpp
// map_clear.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main()
{
    using namespace std;
    map<int, int> m1;
    map<int, int>::size_type i;
    typedef pair<int, int> Int_Pair;

    m1.insert(Int_Pair(1, 1));
    m1.insert(Int_Pair(2, 4));

    i = m1.size();
    cout << "The size of the map is initially "
         << i << "." << endl;

    m1.clear();
    i = m1.size();
    cout << "The size of the map after clearing is "
         << i << "." << endl;
}
```

```Output
The size of the map is initially 2.
The size of the map after clearing is 0.
```

## <a name="const_iterator"></a><a name="const_iterator"></a> `const_iterator`

一种类型，它提供可读取中的元素的双向迭代器 **`const`** `map` 。

```cpp
typedef implementation-defined const_iterator;
```

### <a name="remarks"></a>注解

类型 `const_iterator` 不能用于修改元素的值。

`const_iterator`由映射定义的是对象的元素 [`value_type`](#value_type) ，它的类型为 `pair<constKey, Type>` ，其第一个成员是元素的键，第二个成员是元素所持有的映射基准。

若要取消引用 `const_iterator` `cIter` 指向映射中某个元素的，请使用 `->` 运算符。

若要访问元素的键值，请使用 `cIter`  ->  **`first`** ，它等效于 (\* `cIter`) 。 **`first`**.

若要访问元素的映射基准值，请使用与 `cIter`  ->  **`second`** () 等效的 \* `cIter` 。 **`second`**.

### <a name="example"></a>示例

[`begin`](#begin)有关使用的示例，请参阅示例 `const_iterator` 。

## <a name="const_pointer"></a><a name="const_pointer"></a> `const_pointer`

一种类型，它提供指向 **`const`** 映射中的元素的指针。

```cpp
typedef typename allocator_type::const_pointer const_pointer;
```

### <a name="remarks"></a>注解

类型 `const_pointer` 不能用于修改元素的值。

在大多数情况下， [`iterator`](#iterator) 应该使用来访问 map 对象中的元素。

## <a name="const_reference"></a><a name="const_reference"></a> `const_reference`

一种类型，它提供对 **`const`** 存储在映射中的元素的引用，以便读取和执行 **`const`** 操作。

```cpp
typedef typename allocator_type::const_reference const_reference;
```

### <a name="example"></a>示例

```cpp
// map_const_ref.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );

   // Declare and initialize a const_reference &Ref1
   // to the key of the first element
   const int &Ref1 = ( m1.begin( ) -> first );

   // The following line would cause an error as the
   // non-const_reference can't be used to access the key
   // int &Ref1 = ( m1.begin( ) -> first );

   cout << "The key of first element in the map is "
        << Ref1 << "." << endl;

   // Declare and initialize a reference &Ref2
   // to the data value of the first element
   int &Ref2 = ( m1.begin( ) -> second );

   cout << "The data value of first element in the map is "
        << Ref2 << "." << endl;
}
```

```Output
The key of first element in the map is 1.
The data value of first element in the map is 10.
```

## <a name="const_reverse_iterator"></a><a name="const_reverse_iterator"></a> `const_reverse_iterator`

一种类型，它提供可读取中的任何元素的双向迭代器 **`const`** `map` 。

```cpp
typedef std::reverse_iterator<const_iterator> const_reverse_iterator;
```

### <a name="remarks"></a>注解

类型 `const_reverse_iterator` 无法修改元素的值，它用于反向循环访问映射。

`const_reverse_iterator`由映射定义的是对象的元素 [`value_type`](#value_type) ，它的类型为 `pair<const Key, Type>` ，其第一个成员是元素的键，第二个成员是元素所持有的映射基准。

若要取消引用指向 map 中元素的 `const_reverse_iterator crIter`，请使用 `->` 运算符。

若要访问元素的键值，请使用 `crIter`  ->  **`first`** ，它等效于 (\* `crIter`) 。 **`first`**

若要访问元素的映射基准值，请使用 `crIter`  ->  **`second`** ，它等效于 (\* `crIter`) 。 **`first`**

### <a name="example"></a>示例

[`rend`](#rend)有关如何声明和使用的示例，请参见的示例 `const_reverse_iterator` 。

## <a name="count"></a><a name="count"></a> `count`

返回 map 中其键与指定了参数的键匹配的元素数量。

```cpp
size_type count(const Key& key) const;
```

### <a name="parameters"></a>参数

*`key`*\
要从 map 中进行匹配的元素的键值。

### <a name="return-value"></a>返回值

如果 map 包含其排序键与参数键匹配的元素，则返回 1；如果 map 不包含带有匹配键的元素，则返回 0。

### <a name="remarks"></a>注解

成员函数返回以下范围内的元素 *x* 的数量

\[ lower_bound (*密钥*) ，upper_bound (*密钥*) ) 

对于 map（唯一的关联容器），数量为 0 或 1。

### <a name="example"></a>示例

下面的示例演示成员函数的用法 `map::count` 。

```cpp
// map_count.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main()
{
    using namespace std;
    map<int, int> m1;
    map<int, int>::size_type i;
    typedef pair<int, int> Int_Pair;

    m1.insert(Int_Pair(1, 1));
    m1.insert(Int_Pair(2, 1));
    m1.insert(Int_Pair(1, 4));
    m1.insert(Int_Pair(2, 1));

    // Keys must be unique in map, so duplicates are ignored
    i = m1.count(1);
    cout << "The number of elements in m1 with a sort key of 1 is: "
         << i << "." << endl;

    i = m1.count(2);
    cout << "The number of elements in m1 with a sort key of 2 is: "
         << i << "." << endl;

    i = m1.count(3);
    cout << "The number of elements in m1 with a sort key of 3 is: "
         << i << "." << endl;
}
```

```Output
The number of elements in m1 with a sort key of 1 is: 1.
The number of elements in m1 with a sort key of 2 is: 1.
The number of elements in m1 with a sort key of 3 is: 0.
```

## <a name="contains"></a><a name="contains"></a> `contains`

检查中是否存在具有指定键的元素 `map` 。

```cpp
bool contains(const Key& key) const;
template<class K> bool contains(const K& key) const;
```

### <a name="parameters"></a>参数

*`K`*\
键的类型。

*`key`*\
要查找的元素的键值。

### <a name="return-value"></a>返回值

`true` 如果在容器中找到元素，则为; 否则为。 `false` 否则为。

### <a name="remarks"></a>注解

`contains()` 是 c + + 20 中的新增项。 若要使用它，请指定 [`/std:c++latest`](../build/reference/std-specify-language-standard-version.md) 编译器选项。

`template<class K> bool contains(const K& key) const` 如果是透明的，则仅参与重载决策 `key_compare` 。 有关详细信息，请参阅 [关联容器中的异类查找](./stl-containers.md#heterogeneous-lookup-in-associative-containers-c14) 。

### <a name="example"></a>示例

```cpp
// Requires /std:c++latest
#include <map>
#include <string>
#include <iostream>
#include <functional>

int main()
{
    std::map<int, bool> m = {{0, true},{1, false}};

    std::cout << std::boolalpha; // so booleans show as 'true' or 'false'
    std::cout << m.contains(1) << '\n';
    std::cout << m.contains(2) << '\n';

    // call template function
    std::map<std::string, int, std::less<>> m2 = {{"ten", 10}, {"twenty", 20}, {"thirty", 30}};
    std::cout << m2.contains("ten");

    return 0;
}
```

```Output
true
false
true
```

## <a name="crbegin"></a><a name="crbegin"></a> `crbegin`

返回一个常量迭代器，此迭代器用于寻址反向映射中的第一个元素。

```cpp
const_reverse_iterator crbegin() const;
```

### <a name="return-value"></a>返回值

一种常量反向双向迭代器，用于寻址反向 [`map`](../standard-library/map-class.md) 或处理非反向中最后一个元素之后的第一个元素 `map` 。

### <a name="remarks"></a>注解

`crbegin` 用于反向，正 `map` 如 [`begin`](#begin) 用于 `map` 。

如果返回值为 `crbegin` ，则 `map` 无法修改对象

`crbegin` 可用于向后循环访问 `map`。

### <a name="example"></a>示例

```cpp
// map_crbegin.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;

   map <int, int> :: const_reverse_iterator m1_crIter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 3, 30 ) );

   m1_crIter = m1.crbegin( );
   cout << "The first element of the reversed map m1 is "
        << m1_crIter -> first << "." << endl;
}
```

```Output
The first element of the reversed map m1 is 3.
```

## <a name="crend"></a><a name="crend"></a> `crend`

返回一个常量迭代器，此迭代器用于寻址反向映射中最后一个元素之后的位置。

```cpp
const_reverse_iterator crend() const;
```

### <a name="return-value"></a>返回值

用于发现反向 (中最后一个元素之后的位置的常量反向双向迭代器， [`map`](../standard-library/map-class.md) 非反向) 中第一个元素之前的位置 `map` 。

### <a name="remarks"></a>注解

`crend` 与反向映射一起使用，就像 [`end`](#end) 使用时一样 `map` 。

如果返回值为 `crend` ，则 `map` 无法修改对象。

`crend` 可用于测试反向迭代器是否已到达其 `map` 的末尾。

不应对 `crend` 返回的值取消引用。

### <a name="example"></a>示例

```cpp
// map_crend.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;

   map <int, int> :: const_reverse_iterator m1_crIter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 3, 30 ) );

   m1_crIter = m1.crend( );
   m1_crIter--;
   cout << "The last element of the reversed map m1 is "
        << m1_crIter -> first << "." << endl;
}
```

```Output
The last element of the reversed map m1 is 1.
```

## <a name="difference_type"></a><a name="difference_type"></a> `difference_type`

一种有符号整数类型，此类型可用于表示映射中迭代器指向的元素间范围内的元素数量。

```cpp
typedef allocator_type::difference_type difference_type;
```

### <a name="remarks"></a>注解

`difference_type` 是通过容器迭代器减少或递增时返回的类型。 `difference_type` 通常用于表示迭代器 `first` 和 `last` 之间的范围 *[ first,  last)* 内元素的数目，包括 `first` 指向的元素以及那一系列元素，但不包括 `last` 指向的元素。

尽管适用 `difference_type` 于满足输入迭代器要求的所有迭代器（包括可逆容器支持的双向迭代器的类，如集），但迭代器之间的减法仅受随机访问容器（如 vector）提供的随机访问迭代器支持。

### <a name="example"></a>示例

```cpp
// map_diff_type.cpp
// compile with: /EHsc
#include <iostream>
#include <map>
#include <algorithm>

int main( )
{
   using namespace std;
   map <int, int> m1;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 3, 20 ) );
   m1.insert ( Int_Pair ( 2, 30 ) );

   map <int, int>::iterator m1_Iter, m1_bIter, m1_eIter;
   m1_bIter = m1.begin( );
   m1_eIter = m1.end( );

   // Count the number of elements in a map
   map <int, int>::difference_type  df_count = 1;
   m1_Iter = m1.begin( );
   while ( m1_Iter != m1_eIter)
   {
      df_count++;
      m1_Iter++;
   }

   cout << "The number of elements in the map m1 is: "
        << df_count << "." << endl;
}
```

```Output
The number of elements in the map m1 is: 4.
```

## <a name="emplace"></a><a name="emplace"></a> `emplace`

向映射就地插入构造的元素（不执行复制或移动操作）。

```cpp
template <class... Args>
pair<iterator, bool>
emplace(
    Args&&... args);
```

### <a name="parameters"></a>参数

*`args`*\
用于构造要插入到映射中的元素的转发自变量，除非它已包含其值具有相同排序的元素。

### <a name="return-value"></a>返回值

一个 [`pair`](../standard-library/pair-structure.md) **`bool`** ，其组件为 `true` ，如果已执行插入操作，并且 `false` 映射已包含排序中等效值的元素，则为。 返回值对的迭代器组件指向新插入的元素 **`bool`** （如果组件为 true）或现有元素（如果 **`bool`** 组件为 false）。

若要访问一个 `pair` `pr` 的迭代器组件，请使用 `pr.first`；若要取消引用它，请使用 `*pr.first`。 若要访问 **`bool`** 组件，请使用 `pr.second` 。 有关示例，请参阅本文后面的示例代码。

### <a name="remarks"></a>注解

此函数不会使迭代器或引用无效。

在定位期间，如果引发异常，则不会修改容器的状态。

[`value_type`](#value_type)元素的是一个对，因此元素的值将是一个有序对，其中第一个组件等于键值，第二个组件等于元素的数据值。

### <a name="example"></a>示例

```cpp
// map_emplace.cpp
// compile with: /EHsc
#include <map>
#include <string>
#include <iostream>

using namespace std;

template <typename M> void print(const M& m) {
    cout << m.size() << " elements: ";

    for (const auto& p : m) {
        cout << "(" << p.first << ", " << p.second << ") ";
    }

    cout << endl;
}

int main()
{
    map<int, string> m1;

    auto ret = m1.emplace(10, "ten");

    if (!ret.second){
        auto pr = *ret.first;
        cout << "Emplace failed, element with key 10 already exists."
            << endl << "  The existing element is (" << pr.first << ", " << pr.second << ")"
            << endl;
        cout << "map not modified" << endl;
    }
    else{
        cout << "map modified, now contains ";
        print(m1);
    }
    cout << endl;

    ret = m1.emplace(10, "one zero");

    if (!ret.second){
        auto pr = *ret.first;
        cout << "Emplace failed, element with key 10 already exists."
            << endl << "  The existing element is (" << pr.first << ", " << pr.second << ")"
            << endl;
    }
    else{
        cout << "map modified, now contains ";
        print(m1);
    }
    cout << endl;
}
```

## <a name="emplace_hint"></a><a name="emplace_hint"></a> `emplace_hint`

使用位置提示就地插入构造的元素（不执行复制或移动操作）。

```cpp
template <class... Args>
iterator emplace_hint(
    const_iterator where,
    Args&&... args);
```

### <a name="parameters"></a>参数

*`args`*\
用于构造要插入到映射中的元素的转发自变量，除非该映射已包含该元素，或更普遍的情况是除非它已包含其键是等效排序的元素。

*`where`*\
开始搜索正确插入点的位置。  (如果该点紧靠 *在某个位置* 之前，则插入可能发生在分期常量时间内，而非对数时间内。 ) 

### <a name="return-value"></a>返回值

指向新插入的元素的迭代器。

如果因元素已存在导致插入失败，则将迭代器返回具有该键的现有元素。

### <a name="remarks"></a>注解

此函数不会使迭代器或引用无效。

在定位期间，如果引发异常，则不会修改容器的状态。

[`value_type`](#value_type)元素的是一个对，因此元素的值将是一个有序对，其中第一个组件等于键值，第二个组件等于元素的数据值。

### <a name="example"></a>示例

```cpp
// map_emplace.cpp
// compile with: /EHsc
#include <map>
#include <string>
#include <iostream>

using namespace std;

template <typename M> void print(const M& m) {
    cout << m.size() << " elements: " << endl;

    for (const auto& p : m) {
        cout << "(" << p.first <<  "," << p.second << ") ";
    }

    cout << endl;
}

int main()
{
    map<string, string> m1;

    // Emplace some test data
    m1.emplace("Anna", "Accounting");
    m1.emplace("Bob", "Accounting");
    m1.emplace("Carmine", "Engineering");

    cout << "map starting data: ";
    print(m1);
    cout << endl;

    // Emplace with hint
    // m1.end() should be the "next" element after this emplacement
    m1.emplace_hint(m1.end(), "Doug", "Engineering");

    cout << "map modified, now contains ";
    print(m1);
    cout << endl;
}
```

## <a name="empty"></a><a name="empty"></a> `empty`

测试 map 是否为空。

```cpp
bool empty() const;
```

### <a name="return-value"></a>返回值

**`true`** 如果映射为空，则为; 否则为。 **`false`** 如果映射不为空，则为。

### <a name="example"></a>示例

```cpp
// map_empty.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1, m2;

   typedef pair <int, int> Int_Pair;
   m1.insert ( Int_Pair ( 1, 1 ) );

   if ( m1.empty( ) )
      cout << "The map m1 is empty." << endl;
   else
      cout << "The map m1 is not empty." << endl;

   if ( m2.empty( ) )
      cout << "The map m2 is empty." << endl;
   else
      cout << "The map m2 is not empty." << endl;
}
```

```Output
The map m1 is not empty.
The map m2 is empty.
```

## <a name="end"></a><a name="end"></a> `end`

返回超过末尾迭代器。

```cpp
const_iterator end() const;

iterator end();
```

### <a name="return-value"></a>返回值

超过末尾迭代器。 如果映射为空，则 `map::end() == map::begin()`。

### <a name="remarks"></a>注解

`end` 用于测试迭代器是否已超过其映射的结尾。

不应对 `end` 返回的值取消引用。

有关代码示例，请参见 [`map::find`](#find) 。

## <a name="equal_range"></a><a name="equal_range"></a> `equal_range`

返回一对迭代器，这两个迭代器表示键的和键的 [`lower_bound`](#lower_bound) [`upper_bound`](#upper_bound) 。

```cpp
pair <const_iterator, const_iterator> equal_range (const Key& key) const;

pair <iterator, iterator> equal_range (const Key& key);
```

### <a name="parameters"></a>参数

*`key`*\
要与当前搜索的映射中元素的排序键进行比较的参数键值。

### <a name="return-value"></a>返回值

若要访问成员函数返回的 `pr` 对的第一个迭代器，请使用 `pr`. **首先**，若要取消引用下限迭代器，请使用 \* ( `pr` 。 **第一个**) 。 若要访问成员函数返回的 `pr` 对的第二个迭代器，请使用 `pr`. **其次**，若要取消引用上限迭代器，请使用 \* ( `pr` 。 **第二**) 。

### <a name="example"></a>示例

```cpp
// map_equal_range.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   typedef map <int, int, less<int> > IntMap;
   IntMap m1;
   map <int, int> :: const_iterator m1_RcIter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 3, 30 ) );

   pair <IntMap::const_iterator, IntMap::const_iterator> p1, p2;
   p1 = m1.equal_range( 2 );

   cout << "The lower bound of the element with "
        << "a key of 2 in the map m1 is: "
        << p1.first -> second << "." << endl;

   cout << "The upper bound of the element with "
        << "a key of 2 in the map m1 is: "
        << p1.second -> second << "." << endl;

   // Compare the upper_bound called directly
   m1_RcIter = m1.upper_bound( 2 );

   cout << "A direct call of upper_bound( 2 ) gives "
        << m1_RcIter -> second << "," << endl
        << "matching the 2nd element of the pair"
        << " returned by equal_range( 2 )." << endl;

   p2 = m1.equal_range( 4 );

   // If no match is found for the key,
   // both elements of the pair return end( )
   if ( ( p2.first == m1.end( ) ) && ( p2.second == m1.end( ) ) )
      cout << "The map m1 doesn't have an element "
           << "with a key less than 40." << endl;
   else
      cout << "The element of map m1 with a key >= 40 is: "
           << p2.first -> first << "." << endl;
}
```

```Output
The lower bound of the element with a key of 2 in the map m1 is: 20.
The upper bound of the element with a key of 2 in the map m1 is: 30.
A direct call of upper_bound( 2 ) gives 30,
matching the 2nd element of the pair returned by equal_range( 2 ).
The map m1 doesn't have an element with a key less than 40.
```

## <a name="erase"></a><a name="erase"></a> `erase`

从 map 中的指定位置移除一个元素或元素范围，或者移除与指定键匹配的元素。

```cpp
iterator erase(
    const_iterator Where);

iterator erase(
    const_iterator First,
    const_iterator Last);

size_type erase(
    const key_type& Key);
```

### <a name="parameters"></a>参数

*`Where`*\
要移除的元素的位置。

*`First`*\
要移除的第一个元素的位置。

*`Last`*\
要移除的刚超出最后一个元素的位置。

*`Key`*\
要移除的元素的关键值。

### <a name="return-value"></a>返回值

对于前两个成员函数，则为双向迭代器，它指定已删除的任何元素之外留存的第一个元素，如果此类元素不存在，则为 map 末尾的元素。

对于第三个成员函数，则返回已从 map 中移除的元素的数目。

### <a name="example"></a>示例

```cpp
// map_erase.cpp
// compile with: /EHsc
#include <map>
#include <string>
#include <iostream>
#include <iterator> // next() and prev() helper functions
#include <utility>  // make_pair()

using namespace std;

using mymap = map<int, string>;

void printmap(const mymap& m) {
    for (const auto& elem : m) {
        cout << " [" << elem.first << ", " << elem.second << "]";
    }
    cout << endl << "size() == " << m.size() << endl << endl;
}

int main()
{
    mymap m1;

    // Fill in some data to test with, one at a time
    m1.insert(make_pair(1, "A"));
    m1.insert(make_pair(2, "B"));
    m1.insert(make_pair(3, "C"));
    m1.insert(make_pair(4, "D"));
    m1.insert(make_pair(5, "E"));

    cout << "Starting data of map m1 is:" << endl;
    printmap(m1);
    // The 1st member function removes an element at a given position
    m1.erase(next(m1.begin()));
    cout << "After the 2nd element is deleted, the map m1 is:" << endl;
    printmap(m1);

    // Fill in some data to test with, one at a time, using an initializer list
    mymap m2
    {
        { 10, "Bob" },
        { 11, "Rob" },
        { 12, "Robert" },
        { 13, "Bert" },
        { 14, "Bobby" }
    };

    cout << "Starting data of map m2 is:" << endl;
    printmap(m2);
    // The 2nd member function removes elements
    // in the range [First, Last)
    m2.erase(next(m2.begin()), prev(m2.end()));
    cout << "After the middle elements are deleted, the map m2 is:" << endl;
    printmap(m2);

    mymap m3;

    // Fill in some data to test with, one at a time, using emplace
    m3.emplace(1, "red");
    m3.emplace(2, "yellow");
    m3.emplace(3, "blue");
    m3.emplace(4, "green");
    m3.emplace(5, "orange");
    m3.emplace(6, "purple");
    m3.emplace(7, "pink");

    cout << "Starting data of map m3 is:" << endl;
    printmap(m3);
    // The 3rd member function removes elements with a given Key
    mymap::size_type count = m3.erase(2);
    // The 3rd member function also returns the number of elements removed
    cout << "The number of elements removed from m3 is: " << count << "." << endl;
    cout << "After the element with a key of 2 is deleted, the map m3 is:" << endl;
    printmap(m3);
}
```

## <a name="find"></a><a name="find"></a> `find`

返回引用映射当中具有与指定键等效的键的元素的位置的迭代器。

```cpp
iterator find(const Key& key);

const_iterator find(const Key& key) const;
```

### <a name="parameters"></a>参数

*`key`*\
要搜索的映射中的元素的排序键与之匹配的键值。

### <a name="return-value"></a>返回值

一个迭代器，它引用具有指定键的元素的位置，或在)  (中最后一个元素之后的位置（ `map` `map::end()` 如果找不到该键的匹配项）。

### <a name="remarks"></a>注解

成员函数返回一个迭代器，该迭代器引用中 `map` 其排序键与二元谓词下的参数键等效的元素，该谓词基于小于比较关系进行排序。

如果将的返回值 `find` 分配给 `const_iterator` ，则无法修改地图对象。 如果将的返回值 `find` 分配给 `iterator` ，则可以修改 map 对象

### <a name="example"></a>示例

```cpp
// compile with: /EHsc /W4 /MTd
#include <map>
#include <iostream>
#include <vector>
#include <string>
#include <utility>  // make_pair()

using namespace std;

template <typename A, typename B> void print_elem(const pair<A, B>& p) {
    cout << "(" << p.first << ", " << p.second << ") ";
}

template <typename T> void print_collection(const T& t) {
    cout << t.size() << " elements: ";

    for (const auto& p : t) {
        print_elem(p);
    }
    cout << endl;
}

template <typename C, class T> void findit(const C& c, T val) {
    cout << "Trying find() on value " << val << endl;
    auto result = c.find(val);
    if (result != c.end()) {
        cout << "Element found: "; print_elem(*result); cout << endl;
    } else {
        cout << "Element not found." << endl;
    }
}

int main()
{
    map<int, string> m1({ { 40, "Zr" }, { 45, "Rh" } });
    cout << "The starting map m1 is (key, value):" << endl;
    print_collection(m1);

    vector<pair<int, string>> v;
    v.push_back(make_pair(43, "Tc"));
    v.push_back(make_pair(41, "Nb"));
    v.push_back(make_pair(46, "Pd"));
    v.push_back(make_pair(42, "Mo"));
    v.push_back(make_pair(44, "Ru"));
    v.push_back(make_pair(44, "Ru")); // attempt a duplicate

    cout << "Inserting the following vector data into m1:" << endl;
    print_collection(v);

    m1.insert(v.begin(), v.end());

    cout << "The modified map m1 is (key, value):" << endl;
    print_collection(m1);
    cout << endl;
    findit(m1, 45);
    findit(m1, 6);
}
```

## <a name="get_allocator"></a><a name="get_allocator"></a> `get_allocator`

返回用于构造 map 的分配器对象的一个副本。

```cpp
allocator_type get_allocator() const;
```

### <a name="return-value"></a>返回值

map 使用的分配器。

### <a name="remarks"></a>注解

map 类的分配器指定类管理存储的方式。 C++ 标准库容器类提供的默认分配器足以满足大多编程需求。 编写和使用你自己的分配器类是高级 C++ 主题。

### <a name="example"></a>示例

```cpp
// map_get_allocator.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int>::allocator_type m1_Alloc;
   map <int, int>::allocator_type m2_Alloc;
   map <int, double>::allocator_type m3_Alloc;
   map <int, int>::allocator_type m4_Alloc;

   // The following lines declare objects
   // that use the default allocator.
   map <int, int> m1;
   map <int, int, allocator<int> > m2;
   map <int, double, allocator<double> > m3;

   m1_Alloc = m1.get_allocator( );
   m2_Alloc = m2.get_allocator( );
   m3_Alloc = m3.get_allocator( );

   cout << "The number of integers that can be allocated\n"
        << "before free memory is exhausted: "
        << m2.max_size( ) << ".\n" << endl;

   cout << "The number of doubles that can be allocated\n"
        << "before free memory is exhausted: "
        << m3.max_size( ) <<  ".\n" << endl;

   // The following line creates a map m4
   // with the allocator of map m1.
   map <int, int> m4( less<int>( ), m1_Alloc );

   m4_Alloc = m4.get_allocator( );

   // Two allocators are interchangeable if
   // storage allocated from each can be
   // deallocated with the other
   if( m1_Alloc == m4_Alloc )
   {
      cout << "The allocators are interchangeable." << endl;
   }
   else
   {
      cout << "The allocators are not interchangeable." << endl;
   }
}
```

## <a name="insert"></a><a name="insert"></a> `insert`

将一个元素或元素范围插入到映射中。

```cpp
// (1) single element
pair<iterator, bool> insert(
    const value_type& Val);

// (2) single element, perfect forwarded
template <class ValTy>
pair<iterator, bool>
insert(
    ValTy&& Val);

// (3) single element with hint
iterator insert(
    const_iterator Where,
    const value_type& Val);

// (4) single element, perfect forwarded, with hint
template <class ValTy>
iterator insert(
    const_iterator Where,
    ValTy&& Val);

// (5) range
template <class InputIterator>
void insert(
    InputIterator First,
    InputIterator Last);

// (6) initializer list
void insert(
    initializer_list<value_type>
IList);
```

### <a name="parameters"></a>参数

*`Val`*\
要插入到映射中的元素的值，除非它已包含其键具有等效排序的元素。

*`Where`*\
开始搜索正确插入点的位置。  (如果该点紧接 *`Where`* 在之前，则插入可能发生在分期常量时间内，而非对数时间内。 ) 

*`ValTy`*\
一个模板参数，该参数指定映射可用于构造元素的参数类型 [`value_type`](#value_type) ，并将作为参数完美转发 *`Val`* 。

*`First`*\
要复制的第一个元素的位置。

*`Last`*\
要复制的最后一个元素以外的位置。

*`InputIterator`*\
满足输入迭代器要求的模板函数自变量，该 [输入迭代器](../standard-library/input-iterator-tag-struct.md) 指向可用于构造对象的类型的元素 [`value_type`](#value_type) 。

*`IList`*\
[`initializer_list`](../standard-library/initializer-list.md)要从中复制元素的。

### <a name="return-value"></a>返回值

单个元素成员函数 (1) 和 (2) 返回， [`pair`](../standard-library/pair-structure.md) **`bool`** 如果已进行插入，则其组件为 true; 如果映射已经包含一个其键在排序中具有等效值的元素，则返回 false。 返回值对的迭代器组件指向新插入的元素 **`bool`** （如果组件为 true）或现有元素（如果 **`bool`** 组件为 false）。

附带提示的单个元素成员函数 (3) 和 (4) 将返回迭代器，该迭代器指向将新元素插入到映射中的位置，如果具有等效键的元素已经存在，则指向现有元素。

### <a name="remarks"></a>注解

任何迭代器、指针或引用都不会因为此函数而失效。

在只插入一个元素的过程中，如果引发异常，则不会修改容器的状态。 在插入多个元素的过程中，如果引发异常，则会使容器处于未指定但有效的状态。

若要访问 `pair` `pr` 由单个元素成员函数返回的的迭代器组件，请使用 `pr.first` ; 若要在返回的对中取消引用迭代器，请使用 `*pr.first` ，为你提供一个元素。 若要访问 **`bool`** 组件，请使用 `pr.second` 。 有关示例，请参阅本文后面的示例代码。

[`value_type`](#value_type)容器的是属于该容器的 typedef; 对于 map，为 `map<K, V>::value_type` `pair<const K, V>` 。 元素的值是一个有序对，其中第一个组件相当于键值，第二个组件相当于该元素的数据值。

范围成员函数 (5) 将元素值序列插入到映射中，它对应于迭代器在范围 `[First, Last)` 中所处理的每一个元素；因此，不会插入 `Last`。 容器成员函数 `end()` 是指容器中最后一个元素之后的位置，例如，`m.insert(v.begin(), v.end());` 语句尝试将 `v` 的所有元素插入到 `m` 中。 只插入在该范围中具有唯一值的元素；忽略副本。 若要观察拒绝了哪些元素，请使用单个元素版本的 `insert`。

初始值设定项列表成员函数 (6) 使用将 [`initializer_list`](../standard-library/initializer-list.md) 元素复制到映射中。

若要插入就地构造的元素（即不执行复制或移动操作），请参阅 [`map::emplace`](#emplace) 和 [`map::emplace_hint`](#emplace_hint) 。

### <a name="example"></a>示例

```cpp
// map_insert.cpp
// compile with: /EHsc
#include <map>
#include <iostream>
#include <string>
#include <vector>
#include <utility>  // make_pair()

using namespace std;

template <typename M> void print(const M& m) {
    cout << m.size() << " elements: ";

    for (const auto& p : m) {
        cout << "(" << p.first << ", " << p.second << ") ";
    }

    cout << endl;
}

int main()
{

    // insert single values
    map<int, int> m1;
    // call insert(const value_type&) version
    m1.insert({ 1, 10 });
    // call insert(ValTy&&) version
    m1.insert(make_pair(2, 20));

    cout << "The original key and mapped values of m1 are:" << endl;
    print(m1);

    // intentionally attempt a duplicate, single element
    auto ret = m1.insert(make_pair(1, 111));
    if (!ret.second){
        auto pr = *ret.first;
        cout << "Insert failed, element with key value 1 already exists."
            << endl << "  The existing element is (" << pr.first << ", " << pr.second << ")"
            << endl;
    }
    else{
        cout << "The modified key and mapped values of m1 are:" << endl;
        print(m1);
    }
    cout << endl;

    // single element, with hint
    m1.insert(m1.end(), make_pair(3, 30));
    cout << "The modified key and mapped values of m1 are:" << endl;
    print(m1);
    cout << endl;

    // The templatized version inserting a jumbled range
    map<int, int> m2;
    vector<pair<int, int>> v;
    v.push_back(make_pair(43, 294));
    v.push_back(make_pair(41, 262));
    v.push_back(make_pair(45, 330));
    v.push_back(make_pair(42, 277));
    v.push_back(make_pair(44, 311));

    cout << "Inserting the following vector data into m2:" << endl;
    print(v);

    m2.insert(v.begin(), v.end());

    cout << "The modified key and mapped values of m2 are:" << endl;
    print(m2);
    cout << endl;

    // The templatized versions move-constructing elements
    map<int, string>  m3;
    pair<int, string> ip1(475, "blue"), ip2(510, "green");

    // single element
    m3.insert(move(ip1));
    cout << "After the first move insertion, m3 contains:" << endl;
    print(m3);

    // single element with hint
    m3.insert(m3.end(), move(ip2));
    cout << "After the second move insertion, m3 contains:" << endl;
    print(m3);
    cout << endl;

    map<int, int> m4;
    // Insert the elements from an initializer_list
    m4.insert({ { 4, 44 }, { 2, 22 }, { 3, 33 }, { 1, 11 }, { 5, 55 } });
    cout << "After initializer_list insertion, m4 contains:" << endl;
    print(m4);
    cout << endl;
}
```

## <a name="iterator"></a><a name="iterator"></a> `iterator`

一种类型，此类型提供可读取或修改 map 中的任何元素的双向迭代器。

```cpp
typedef implementation-defined iterator;
```

### <a name="remarks"></a>注解

映射所定义的迭代器指向属于对象的元素 [`value_type`](#value_type) ，它的类型为 `pair<const Key, Type>` ，其第一个成员是元素的键，第二个成员是元素所持有的映射基准。

若要取消引用指向映射中某个元素的迭代器 *Iter* ，请使用 `->` 运算符。

若要访问元素的键值，请使用 `Iter->first` 等效于的 `(*Iter).first` 。 若要访问元素的映射基准值，请使用 `Iter->second` 等效于的 `(*Iter).second` 。

### <a name="example"></a>示例

[`begin`](#begin)有关如何声明和使用的示例，请参阅示例 `iterator` 。

## <a name="key_comp"></a><a name="key_comp"></a> `key_comp`

检索用于对 map 中的键进行排序的比较对象副本。

```cpp
key_compare key_comp() const;
```

### <a name="return-value"></a>返回值

返回 map 用来对其元素进行排序的函数对象。

### <a name="remarks"></a>注解

存储对象会定义成员函数

`bool operator(const Key& left, const Key& right);`

**`true`** 如果 `left` `right` 在排序顺序中先于且不等于，则返回。

### <a name="example"></a>示例

```cpp
// map_key_comp.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;

   map <int, int, less<int> > m1;
   map <int, int, less<int> >::key_compare kc1 = m1.key_comp( ) ;
   bool result1 = kc1( 2, 3 ) ;
   if( result1 == true )
   {
      cout << "kc1( 2,3 ) returns value of true, "
           << "where kc1 is the function object of m1."
           << endl;
   }
   else
   {
      cout << "kc1( 2,3 ) returns value of false "
           << "where kc1 is the function object of m1."
           << endl;
   }

   map <int, int, greater<int> > m2;
   map <int, int, greater<int> >::key_compare kc2 = m2.key_comp( );
   bool result2 = kc2( 2, 3 ) ;
   if( result2 == true )
   {
      cout << "kc2( 2,3 ) returns value of true, "
           << "where kc2 is the function object of m2."
           << endl;
   }
   else
   {
      cout << "kc2( 2,3 ) returns value of false, "
           << "where kc2 is the function object of m2."
           << endl;
   }
}
```

```Output
kc1( 2,3 ) returns value of true, where kc1 is the function object of m1.
kc2( 2,3 ) returns value of false, where kc2 is the function object of m2.
```

## <a name="key_compare"></a><a name="key_compare"></a> `key_compare`

一种提供函数对象的类型，该函数对象可比较两个排序键以确定 `map` 中两个元素的相对顺序。

```cpp
typedef Traits key_compare;
```

### <a name="remarks"></a>注解

`key_compare` 是模板参数的同义词 *`Traits`* 。

有关的详细信息 *`Traits`* ，请参阅 [ `map` 类](../standard-library/map-class.md)主题。

### <a name="example"></a>示例

[`key_comp`](#key_comp)有关如何声明和使用的示例，请参阅示例 `key_compare` 。

## <a name="key_type"></a><a name="key_type"></a> `key_type`

用于描述存储在 map 内每个元素中的排序键的类型。

```cpp
typedef Key key_type;
```

### <a name="remarks"></a>注解

`key_type` 是模板参数的同义词 *`Key`* 。

有关的详细信息 *`Key`* ，请参阅 [ `map` 类](../standard-library/map-class.md)主题的 "**备注**" 部分。

### <a name="example"></a>示例

[`value_type`](#value_type)有关如何声明和使用的示例，请参阅示例 `key_type` 。

## <a name="lower_bound"></a><a name="lower_bound"></a> `lower_bound`

返回一个迭代器，此迭代器指向 map 中其键值等于或大于指定键的键值的第一个元素。

```cpp
iterator lower_bound(const Key& key);

const_iterator lower_bound(const Key& key) const;
```

### <a name="parameters"></a>参数

*`key`*\
要与当前搜索的映射中元素的排序键进行比较的参数键值。

### <a name="return-value"></a>返回值

一个 `iterator` 或 `const_iterator` ，它用于寻址映射中其键等于或大于参数键的元素的位置，或用于满足 if 中最后一个元素之后的位置（ `map` 如果找不到该键的匹配项）。

如果将的返回值 `lower_bound` 分配给 `const_iterator` ，则无法修改地图对象。 如果将的返回值 `lower_bound` 分配给 `iterator` ，则可以修改地图对象。

### <a name="example"></a>示例

```cpp
// map_lower_bound.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;
   map <int, int> :: const_iterator m1_AcIter, m1_RcIter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 3, 30 ) );

   m1_RcIter = m1.lower_bound( 2 );
   cout << "The first element of map m1 with a key of 2 is: "
        << m1_RcIter -> second << "." << endl;

   // If no match is found for this key, end( ) is returned
   m1_RcIter = m1. lower_bound ( 4 );

   if ( m1_RcIter == m1.end( ) )
      cout << "The map m1 doesn't have an element "
           << "with a key of 4." << endl;
   else
      cout << "The element of map m1 with a key of 4 is: "
           << m1_RcIter -> second << "." << endl;

   // The element at a specific location in the map can be found
   // using a dereferenced iterator addressing the location
   m1_AcIter = m1.end( );
   m1_AcIter--;
   m1_RcIter = m1. lower_bound ( m1_AcIter -> first );
   cout << "The element of m1 with a key matching "
        << "that of the last element is: "
        << m1_RcIter -> second << "." << endl;
}
```

```Output
The first element of map m1 with a key of 2 is: 20.
The map m1 doesn't have an element with a key of 4.
The element of m1 with a key matching that of the last element is: 30.
```

## <a name="map"></a><a name="map"></a> `map`

构造一个空的或者是其他某个 map 的全部或部分副本的 map 。

```cpp
map();

explicit map(
    const Traits& Comp);

map(
    const Traits& Comp,
    const Allocator& Al);

map(
    const map& Right);

map(
    map&& Right);

map(
    initializer_list<value_type> IList);

map(
    initializer_list<value_type> IList,
    const Traits& Comp);

map(
    initializer_list<value_type> IList,
    const Traits& Comp,
    const Allocator& Allocator);

template <class InputIterator>
map(
    InputIterator First,
    InputIterator Last);

template <class InputIterator>
map(
    InputIterator First,
    InputIterator Last,
    const Traits& Comp);

template <class InputIterator>
map(
    InputIterator First,
    InputIterator Last,
    const Traits& Comp,
    const Allocator& Al);
```

### <a name="parameters"></a>参数

*`Al`*\
要用于此 map 对象的存储分配器类，默认为 `Allocator`。

*`Comp`*\
用于对 `map` 中元素排序的类型 `const Traits` 的比较函数，默认为 `hash_compare`。

*`Right`*\
所构造集要作为其副本的映射。

*`First`*\
要复制的范围元素中的第一个元素的位置。

*`Last`*\
要复制的元素范围以外的第一个元素的位置。

*`IList`*\
要从中复制元素的 initializer_list。

### <a name="remarks"></a>注解

所有构造函数都存储一种类型的分配器对象，该对象管理映射的内存存储，以后可通过调用返回 [`get_allocator`](#get_allocator) 。 此分配器参数在类声明中常省略，并预处理用于代替备用分配器的宏。

所有构造函数对它们的 map 进行初始化。

所有构造函数都存储一个类型特性的函数对象，该函数对象用于在映射的键之间建立顺序，且稍后可通过调用返回 [`key_comp`](#key_comp) 。

前三个构造函数指定一个空的初始映射，第二个指定比较函数的类型 (*`Comp`*) 将用于建立元素的顺序，第三个构造函数显式指定要使用)  (的分配器类型 *`Al`* 。 关键字关键字 **`explicit`** 取消了某些类型的自动类型转换。

第四个构造函数指定映射的副本 *`Right`* 。

第五个构造函数通过移动指定映射的副本 *`Right`* 。

第六个、第七个和第八个构造函数使用从中 `initializer_list` 复制成员的。

接下来的三个构造函数复制 map 的范围 `[First, Last)`，其指定类 `Traits` 和 Allocator 的比较函数类型和分配器时更加明确。

### <a name="example"></a>示例

```cpp
// map_map.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main()
{
    using namespace std;
    typedef pair <int, int> Int_Pair;
    map <int, int>::iterator m1_Iter, m3_Iter, m4_Iter, m5_Iter, m6_Iter, m7_Iter;
    map <int, int, less<int> >::iterator m2_Iter;

    // Create an empty map m0 of key type integer
    map <int, int> m0;

    // Create an empty map m1 with the key comparison
    // function of less than, then insert 4 elements
    map <int, int, less<int> > m1;
    m1.insert(Int_Pair(1, 10));
    m1.insert(Int_Pair(2, 20));
    m1.insert(Int_Pair(3, 30));
    m1.insert(Int_Pair(4, 40));

    // Create an empty map m2 with the key comparison
    // function of greater than, then insert 2 elements
    map <int, int, less<int> > m2;
    m2.insert(Int_Pair(1, 10));
    m2.insert(Int_Pair(2, 20));

    // Create a map m3 with the
    // allocator of map m1
    map <int, int>::allocator_type m1_Alloc;
    m1_Alloc = m1.get_allocator();
    map <int, int> m3(less<int>(), m1_Alloc);
    m3.insert(Int_Pair(3, 30));

    // Create a copy, map m4, of map m1
    map <int, int> m4(m1);

    // Create a map m5 by copying the range m1[ first,  last)
    map <int, int>::const_iterator m1_bcIter, m1_ecIter;
    m1_bcIter = m1.begin();
    m1_ecIter = m1.begin();
    m1_ecIter++;
    m1_ecIter++;
    map <int, int> m5(m1_bcIter, m1_ecIter);

    // Create a map m6 by copying the range m4[ first,  last)
    // and with the allocator of map m2
    map <int, int>::allocator_type m2_Alloc;
    m2_Alloc = m2.get_allocator();
    map <int, int> m6(m4.begin(), ++m4.begin(), less<int>(), m2_Alloc);

    cout << "m1 =";
    for (auto i : m1)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    cout << "m2 =";
    for(auto i : m2)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    cout << "m3 =";
    for (auto i : m3)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    cout << "m4 =";
    for (auto i : m4)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    cout << "m5 =";
    for (auto i : m5)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    cout << "m6 =";
    for (auto i : m6)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    // Create a map m7 by moving m5
    cout << "m7 =";
    map<int, int> m7(move(m5));
    for (auto i : m7)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    // Create a map m8 by copying in an initializer_list
    map<int, int> m8{ { { 1, 1 }, { 2, 2 }, { 3, 3 }, { 4, 4 } } };
    cout << "m8: = ";
    for (auto i : m8)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    // Create a map m9 with an initializer_list and a comparator
    map<int, int> m9({ { 5, 5 }, { 6, 6 }, { 7, 7 }, { 8, 8 } }, less<int>());
    cout << "m9: = ";
    for (auto i : m9)
        cout << i.first << " " << i.second << ", ";
    cout << endl;

    // Create a map m10 with an initializer_list, a comparator, and an allocator
    map<int, int> m10({ { 9, 9 }, { 10, 10 }, { 11, 11 }, { 12, 12 } }, less<int>(), m9.get_allocator());
    cout << "m10: = ";
    for (auto i : m10)
        cout << i.first << " " << i.second << ", ";
    cout << endl;
}
```

## <a name="mapped_type"></a><a name="mapped_type"></a> `mapped_type`

一种类型，此类型表示存储在 map 中的数据。

```cpp
typedef Type mapped_type;
```

### <a name="remarks"></a>注解

类型 `mapped_type` 是类的 *类型* 模板参数的同义词。

有关的详细信息 *`Type`* ，请参阅 [ `map` 类](../standard-library/map-class.md)主题。

### <a name="example"></a>示例

[`value_type`](#value_type)有关如何声明和使用的示例，请参阅示例 `mapped_type` 。

## <a name="max_size"></a><a name="max_size"></a> `max_size`

返回映射的最大长度。

```cpp
size_type max_size() const;
```

### <a name="return-value"></a>返回值

map 可能的最大长度。

### <a name="example"></a>示例

```cpp
// map_max_size.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;
   map <int, int> :: size_type i;

   i = m1.max_size( );
   cout << "The maximum possible length "
        << "of the map is " << i << "."
        << endl << "(Magnitude is machine specific.)";
}
```

## <a name="operator"></a><a name="op_at"></a> `operator[]`

将元素插入到具有指定键值的映射。

```cpp
Type& operator[](const Key& key);

Type& operator[](Key&& key);
```

### <a name="parameters"></a>参数

*`key`*\
要插入的元素的键值。

### <a name="return-value"></a>返回值

对插入元素的数据值的引用。

### <a name="remarks"></a>注解

如果未找到参数键值，则它将与数据类型的默认值一起插入。

`operator[]` 可用于将元素插入到映射中， `m` `m[key] = DataValue;` 其中， `DataValue` 是 `mapped_type` 具有键值的元素的值 *`key`* 。

使用 `operator[]` 插入元素时，返回的引用不指示插入是更改预先存在的元素还是创建一个新元素。 成员函数 [`find`](#find) 和 [`insert`](#insert) 可用于确定具有指定键的元素在插入前是否已存在。

### <a name="example"></a>示例

```cpp
// map_op_insert.cpp
// compile with: /EHsc
#include <map>
#include <iostream>
#include <string>

int main( )
{
   using namespace std;
   typedef pair <const int, int> cInt2Int;
   map <int, int> m1;
   map <int, int> :: iterator pIter;

   // Insert a data value of 10 with a key of 1
   // into a map using the operator[] member function
   m1[ 1 ] = 10;

   // Compare other ways to insert objects into a map
   m1.insert ( map <int, int> :: value_type ( 2, 20 ) );
   m1.insert ( cInt2Int ( 3, 30 ) );

   cout  << "The keys of the mapped elements are:";
   for ( pIter = m1.begin( ) ; pIter != m1.end( ) ; pIter++ )
      cout << " " << pIter -> first;
   cout << "." << endl;

   cout  << "The values of the mapped elements are:";
   for ( pIter = m1.begin( ) ; pIter != m1.end( ) ; pIter++ )
      cout << " " << pIter -> second;
   cout << "." << endl;

   // If the key already exists, operator[]
   // changes the value of the datum in the element
   m1[ 2 ] = 40;

   // operator[] will also insert the value of the data
   // type's default constructor if the value is unspecified
   m1[5];

   cout  << "The keys of the mapped elements are now:";
   for ( pIter = m1.begin( ) ; pIter != m1.end( ) ; pIter++ )
      cout << " " << pIter -> first;
   cout << "." << endl;

   cout  << "The values of the mapped elements are now:";
   for ( pIter = m1.begin( ) ; pIter != m1.end( ) ; pIter++ )
      cout << " " << pIter -> second;
   cout << "." << endl;

// insert by moving key
    map<string, int> c2;
    string str("abc");
    cout << "c2[move(str)] == " << c2[move(str)] << endl;
    cout << "c2["abc"] == " << c2["abc"] << endl;

    return (0);
}
```

```Output
The keys of the mapped elements are: 1 2 3.
The values of the mapped elements are: 10 20 30.
The keys of the mapped elements are now: 1 2 3 5.
The values of the mapped elements are now: 10 40 30 0.
c2[move(str)] == 0
c2["abc"] == 1
```

## <a name="operator"></a><a name="op_eq"></a> `operator=`

将一个映射中的元素替换为另一映射副本。

```cpp
map& operator=(const map& right);
map& operator=(map&& right);
```

### <a name="parameters"></a>参数

*`right`*\
[`map`](../standard-library/map-class.md)要复制到中的 `map` 。

### <a name="remarks"></a>注解

清除中的任何现有元素后 `map` ，会 `operator=` 将的内容复制或移动 *`right`* 到地图中。

### <a name="example"></a>示例

```cpp
// map_operator_as.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
   {
   using namespace std;
   map<int, int> v1, v2, v3;
   map<int, int>::iterator iter;

   v1.insert(pair<int, int>(1, 10));

   cout << "v1 = " ;
   for (iter = v1.begin(); iter != v1.end(); iter++)
      cout << iter->second << " ";
   cout << endl;

   v2 = v1;
   cout << "v2 = ";
   for (iter = v2.begin(); iter != v2.end(); iter++)
      cout << iter->second << " ";
   cout << endl;

// move v1 into v2
   v2.clear();
   v2 = move(v1);
   cout << "v2 = ";
   for (iter = v2.begin(); iter != v2.end(); iter++)
      cout << iter->second << " ";
   cout << endl;
   }
```

## <a name="pointer"></a><a name="pointer"></a> `pointer`

一种类型，此类型提供指向 map 中元素的指针。

```cpp
typedef typename allocator_type::pointer pointer;
```

### <a name="remarks"></a>注解

类型 `pointer` 可用于修改元素的值。

在大多数情况下， [`iterator`](#iterator) 应该使用来访问 map 对象中的元素。

## <a name="rbegin"></a><a name="rbegin"></a> rbegin

返回一个迭代器，此迭代器用于寻址反向 map 中的第一个元素。

```cpp
const_reverse_iterator rbegin() const;

reverse_iterator rbegin();
```

### <a name="return-value"></a>返回值

一个反向双向迭代器，用于寻址反向 map 中的第一个元素或寻址曾是非反向 map 中的最后一个元素的元素。

### <a name="remarks"></a>注解

`rbegin` 与反向映射一起使用，就像 [`begin`](#begin) 与映射一起使用一样。

如果将的返回值 `rbegin` 分配给 `const_reverse_iterator` ，则不能修改 map 对象。 如果将 `rbegin` 的返回值赋给 `reverse_iterator`，则可以修改 map 对象。

`rbegin` 可用于向后循环访问 map。

### <a name="example"></a>示例

```cpp
// map_rbegin.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;

   map <int, int> :: iterator m1_Iter;
   map <int, int> :: reverse_iterator m1_rIter;
   map <int, int> :: const_reverse_iterator m1_crIter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 3, 30 ) );

   m1_rIter = m1.rbegin( );
   cout << "The first element of the reversed map m1 is "
        << m1_rIter -> first << "." << endl;

   // begin can be used to start an iteration
   // through a map in a forward order
   cout << "The map is: ";
   for ( m1_Iter = m1.begin( ) ; m1_Iter != m1.end( ); m1_Iter++)
      cout << m1_Iter -> first << " ";
      cout << "." << endl;

   // rbegin can be used to start an iteration
   // through a map in a reverse order
   cout << "The reversed map is: ";
   for ( m1_rIter = m1.rbegin( ) ; m1_rIter != m1.rend( ); m1_rIter++)
      cout << m1_rIter -> first << " ";
      cout << "." << endl;

   // A map element can be erased by dereferencing to its key
   m1_rIter = m1.rbegin( );
   m1.erase ( m1_rIter -> first );

   m1_rIter = m1.rbegin( );
   cout << "After the erasure, the first element "
        << "in the reversed map is "
        << m1_rIter -> first << "." << endl;
}
```

```Output
The first element of the reversed map m1 is 3.
The map is: 1 2 3 .
The reversed map is: 3 2 1 .
After the erasure, the first element in the reversed map is 2.
```

## <a name="reference"></a><a name="reference"></a> `reference`

一种类型，此类型提供对存储在 map 中的元素的引用。

```cpp
typedef typename allocator_type::reference reference;
```

### <a name="example"></a>示例

```cpp
// map_reference.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );

   // Declare and initialize a const_reference &Ref1
   // to the key of the first element
   const int &Ref1 = ( m1.begin( ) -> first );

   // The following line would cause an error because the
   // non-const_reference can't be used to access the key
   // int &Ref1 = ( m1.begin( ) -> first );

   cout << "The key of first element in the map is "
        << Ref1 << "." << endl;

   // Declare and initialize a reference &Ref2
   // to the data value of the first element
   int &Ref2 = ( m1.begin( ) -> second );

   cout << "The data value of first element in the map is "
        << Ref2 << "." << endl;

   //The non-const_reference can be used to modify the
   //data value of the first element
   Ref2 = Ref2 + 5;
   cout << "The modified data value of first element is "
        << Ref2 << "." << endl;
}
```

```Output
The key of first element in the map is 1.
The data value of first element in the map is 10.
The modified data value of first element is 15.
```

## <a name="rend"></a><a name="rend"></a> `rend`

返回一个迭代器，此迭代器用于寻址反向 map 中最后一个元素之后的位置。

```cpp
const_reverse_iterator rend() const;

reverse_iterator rend();
```

### <a name="return-value"></a>返回值

一个反向双向迭代器，用于寻址反向 map 中最后一个元素之后的位置（非反向 map 中第一个元素之前的位置）。

### <a name="remarks"></a>注解

`rend` 与反向映射一起使用，就像 [`end`](#end) 与映射一起使用一样。

如果将的返回值 `rend` 分配给 `const_reverse_iterator` ，则不能修改 map 对象。 如果将 `rend` 的返回值赋给 `reverse_iterator`，则可以修改 map 对象。

`rend` 可用于测试反向迭代器是否已到达其 map 的末尾。

不应对 `rend` 返回的值取消引用。

### <a name="example"></a>示例

```cpp
// map_rend.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;

   map <int, int> :: iterator m1_Iter;
   map <int, int> :: reverse_iterator m1_rIter;
   map <int, int> :: const_reverse_iterator m1_crIter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 3, 30 ) );

   m1_rIter = m1.rend( );
   m1_rIter--;
   cout << "The last element of the reversed map m1 is "
        << m1_rIter -> first << "." << endl;

   // begin can be used to start an iteration
   // through a map in a forward order
   cout << "The map is: ";
   for ( m1_Iter = m1.begin( ) ; m1_Iter != m1.end( ); m1_Iter++)
      cout << m1_Iter -> first << " ";
      cout << "." << endl;

   // rbegin can be used to start an iteration
   // through a map in a reverse order
   cout << "The reversed map is: ";
   for ( m1_rIter = m1.rbegin( ) ; m1_rIter != m1.rend( ); m1_rIter++)
      cout << m1_rIter -> first << " ";
      cout << "." << endl;

   // A map element can be erased by dereferencing to its key
   m1_rIter = --m1.rend( );
   m1.erase ( m1_rIter -> first );

   m1_rIter = m1.rend( );
   m1_rIter--;
   cout << "After the erasure, the last element "
        << "in the reversed map is "
        << m1_rIter -> first << "." << endl;
}
```

```Output
The last element of the reversed map m1 is 1.
The map is: 1 2 3 .
The reversed map is: 3 2 1 .
After the erasure, the last element in the reversed map is 2.
```

## <a name="reverse_iterator"></a><a name="reverse_iterator"></a> `reverse_iterator`

一种类型，此类型提供可读取或修改反向 map 中的元素的双向迭代器。

```cpp
typedef std::reverse_iterator<iterator> reverse_iterator;
```

### <a name="remarks"></a>注解

类型 `reverse_iterator` 无法修改元素的值，它用于反向循环访问映射。

`reverse_iterator`由映射定义的是对象的元素 [`value_type`](#value_type) ，它的类型为 `pair<const Key, Type>` ，其第一个成员是元素的键，第二个成员是元素所持有的映射基准。

若要取消引用 `reverse_iterator` 指向映射中某个元素的 *rIter* ，请使用 `->` 运算符。

若要访问元素的键值，请使用 `rIter` -> **first**，其等同于 (\* `rIter`)。 **第一** 种。 若要访问元素的映射值，请使用 `rIter` -> **second**，其作用与 (\* `rIter`). **第一** 种。

### <a name="example"></a>示例

[`rbegin`](#rbegin)有关如何声明和使用的示例，请参阅示例 `reverse_iterator` 。

## <a name="size"></a><a name="size"></a> `size`

返回 `map` 中的元素数量。

```cpp
size_type size() const;
```

### <a name="return-value"></a>返回值

映射的当前长度。

### <a name="example"></a>示例

下面的示例演示成员函数的用法 `map::size` 。

```cpp
// map_size.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main()
{
    using namespace std;
    map<int, int> m1, m2;
    map<int, int>::size_type i;
    typedef pair<int, int> Int_Pair;

    m1.insert(Int_Pair(1, 1));
    i = m1.size();
    cout << "The map length is " << i << "." << endl;

    m1.insert(Int_Pair(2, 4));
    i = m1.size();
    cout << "The map length is now " << i << "." << endl;
}
```

```Output
The map length is 1.
The map length is now 2.
```

## <a name="size_type"></a><a name="size_type"></a> `size_type`

一种无符号整数类型，此类型可表示 map 中的元素数量。

```cpp
typedef typename allocator_type::size_type size_type;
```

### <a name="example"></a>示例

[`size`](#size)有关如何声明和使用的示例，请参见的示例 `size_type` 。

## <a name="swap"></a><a name="swap"></a> 购

交换两个映射的元素。

```cpp
void swap(
    map<Key, Type, Traits, Allocator>& right);
```

### <a name="parameters"></a>参数

*`right`*\
参数 map，提供与目标 map 进行交换的元素。

### <a name="remarks"></a>注解

此成员函数不会使后列项失效：用于在正在交换元素的两个 map 中指定元素的任何引用、指针或迭代器。

### <a name="example"></a>示例

```cpp
// map_swap.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1, m2, m3;
   map <int, int>::iterator m1_Iter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 3, 30 ) );
   m2.insert ( Int_Pair ( 10, 100 ) );
   m2.insert ( Int_Pair ( 20, 200 ) );
   m3.insert ( Int_Pair ( 30, 300 ) );

   cout << "The original map m1 is:";
   for ( m1_Iter = m1.begin( ); m1_Iter != m1.end( ); m1_Iter++ )
      cout << " " << m1_Iter -> second;
   cout   << "." << endl;

   // This is the member function version of swap
   //m2 is said to be the argument map; m1 the target map
   m1.swap( m2 );

   cout << "After swapping with m2, map m1 is:";
   for ( m1_Iter = m1.begin( ); m1_Iter != m1.end( ); m1_Iter++ )
      cout << " " << m1_Iter -> second;
   cout  << "." << endl;

   // This is the specialized template version of swap
   swap( m1, m3 );

   cout << "After swapping with m3, map m1 is:";
   for ( m1_Iter = m1.begin( ); m1_Iter != m1.end( ); m1_Iter++ )
      cout << " " << m1_Iter -> second;
   cout   << "." << endl;
}
```

```Output
The original map m1 is: 10 20 30.
After swapping with m2, map m1 is: 100 200.
After swapping with m3, map m1 is: 300.
```

## <a name="upper_bound"></a><a name="upper_bound"></a> `upper_bound`

返回一个迭代器，此迭代器指向 map 中其键值大于指定键的键值的第一个元素。

```cpp
iterator upper_bound(const Key& key);

const_iterator upper_bound(const Key& key) const;
```

### <a name="parameters"></a>参数

*`key`*\
要与当前搜索的 map 中元素的排序键值进行比较的参数键值。

### <a name="return-value"></a>返回值

一个 `iterator` 或 `const_iterator` ，用于寻址映射中其键大于参数键的元素的位置，或 `map` 如果未找到键的匹配项，则寻址中最后一个元素之后的位置。

如果将返回值赋给 `const_iterator` ，则不能修改 map 对象。 如果将返回值赋给 `iterator` ，则可以修改地图对象。

### <a name="example"></a>示例

```cpp
// map_upper_bound.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   map <int, int> m1;
   map <int, int> :: const_iterator m1_AcIter, m1_RcIter;
   typedef pair <int, int> Int_Pair;

   m1.insert ( Int_Pair ( 1, 10 ) );
   m1.insert ( Int_Pair ( 2, 20 ) );
   m1.insert ( Int_Pair ( 3, 30 ) );

   m1_RcIter = m1.upper_bound( 2 );
   cout << "The first element of map m1 with a key "
        << "greater than 2 is: "
        << m1_RcIter -> second << "." << endl;

   // If no match is found for the key, end is returned
   m1_RcIter = m1. upper_bound ( 4 );

   if ( m1_RcIter == m1.end( ) )
      cout << "The map m1 doesn't have an element "
           << "with a key greater than 4." << endl;
   else
      cout << "The element of map m1 with a key > 4 is: "
           << m1_RcIter -> second << "." << endl;

   // The element at a specific location in the map can be found
   // using a dereferenced iterator addressing the location
   m1_AcIter = m1.begin( );
   m1_RcIter = m1. upper_bound ( m1_AcIter -> first );
   cout << "The 1st element of m1 with a key greater than\n"
        << "that of the initial element of m1 is: "
        << m1_RcIter -> second << "." << endl;
}
```

```Output
The first element of map m1 with a key greater than 2 is: 30.
The map m1 doesn't have an element with a key greater than 4.
The 1st element of m1 with a key greater than
that of the initial element of m1 is: 20.
```

## <a name="value_comp"></a><a name="value_comp"></a> `value_comp`

此成员函数返回一个函数对象，该函数对象可通过比较 map 中元素的键值来确定元素顺序。

```cpp
value_compare value_comp() const;
```

### <a name="return-value"></a>返回值

返回 map 用来对其元素进行排序的比较函数对象。

### <a name="remarks"></a>注解

对于 map *m*，如果两个元素 *e1* (*版 k1*， *d1*) 和 *e2* (*k2*， *D2*) 为类型为的对象 `value_type` ，其中 *版 k1* 和 *版 k1* 是其类型的键， `key_type` *d1* 和 *D2* 是其类型的数据 `mapped_type` ，则 `m.value_comp(e1, e2)` 等效于 `m.key_comp(k1, k2)` 。 存储对象会定义成员函数

`bool operator( value_type& left, value_type& right);`

如果的 **`true`** 键值 `left` 先于且不等于排序顺序中的键值，则返回 `right` 。

### <a name="example"></a>示例

```cpp
// map_value_comp.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;

   map <int, int, less<int> > m1;
   map <int, int, less<int> >::value_compare vc1 = m1.value_comp( );
   pair< map<int,int>::iterator, bool > pr1, pr2;

   pr1= m1.insert ( map <int, int> :: value_type ( 1, 10 ) );
   pr2= m1.insert ( map <int, int> :: value_type ( 2, 5 ) );

   if( vc1( *pr1.first, *pr2.first ) == true )
   {
      cout << "The element ( 1,10 ) precedes the element ( 2,5 )."
           << endl;
   }
   else
   {
      cout << "The element ( 1,10 ) does not precede the element ( 2,5 )."
           << endl;
   }

   if(vc1( *pr2.first, *pr1.first ) == true )
   {
      cout << "The element ( 2,5 ) precedes the element ( 1,10 )."
           << endl;
   }
   else
   {
      cout << "The element ( 2,5 ) does not precede the element ( 1,10 )."
           << endl;
   }
}
```

```Output
The element ( 1,10 ) precedes the element ( 2,5 ).
The element ( 2,5 ) does not precede the element ( 1,10 ).
```

## <a name="value_type"></a><a name="value_type"></a> `value_type`

存储为 map 中的元素的对象的类型。

```cpp
typedef pair<const Key, Type> value_type;
```

### <a name="example"></a>示例

```cpp
// map_value_type.cpp
// compile with: /EHsc
#include <map>
#include <iostream>

int main( )
{
   using namespace std;
   typedef pair <const int, int> cInt2Int;
   map <int, int> m1;
   map <int, int> :: key_type key1;
   map <int, int> :: mapped_type mapped1;
   map <int, int> :: value_type value1;
   map <int, int> :: iterator pIter;

   // value_type can be used to pass the correct type
   // explicitly to avoid implicit type conversion
   m1.insert ( map <int, int> :: value_type ( 1, 10 ) );

   // Compare other ways to insert objects into a map
   m1.insert ( cInt2Int ( 2, 20 ) );
   m1[ 3 ] = 30;

   // Initializing key1 and mapped1
   key1 = ( m1.begin( ) -> first );
   mapped1 = ( m1.begin( ) -> second );

   cout << "The key of first element in the map is "
        << key1 << "." << endl;

   cout << "The data value of first element in the map is "
        << mapped1 << "." << endl;

   // The following line would cause an error because
   // the value_type isn't assignable
   // value1 = cInt2Int ( 4, 40 );

   cout  << "The keys of the mapped elements are:";
   for ( pIter = m1.begin( ) ; pIter != m1.end( ) ; pIter++ )
      cout << " " << pIter -> first;
   cout << "." << endl;

   cout  << "The values of the mapped elements are:";
   for ( pIter = m1.begin( ) ; pIter != m1.end( ) ; pIter++ )
      cout << " " << pIter -> second;
   cout << "." << endl;
}
```

## <a name="see-also"></a>另请参阅

[容器](./stl-containers.md)\
[C + + 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[C + + 标准库参考](../standard-library/cpp-standard-library-reference.md)
