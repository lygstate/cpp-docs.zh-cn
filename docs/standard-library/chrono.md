---
description: 了解详细信息： &lt; chrono&gt;
title: '&lt;chrono&gt;'
ms.date: 05/07/2019
f1_keywords:
- <chrono>
- chrono/std::chrono::nanoseconds
- chrono/std::chrono::minutes
- chrono/std::chrono::seconds
- chrono/std::chrono::hours
- chrono/std::chrono::milliseconds
- chrono/std::chrono::microseconds
ms.assetid: 844de749-f306-482e-89bc-6f53c99c8324
ms.openlocfilehash: 45e59f4c09371398cc5030b78b6378ad12d6a77b
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539507"
---
# `<chrono>`

包含标准标头 `<chrono>` 以定义表示和操作持续时间和时间时刻的类和函数。

从 Visual Studio 2015 开始，的实现 `steady_clock` 已更改为符合稳定性和单一性的 c + + 标准要求。 `steady_clock` 现在基于 `QueryPerformanceCounter()` 且 `high_resolution_clock` 现在是的 typedef `steady_clock` 。 因此，在 Microsoft c + + 编译器中 `steady_clock::time_point` 现在是 `typedef` 的 `chrono::time_point<steady_clock>` ; 但是，此规则不一定是其他实现的情况。

## <a name="requirements"></a>要求

**标头：**`<chrono>`

**命名空间:** std

## <a name="members"></a>成员

### <a name="classes"></a>类

|“属性”|说明|
|-|-|
|[`duration` 班级](../standard-library/duration-class.md)|描述保持时间间隔的类型。|
|[`time_point` 班级](../standard-library/time-point-class.md)|描述表示时间点的类型。|

### <a name="structs"></a>结构

|名称|说明|
|-|-|
|[`common_type` 构造](../standard-library/common-type-structure.md)|描述和的实例化类模板的专用 [`common_type`](../standard-library/common-type-class.md) 化 `duration` `time_point` 。|
|[`duration_values` 构造](../standard-library/duration-values-structure.md)|提供 `duration` 模板参数 `Rep` 的特定值。|
|[`high_resolution_clock` 结构](../standard-library/high-resolution-clock-struct.md)||
|[`steady_clock` 结构](../standard-library/steady-clock-struct.md)|表示 `steady` 时钟。|
|[`system_clock` 构造](../standard-library/system-clock-structure.md)|表示一个 *`clock type`* ，它基于系统的实时时钟。|
|[`treat_as_floating_point` 构造](../standard-library/treat-as-floating-point-structure.md)|指定是否可将一种类型视为浮点类型。|

### <a name="functions"></a>函数

|名称|说明|
|-|-|
|[`duration_cast`](../standard-library/chrono-functions.md#duration_cast)|将 `duration` 对象转换为指定类型。|
|[`time_point_cast`](../standard-library/chrono-functions.md#time_point_cast)|将 `time_point` 对象转换为指定类型。|

### <a name="operators"></a>运算符

|名称|说明|
|-|-|
|[`operator-`](../standard-library/chrono-operators.md#operator-)|用于对 `duration` 和 `time_point` 对象进行减法或求反运算的运算符。|
|[`operator!=`](../standard-library/chrono-operators.md#op_neq)|与 `duration` 或 `time_point` 对象一起使用的不等运算符。|
|[`operator modulo`](../standard-library/chrono-operators.md#op_modulo)|用于对 `duration` 对象进行取模操作的运算符。|
|[`operator*`](../standard-library/chrono-operators.md#op_star)|`duration` 对象的乘法运算符。|
|[`operator/`](../standard-library/chrono-operators.md#op_div)|`duration` 对象的除法运算符。|
|[`operator+`](../standard-library/chrono-operators.md#op_add)|将 `duration` 和 `time_point` 对象相加。|
|[`operator<`](../standard-library/chrono-operators.md#op_lt)|确定一个 `duration` 或 `time_point` 对象是否小于另一个 `duration` 或 `time_point` 对象。|
|[`operator<=`](../standard-library/chrono-operators.md#op_lt_eq)|确定一个 `duration` 或 `time_point` 对象是否小于或等于另一个 `duration` 或 `time_point` 对象。|
|[operator = =](../standard-library/chrono-operators.md#op_eq_eq)|确定两个 `duration` 对象是否表示相同长度的时间间隔，或两个 `time_point` 对象是否表示相同的时间点。|
|[`operator>`](../standard-library/chrono-operators.md#op_gt)|确定一个 `duration` 或 `time_point` 对象是否大于另一个 `duration` 或 `time_point` 对象。|
|[`operator>=`](../standard-library/chrono-operators.md#op_gt_eq)|确定一个 `duration` 或 `time_point` 对象是否大于或等于另一个 `duration` 或 `time_point` 对象。|

### <a name="typedefs-predefined-duration-types"></a>Typedef (预定义的持续时间类型) 

有关在以下 typedef 中使用的比率类型的详细信息，请参阅 [`<ratio>`](../standard-library/ratio.md) 。

|名称|说明|
|-|-|
|`typedef duration<long long, nano> nanoseconds;`|`duration`计时周期为1纳秒的类型的同义词。|
|`typedef duration<long long, micro> microseconds;`|`duration`计时周期为1微秒的类型的同义词。|
|`typedef duration<long long, milli> milliseconds;`|`duration`计时周期为1毫秒的类型的同义词。|
|`typedef duration<long long> seconds;`|`duration`计时周期为1秒的类型的同义词。|
|`typedef duration<int, ratio<60> > minutes;`|`duration`计时周期为1分钟的类型的同义词。|
|`typedef duration<int, ratio<3600> > hours;`|`duration`计时周期为1小时的类型的同义词。|

### <a name="literals"></a>文本

**(c + + 11)**`<chrono>`标头定义了以下 [用户定义的文本](../cpp/user-defined-literals-cpp.md)，您可以使用这些文本来更方便地使用、类型安全和代码的可维护性。 这些文本在 `literals::chrono_literals` 内联命名空间中定义，当处于范围内时在范围内 `std::chrono` 。

|声明|说明|
|-|-|
|`hours operator "" h(unsigned long long Val)`|指定整数值形式的小时数。|
|`duration<double, ratio<3600> > operator "" h(long double Val)`|指定浮点值形式的小时数。|
|`minutes (operator "" min)(unsigned long long Val)`|指定整数值形式的分钟数。|
|`duration<double, ratio<60> > (operator "" min)( long double Val)`|指定浮点值形式的分钟数。|
|`seconds operator "" s(unsigned long long Val)`|指定整数值形式的分钟数。|
|`duration<double> operator "" s(long double Val)`|指定浮点值形式的描述。|
|`milliseconds operator "" ms(unsigned long long Val)`|指定整数值形式的毫秒数。|
|`duration<double, milli> operator "" ms(long double Val)`|指定浮点值形式的毫秒数。|
|`microseconds operator "" us(unsigned long long Val)`|指定整数值形式的微秒数。|
|`duration<double, micro> operator "" us(long double Val)`|指定浮点值形式的微秒数。|
|`nanoseconds operator "" ns(unsigned long long Val)`|指定整数值形式的纳秒数。|
|`duration<double, nano> operator "" ns(long double Val)`|指定浮点值形式的纳秒数。|

下面的示例演示如何使用 chrono 文本。

```cpp
constexpr auto day = 24h;
constexpr auto week = 24h* 7;
constexpr auto my_duration_unit = 108ms;
```

## <a name="see-also"></a>另请参阅

[头文件引用](../standard-library/cpp-standard-library-header-files.md)
