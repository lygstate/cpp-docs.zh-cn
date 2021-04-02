---
title: fmin、fminf、fminl
description: 适用于 fmin、fminf 和 fminl 的 API 参考;它确定了两个值中较小的一个。
ms.date: 9/1/2020
api_name:
- fmin
- fminf
- fminl
api_location:
- msvcrt.dll
- msvcr80.dll
- msvcr90.dll
- msvcr100.dll
- msvcr100_clr0400.dll
- msvcr110.dll
- msvcr110_clr0400.dll
- msvcr120.dll
- msvcr120_clr0400.dll
- ucrtbase.dll
- api-ms-win-crt-math-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- fmin
- fminf
- fminl
- math/fmin
- math/fminf
- math/fminl
helpviewer_keywords:
- fmin function
- fminf function
- fminl function
ms.assetid: 1916dfb5-99c1-4b0d-aefb-513525c3f2ac
ms.openlocfilehash: 007eae82ca60796d7a81b34e6419d21585c708d0
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099711"
---
# <a name="fmin-fminf-fminl"></a>fmin、fminf、fminl

确定两个指定值的较小值。

## <a name="syntax"></a>语法

```C
double fmin(
   double x,
   double y
);

float fmin(
   float x,
   float y
); //C++ only

long double fmin(
   long double x,
   long double y
); //C++ only

float fminf(
   float x,
   float y
);

long double fminl(
   long double x,
   long double y
);

#define fmin(x) // Requires C11 or higher
```

### <a name="parameters"></a>参数

*x-blade*\
要比较的第一个值。

*误差*\
要比较的第二个值。

## <a name="return-value"></a>返回值

如果成功，则返回 *x* 或 *y* 中的较小者。

|输入|结果|
|-----------|------------|
|*x* 为 NaN|*y*|
|*y* 为 NaN|*x*|
|*x* 和 *y* 为 NaN|NaN|

函数不会导致调用 [_matherr](matherr.md) ，导致任何浮点异常或更改 **errno** 的值。

## <a name="remarks"></a>注解

由于 c + + 允许重载，因此你可以调用采用并返回和类型的 **fmin** 的重载 **`float`** **`long double`** 。 在 C 程序中，除非使用 \<tgmath.h> 宏调用此函数，否则， **fmin** 始终采用并返回 **`double`** 。

如果使用 \<tgmath.h> `fmin()` 宏，则参数的类型将决定选择哪个版本的函数。 有关详细信息，请参阅 [类型-泛型数学](../../c-runtime-library/tgmath.md) 。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**fmin**、 **fminf**、 **fminl**|Ansi-c \<math.h><br />C + +： \<math.h> 或 \<cmath>|
|**fmin** 宏 | \<tgmath.h> |

有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="see-also"></a>另请参阅

[字母函数引用](crt-alphabetical-function-reference.md)<br/>
[fmax、fmaxf、fmaxl](fmax-fmaxf-fmaxl.md)<br/>
