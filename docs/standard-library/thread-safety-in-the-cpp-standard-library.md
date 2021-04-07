---
description: 详细了解： c + + 标准库中的线程安全
title: C++ 标准库中的线程安全
ms.date: 11/04/2016
helpviewer_keywords:
- thread safety
- C++ Standard Library, thread safety
- thread safety, C++ Standard Library
ms.assetid: 9351c8fb-4539-4728-b0e9-226e2ac4284b
ms.openlocfilehash: 21b4575a217182ef90f8ee506064aab868b9cda9
ms.sourcegitcommit: a89eac9acdbd54a181e3bd5d5bc71a3ef3c1abca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "106506073"
---
# <a name="thread-safety-in-the-c-standard-library"></a>C++ 标准库中的线程安全

以下线程安全规则应用到标准 C++ 库中的所有类，这也包括 `shared_ptr`，如下所述。  有时提供更强的保证（例如，如下所述的标准 iostream 对象）和用于多线程的类型，如中所述 [`<atomic>`](../standard-library/atomic.md) 。

从多个线程读取某个对象时，该对象是线程安全的。 例如，给定对象 A，可安全地同时从线程 1 和线程 2 读取 A。

如果要通过某个线程写入到对象，则必须保护相同线程或其他线程上所有对该对象的读取和写入。 例如，给定对象 A，如果线程 1 将写入到 A，则必须阻止线程 2 读取或写入 A。

即使另一个线程正在读取或写入同一类型的不同实例，也可以安全地读取和写入某个类型的实例。 例如，如果给定的对象 A 和 B 属于同一类型，则在线程1中写入时是安全的，并且在线程2中读取 B。

## <a name="shared_ptr"></a>shared_ptr

[`shared_ptr`](../standard-library/shared-ptr-class.md)即使对象是共享所有权的副本，多个线程也可以同时读取和写入不同的对象。

## <a name="iostream"></a>iostream

标准 iostream 对象 `cin` 、 `cout` 、、、、、 `cerr` `clog` `wcin` `wcout` `wcerr` 和遵循与 `wclog` 其他类相同的规则，但这种情况例外：可以安全地从多个线程写入一个对象。 例如，线程1可以与 [`cout`](../standard-library/iostream.md#cout) 线程2同时写入。 但是，此操作可能会导致两个线程的输出相混合。

> [!NOTE]
> 不会将读取流缓冲区视为读取操作。 由于类的状态发生了更改，因此它被认为是写入操作。

## <a name="see-also"></a>另请参阅

[C + + 标准库概述](../standard-library/cpp-standard-library-overview.md)
