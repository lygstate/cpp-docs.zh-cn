---
description: 了解详细信息： unique_ptr 类
title: unique_ptr 类
ms.date: 11/04/2016
f1_keywords:
- memory/std::unique_ptr
- memory/std::unique_ptr::deleter_type
- memory/std::unique_ptr::element_type
- memory/std::unique_ptr::pointer
- memory/std::unique_ptr::get
- memory/std::unique_ptr::get_deleter
- memory/std::unique_ptr::release
- memory/std::unique_ptr::reset
- memory/std::unique_ptr::swap
helpviewer_keywords:
- std::unique_ptr [C++]
- std::unique_ptr [C++], deleter_type
- std::unique_ptr [C++], element_type
- std::unique_ptr [C++], pointer
- std::unique_ptr [C++], get
- std::unique_ptr [C++], get_deleter
- std::unique_ptr [C++], release
- std::unique_ptr [C++], reset
- std::unique_ptr [C++], swap
ms.assetid: acdf046b-831e-4a4a-83aa-6d4ee467db9a
ms.openlocfilehash: fe47240e43781e95af5b4a802c2d387f3bd183b8
ms.sourcegitcommit: a89eac9acdbd54a181e3bd5d5bc71a3ef3c1abca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "106506060"
---
# <a name="unique_ptr-class"></a>`unique_ptr` 类

存储指向拥有的对象或数组的指针。 此对象/数组仅由 `unique_ptr` 拥有。 `unique_ptr` 被销毁后，此对象/数组也将被销毁。

## <a name="syntax"></a>语法

```cpp
class unique_ptr {
public:
    unique_ptr();
    unique_ptr(nullptr_t Nptr);
    explicit unique_ptr(pointer Ptr);
    unique_ptr(pointer Ptr,
        typename conditional<is_reference<Del>::value, Del,
        typename add_reference<const Del>::type>::type Deleter);
    unique_ptr(pointer Ptr,
        typename remove_reference<Del>::type&& Deleter);
    unique_ptr(unique_ptr&& Right);
    template <class T2, Class Del2>
    unique_ptr(unique_ptr<T2, Del2>&& Right);
    unique_ptr(const unique_ptr& Right) = delete;
    unique_ptr& operator=(const unique_ptr& Right) = delete;
};

//Specialization for arrays:
template <class T, class D>
class unique_ptr<T[], D> {
public:
    typedef pointer;
    typedef T element_type;
    typedef D deleter_type;
    constexpr unique_ptr() noexcept;
    template <class U>
    explicit unique_ptr(U p) noexcept;
    template <class U>
    unique_ptr(U p, see below d) noexcept;
    template <class U>
    unique_ptr(U p, see below d) noexcept;
    unique_ptr(unique_ptr&& u) noexcept;
    constexpr unique_ptr(nullptr_t) noexcept : unique_ptr() { }     template <class U, class E>
        unique_ptr(unique_ptr<U, E>&& u) noexcept;
    ~unique_ptr();
    unique_ptr& operator=(unique_ptr&& u) noexcept;
    template <class U, class E>
    unique_ptr& operator=(unique_ptr<U, E>&& u) noexcept;
    unique_ptr& operator=(nullptr_t) noexcept;
    T& operator[](size_t i) const;

    pointer get() const noexcept;
    deleter_type& get_deleter() noexcept;
    const deleter_type& get_deleter() const noexcept;
    explicit operator bool() const noexcept;
    pointer release() noexcept;
    void reset(pointer p = pointer()) noexcept;
    void reset(nullptr_t = nullptr) noexcept;
    template <class U>
    void reset(U p) noexcept = delete;
    void swap(unique_ptr& u) noexcept;  // disable copy from lvalue unique_ptr(const unique_ptr&) = delete;
    unique_ptr& operator=(const unique_ptr&) = delete;
};
```

### <a name="parameters"></a>参数

*`Right`*\
`unique_ptr`。

*`Nptr`*\
类型为 `rvalue` 的 `std::nullptr_t`。

*`Ptr`*\
`pointer`。

*`Deleter`*\
绑定到 `deleter` 的 `unique_ptr` 函数。

## <a name="exceptions"></a>例外

`unique_ptr` 不生成异常。

## <a name="remarks"></a>备注

`unique_ptr` 类取代 `auto_ptr`，并可用作 C++ 标准库容器的元素。

使用 [`make_unique`](../standard-library/memory-functions.md#make_unique) helper 函数可高效创建的新实例 `unique_ptr` 。

`unique_ptr` 唯一管理资源。 每个 `unique_ptr` 对象均存储一个指向其拥有的对象的指针，或存储一个 null 指针。 资源只能由一个 `unique_ptr` 对象拥有；当拥有特定资源的 `unique_ptr` 对象被销毁后，资源将释放。 `unique_ptr`对象可以移动，但不能复制; 有关详细信息，请参阅[右值引用 `&&` 声明符： ](../cpp/rvalue-reference-declarator-amp-amp.md)。

资源通过调用 `deleter` 类型的已存储 `Del` 对象来释放，此对象知道如何为特定 `unique_ptr` 分配资源。 默认情况下， `deleter` `default_delete<T>` 假定指向的资源通过 `ptr` 分配 **`new`** ，并且可以通过调用来释放它 `delete _Ptr` 。  (部分专用化 `unique_ptr<T[]>` 管理通过分配的数组对象 `new[]` ，并具有 `deleter` `default_delete<T[]>` 专用于调用的默认值 `delete[] ptr` 。 ) 

指向拥有的资源的存储指针 `stored_ptr` 具有类型 `pointer`。 如果已定义，此为 `Del::pointer`，如果未定义，则为 `T *`。 如果 `deleter` 无状态，则存储的 `stored_deleter` 对象 `deleter` 不占用任何空间。 请注意，`Del` 可以为引用类型。

## <a name="members"></a>成员

### <a name="constructors"></a>构造函数

|名称|说明|
|-|-|
|[`unique_ptr`](#unique_ptr)|`unique_ptr` 有七个构造函数。|

### <a name="typedefs"></a>Typedef

|名称|说明|
|-|-|
|[`deleter_type`](#deleter_type)|模板参数 `Del` 的同义词。|
|[`element_type`](#element_type)|模板参数 `T` 的同义词。|
|[`pointer`](#pointer)|如果已定义，为 `Del::pointer` 的同义词，否则为 `T *` 的同义词。|

### <a name="functions"></a>函数

|名称|说明|
|-|-|
|[`get`](#get)|返回 `stored_ptr`。|
|[`get_deleter`](#get_deleter)|返回对 `stored_deleter` 的引用。|
|[`release`](#release)|将 `pointer()` 存储在 `stored_ptr` 中并返回其先前内容。|
|[`reset`](#reset)|释放当前拥有的资源并接受新资源。|
|[`swap`](#swap)|使用提供的 `deleter` 交换资源和 `unique_ptr`。|

### <a name="operators"></a>运算符

|名称|说明|
|-|-|
|**`operator bool`**|运算符返回可转换为的类型的值 **`bool`** 。 如果转换为，则为 **`bool`** ; **`true`** `get() != pointer()` 否则为 **`false`** 。|
|`operator->`|成员函数返回 `stored_ptr`。|
|`operator*`|成员函数返回 `*stored_ptr`。|
|[`operator=`](#unique_ptr_operator_eq)|将 `unique_ptr`（或 `pointer-type`）的值分配给当前 `unique_ptr`。|

### <a name="deleter_type"></a><a name="deleter_type"></a> `deleter_type`

类型是模板参数 `Del` 的同义词。

```cpp
typedef Del deleter_type;
```

#### <a name="remarks"></a>备注

类型是模板参数 `Del` 的同义词。

### <a name="element_type"></a><a name="element_type"></a> `element_type`

类型是模板参数 `Type` 的同义词。

```cpp
typedef Type element_type;
```

#### <a name="remarks"></a>备注

类型是模板参数 `Ty` 的同义词。

### <a name="get"></a><a name="get"></a> `get`

返回 `stored_ptr`。

```cpp
pointer get() const;
```

#### <a name="remarks"></a>备注

成员函数返回 `stored_ptr`。

### <a name="get_deleter"></a><a name="get_deleter"></a> `get_deleter`

返回对 `stored_deleter` 的引用。

```cpp
Del& get_deleter();

const Del& get_deleter() const;
```

#### <a name="remarks"></a>备注

成员函数返回对 `stored_deleter` 的引用。

### <a name="operator"></a><a name="unique_ptr_operator_eq"></a> `operator=`

将提供的 `unique_ptr` 的地址分配给当前地址。

```cpp
unique_ptr& operator=(unique_ptr&& right);
template <class U, Class Del2>
unique_ptr& operator=(unique_ptr<Type, Del>&& right);
unique_ptr& operator=(pointer-type);
```

#### <a name="parameters"></a>参数

一个 `unique_ptr` 引用，用于将值 of 分配给当前 `unique_ptr`。

#### <a name="remarks"></a>备注

成员函数调用 `reset(right.release())` 并移动 `right.stored_deleter` 到 `stored_deleter` ，然后返回 **`*this`** 。

### <a name="pointer"></a><a name="pointer"></a> `pointer`

如果已定义，为 `Del::pointer` 的同义词，否则为 `Type *` 的同义词。

```cpp
typedef T1 pointer;
```

#### <a name="remarks"></a>备注

如果已定义，则此类型为 `Del::pointer` 的同义词，否则为 `Type *` 的同义词。

### <a name="release"></a><a name="release"></a> `release`

释放返回到调用方的存储指针的所有权，并将存储的指针值设置为 **`nullptr`** 。

```cpp
pointer release();
```

#### <a name="remarks"></a>备注

使用 `release`接管`unique_ptr`存储的原始指针的所有权。 调用方负责返回的指针的删除。 `unique-ptr`设置为空的默认构造状态。 在调用到`unique_ptr`后，您可以将兼容类型的另一个指针分配到`release`。

#### <a name="example"></a>示例

此示例显示发布的调用方如何负责返回的对象：

```cpp
// stl_release_unique.cpp
// Compile by using: cl /W4 /EHsc stl_release_unique.cpp
#include <iostream>
#include <memory>

struct Sample {
   int content_;
   Sample(int content) : content_(content) {
      std::cout << "Constructing Sample(" << content_ << ")" << std::endl;
   }
   ~Sample() {
      std::cout << "Deleting Sample(" << content_ << ")" << std::endl;
   }
};

void ReleaseUniquePointer() {
   // Use make_unique function when possible.
   auto up1 = std::make_unique<Sample>(3);
   auto up2 = std::make_unique<Sample>(42);

   // Take over ownership from the unique_ptr up2 by using release
   auto ptr = up2.release();
   if (up2) {
      // This statement does not execute, because up2 is empty.
      std::cout << "up2 is not empty." << std::endl;
   }
   // We are now responsible for deletion of ptr.
   delete ptr;
   // up1 deletes its stored pointer when it goes out of scope.
}

int main() {
   ReleaseUniquePointer();
}
```

```Output
Constructing Sample(3)
Constructing Sample(42)
Deleting Sample(42)
Deleting Sample(3)
```

### <a name="reset"></a><a name="reset"></a> `reset`

取得指针参数的所有权，然后删除原始存储的指针。 如果新指针与原始存储指针相同，将 `reset` 删除指针并将存储的指针设置为 **`nullptr`** 。

```cpp
void reset(pointer ptr = pointer());
void reset(nullptr_t ptr);
```

#### <a name="parameters"></a>参数

*`ptr`*\
指向要取得所有权的资源的指针。

#### <a name="remarks"></a>备注

使用将所 `reset` 拥有的存储更改 [`pointer`](#pointer) `unique_ptr` 为 *ptr* ，然后删除原始存储的指针。 如果 `unique_ptr` 不为空，则 `reset` 调用由 [`get_deleter`](#get_deleter) 原始存储指针上的返回的删除器函数。

因为 `reset` 首先将存储新指针 *`ptr`* ，然后删除原始存储的指针，如果与原始存储指针相同，则可以 `reset` 立即删除 *`ptr`* 。

### <a name="swap"></a><a name="swap"></a> `swap`

交换两个 `unique_ptr` 对象之间的指针。

```cpp
void swap(unique_ptr& right);
```

#### <a name="parameters"></a>参数

*`right`*\
用于交换指针的 `unique_ptr`。

#### <a name="remarks"></a>备注

成员函数将 `stored_ptr` 与 `right.stored_ptr`、`stored_deleter` 与 `right.stored_deleter` 进行交换。

### <a name="unique_ptr"></a><a name="unique_ptr"></a> `unique_ptr`

`unique_ptr` 有七个构造函数。

```cpp
unique_ptr();

unique_ptr(nullptr_t);
explicit unique_ptr(pointer ptr);

unique_ptr(
    Type* ptr,
    typename conditional<
    is_reference<Del>::value,
    Del,
    typename add_reference<const Del>::type>::type _Deleter);

unique_ptr(pointer ptr, typename remove_reference<Del>::type&& _Deleter);
unique_ptr(unique_ptr&& right);
template <class Ty2, Class Del2>
    unique_ptr(unique_ptr<Ty2, Del2>&& right);
```

#### <a name="parameters"></a>参数

*`ptr`*\
指向要分配给的资源的指针 `unique_ptr` 。

*`_Deleter`*\
要分配给 `unique_ptr` 的 `deleter`。

*`right`*\
`unique_ptr` 的 `rvalue reference`，其中 `unique_ptr` 字段为分配给最近构造的 `unique_ptr` 的移动。

#### <a name="remarks"></a>备注

前两个构造函数用于构造不管理任何资源的对象。 第三个构造函数在中存储 *ptr* `stored_ptr` 。 第四个构造函数 *`ptr`* 在 `stored_ptr` 和中存储 `deleter` `stored_deleter` 。

第五个构造函数存储 *`ptr`* 在中 `stored_ptr` 并移 `deleter` 入 `stored_deleter` 。 第六和第七个构造函数用于将 `right.release()` 存储到 `stored_ptr` 中和将 `right.get_deleter()` 移动到 `stored_deleter` 中。

### <a name="unique_ptr"></a><a name="dtorunique_ptr"></a> `~unique_ptr`

`unique_ptr` 的析构函数销毁 `unique_ptr` 对象。

```cpp
~unique_ptr();
```

#### <a name="remarks"></a>备注

析构函数调用 `get_deleter()(stored_ptr)`。
