---
description: 详细了解： c + + 标准库中的函数对象
title: C++ 标准库中的函数对象
ms.date: 03/15/2019
helpviewer_keywords:
- functors
- C++ Standard Library, functors
- C++ Standard Library, function objects
- function objects
ms.assetid: 85f8a735-2c7b-4f10-9c4d-95c666ec4192
ms.openlocfilehash: 2c8e5995beabb63ff3b53c52874bb5b7c5f2a61e
ms.sourcegitcommit: a89eac9acdbd54a181e3bd5d5bc71a3ef3c1abca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "106506021"
---
# <a name="function-objects-in-the-c-standard-library"></a>C++ 标准库中的函数对象

*函数对象*（也称 *函子*）是实现 operator() 的任何类型。 此运算符被称为 *调用运算符* （有时称为 *应用程序运算符*）。 C++ 标准库主要使用函数对象作为容器和算法内的排序条件。

相对于直接函数调用，函数对象有两个优势。 第一个是函数对象可包含状态。 第二个是函数对象是一个类型，因此可用作模板参数。

## <a name="creating-a-function-object"></a>创建函数对象

若要创建函数对象，请创建一个类型并实现 operator()，例如：

```cpp
class Functor
{
public:
    int operator()(int a, int b)
    {
        return a < b;
    }
};

int main()
{
    Functor f;
    int a = 5;
    int b = 7;
    int ans = f(a, b);
}
```

`main` 函数的最后一行显示了函数对象的调用方式。 此调用看起来像是对函数的调用，但实际上它调用的是函子类型的 operator () 。 调用函数对象和函数之间的相似性在于生成术语函数对象的方式。

## <a name="function-objects-and-containers"></a>函数对象和容器

C + + 标准库在标头文件中包含若干函数对象 [`<functional>`](../standard-library/functional.md) 。 这些函数对象的一个用途是用作容器的排序条件。 例如， `set` 容器声明如下：

```cpp
template <class Key,
    class Traits=less<Key>,
    class Allocator=allocator<Key>>
class set
```

第二个模板函数是函数对象 `less`。 **`true`** 如果第一个参数小于第二个参数，则此函数对象返回。 因为某些容器对其元素进行排序，所以容器需要一种方法来比较两个元素。 使用函数对象进行比较。 你可以创建函数对象并在容器的模板列表中指定它，从而定义你自己的排序条件。

## <a name="function-objects-and-algorithms"></a>函数对象和算法

函数对象的另一个用法是在算法中。 例如， `remove_if` 算法声明如下：

```cpp
template <class ForwardIterator, class Predicate>
ForwardIterator remove_if(
    ForwardIterator first,
    ForwardIterator last,
    Predicate pred);
```

`remove_if` 的最后一个参数是返回布尔值（一个 *谓词*）的函数对象。 如果函数对象的结果是 **`true`** ，则将从迭代器和正在访问的容器中删除元素 `first` `last` 。 您可以使用在该参数的标头中声明的任何函数对象， [`<functional>`](../standard-library/functional.md) 也可以创建自己的函数对象 `pred` 。

## <a name="see-also"></a>另请参阅

[C + + 标准库参考](../standard-library/cpp-standard-library-reference.md)
