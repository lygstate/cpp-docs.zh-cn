---
title: vector 类
description: 适用于类 vector 的 Microsoft c + + 标准库实现的参考。
ms.date: 02/23/2021
f1_keywords:
- vector/std::vector::allocator_type
- vector/std::vector::const_iterator
- vector/std::vector::const_pointer
- vector/std::vector::const_reference
- vector/std::vector::const_reverse_iterator
- vector/std::vector::difference_type
- vector/std::vector::iterator
- vector/std::vector::pointer
- vector/std::vector::reference
- vector/std::vector::reverse_iterator
- vector/std::vector::size_type
- vector/std::vector::value_type
- vector/std::vector::assign
- vector/std::vector::at
- vector/std::vector::back
- vector/std::vector::begin
- vector/std::vector::capacity
- vector/std::vector::cbegin
- vector/std::vector::cend
- vector/std::vector::crbegin
- vector/std::vector::crend
- vector/std::vector::clear
- vector/std::vector::data
- vector/std::vector::emplace
- vector/std::vector::emplace_back
- vector/std::vector::empty
- vector/std::vector::end
- vector/std::vector::erase
- vector/std::vector::front
- vector/std::vector::get_allocator
- vector/std::vector::insert
- vector/std::vector::max_size
- vector/std::vector::pop_back
- vector/std::vector::push_back
- vector/std::vector::rbegin
- vector/std::vector::rend
- vector/std::vector::reserve
- vector/std::vector::resize
- vector/std::vector::shrink_to_fit
- vector/std::vector::size
- vector/std::vector::swap
helpviewer_keywords:
- std::vector [C++], allocator_type
- std::vector [C++], const_iterator
- std::vector [C++], const_pointer
- std::vector [C++], const_reference
- std::vector [C++], const_reverse_iterator
- std::vector [C++], difference_type
- std::vector [C++], iterator
- std::vector [C++], pointer
- std::vector [C++], reference
- std::vector [C++], reverse_iterator
- std::vector [C++], size_type
- std::vector [C++], value_type
- std::vector [C++], assign
- std::vector [C++], at
- std::vector [C++], back
- std::vector [C++], begin
- std::vector [C++], capacity
- std::vector [C++], cbegin
- std::vector [C++], cend
- std::vector [C++], crbegin
- std::vector [C++], crend
- std::vector [C++], clear
- std::vector [C++], data
- std::vector [C++], emplace
- std::vector [C++], emplace_back
- std::vector [C++], empty
- std::vector [C++], end
- std::vector [C++], erase
- std::vector [C++], front
- std::vector [C++], get_allocator
- std::vector [C++], insert
- std::vector [C++], max_size
- std::vector [C++], pop_back
- std::vector [C++], push_back
- std::vector [C++], rbegin
- std::vector [C++], rend
- std::vector [C++], reserve
- std::vector [C++], resize
- std::vector [C++], shrink_to_fit
- std::vector [C++], size
- std::vector [C++], swap
ms.openlocfilehash: bcc6049c5b1040ea2bf3772a851ed26d40a4c608
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099282"
---
# <a name="vector-class"></a>`vector` 类

C + + 标准库 vector 类是序列容器的类模板。 矢量以线性方式存储给定类型的元素，并允许快速随机访问任何元素。 当随机访问性能处于高级版时，矢量是序列的首选容器。

## <a name="syntax"></a>语法

```cpp
template <class Type, class Allocator = allocator<Type>>
class vector
```

### <a name="parameters"></a>参数

*`Type`*\
要存储在矢量中的元素数据类型

*`Allocator`*\
表示所存储分配器对象的类型，该分配器对象封装有关矢量的内存分配和解除分配的详细信息。 此参数为可选参数，默认值为 `allocator<Type>`。

## <a name="remarks"></a>注解

向量允许在序列末尾插入和删除常量事件。 若要在矢量中间插入或删除元素，则需要线性时间。 [ `deque` 类](../standard-library/deque-class.md)容器在序列的开头和结尾处速度更快。 [ `list` 类](../standard-library/list-class.md)容器在序列内任何位置的插入和删除速度更快。

当成员函数必须将矢量对象中所含序列增加到超过其当前存储容量时，将进行矢量重新分配。 其他的插入和删除均可能改变序列中的各个存储地址。 在所有此类情况下，指向序列更改部分的迭代器或引用将变为无效。 如果未进行重新分配，则只有插入/删除点前的迭代器和引用保持有效。

[ `vector<bool>` 类](../standard-library/vector-bool-class.md)是类型的元素的类模板向量的完全专用化 **`bool`** 。 它具有用于专用化的基础类型的分配器。

[ `vector<bool>` 引用类](../standard-library/vector-bool-class.md#reference_class)是一个嵌套类，其对象可提供对对象中 (单个位) 的元素的引用 `vector<bool>` 。

## <a name="members"></a>成员

### <a name="constructors"></a>构造函数

|名称|说明|
|-|-|
|[`vector`](#vector)|构造一个向量，它具有特定大小、具有特定值的元素、具有特定 `allocator`，或将其构造成某个其它向量的副本。|

### <a name="typedefs"></a>Typedef

|名称|说明|
|-|-|
|`[allocator_type]` (#allocator_type) |一个类型，它表示矢量对象的 `allocator` 类。|
|[`const_iterator`](#const_iterator)|一种类型，它提供可读取矢量中元素的随机访问迭代器 **`const`** 。|
|[`const_pointer`](#const_pointer)|一种类型，它提供指向 **`const`** 矢量中元素的指针。|
|[`const_reference`](#const_reference)|一种类型，该类型提供对 **`const`** 存储在向量中的元素的引用。 它用于读取和执行 **`const`** 操作。|
|[`const_reverse_iterator`](#const_reverse_iterator)|一种类型，它提供可读取矢量中任何元素的随机访问迭代器 **`const`** 。|
|[`difference_type`](#difference_type)|一个类型，它提供矢量中两个元素的址间的差异。|
|[`iterator`](#iterator)|一个类型，它提供可读取或修改向量中任何元素的随机访问迭代器。|
|[`pointer`](#pointer)|一个类型，提供指向向量中元素的指针。|
|[`reference`](#reference)|一个类型，它提供对向量中存储的元素的引用。|
|[`reverse_iterator`](#reverse_iterator)|一个类型，它提供可读取或修改反向矢量中的任意元素的随机访问迭代器。|
|[`size_type`](#size_type)|一个类型，它计算矢量中的元素数目。|
|[`value_type`](#value_type)|一个类型，它代表向量中存储的数据类型。|

### <a name="functions"></a>函数

|名称|说明|
|-|-|
|[`assign`](#assign)|清除矢量并将指定的元素复制到该空矢量。|
|[`at`](#at)|返回对矢量中指定位置的元素的引用。|
|[`back`](#back)|返回对向量中最后一个元素的引用。|
|[`begin`](#begin)|对该向量中第一个元素返回随机访问迭代器。|
|[`capacity`](#capacity)|返回在不分配更多的存储的情况下向量可以包含的元素数。|
|[`cbegin`](#cbegin)|返回指向向量中第一个元素的随机访问常量迭代器。|
|[`cend`](#cend)|返回一个随机访问常量迭代器，它指向刚超过矢量末尾的位置。|
|[`crbegin`](#crbegin)|返回一个指向反向矢量中第一个元素的常量迭代器。|
|[`crend`](#crend)|返回一个指向反向矢量末尾的常量迭代器。|
|[`clear`](#clear)|清除向量的元素。|
|[`data`](#data)|返回指向向量中第一个元素的指针。|
|[`emplace`](#emplace)|将就地构造的元素插入到指定位置的向量中。|
|[`emplace_back`](#emplace_back)|将一个就地构造的元素添加到向量末尾。|
|[`empty`](#empty)|测试矢量容器是否为空。|
|[`end`](#end)|返回指向矢量末尾的随机访问迭代器。|
|[`erase`](#erase)|从指定位置删除向量中的一个元素或一系列元素。|
|[`front`](#front)|返回对向量中第一个元素的引用。|
|[`get_allocator`](#get_allocator)|将对象返回到矢量使用的 `allocator` 类。|
|[`insert`](#insert)|将一个或多个元素插入到指定位置的向量中。|
|[`max_size`](#max_size)|返回向量的最大长度。|
|[`pop_back`](#pop_back)|删除矢量末尾处的元素。|
|[`push_back`](#push_back)|在矢量末尾处添加一个元素。|
|[`rbegin`](#rbegin)|返回指向反向向量中第一个元素的迭代器。|
|[`rend`](#rend)|返回一个指向反向矢量末尾的迭代器。|
|[`reserve`](#reserve)|保留向量对象的最小存储长度。|
|[`resize`](#resize)|为矢量指定新的大小。|
|[`shrink_to_fit`](#shrink_to_fit)|放弃额外容量。|
|[`size`](#size)|返回向量中的元素数量。|
|[`swap`](#swap)|交换两个向量的元素。|

### <a name="operators"></a>运算符

|名称|说明|
|-|-|
|[`operator[]`](#op_at)|返回对指定位置的矢量元素的引用。|
|[`operator=`](#op_eq)|用另一个向量的副本替换该向量中的元素。|

## <a name="allocator_type"></a><a name="allocator_type"></a> `allocator_type`

一个类型，它代表向量对象的分配器类。

```cpp
typedef Allocator allocator_type;
```

### <a name="remarks"></a>注解

`allocator_type` 是模板参数 `Allocator` 的同义词。

### <a name="example"></a>示例

有关使用 `allocator_type` 的示例，请参阅 [get_allocator](#get_allocator) 的示例。

## <a name="assign"></a><a name="assign"></a> `assign`

清除矢量并将指定的元素复制到该空矢量。

```cpp
void assign(size_type count, const Type& value);
void assign(initializer_list<Type> init_list);

template <class InputIterator>
void assign(InputIterator first, InputIterator last);
```

### <a name="parameters"></a>参数

*`first`*\
要复制的元素范围内的第一个元素的位置。

*`last`*\
要复制的元素范围外的第一个元素的位置。

*`count`*\
要插入到矢量的元素的副本数。

*`value`*\
插入到向量中的元素的值。

*`init_list`*\
包含要插入的元素的 initializer_list。

### <a name="remarks"></a>注解

首先， `assign` 清除向量中的任何现有元素。 然后，将 `assign` 原始向量中指定范围的元素插入到向量中，或将新的指定值元素的副本插入到向量中。

### <a name="example"></a>示例

```cpp
/ vector_assign.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main()
{
    using namespace std;
    vector<int> v1, v2, v3;

    v1.push_back(10);
    v1.push_back(20);
    v1.push_back(30);
    v1.push_back(40);
    v1.push_back(50);

    cout << "v1 = ";
    for (auto& v : v1){
        cout << v << " ";
    }
    cout << endl;

    v2.assign(v1.begin(), v1.end());
    cout << "v2 = ";
    for (auto& v : v2){
        cout << v << " ";
    }
    cout << endl;

    v3.assign(7, 4);
    cout << "v3 = ";
    for (auto& v : v3){
        cout << v << " ";
    }
    cout << endl;

    v3.assign({ 5, 6, 7 });
    for (auto& v : v3){
        cout << v << " ";
    }
    cout << endl;
}
```

## <a name="at"></a><a name="at"></a> `at`

返回对矢量中指定位置的元素的引用。

```cpp
reference at(size_type position);

const_reference at(size_type position) const;
```

### <a name="parameters"></a>参数

*`position`*\
要在矢量中引用的元素的下标或位置编号。

### <a name="return-value"></a>返回值

对自变量中的下标元素的引用。 如果 *`position`* 大于矢量的大小，将 `at` 引发异常。

### <a name="remarks"></a>注解

如果将的返回值 `at` 分配给 `const_reference` ，则无法修改矢量对象。 如果将 `at` 的返回值分配给 `reference`，则可以修改矢量对象。

### <a name="example"></a>示例

```cpp
// vector_at.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;

   v1.push_back( 10 );
   v1.push_back( 20 );

   const int &i = v1.at( 0 );
   int &j = v1.at( 1 );
   cout << "The first element is " << i << endl;
   cout << "The second element is " << j << endl;
}
```

```Output
The first element is 10
The second element is 20
```

## <a name="back"></a><a name="back"></a> `back`

返回对向量中最后一个元素的引用。

```cpp
reference back();

const_reference back() const;
```

### <a name="return-value"></a>返回值

向量的最后一个元素。 如果向量为空，则返回值不确定。

### <a name="remarks"></a>注解

如果将的返回值 `back` 分配给 `const_reference` ，则无法修改矢量对象。 如果将 `back` 的返回值分配给 `reference`，则可以修改矢量对象。

当使用 [`_ITERATOR_DEBUG_LEVEL`](../standard-library/iterator-debug-level.md) 定义为1或2的进行编译时，如果尝试访问空向量中的元素，将发生运行时错误。 有关详细信息，请参阅 [检查迭代](../standard-library/checked-iterators.md)器。

### <a name="example"></a>示例

```cpp
// vector_back.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main() {
   using namespace std;
   vector <int> v1;

   v1.push_back( 10 );
   v1.push_back( 11 );

   int& i = v1.back( );
   const int& ii = v1.front( );

   cout << "The last integer of v1 is " << i << endl;
   i--;
   cout << "The next-to-last integer of v1 is "<< ii << endl;
}
```

## <a name="begin"></a><a name="begin"></a> `begin`

对该向量中第一个元素返回随机访问迭代器。

```cpp
const_iterator begin() const;

iterator begin();
```

### <a name="return-value"></a>返回值

发现 `vector` 中第一个元素或空 `vector` 之后的位置的随机访问迭代器。 请始终比较返回的值 [`vector::end`](#end) 以确保它有效。

### <a name="remarks"></a>注解

如果将的返回值 `begin` 分配给 [`vector::const_iterator`](#const_iterator) ，则 `vector` 无法修改对象。 如果将的返回值 `begin` 分配给 [`vector::iterator`](#iterator) ，则 `vector` 可以修改该对象。

### <a name="example"></a>示例

```cpp
// vector_begin.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main()
{
    using namespace std;
    vector<int> c1;
    vector<int>::iterator c1_Iter;
    vector<int>::const_iterator c1_cIter;

    c1.push_back(1);
    c1.push_back(2);

    cout << "The vector c1 contains elements:";
    c1_Iter = c1.begin();
    for (; c1_Iter != c1.end(); c1_Iter++)
    {
        cout << " " << *c1_Iter;
    }
    cout << endl;

    cout << "The vector c1 now contains elements:";
    c1_Iter = c1.begin();
    *c1_Iter = 20;
    for (; c1_Iter != c1.end(); c1_Iter++)
    {
        cout << " " << *c1_Iter;
    }
    cout << endl;

    // The following line would be an error because iterator is const
    // *c1_cIter = 200;
}
```

```Output
The vector c1 contains elements: 1 2
The vector c1 now contains elements: 20 2
```

## <a name="capacity"></a><a name="capacity"></a> `capacity`

返回在不分配更多的存储的情况下向量可以包含的元素数。

```cpp
size_type capacity() const;
```

### <a name="return-value"></a>返回值

分配给该向量的当前存储长度。

### <a name="remarks"></a>注解

[`resize`](#resize)如果分配足够的内存来容纳此函数，则成员函数将更有效。 使用成员函数 [`reserve`](#reserve) 指定分配的内存量。

### <a name="example"></a>示例

```cpp
// vector_capacity.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;

   v1.push_back( 1 );
   cout << "The length of storage allocated is "
        << v1.capacity( ) << "." << endl;

   v1.push_back( 2 );
   cout << "The length of storage allocated is now "
        << v1.capacity( ) << "." << endl;
}
```

```Output
The length of storage allocated is 1.
The length of storage allocated is now 2.
```

## <a name="cbegin"></a><a name="cbegin"></a> `cbegin`

返回一个 **`const`** 迭代器，该迭代器用于寻址范围内的第一个元素。

```cpp
const_iterator cbegin() const;
```

### <a name="return-value"></a>返回值

一个 **`const`** 随机访问迭代器，指向范围的第一个元素，或刚超出空范围末尾 (空范围) 的位置 `cbegin() == cend()` 。

### <a name="remarks"></a>注解

如果返回值为 `cbegin` ，则不能修改范围中的元素。

可以使用此成员函数替代 `begin()` 成员函数，以保证返回值为 `const_iterator`。 通常，它与 [`auto`](../cpp/auto-cpp.md) 类型推导关键字一起使用，如下面的示例中所示。 在此示例中，将视为 `Container` 支持和的任何类型的可修改 (非 **`const`**) 容器 `begin()` `cbegin()` 。

```cpp
auto i1 = Container.begin();
// i1 is Container<T>::iterator
auto i2 = Container.cbegin();

// i2 is Container<T>::const_iterator
```

## <a name="cend"></a><a name="cend"></a> `cend`

返回 **`const`** 后端迭代器，该迭代器指向矢量最后一个元素之后的元素。

```cpp
const_iterator cend() const;
```

### <a name="return-value"></a>返回值

`const`向量的过去的迭代器。 它指向矢量最后一个元素之后的元素。 该元素是占位符，不应取消引用。 仅将它用于比较。 如果向量为空，则为 `vector::cend() == vector::cbegin()` 。

### <a name="remarks"></a>注解

`cend` 用于测试迭代器是否超过了其范围的末尾。

可以使用此成员函数替代 `end()` 成员函数，以保证返回值为 `const_iterator`。 通常，它与 [`auto`](../cpp/auto-cpp.md) 类型推导关键字一起使用，如下面的示例中所示。 在此示例中，将视为 `Container` 支持和的任何类型的可修改 (非 **`const`**) 容器 `end()` `cend()` 。

```cpp
auto i1 = Container.end();
// i1 is Container<T>::iterator
auto i2 = Container.cend();

// i2 is Container<T>::const_iterator
```

返回的值 `cend` 不应被取消引用。 仅将它用于比较。

## <a name="clear"></a><a name="clear"></a> `clear`

清除向量的元素。

```cpp
void clear();
```

### <a name="example"></a>示例

```cpp
// vector_clear.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;

   v1.push_back( 10 );
   v1.push_back( 20 );
   v1.push_back( 30 );

   cout << "The size of v1 is " << v1.size( ) << endl;
   v1.clear( );
   cout << "The size of v1 after clearing is " << v1.size( ) << endl;
}
```

```Output
The size of v1 is 3
The size of v1 after clearing is 0
```

## <a name="const_iterator"></a><a name="const_iterator"></a> `const_iterator`

一种类型，它提供可读取矢量中元素的随机访问迭代器 **`const`** 。

```cpp
typedef implementation-defined const_iterator;
```

### <a name="remarks"></a>注解

类型 `const_iterator` 不能用于修改元素的值。

### <a name="example"></a>示例

有关使用 `const_iterator` 的示例，请参阅 [back](#back) 的示例。

## <a name="const_pointer"></a><a name="const_pointer"></a> `const_pointer`

一种类型，它提供指向 **`const`** 矢量中元素的指针。

```cpp
typedef typename Allocator::const_pointer const_pointer;
```

### <a name="remarks"></a>注解

类型 `const_pointer` 不能用于修改元素的值。

[iterator](#iterator) 更常用于访问矢量元素。

## <a name="const_reference"></a><a name="const_reference"></a> `const_reference`

一种类型，该类型提供对 **`const`** 存储在向量中的元素的引用。 它用于读取和执行 **`const`** 操作。

```cpp
typedef typename Allocator::const_reference const_reference;
```

### <a name="remarks"></a>注解

类型 `const_reference` 不能用于修改元素的值。

### <a name="example"></a>示例

```cpp
// vector_const_ref.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;

   v1.push_back( 10 );
   v1.push_back( 20 );

   const vector <int> v2 = v1;
   const int &i = v2.front( );
   const int &j = v2.back( );
   cout << "The first element is " << i << endl;
   cout << "The second element is " << j << endl;

   // The following line would cause an error as v2 is const
   // v2.push_back( 30 );
}
```

```Output
The first element is 10
The second element is 20
```

## <a name="const_reverse_iterator"></a><a name="const_reverse_iterator"></a> `const_reverse_iterator`

一种类型，它提供可读取矢量中任何元素的随机访问迭代器 **`const`** 。

```cpp
typedef std::reverse_iterator<const_iterator> const_reverse_iterator;
```

### <a name="remarks"></a>注解

类型 `const_reverse_iterator` 无法修改元素的值，它用于反向循环访问矢量。

### <a name="example"></a>示例

[`rbegin`](#rbegin)有关如何声明和使用迭代器的示例，请参阅。

## <a name="crbegin"></a><a name="crbegin"></a> `crbegin`

返回一个指向反向矢量中第一个元素的常量迭代器。

```cpp
const_reverse_iterator crbegin() const;
```

### <a name="return-value"></a>返回值

一种常量反向随机访问迭代器，用于寻址反向 [`vector`](../standard-library/vector-class.md) 或处理非反向中最后一个元素之后的第一个元素 `vector` 。

### <a name="remarks"></a>注解

如果返回值为 `crbegin` ，则 `vector` 无法修改对象。

### <a name="example"></a>示例

```cpp
// vector_crbegin.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::iterator v1_Iter;
   vector <int>::const_reverse_iterator v1_rIter;

   v1.push_back( 1 );
   v1.push_back( 2 );

   v1_Iter = v1.begin( );
   cout << "The first element of vector is "
        << *v1_Iter << "." << endl;

   v1_rIter = v1.crbegin( );
   cout << "The first element of the reversed vector is "
        << *v1_rIter << "." << endl;
}
```

```Output
The first element of vector is 1.
The first element of the reversed vector is 2.
```

## <a name="crend"></a><a name="crend"></a> `crend`

返回一个 `const` 后端反向迭代器，该迭代器指向反向向量的最后一个元素之后的元素。

```cpp
const_reverse_iterator crend() const;
```

### <a name="return-value"></a>返回值

`const`反向向量的反向结束迭代器。 它指向反向向量的最后一个元素之后的元素，该元素与非反转向量的第一个元素之前的元素相同。 该元素是占位符，不应取消引用。 仅将它用于比较。

### <a name="remarks"></a>注解

`crend` 用于反向，正 `vector` 如 [`vector::cend`](#cend) 用于 `vector` 。

如果返回值为 `crend` (适当递减的) ，则 `vector` 无法修改对象。

`crend` 可用于测试反向迭代器是否已到达其 `vector` 的末尾。

返回的值 `crend` 不应被取消引用。 仅将它用于比较。

### <a name="example"></a>示例

```cpp
// vector_crend.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::const_reverse_iterator v1_rIter;

   v1.push_back( 1 );
   v1.push_back( 2 );

   for ( v1_rIter = v1.rbegin( ) ; v1_rIter != v1.rend( ) ; v1_rIter++ )
      cout << *v1_rIter << endl;
}
```

```Output
2
1
```

## <a name="data"></a><a name="data"></a> `data`

返回指向向量中第一个元素的指针。

```cpp
const_pointer data() const;

pointer data();
```

### <a name="return-value"></a>返回值

一个指针，指向中的第一个元素 [`vector`](../standard-library/vector-class.md) 或空后面的位置 `vector` 。

### <a name="example"></a>示例

```cpp
// vector_data.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main()
{
    using namespace std;
    vector<int> c1;
    vector<int>::pointer c1_ptr;
    vector<int>::const_pointer c1_cPtr;

    c1.push_back(1);
    c1.push_back(2);

    cout << "The vector c1 contains elements:";
    c1_cPtr = c1.data();
    for (size_t n = c1.size(); 0 < n; --n, c1_cPtr++)
    {
        cout << " " << *c1_cPtr;
    }
    cout << endl;

    cout << "The vector c1 now contains elements:";
    c1_ptr = c1.data();
    *c1_ptr = 20;
    for (size_t n = c1.size(); 0 < n; --n, c1_ptr++)
    {
        cout << " " << *c1_ptr;
    }
    cout << endl;
}
```

```Output
The vector c1 contains elements: 1 2
The vector c1 now contains elements: 20 2
```

## <a name="difference_type"></a><a name="difference_type"></a> `difference_type`

一个类型，它提供引用同一向量中元素的两个迭代器之间的差异。

```cpp
typedef typename Allocator::difference_type difference_type;
```

### <a name="remarks"></a>注解

`difference_type` 也可以被描述为两个指针之间的元素数，因为指向一个元素的指针包含其地址。

[iterator](#iterator) 更常用于访问矢量元素。

### <a name="example"></a>示例

```cpp
// vector_diff_type.cpp
// compile with: /EHsc
#include <iostream>
#include <vector>
#include <algorithm>

int main( )
{
   using namespace std;

   vector <int> c1;
   vector <int>::iterator c1_Iter, c2_Iter;

   c1.push_back( 30 );
   c1.push_back( 20 );
   c1.push_back( 30 );
   c1.push_back( 10 );
   c1.push_back( 30 );
   c1.push_back( 20 );

   c1_Iter = c1.begin( );
   c2_Iter = c1.end( );

   vector <int>::difference_type   df_typ1, df_typ2, df_typ3;

   df_typ1 = count( c1_Iter, c2_Iter, 10 );
   df_typ2 = count( c1_Iter, c2_Iter, 20 );
   df_typ3 = count( c1_Iter, c2_Iter, 30 );
   cout << "The number '10' is in c1 collection " << df_typ1 << " times.\n";
   cout << "The number '20' is in c1 collection " << df_typ2 << " times.\n";
   cout << "The number '30' is in c1 collection " << df_typ3 << " times.\n";
}
```

```Output
The number '10' is in c1 collection 1 times.
The number '20' is in c1 collection 2 times.
The number '30' is in c1 collection 3 times.
```

## <a name="emplace"></a><a name="emplace"></a> `emplace`

将就地构造的元素插入到指定位置的向量中。

```cpp
template <class... Types>
iterator emplace(
    const_iterator position,
    Types&&... args);
```

### <a name="parameters"></a>参数

*`position`*\
中 [`vector`](../standard-library/vector-class.md) 插入第一个元素的位置。

*`args`*\
构造函数参数。 函数根据所提供的自变量来推断要调用的构造函数重载。

### <a name="return-value"></a>返回值

该函数将返回一个指向 `vector` 中新元素的插入位置的迭代器。

### <a name="remarks"></a>注解

任何插入操作都可能会消耗大量资源，请参阅[ `vector` 类](../standard-library/vector-class.md)以了解性能的讨论 `vector` 。

### <a name="example"></a>示例

```cpp
// vector_emplace.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::iterator Iter;

   v1.push_back( 10 );
   v1.push_back( 20 );
   v1.push_back( 30 );

   cout << "v1 =" ;
   for ( Iter = v1.begin( ) ; Iter != v1.end( ) ; Iter++ )
      cout << " " << *Iter;
   cout << endl;

// initialize a vector of vectors by moving v1
   vector < vector <int> > vv1;

   vv1.emplace( vv1.begin(), move( v1 ) );
   if ( vv1.size( ) != 0 && vv1[0].size( ) != 0 )
      {
      cout << "vv1[0] =";
      for (Iter = vv1[0].begin( ); Iter != vv1[0].end( ); Iter++ )
         cout << " " << *Iter;
      cout << endl;
      }
}
```

```Output
v1 = 10 20 30
vv1[0] = 10 20 30
```

## <a name="emplace_back"></a><a name="emplace_back"></a> `emplace_back`

将一个就地构造的元素添加到向量末尾。

```cpp
template <class... Types>
void emplace_back(Types&&... args);
```

### <a name="parameters"></a>参数

*`args`*\
构造函数参数。 函数根据所提供的自变量来推断要调用的构造函数重载。

### <a name="example"></a>示例

```cpp
#include <vector>
struct obj
{
   obj(int, double) {}
};

int main()
{
   std::vector<obj> v;
   v.emplace_back(1, 3.14); // obj in created in place in the vector
}
```

## <a name="empty"></a><a name="empty"></a> `empty`

测试矢量是否为空。

```cpp
bool empty() const;
```

### <a name="return-value"></a>返回值

**`true`** 如果向量为空，则为; 否则为。 **`false`** 如果矢量不为空，则为。

### <a name="example"></a>示例

```cpp
// vector_empty.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;

   v1.push_back( 10 );

   if ( v1.empty( ) )
      cout << "The vector is empty." << endl;
   else
      cout << "The vector is not empty." << endl;
}
```

```Output
The vector is not empty.
```

## <a name="end"></a><a name="end"></a> `end`

返回后端迭代器，该迭代器指向矢量最后一个元素之后的元素。

```cpp
iterator end();

const_iterator end() const;
```

### <a name="return-value"></a>返回值

向量的过去的迭代器。 它指向矢量最后一个元素之后的元素。 该元素是占位符，不应取消引用。 仅将它用于比较。 如果向量为空，则为 `vector::end() == vector::begin()` 。

### <a name="remarks"></a>注解

如果将的返回值 `end` 分配给类型的变量 `const_iterator` ，则不能修改矢量对象。 如果将的返回值 `end` 分配给类型的变量 `iterator` ，则可以修改矢量对象。

### <a name="example"></a>示例

```cpp
// vector_end.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>
int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::iterator v1_Iter;

   v1.push_back( 1 );
   v1.push_back( 2 );

   for ( v1_Iter = v1.begin( ) ; v1_Iter != v1.end( ) ; v1_Iter++ )
      cout << *v1_Iter << endl;
}
```

```Output
1
2
```

## <a name="erase"></a><a name="erase"></a> `erase`

从指定位置删除向量中的一个元素或一系列元素。

```cpp
iterator erase(
    const_iterator position);

iterator erase(
    const_iterator first,
    const_iterator last);
```

### <a name="parameters"></a>参数

*`position`*\
要从向量中移除的元素的位置。

*`first`*\
要从向量中移除的第一个元素的位置。

*`last`*\
紧接要从向量中移除的最后一个元素的位置。

### <a name="return-value"></a>返回值

一个迭代器，它指定已移除的任何元素之外保留的第一个元素或指向向量末尾的指针（若此类元素不存在）。

### <a name="example"></a>示例

```cpp
// vector_erase.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::iterator Iter;

   v1.push_back( 10 );
   v1.push_back( 20 );
   v1.push_back( 30 );
   v1.push_back( 40 );
   v1.push_back( 50 );

   cout << "v1 =" ;
   for ( Iter = v1.begin( ) ; Iter != v1.end( ) ; Iter++ )
      cout << " " << *Iter;
   cout << endl;

   v1.erase( v1.begin( ) );
   cout << "v1 =";
   for ( Iter = v1.begin( ) ; Iter != v1.end( ) ; Iter++ )
      cout << " " << *Iter;
   cout << endl;

   v1.erase( v1.begin( ) + 1, v1.begin( ) + 3 );
   cout << "v1 =";
   for ( Iter = v1.begin( ) ; Iter != v1.end( ) ; Iter++ )
      cout << " " << *Iter;
   cout << endl;
}
```

```Output
v1 = 10 20 30 40 50
v1 = 20 30 40 50
v1 = 20 50
```

## <a name="front"></a><a name="front"></a> `front`

返回对向量中第一个元素的引用。

```cpp
reference front();

const_reference front() const;
```

### <a name="return-value"></a>返回值

对向量对象中第一个元素的引用。 如果向量为空，则返回值不确定。

### <a name="remarks"></a>注解

如果将的返回值 `front` 分配给 `const_reference` ，则无法修改矢量对象。 如果将的返回值 `front` 分配给 **`reference`** ，则可以修改矢量对象。

当使用 [`_ITERATOR_DEBUG_LEVEL`](../standard-library/iterator-debug-level.md) 定义为1或2的进行编译时，如果尝试访问空向量中的元素，将发生运行时错误。 有关详细信息，请参阅 [检查迭代](../standard-library/checked-iterators.md)器。

### <a name="example"></a>示例

```cpp
// vector_front.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;

   v1.push_back( 10 );
   v1.push_back( 11 );

   int& i = v1.front( );
   const int& ii = v1.front( );

   cout << "The first integer of v1 is "<< i << endl;
   // by incrementing i, we move the front reference to the second element
   i++;
   cout << "Now, the first integer of v1 is "<< i << endl;
}
```

## <a name="get_allocator"></a><a name="get_allocator"></a> `get_allocator`

返回用于构造矢量的分配器对象的一个副本。

```cpp
Allocator get_allocator() const;
```

### <a name="return-value"></a>返回值

向量所使用的分配器。

### <a name="remarks"></a>注解

矢量类的分配器指定类管理存储的方式。 C++ 标准库容器类提供的默认分配器足以满足大多编程需求。 编写和使用你自己的分配器类是高级 c + + 功能。

### <a name="example"></a>示例

```cpp
// vector_get_allocator.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   // The following lines declare objects that use the default allocator.
   vector<int> v1;
   vector<int, allocator<int> > v2 = vector<int, allocator<int> >(allocator<int>( )) ;

   // v3 will use the same allocator class as v1
   vector <int> v3( v1.get_allocator( ) );

   vector<int>::allocator_type xvec = v3.get_allocator( );
   // You can now call functions on the allocator class used by vec
}
```

## <a name="insert"></a><a name="insert"></a> `insert`

将一个元素或多个元素或一系列元素插入到指定位置的向量中。

```cpp
iterator insert(
    const_iterator position,
    const Type& value);

iterator insert(
    const_iterator position,
    Type&& value);

void insert(
    const_iterator position,
    size_type count,
    const Type& value);

template <class InputIterator>
void insert(
    const_iterator position,
    InputIterator first,
    InputIterator last);
```

### <a name="parameters"></a>参数

*`position`*\
向量中插入第一个元素的位置。

*`value`*\
插入到向量中的元素的值。

*`count`*\
插入向量中的元素数目。

*`first`*\
要复制的范围元素中的第一个元素的位置。

*`last`*\
要复制的元素范围以外的第一个元素的位置。

### <a name="return-value"></a>返回值

前两个 `insert` 函数返回一个指定新元素插入到向量的位置的迭代器。

### <a name="remarks"></a>注解

作为前置条件， *`first`* *`last`* 不能将迭代器放入矢量，或者行为未定义。 任何插入操作都可能会消耗大量资源，请参阅[ `vector` 类](../standard-library/vector-class.md)以了解性能的讨论 `vector` 。

### <a name="example"></a>示例

```cpp
// vector_insert.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::iterator Iter;

   v1.push_back( 10 );
   v1.push_back( 20 );
   v1.push_back( 30 );

   cout << "v1 =" ;
   for ( Iter = v1.begin( ) ; Iter != v1.end( ) ; Iter++ )
      cout << " " << *Iter;
   cout << endl;

   v1.insert( v1.begin( ) + 1, 40 );
   cout << "v1 =";
   for ( Iter = v1.begin( ) ; Iter != v1.end( ) ; Iter++ )
      cout << " " << *Iter;
   cout << endl;
   v1.insert( v1.begin( ) + 2, 4, 50 );

   cout << "v1 =";
   for ( Iter = v1.begin( ) ; Iter != v1.end( ) ; Iter++ )
      cout << " " << *Iter;
   cout << endl;

   const auto v2 = v1;
   v1.insert( v1.begin( )+1, v2.begin( )+2, v2.begin( )+4 );
   cout << "v1 =";
   for (Iter = v1.begin( ); Iter != v1.end( ); Iter++ )
      cout << " " << *Iter;
   cout << endl;

// initialize a vector of vectors by moving v1
   vector < vector <int> > vv1;

   vv1.insert( vv1.begin(), move( v1 ) );
   if ( vv1.size( ) != 0 && vv1[0].size( ) != 0 )
      {
      cout << "vv1[0] =";
      for (Iter = vv1[0].begin( ); Iter != vv1[0].end( ); Iter++ )
         cout << " " << *Iter;
      cout << endl;
      }
}
```

```Output
v1 = 10 20 30
v1 = 10 40 20 30
v1 = 10 40 50 50 50 50 20 30
v1 = 10 50 50 40 50 50 50 50 20 30
vv1[0] = 10 50 50 40 50 50 50 50 20 30
```

## <a name="iterator"></a><a name="iterator"></a> `iterator`

一个类型，它提供可读取或修改向量中任何元素的随机访问迭代器。

```cpp
typedef implementation-defined iterator;
```

### <a name="remarks"></a>注解

类型 **`iterator`** 可用于修改元素的值。

### <a name="example"></a>示例

请参阅的示例 [`begin`](#begin) 。

## <a name="max_size"></a><a name="max_size"></a> `max_size`

返回向量的最大长度。

```cpp
size_type max_size() const;
```

### <a name="return-value"></a>返回值

向量的最大可取长度。

### <a name="example"></a>示例

```cpp
// vector_max_size.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::size_type i;

   i = v1.max_size( );
   cout << "The maximum possible length of the vector is " << i << "." << endl;
}
```

## <a name="operator"></a><a name="op_at"></a> `operator[]`

返回对指定位置的矢量元素的引用。

```cpp
reference operator[](size_type position);

const_reference operator[](size_type position) const;
```

### <a name="parameters"></a>参数

*`position`*\
矢量元素的位置。

### <a name="return-value"></a>返回值

如果指定的位置大于或等于容器大小，则结果为 undefined。

### <a name="remarks"></a>注解

如果将的返回值 `operator[]` 分配给 `const_reference` ，则无法修改矢量对象。 如果将 `operator[]` 的返回值分配给引用，则可以修改矢量对象。

当使用 [`_ITERATOR_DEBUG_LEVEL`](../standard-library/iterator-debug-level.md) 定义为1或2的进行编译时，如果尝试访问向量边界之外的元素，将发生运行时错误。 有关详细信息，请参阅 [检查迭代](../standard-library/checked-iterators.md)器。

### <a name="example"></a>示例

```cpp
// vector_op_ref.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;

   v1.push_back( 10 );
   v1.push_back( 20 );

   int& i = v1[1];
   cout << "The second integer of v1 is " << i << endl;
}
```

## <a name="operator"></a><a name="op_eq"></a> `operator=`

用另一个向量的副本替换该向量中的元素。

```cpp
vector& operator=(const vector& right);

vector& operator=(vector&& right);
```

### <a name="parameters"></a>参数

*`right`*\
[`vector`](../standard-library/vector-class.md)要复制到中的 `vector` 。

### <a name="remarks"></a>注解

清除中的任何现有元素后 `vector` ，会 `operator=` 将的内容复制或移动 *`right`* 到 `vector` 。

### <a name="example"></a>示例

```cpp
// vector_operator_as.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector<int> v1, v2, v3;
   vector<int>::iterator iter;

   v1.push_back(10);
   v1.push_back(20);
   v1.push_back(30);
   v1.push_back(40);
   v1.push_back(50);

   cout << "v1 = " ;
   for (iter = v1.begin(); iter != v1.end(); iter++)
      cout << *iter << " ";
   cout << endl;

   v2 = v1;
   cout << "v2 = ";
   for (iter = v2.begin(); iter != v2.end(); iter++)
      cout << *iter << " ";
   cout << endl;

// move v1 into v2
   v2.clear();
   v2 = move(v1);
   cout << "v2 = ";
   for (iter = v2.begin(); iter != v2.end(); iter++)
      cout << *iter << " ";
   cout << endl;
}
```

## <a name="pointer"></a><a name="pointer"></a> `pointer`

一个类型，提供指向向量中元素的指针。

```cpp
typedef typename Allocator::pointer pointer;
```

### <a name="remarks"></a>注解

类型 **`pointer`** 可用于修改元素的值。

### <a name="example"></a>示例

```cpp
// vector_pointer.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
    using namespace std;
    vector<int> v;
    v.push_back( 11 );
    v.push_back( 22 );

    vector<int>::pointer ptr = &v[0];
    cout << *ptr << endl;
    ptr++;
    cout << *ptr << endl;
    *ptr = 44;
    cout << *ptr << endl;
}
```

```Output
11
22
44
```

## <a name="pop_back"></a><a name="pop_back"></a> `pop_back`

删除矢量末尾处的元素。

```cpp
void pop_back();
```

### <a name="remarks"></a>注解

有关代码示例，请参阅 [vector::push_back()](#push_back)。

## <a name="push_back"></a><a name="push_back"></a> `push_back`

在矢量末尾处添加一个元素。

```cpp
void push_back(const T& value);

void push_back(T&& value);
```

### <a name="parameters"></a>参数

*`value`*\
要赋给添加到矢量末尾处的元素的值。

### <a name="example"></a>示例

```cpp
// compile with: /EHsc /W4
#include <vector>
#include <iostream>

using namespace std;

template <typename T> void print_elem(const T& t) {
    cout << "(" << t << ") ";
}

template <typename T> void print_collection(const T& t) {
    cout << "  " << t.size() << " elements: ";

    for (const auto& p : t) {
        print_elem(p);
    }
    cout << endl;
}

int main()
{
    vector<int> v;
    for (int i = 0; i < 10; ++i) {
        v.push_back(10 + i);
    }

    cout << "vector data: " << endl;
    print_collection(v);

    // pop_back() until it's empty, printing the last element as we go
    while (v.begin() != v.end()) {
        cout << "v.back(): "; print_elem(v.back()); cout << endl;
        v.pop_back();
    }
}
```

## <a name="rbegin"></a><a name="rbegin"></a> `rbegin`

返回指向反向向量中第一个元素的迭代器。

```cpp
reverse_iterator rbegin();
const_reverse_iterator rbegin() const;
```

### <a name="return-value"></a>返回值

发现反向矢量中的第一个元素或发现曾是非反向矢量中的最后一个元素的反向双向迭代器。

### <a name="remarks"></a>注解

如果将的返回值 `rbegin` 分配给 `const_reverse_iterator` ，则无法修改矢量对象。 如果将 `rbegin` 的返回值分配给 `reverse_iterator`，则可以修改矢量对象。

### <a name="example"></a>示例

```cpp
// vector_rbegin.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::iterator v1_Iter;
   vector <int>::reverse_iterator v1_rIter;

   v1.push_back( 1 );
   v1.push_back( 2 );

   v1_Iter = v1.begin( );
   cout << "The first element of vector is "
        << *v1_Iter << "." << endl;

   v1_rIter = v1.rbegin( );
   cout << "The first element of the reversed vector is "
        << *v1_rIter << "." << endl;
}
```

```Output
The first element of vector is 1.
The first element of the reversed vector is 2.
```

## <a name="reference"></a><a name="reference"></a> `reference`

一个类型，它提供对向量中存储的元素的引用。

```cpp
typedef typename Allocator::reference reference;
```

### <a name="example"></a>示例

[`at`](#at)有关如何 **`reference`** 在 vector 类中使用的示例，请参阅。

## <a name="rend"></a><a name="rend"></a> `rend`

返回一个后端反向迭代器，该迭代器指向反向向量的最后一个元素之后的元素。

```cpp
const_reverse_iterator rend() const;
reverse_iterator rend();
```

### <a name="return-value"></a>返回值

反向向量的反向结束迭代器。 它指向反向向量的最后一个元素之后的元素，该元素与非反转向量的第一个元素之前的元素相同。 该元素是占位符，不应取消引用。 仅将它用于比较。

### <a name="remarks"></a>注解

`rend` 与反向矢量一起使用，就像 [`end`](#end) 与矢量一起使用一样。

如果将的返回值 `rend` 分配给 `const_reverse_iterator` ，则无法修改矢量对象。 如果将 `rend` 的返回值分配给 `reverse_iterator`，则可以修改矢量对象。

`rend` 可用于测试反向迭代器是否已到达其矢量末尾。

返回的值 `rend` 不应被取消引用。 仅将它用于比较。

### <a name="example"></a>示例

```cpp
// vector_rend.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::reverse_iterator v1_rIter;

   v1.push_back( 1 );
   v1.push_back( 2 );

   for ( v1_rIter = v1.rbegin( ) ; v1_rIter != v1.rend( ) ; v1_rIter++ )
      cout << *v1_rIter << endl;
}
```

```Output
2
1
```

## <a name="reserve"></a><a name="reserve"></a> `reserve`

为向量对象保留最小的存储长度，必要时为其分配空间。

```cpp
void reserve(size_type count);
```

### <a name="parameters"></a>参数

*`count`*\
要分配给向量的最小存储长度。

### <a name="example"></a>示例

```cpp
// vector_reserve.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   //vector <int>::iterator Iter;

   v1.push_back( 1 );
   cout << "Current capacity of v1 = "
      << v1.capacity( ) << endl;
   v1.reserve( 20 );
   cout << "Current capacity of v1 = "
      << v1.capacity( ) << endl;
}
```

```Output
Current capacity of v1 = 1
Current capacity of v1 = 20
```

## <a name="resize"></a><a name="resize"></a> `resize`

为矢量指定新的大小。

```cpp
void resize(size_type new_size);
void resize(size_type new_size, Type value);
```

### <a name="parameters"></a>参数

*`new_size`*\
矢量的新大小。

*`value`*\
新大小大于旧大小时添加至矢量的新元素的初始化值。 如果省略该值，则新对象将使用其默认构造函数。

### <a name="remarks"></a>注解

如果容器的大小小于请求的大小，则 *`new_size`* `resize` 会将元素添加到向量，直到达到请求的大小。 如果容器的大小大于请求的大小，则 `resize` 删除接近容器末尾的元素，直到达到大小 *`new_size`* 。 如果容器的当前大小与请求的大小相同，则不执行任何操作。

[`size`](#size) 反映矢量的当前大小。

### <a name="example"></a>示例

```cpp
// vectorsizing.cpp
// compile with: /EHsc /W4
// Illustrates vector::reserve, vector::max_size,
// vector::resize, vector::resize, and vector::capacity.
//
// Functions:
//
//    vector::max_size - Returns maximum number of elements vector could
//                       hold.
//
//    vector::capacity - Returns number of elements for which memory has
//                       been allocated.
//
//    vector::size - Returns number of elements in the vector.
//
//    vector::resize - Reallocates memory for vector, preserves its
//                     contents if new size is larger than existing size.
//
//    vector::reserve - Allocates elements for vector to ensure a minimum
//                      size, preserving its contents if the new size is
//                      larger than existing size.
//
//    vector::push_back - Appends (inserts) an element to the end of a
//                        vector, allocating memory for it if necessary.
//
//////////////////////////////////////////////////////////////////////

// The debugger cannot handle symbols more than 255 characters long.
// The C++ Standard Library often creates symbols longer than that.
// The warning can be disabled:
//#pragma warning(disable:4786)

#include <iostream>
#include <vector>
#include <string>

using namespace std;

template <typename C> void print(const string& s, const C& c) {
    cout << s;

    for (const auto& e : c) {
        cout << e << " ";
    }
    cout << endl;
}

void printvstats(const vector<int>& v) {
    cout << "   the vector's size is: " << v.size() << endl;
    cout << "   the vector's capacity is: " << v.capacity() << endl;
    cout << "   the vector's maximum size is: " << v.max_size() << endl;
}

int main()
{
    // declare a vector that begins with 0 elements.
    vector<int> v;

    // Show statistics about vector.
    cout << endl << "After declaring an empty vector:" << endl;
    printvstats(v);
    print("   the vector's contents: ", v);

    // Add one element to the end of the vector.
    v.push_back(-1);
    cout << endl << "After adding an element:" << endl;
    printvstats(v);
    print("   the vector's contents: ", v);

    for (int i = 1; i < 10; ++i) {
        v.push_back(i);
    }
    cout << endl << "After adding 10 elements:" << endl;
    printvstats(v);
    print("   the vector's contents: ", v);

    v.resize(6);
    cout << endl << "After resizing to 6 elements without an initialization value:" << endl;
    printvstats(v);
    print("   the vector's contents: ", v);

    v.resize(9, 999);
    cout << endl << "After resizing to 9 elements with an initialization value of 999:" << endl;
    printvstats(v);
    print("   the vector's contents: ", v);

    v.resize(12);
    cout << endl << "After resizing to 12 elements without an initialization value:" << endl;
    printvstats(v);
    print("   the vector's contents: ", v);

    // Ensure there's room for at least 1000 elements.
    v.reserve(1000);
    cout << endl << "After vector::reserve(1000):" << endl;
    printvstats(v);

    // Ensure there's room for at least 2000 elements.
    v.resize(2000);
    cout << endl << "After vector::resize(2000):" << endl;
    printvstats(v);
}
```

## <a name="reverse_iterator"></a><a name="reverse_iterator"></a> `reverse_iterator`

一个类型，它提供可读取或修改反向矢量中的任意元素的随机访问迭代器。

```cpp
typedef std::reverse_iterator<iterator> reverse_iterator;
```

### <a name="remarks"></a>注解

`reverse_iterator` 类型用于反向循环访问向量。

### <a name="example"></a>示例

请参阅的示例 [`rbegin`](#rbegin) 。

## <a name="shrink_to_fit"></a><a name="shrink_to_fit"></a> `shrink_to_fit`

放弃额外容量。

```cpp
void shrink_to_fit();
```

### <a name="example"></a>示例

```cpp
// vector_shrink_to_fit.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   //vector <int>::iterator Iter;

   v1.push_back( 1 );
   cout << "Current capacity of v1 = "
      << v1.capacity( ) << endl;
   v1.reserve( 20 );
   cout << "Current capacity of v1 = "
      << v1.capacity( ) << endl;
   v1.shrink_to_fit();
   cout << "Current capacity of v1 = "
      << v1.capacity( ) << endl;
}
```

```Output
Current capacity of v1 = 1
Current capacity of v1 = 20
Current capacity of v1 = 1
```

## <a name="size"></a><a name="size"></a> `size`

返回向量中的元素数量。

```cpp
size_type size() const;
```

### <a name="return-value"></a>返回值

向量的当前长度。

### <a name="example"></a>示例

```cpp
// vector_size.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1;
   vector <int>::size_type i;

   v1.push_back( 1 );
   i = v1.size( );
   cout << "Vector length is " << i << "." << endl;

   v1.push_back( 2 );
   i = v1.size( );
   cout << "Vector length is now " << i << "." << endl;
}
```

```Output
Vector length is 1.
Vector length is now 2.
```

## <a name="size_type"></a><a name="size_type"></a> `size_type`

一个类型，它计算矢量中的元素数目。

```cpp
typedef typename Allocator::size_type size_type;
```

### <a name="example"></a>示例

请参阅的示例 [`capacity`](#capacity) 。

## <a name="swap"></a><a name="swap"></a> `swap`

交换两个向量的元素。

```cpp
void swap(
    vector<Type, Allocator>& right);

friend void swap(
    vector<Type, Allocator>& left,
    vector<Type, Allocator>& right);
```

### <a name="parameters"></a>参数

*`right`*\
提供要交换的元素的向量。 或，其元素要与矢量中的元素进行交换的向量 *`left`* 。

*`left`*\
一个向量，其元素将与矢量中的元素进行交换 *`right`* 。

### <a name="example"></a>示例

```cpp
// vector_swap.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector <int> v1, v2;

   v1.push_back( 1 );
   v1.push_back( 2 );
   v1.push_back( 3 );

   v2.push_back( 10 );
   v2.push_back( 20 );

   cout << "The number of elements in v1 = " << v1.size( ) << endl;
   cout << "The number of elements in v2 = " << v2.size( ) << endl;
   cout << endl;

   v1.swap( v2 );

   cout << "The number of elements in v1 = " << v1.size( ) << endl;
   cout << "The number of elements in v2 = " << v2.size( ) << endl;
}
```

```Output
The number of elements in v1 = 3
The number of elements in v2 = 2

The number of elements in v1 = 2
The number of elements in v2 = 3
```

## <a name="value_type"></a><a name="value_type"></a> `value_type`

一个类型，它代表向量中存储的数据类型。

```cpp
typedef typename Allocator::value_type value_type;
```

### <a name="remarks"></a>注解

`value_type` 是模板参数 `Type` 的同义词。

### <a name="example"></a>示例

```cpp
// vector_value_type.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main( )
{
   using namespace std;
   vector<int>::value_type AnInt;
   AnInt = 44;
   cout << AnInt << endl;
}
```

```Output
44
```

## <a name="vector"></a><a name="vector"></a> `vector`

构造向量。 重载构造特定大小的向量，或具有特定值的元素。 或作为某些其他矢量的全部或部分的副本。 某些重载还允许您指定要使用的分配器。

```cpp
vector();
explicit vector(const Allocator& allocator);
explicit vector(size_type count);
vector(size_type count, const Type& value);
vector(size_type count, const Type& value, const Allocator& allocator);

vector(const vector& source);
vector(vector&& source);
vector(initializer_list<Type> init_list, const Allocator& allocator);

template <class InputIterator>
vector(InputIterator first, InputIterator last);
template <class InputIterator>
vector(InputIterator first, InputIterator last, const Allocator& allocator);
```

### <a name="parameters"></a>参数

*`allocator`*\
要用于此对象的分配器类。 [`get_allocator`](#get_allocator) 返回对象的分配器类。

*`count`*\
构造的矢量中的元素数。

*`value`*\
构造的矢量中的元素值。

*`source`*\
要成为副本的构造的矢量中的矢量。

*`first`*\
要复制的元素范围内的第一个元素的位置。

*`last`*\
要复制的元素范围外的第一个元素的位置。

*`init_list`*\
`initializer_list`包含要复制的元素的。

### <a name="remarks"></a>注解

所有构造函数都存储分配器对象 (*`allocator`*) 并初始化向量。

前两个构造函数指定一个空初始矢量。 第二个构造函数显式指定要使用) 的分配器类型 (*`allocator`* 。

第三个构造函数指定 (*`count`* 类的默认值元素) 元素的重复 `Type` 。

第四个和第五个构造函数指定 (*`count`*) 的值元素的重复 *`value`* 。

第六个构造函数指定矢量的副本 *`source`* 。

第七个构造函数移动矢量 *`source`* 。

第八个构造函数使用 initializer_list 指定元素。

第九个和第十个构造函数复制矢量的范围（`first`、`last`）。

### <a name="example"></a>示例

```cpp
// vector_ctor.cpp
// compile with: /EHsc
#include <vector>
#include <iostream>

int main()
{
    using namespace std;
    vector <int>::iterator v1_Iter, v2_Iter, v3_Iter, v4_Iter, v5_Iter, v6_Iter;

    // Create an empty vector v0
    vector <int> v0;

    // Create a vector v1 with 3 elements of default value 0
    vector <int> v1(3);

    // Create a vector v2 with 5 elements of value 2
    vector <int> v2(5, 2);

    // Create a vector v3 with 3 elements of value 1 and with the allocator
    // of vector v2
    vector <int> v3(3, 1, v2.get_allocator());

    // Create a copy, vector v4, of vector v2
    vector <int> v4(v2);

    // Create a new temporary vector for demonstrating copying ranges
    vector <int> v5(5);
    for (auto i : v5) {
        v5[i] = i;
    }

    // Create a vector v6 by copying the range v5[ first,  last)
    vector <int> v6(v5.begin() + 1, v5.begin() + 3);

    cout << "v1 =";
    for (auto& v : v1){
        cout << " " << v;
    }
    cout << endl;

    cout << "v2 =";
    for (auto& v : v2){
        cout << " " << v;
    }
    cout << endl;

    cout << "v3 =";
    for (auto& v : v3){
        cout << " " << v;
    }
    cout << endl;
    cout << "v4 =";
    for (auto& v : v4){
        cout << " " << v;
    }
    cout << endl;

    cout << "v5 =";
    for (auto& v : v5){
        cout << " " << v;
    }
    cout << endl;

    cout << "v6 =";
    for (auto& v : v6){
        cout << " " << v;
    }
    cout << endl;

    // Move vector v2 to vector v7
    vector <int> v7(move(v2));
    vector <int>::iterator v7_Iter;

    cout << "v7 =";
    for (auto& v : v7){
        cout << " " << v;
    }
    cout << endl;

    vector<int> v8{ { 1, 2, 3, 4 } };
    for (auto& v : v8){
        cout << " " << v ;
    }
    cout << endl;
}
```

```Output
v1 = 0 0 0v2 = 2 2 2 2 2v3 = 1 1 1v4 = 2 2 2 2 2v5 = 0 1 2 3 4v6 = 1 2v7 = 2 2 2 2 21 2 3 4
```

## <a name="see-also"></a>另请参阅

[C + + 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[C + + 标准库参考](../standard-library/cpp-standard-library-reference.md)
