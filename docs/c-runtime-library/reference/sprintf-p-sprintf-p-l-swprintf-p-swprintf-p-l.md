---
description: 了解详细信息： _sprintf_p、_sprintf_p_l、_swprintf_p、_swprintf_p_l
title: _sprintf_p, _sprintf_p_l, _swprintf_p, _swprintf_p_l
ms.date: 3/9/2021
api_name:
- _sprintf_p
- _swprintf_p_l
- _swprintf_p
- _sprintf_p_l
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
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _sprintf_p
- _swprintf_p_l
- _sprintf_p_l
- _swprintf_p
- sprintf_p
- swprint_p_l
- swprintf_p
- swprintf_p_l
helpviewer_keywords:
- sprintf_p_l function
- swprintf_p function
- swprintf_p_l function
- _sprintf_p function
- _sprintf_p_l function
- _swprintf_p function
- sprintf_p function
- _stprintf_p function
- stprintf_p function
- _swprintf_p_l function
- stprintf_p_l function
- formatted text [C++]
- _stprintf_p_l function
ms.openlocfilehash: 2f0b6dad129a8f3f2f91bf1244c77ae5691a679e
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539273"
---
# <a name="_sprintf_p-_sprintf_p_l-_swprintf_p-_swprintf_p_l"></a>`_sprintf_p`, `_sprintf_p_l`, `_swprintf_p`, `_swprintf_p_l`

利用指定参数在格式字符串中使用的顺序的能力将带格式的数据写入字符串。

## <a name="syntax"></a>语法

```C
int _sprintf_p(
   char *buffer,
   size_t sizeOfBuffer,
   const char *format [,
   argument_list]
);
int _sprintf_p_l(
   char *buffer,
   size_t sizeOfBuffer,
   const char *format,
   locale_t locale [,
   argument_list]
);
int _swprintf_p(
   wchar_t *buffer,
   size_t sizeOfBuffer,
   const wchar_t *format [,
   argument_list]
);
int _swprintf_p_l(
   wchar_t *buffer,
   size_t sizeOfBuffer,
   const wchar_t *format,
   locale_t locale [,
   argument_list]
);
```

### <a name="parameters"></a>参数

*`buffer`*<br/>
输出的存储位置

*`sizeOfBuffer`*<br/>
可存储的最多字符数。

*`format`*<br/>
窗体控件字符串。

*`argument_list`*<br/>
格式字符串的可选参数。

*`locale`*<br/>
要使用的区域设置。

有关更多信息，请参见 [格式规范](../../c-runtime-library/format-specification-syntax-printf-and-wprintf-functions.md)。

## <a name="return-value"></a>返回值

写入的字符数; 如果出现错误，则为-1。

## <a name="remarks"></a>注解

**`_sprintf_p`** 函数在中设置和存储一系列字符和值 *`buffer`* 。 *`argument_list`* 如果根据中的相应格式规范转换和输出任何) ，则 (中的每个参数 *`format`* 。 *Format* 参数使用 [ `printf` 和 `wprintf` 函数的格式规范语法](../../c-runtime-library/format-specification-syntax-printf-and-wprintf-functions.md)。 null 字符追加在写入的最后一个字符后。 如果在重叠的字符串之间发生复制，则此行为不确定。 和之间的差异在于 **`_sprintf_p`** **`sprintf_s`** **`_sprintf_p`** 支持位置参数，这允许指定格式字符串中使用参数的顺序。 有关详细信息，请参阅[ `printf_p` 位置参数](../../c-runtime-library/printf-p-positional-parameters.md)。

**`_swprintf_p`** 是的宽字符版本 **`_sprintf_p`** ; 的指针参数 **`_swprintf_p`** 是宽字符字符串。 中对编码错误的检测 **`_swprintf_p`** 可能与中的不同 **`_sprintf_p`** 。 **`_swprintf_p`** 和 **`fwprintf_p`** 的行为方式相同，只不过将 **`_swprintf_p`** 输出写入字符串而不是类型的目标 **`FILE`** ，并且 **`_swprintf_p`** 需要 *`count`* 参数来指定要写入的最大字符数。 这些带有后缀的函数的版本 **`_l`** 相同，只不过它们使用传入的区域设置参数而不是当前线程区域设置。

**`_sprintf_p`** 返回存储在中的字节数 *`buffer`* ，不包括终止 null 字符。 **`_swprintf_p`** 返回存储在中的宽字符数 *`buffer`* ，不包括终止 null 宽字符。 如果 *`buffer`* 或 *`format`* 为 null 指针，或如果格式字符串包含无效的格式字符，则将调用无效的参数处理程序，如 [参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许执行继续，则这些函数将返回-1 并将设置 **`errno`** 为 **`EINVAL`** 。

> [!IMPORTANT]
> 从 Windows 10 版本2004开始， (生成 19041) ， `printf` 函数系列按用于舍入的 IEEE 754 规则打印完全可表示的浮点数。 在以前版本的 Windows 中，准确地表示以 "5" 结尾的浮点数始终向上舍入。 IEEE 754 指出它们必须舍入到最接近的偶数 (也称为 "银行家舍入" ) 。 例如，和都 `printf("%1.0f", 1.5)` `printf("%1.0f", 2.5)` 应该舍入为2。 以前，1.5 将舍入为2，2.5 将舍入为3。 此更改只影响精确的可表示数字。 例如，2.35 (当在内存中表示时，) 将继续向上舍入到2.4。 这些函数所做的舍入现在还遵循由设置的浮点舍入模式 [`fesetround`](fegetround-fesetround2.md) 。 以前，舍入始终选择 `FE_TONEAREST` 行为。 此更改仅影响使用 Visual Studio 2019 版本16.2 和更高版本生成的程序。 若要使用旧的浮点舍入行为，请使用 ["legacy_stdio_float_rounding .obj"](../link-options.md)链接。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|`TCHAR.H` 例程|`_UNICODE` & `_MBCS` 未定义|`_MBCS` 明确|`_UNICODE` 明确|
|---------------------|------------------------------------|--------------------|-----------------------|
|**`_stprintf_p`**|**`_sprintf_p`**|**`_sprintf_p`**|**`_swprintf_p`**|
|**`_stprintf_p_l`**|**`_sprintf_p_l`**|**`_sprintf_p_l`**|**`_swprintf_p_l`**|

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**`_sprintf_p`**, **`_sprintf_p_l`**|`<stdio.h>`|
|**`_swprintf_p`**, **`_swprintf_p_l`**|`<stdio.h>` 或 `<wchar.h>`|

有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example-use-_sprintf_p-to-format-data"></a>示例：用于 `_sprintf_p` 设置数据的格式

```C
// crt_sprintf_p.c
// This program uses _sprintf_p to format various
// data and place them in the string named buffer.
//

#include <stdio.h>

int main( void )
{
    char     buffer[200],
            s[] = "computer", c = 'l';
    int      i = 35,
            j;
    float    fp = 1.7320534f;

    // Format and print various data:
    j  = _sprintf_p( buffer, 200,
                     "   String:    %s\n", s );
    j += _sprintf_p( buffer + j, 200 - j,
                     "   Character: %c\n", c );
    j += _sprintf_p( buffer + j, 200 - j,
                     "   Integer:   %d\n", i );
    j += _sprintf_p( buffer + j, 200 - j,
                     "   Real:      %f\n", fp );

    printf( "Output:\n%s\ncharacter count = %d\n",
            buffer, j );
}
```

```Output
Output:
   String:    computer
   Character: l
   Integer:   35
   Real:      1.732053

character count = 79
```

## <a name="example-error-code-handling"></a>示例：错误代码处理

```C
// crt_swprintf_p.c
// This is the wide character example which
// also demonstrates _swprintf_p returning
// error code.
#include <stdio.h>

#define BUFFER_SIZE 100

int main( void )
{
    wchar_t buffer[BUFFER_SIZE];
    int     len;

    len = _swprintf_p(buffer, BUFFER_SIZE, L"%2$s %1$d",
                      0, L" marbles in your head.");
    _printf_p( "Wrote %d characters\n", len );

    // _swprintf_p fails because string contains WEOF (\xffff)
    len = _swprintf_p(buffer, BUFFER_SIZE, L"%s",
                      L"Hello\xffff world" );
    _printf_p( "Wrote %d characters\n", len );
}
```

```Output
Wrote 24 characters
Wrote -1 characters
```

## <a name="see-also"></a>另请参阅

[流 I/O](../../c-runtime-library/stream-i-o.md)<br/>
[`_fprintf_p`, `_fprintf_p_l`, `_fwprintf_p`, `_fwprintf_p_l`](fprintf-p-fprintf-p-l-fwprintf-p-fwprintf-p-l.md)<br/>
[`fprintf`, `_fprintf_l`, `fwprintf`, `_fwprintf_l`](fprintf-fprintf-l-fwprintf-fwprintf-l.md)<br/>
[`_printf_p`, `_printf_p_l`, `_wprintf_p`, `_wprintf_p_l`](printf-p-printf-p-l-wprintf-p-wprintf-p-l.md)<br/>
[`printf`, `_printf_l`, `wprintf`, `_wprintf_l`](printf-printf-l-wprintf-wprintf-l.md)<br/>
[`sprintf`, `_sprintf_l`, `swprintf`, `_swprintf_l`, `__swprintf_l`](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)<br/>
[`scanf`, `_scanf_l`, `wscanf`, `_wscanf_l`](scanf-scanf-l-wscanf-wscanf-l.md)<br/>
[`sscanf`, `_sscanf_l`, `swscanf`, `_swscanf_l`](sscanf-sscanf-l-swscanf-swscanf-l.md)<br/>
[`sscanf_s`, `_sscanf_s_l`, `swscanf_s`, `_swscanf_s_l`](sscanf-s-sscanf-s-l-swscanf-s-swscanf-s-l.md)<br/>
[`vprintf` 函数](../../c-runtime-library/vprintf-functions.md)<br/>
[`printf_p` 位置参数](../../c-runtime-library/printf-p-positional-parameters.md)<br/>
