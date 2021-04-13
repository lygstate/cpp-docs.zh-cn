---
description: '了解详细信息：抽象类 (c + +) '
title: C + +)  (抽象类
ms.date: 02/18/2021
helpviewer_keywords:
- classes [C++], abstract
- base classes [C++], abstract classes [C++]
- abstract classes [C++]
- derived classes [C++], abstract classes [C++]
ms.openlocfilehash: 375dd40c41a9de2b5b66a295cfccaae04d4ccbb8
ms.sourcegitcommit: 10baf2761694a7d9f478e5609f24158ed8258a44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2021
ms.locfileid: "107282617"
---
# <a name="abstract-classes-c"></a>C + +)  (抽象类

抽象类作为可从中派生更具体的类的一般概念的表达。 不能创建抽象类类型的对象。 但是，可以使用指向抽象类类型的指针和引用。

通过声明至少一个纯虚拟成员函数来创建一个抽象类。 这是使用 *纯* 说明符声明 () 语法的虚拟函数 `= 0` 。 派生自抽象类的类必须实现纯虚函数或者它们必须也是抽象类。

请考虑 [虚拟函数](../cpp/virtual-functions.md)中显示的示例。 类 `Account` 的用途是提供通用功能，但 `Account` 类型的对象太通用，因此没什么用。 这意味着 `Account` 非常适合抽象类：

```cpp
// deriv_AbstractClasses.cpp
// compile with: /LD
class Account {
public:
   Account( double d );   // Constructor.
   virtual double GetBalance();   // Obtain balance.
   virtual void PrintBalance() = 0;   // Pure virtual function.
private:
    double _balance;
};
```

此声明与上一个声明的唯一区别是，`PrintBalance` 是用 pure 说明符 (`= 0`) 声明的。

## <a name="restrictions-on-abstract-classes"></a>抽象类限制

抽象类不能用于：

- 变量或成员数据

- 自变量类型

- 函数返回类型

- 显式转换的类型

如果抽象类的构造函数直接或间接地调用纯虚函数，则结果是不确定的。 但是，抽象类的构造函数和析构函数都可以调用其他成员函数。

## <a name="defined-pure-virtual-functions"></a>定义的纯虚函数

可以 *定义* 抽象类中的纯虚函数，或具有实现。 只能使用完全限定的语法来调用此类函数：

*抽象类名称*：：*函数名* () 

在设计其基类包含纯虚析构函数的类层次结构时，定义的纯虚函数很有用。 这是因为，在对象销毁期间始终调用基类析构函数。 请看下面的示例：

```cpp
// deriv_RestrictionsOnUsingAbstractClasses.cpp
// Declare an abstract base class with a pure virtual destructor.
// It's the simplest possible abstract class.
class base
{
public:
    base() {}
    // To define the virtual destructor outside the class:
    virtual ~base() = 0;
    // Microsoft-specific extension to define it inline:
//  virtual ~base() = 0 {};
};

base::~base() {} // required if not using Microsoft extension

class derived : public base
{
public:
    derived() {}
    ~derived() {}
};

int main()
{
    derived aDerived; // destructor called when it goes out of scope
}
```

该示例演示如何通过 Microsoft 编译器扩展将内联定义添加到纯虚拟 `~base()` 。 你还可以通过使用在类的外部定义它 `base::~base() {}` 。

当对象 `aDerived` 超出范围时，将调用类的析构函数 `derived` 。 编译器生成代码以在 `base` 析构函数后隐式调用类的析构函数 `derived` 。 纯虚函数的空实现 `~base` 确保至少存在一个函数的实现。 如果没有此方法，链接器将为隐式调用生成一个无法解析的外部符号错误。

> [!NOTE]
> 在前面的示例中，纯虚函数 `base::~base` 是从 `derived::~derived` 隐式调用的。 还可以使用完全限定的成员函数名称显式调用纯虚函数。 此类函数必须有一个实现，否则调用会导致在链接时出现错误。

## <a name="see-also"></a>另请参阅

[继承](../cpp/inheritance-cpp.md)
