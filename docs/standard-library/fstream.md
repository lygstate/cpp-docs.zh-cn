---
description: 了解详细信息： &lt; m&gt;
title: '&lt;fstream&gt;'
ms.date: 11/04/2016
f1_keywords:
- <fstream>
helpviewer_keywords:
- fstream header
ms.assetid: 660de351-0489-41df-b239-40e0cdcab46b
ms.openlocfilehash: ad6bb7bc319ba25e174f9c65e09f7f35db667167
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539708"
---
# `<fstream>`

定义若干类，这些类支持在存储于外部文件中的序列上的 iostreams 操作。

## <a name="syntax"></a>语法

```cpp
#include <fstream>
```

### <a name="typedefs"></a>Typedef

|类型名称|描述|
|-|-|
|[`filebuf`](../standard-library/fstream-typedefs.md#filebuf)|`basic_filebuf`专用于 **`char`** 模板参数的类型。|
|[`fstream`](../standard-library/fstream-typedefs.md#fstream)|`basic_fstream`专用于 **`char`** 模板参数的类型。|
|[`ifstream`](../standard-library/fstream-typedefs.md#ifstream)|`basic_ifstream`专用于 **`char`** 模板参数的类型。|
|[`ofstream`](../standard-library/fstream-typedefs.md#ofstream)|`basic_ofstream`专用于 **`char`** 模板参数的类型。|
|[`wfstream`](../standard-library/fstream-typedefs.md#wfstream)|`basic_fstream`专用于 **`wchar_t`** 模板参数的类型。|
|[`wifstream`](../standard-library/fstream-typedefs.md#wifstream)|`basic_ifstream`专用于 **`wchar_t`** 模板参数的类型。|
|[`wofstream`](../standard-library/fstream-typedefs.md#wofstream)|`basic_ofstream`专用于 **`wchar_t`** 模板参数的类型。|
|[`wfilebuf`](../standard-library/fstream-typedefs.md#wfilebuf)|`basic_filebuf`专用于 **`wchar_t`** 模板参数的类型。|

### <a name="classes"></a>类

|类|说明|
|-|-|
|[`basic_filebuf`](../standard-library/basic-filebuf-class.md)|类模板描述了一个流缓冲区，该缓冲区控制类型的元素 `Elem` （其字符特征由类确定 `Tr` ）与外部文件中存储的元素序列之间的传输。|
|[`basic_fstream`](../standard-library/basic-fstream-class.md)|类模板描述了一个对象，该对象使用类的流缓冲区控制元素和编码对象的插入和提取，并使用 [`basic_filebuf`](../standard-library/basic-filebuf-class.md) \<**Elem**, **Tr**> 类型的元素 `Elem` ，其字符特征由类确定 `Tr` 。|
|[`basic_ifstream`](../standard-library/basic-ifstream-class.md)|类模板描述了一个对象，该对象控制从类的流缓冲区中提取元素和编码对象 [`basic_filebuf`](../standard-library/basic-filebuf-class.md) \<**Elem**, **Tr**> ，其中包含类型的元素 `Elem` ，其字符特征由类确定 `Tr` 。|
|[`basic_ofstream`](../standard-library/basic-ofstream-class.md)|类模板描述了一个对象，该对象可控制将元素和编码对象插入到类的流缓冲区中 [`basic_filebuf`](../standard-library/basic-filebuf-class.md) \<**Elem**, **Tr**> ，其元素类型为 `Elem` ，其字符特征由类确定 `Tr` 。|

## <a name="see-also"></a>另请参阅

[标头文件引用](../standard-library/cpp-standard-library-header-files.md)\
[C + + 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)\
[iostream 编程](../standard-library/iostream-programming.md)\
[iostreams 约定](../standard-library/iostreams-conventions.md)
