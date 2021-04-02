---
description: 了解更多：编译器错误 C2276
title: 编译器错误 C2276
ms.date: 03/25/2021
f1_keywords:
- C2276
helpviewer_keywords:
- C2276
ms.openlocfilehash: 85a83637e12f0900f3a6840841c7a9a8ed50deee
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099464"
---
# <a name="compiler-error-c2276"></a>编译器错误 C2276

> "*operator*"：绑定成员函数表达式上的非法操作

编译器找到了用于创建指向成员的指针的语法问题。

## <a name="remarks"></a>注解

`C2276`当你尝试通过使用实例变量来限定成员而不是类类型来创建指向成员的指针时，通常会导致错误。 如果尝试使用错误的语法调用成员函数，也可能会看到此错误。

## <a name="example"></a>示例

此示例显示了 C2276 可能发生的几种方法，以及如何修复这些问题：

```cpp
// C2276.cpp
class A {
public:
   int func(){return 0;}
} a;

int (*pf)() = &a.func;   // C2276
// pf isn't qualified by the class type, and it 
// tries to take a member address from an instance of A.
// Try the following line instead:
// int (A::*pf)() = &A::func;

class B : public A {
public:
   void mf() {
      auto x = &this -> func;   // C2276
      // try the following line instead
      // auto x = &B::func;
   }
};

int main() {
   A a3;
   auto pmf1 = &a3.func;   // C2276
   // try the following line instead
   // auto pmf1 = &A::func;
}
```
