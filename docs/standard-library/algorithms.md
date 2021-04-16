---
description: 了解有关以下方面的详细信息：算法
title: 算法
ms.date: 10/18/2018
helpviewer_keywords:
- libraries [C++], C++ algorithm conventions
- algorithms [C++], C++
- C++ Standard Library, algorithms
- algorithm template function C++ library conventions
- conventions [C++], C++ algorithm
ms.assetid: dec9b373-7d5c-46cc-b7d2-21a938ecd0a6
ms.openlocfilehash: b5c053a4ac554685eb4f282db69cc48e99e2212e
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539781"
---
# <a name="algorithms"></a>算法

算法是 C++ 标准库的基础部分。 算法不与容器本身一起使用，而与迭代器一起使用。 因此，大多数（如果不是全部）C++ 标准库容器都可以使用相同的算法。 本部分讨论 C++ 标准库算法的约定和术语。

## <a name="remarks"></a>注解

算法模板函数的说明使用几个速记短语：

- 短语 "in \[ *A*， *B*) " 表示零个或多个离散值的序列 *，从* 向上到，但不包括 *B* 开始。仅当可以从 *a* 中访问 *B* 时，范围有效; 你可以在对象 *n* (*n* a) *中存储*  =   ，将对象递增零次或多次 (+ +*N*) ，并使对象比较等于 *b* ，并 (*N*  ==  *B*) 。

- 短语 " \[ *a*， *B*) " 中的每个 n 表示 *N* 以值 *a* 开头，并递增零次或多次，直至等于值 *B*。*大小写*  ==  不在范围内。

- 短语 "a，b) 中 *n* 的最小 \[ 值， 例如 *x*" 表示为 a、b) 范围中的每个 *n* 确定条件 *x* \[ ，直到满足条件 *x* 。

- 短语 "a，b) 中 *N* 的最高 \[ 值，  *x* 表示为  \[ *a*、 *b*) 范围中的每个 n 确定 x。 每次满足条件 *X* 时，函数都存储 *N* *的一个副本*。 如果发生此类存储，则函数会将 *N* 的最后一个值（等于 *B*）替换为 *K* 的值。但对于双向或随机访问迭代器，它还可以表示 *N* 以范围中的最高值开始，并在范围内递减，直到满足条件 *X* 。

- 表达式（如 *x*  -  *Y*，其中 *x* 和 *Y* 可以是随机访问迭代器以外的迭代器）的数学意义。 **-** 如果该函数必须确定此类值，则它不一定计算运算符。 对于 *X*  +  *n* 和 *x* n 等表达式也是如此  -  ，其中 *N* 是整数类型。

多种算法使用执行成对比较的谓词（例如 with `operator==` ）来生成 **`bool`** 结果。 谓词函数 `operator==` 或其任何替代函数不得更改其任一操作数。 它必须在 **`bool`** 每次计算时都生成相同的结果，并且如果为操作数替换任一操作数的副本，则必须生成相同的结果。

几种算法使用对序列中的元素对执行严格弱排序的谓词。 对于谓词 *pred* (*X*， *Y*) ：

- Strict 表示 *pred* (*x*， *x*) 为 false。

- 弱表示 *x* 和 *y* 具有等效的顺序（如果 \! *pred* (*X*、 *y*)  && \! *pred* (*y*、 *x*)  (*x*  ==  *y* 不需要定义) 。

- 排序意味着 *pred* (*x*， *y*)  && *pred* (*Y*， *z*) 表示 *pred* (*X*， *z*) 。

其中一些算法隐式使用谓词 *x* \< *Y*. Other predicates that typically satisfy the strict weak ordering requirement are *X* > *Y*、 `less` (*x*、 *y*) 和 `greater` (*X*， *y*) 。 但请注意， *X* \<= *Y* and *X* > =  *Y* 等谓词不满足此要求。

范围内的迭代器指定的一系列元素 \[ *`First`* ， *`Last`*) 是按运算符排序的序列 **`<`** 。如果为范围0中的每个 *n* ，为范围0中的每个 n、 \[ *`Last`*  -  *`First`*) 和 (*N* 范围内的每个 *M* ，) 谓词 ( () < (*`Last`*  -  *`First`* \! \* *`First`*  +   \*) ) *`First`*  +  *N* 为 true。  (请注意，元素按升序排序。 ) 谓词函数 `operator<` 或它的任何替换项，不得更改其任一操作数。 它必须在 **`bool`** 每次计算时都生成相同的结果，并且如果为操作数替换任一操作数的副本，则必须生成相同的结果。 此外，必须对它比较的操作数进行严格弱排序。

范围内的迭代器指定的一系列元素 \[ `First` ， `Last`) 是一种排序的堆， `operator<` 如果为1，则对于范围1中的每个 *N* \[ *`Last`*  -  *`First`*) 谓词 \! (\* _第一个_  <  \* (*`First`*  +  *N*) ) 为 true。  (第一个元素是最大的。 ) 其内部结构仅对模板函数 [`make_heap`](algorithm-functions.md#make_heap) 、和是已知 [`pop_heap`](algorithm-functions.md#pop_heap) [`push_heap`](algorithm-functions.md#push_heap) 的。 对于有序序列，谓词函数 `operator<` 或它的任何替换都不得更改其任一操作数，并且它必须对它所比较的操作数施加严格的弱排序。 它必须在 **`bool`** 每次计算时都生成相同的结果，并且如果为操作数替换任一操作数的副本，则必须生成相同的结果。

C + + 标准库算法位于 [`<algorithm>`](algorithm.md) 和 [`<numeric>`](numeric.md) 标头文件中。

## <a name="see-also"></a>另请参阅

[C + + 标准库参考](cpp-standard-library-reference.md)\
[C + + 标准库中的线程安全](thread-safety-in-the-cpp-standard-library.md)
