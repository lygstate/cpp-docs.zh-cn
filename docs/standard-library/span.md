---
title: <span>
description: 标准模板库的 API 参考 (STL) span 命名空间，该命名空间提供了一系列连续的对象。
ms.date: 05/28/2020
f1_keywords:
- <span>
helpviewer_keywords:
- span header
ms.openlocfilehash: 6f8a7e6ecbc02adeae7301dfc7eead2812c3c1f5
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381150"
---
# `<span>`

`span`是一个视图，它是一系列连续的对象。 它提供快速且不安全的访问。 与 `vector` 或不同 `array` ，它不会 "拥有" 它提供访问权限的元素。

有关详细信息，请参阅 [span 类](span-class.md) 。 下面是如何使用范围的示例：

```cpp
#include <span>
#include <iostream>

void Show(std::span<int> someValues)
{
    // show values in reverse
    for (auto rIt = someValues.rbegin(); rIt != someValues.rend(); ++rIt)
    {
        std::cout << *rIt;
    }

    // show a subspan
    for (auto& i : someValues.subspan(1, 2))
    {
        std::cout << i;
    }
}

int main()
{
    int numbers[]{ 0,1,2,3,4 };
    Show(numbers); // note conversion from array to span
}
```

## <a name="requirements"></a>要求

**标头：**\<span>

**命名空间:** std

**编译器选项：** [/std： c + + 最新](../build/reference/std-specify-language-standard-version.md)

## <a name="members"></a>成员

### <a name="classes"></a>类

|“属性”|说明|
|-|:-|
|[格](span-class.md)| 提供对一系列连续对象的视图。 |

### <a name="operators"></a>运算符

|名称|说明|
|-|:-|
|[operator =](span-class.md#op_eq)| 跨度赋值 |
|[运算符后的表达式\[\]](span-class.md#op_at)| 元素访问 |

### <a name="functions"></a>函数

|名称|说明|
|-|:-|
| [as_bytes](span-functions.md#as_bytes)| 获取跨度的基础只读字节。 |
| [as_writable_bytes](span-functions.md#as_writable_bytes) | 获取跨度的基础字节。 |

### <a name="constants"></a>常量

|名称|说明|
|-|:-|
| **dynamic_extent** | 指示范围大小在运行时确定，而不是在编译时确定。 如果范围中的元素数量在编译时是已知的，则会将其指定为 `Extent` 模板参数。 如果在运行时之前不知道该数字，请改为指定 `dynamic_extent` 。 |

## <a name="see-also"></a>请参阅

[头文件引用](../standard-library/cpp-standard-library-header-files.md)
