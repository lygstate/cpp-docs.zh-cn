---
description: 了解详细信息： printf_s、_printf_s_l、wprintf_s、_wprintf_s_l
title: printf_s、_printf_s_l、wprintf_s、_wprintf_s_l
ms.date: 3/9/2021
api_name:
- _printf_s_l
- wprintf_s
- _wprintf_s_l
- printf_s
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
- wprintf_s
- printf_s
helpviewer_keywords:
- wprintf_s function
- tprintf_s function
- _tprintf_s function
- printf_s_l function
- printf_s function
- _printf_s_l function
- printf function, format specification fields
- printf function, using
- _tprintf_s_l function
- wprintf_s_l function
- formatted text [C++]
- tprintf_s_l function
- _wprintf_s_l function
ms.openlocfilehash: 16496d0793b33d15438b0fcd771c62878cfe4b72
ms.sourcegitcommit: b04b39940b0c1e265f80fc1951278fdb05a1b30a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/10/2021
ms.locfileid: "102621446"
---
# <a name="printf_s-_printf_s_l-wprintf_s-_wprintf_s_l"></a>printf_s、_printf_s_l、wprintf_s、_wprintf_s_l

将格式化输出打印至标准输出流 这些版本的 [printf、_printf_l、wprintf、_wprintf_l](printf-printf-l-wprintf-wprintf-l.md) 具有安全增强功能，如 [CRT 中的安全功能](../../c-runtime-library/security-features-in-the-crt.md)所述。

## <a name="syntax"></a>语法

```C
int printf_s(
   const char *format [,
   argument]...
);
int _printf_s_l(
   const char *format,
   locale_t locale [,
   argument]...
);
int wprintf_s(
   const wchar_t *format [,
   argument]...
);
int _wprintf_s_l(
   const wchar_t *format,
   locale_t locale [,
   argument]...
);
```

### <a name="parameters"></a>参数

*format*<br/>
设置控件格式。

argument <br/>
可选参数。

*locale*<br/>
要使用的区域设置。

## <a name="return-value"></a>返回值

返回输出的字符数或负值（如果出错）。

## <a name="remarks"></a>注解

**Printf_s** 函数将一系列字符和值输出到标准输出流（ **stdout**）。 如果参数跟在 *格式* 字符串之后， *格式* 字符串必须包含确定自变量的输出格式的规范。

**Printf_s** 和 **printf** 之间的主要区别在于 **printf_s** 检查格式字符串中的有效格式设置字符，而 **printf** 仅检查格式字符串是否为 null 指针。 如果任一检查失败，将调用无效参数处理程序，如[参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许执行继续，则该函数将返回-1，并将 **errno** 设置为 **EINVAL**。

有关 **errno** 和错误代码的信息，请参阅 [_doserrno、errno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

**printf_s** 和 **fprintf_s** 的行为相同，只是 **printf_s** 将输出写入到 **stdout** ，而不是写入到类型 **文件** 的目标。 有关详细信息，请参阅 [fprintf_s、_fprintf_s_l、fwprintf_s、_fwprintf_s_l](fprintf-s-fprintf-s-l-fwprintf-s-fwprintf-s-l.md).

**wprintf_s** 是 **printf_s** 的宽字符版本; *格式* 是宽字符字符串。 如果在 ANSI 模式下打开流，则 **wprintf_s** 和 **printf_s** 的行为相同。 **printf_s** 当前不支持输出到 UNICODE 流中。

这些具有 **_l** 后缀的函数的版本相同，只不过它们使用传入的区域设置参数而不是当前线程区域设置。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _unicode|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tprintf_s**|**printf_s**|**printf_s**|**wprintf_s**|
|**_tprintf_s_l**|**_printf_s_l**|**_printf_s_l**|**_wprintf_s_l**|

如果参数遵循 *格式*) 格式规范，则 *格式* 参数包括普通字符、转义序列和 (。 普通字符和转义序列将按其外观的顺序复制到 **stdout** 。 例如，行

```C
printf_s("Line one\n\t\tLine two\n");
```

生成输出

```Output
Line one
        Line two
```

[格式规范](../../c-runtime-library/format-specification-syntax-printf-and-wprintf-functions.md) 始终以百分号 (开头 **%**) 并从左向右读取。 **Printf_s** 遇到第一个格式规范时 (如果任何) ，它会在 *格式* 后转换第一个参数的值，并相应地输出它。 第二个格式规范致使第二个自变量转换并输出，依此类推。 如果存在比格式规范更多的自变量，则多出的自变量将被忽略。 如果全部格式规范没有足够自变量，则结果不确定。

> [!IMPORTANT]
> 确保 format 不是用户定义的字符串。
>
>
> 从 Windows 10 版本2004开始， (生成 19041) ， `printf` 函数系列按用于舍入的 IEEE 754 规则打印完全可表示的浮点数。 在以前版本的 Windows 中，准确地表示以 "5" 结尾的浮点数始终向上舍入。 IEEE 754 指出它们必须舍入到最接近的偶数 (也称为 "银行家舍入" ) 。 例如，和都 `printf("%1.0f", 1.5)` `printf("%1.0f", 2.5)` 应该舍入为2。 以前，1.5 将舍入为2，2.5 将舍入为3。 此更改只影响精确的可表示数字。 例如，2.35 (当在内存中表示时，) 将继续向上舍入到2.4。 这些函数所做的舍入现在还遵循由设置的浮点舍入模式 [`fesetround`](fegetround-fesetround2.md) 。 以前，舍入始终选择 `FE_TONEAREST` 行为。 此更改仅影响使用 Visual Studio 2019 版本16.2 和更高版本生成的程序。 若要使用旧的浮点舍入行为，请使用链接 [`legacy_stdio_float_rounding.obj`](../link-options.md) 。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**printf_s**， **_printf_s_l**|\<stdio.h>|
|**wprintf_s**， **_wprintf_s_l**|\<stdio.h> 或 \<wchar.h>|

通用 Windows 平台 (UWP) 应用中不支持控制台。 与控制台、 **stdin**、 **stdout** 和 **stderr** 关联的标准流句柄必须重定向，然后 C 运行时函数才能在 UWP 应用中使用它们。 有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

通用 Windows 平台 (UWP) 应用中不支持控制台。 与控制台、 **stdin**、 **stdout** 和 **stderr** 关联的标准流句柄必须重定向，然后 C 运行时函数才能在 UWP 应用中使用它们。 有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_printf_s.c
/* This program uses the printf_s and wprintf_s functions
* to produce formatted output.
*/

#include <stdio.h>

int main( void )
{
   char   ch = 'h', *string = "computer";
   int    count = -9234;
   double fp = 251.7366;
   wchar_t wch = L'w', *wstring = L"Unicode";

   /* Display integers. */
   printf_s( "Integer formats:\n"
           "   Decimal: %d  Justified: %.6d  Unsigned: %u\n",
           count, count, count );

   printf_s( "Decimal %d as:\n   Hex: %Xh  C hex: 0x%x  Octal: %o\n",
            count, count, count, count );

   /* Display in different radixes. */
   printf_s( "Digits 10 equal:\n   Hex: %i  Octal: %i  Decimal: %i\n",
            0x10, 010, 10 );

   /* Display characters. */

   printf_s("Characters in field (1):\n%10c%5hc%5C%5lc\n", ch, ch, wch, wch);
   wprintf_s(L"Characters in field (2):\n%10C%5hc%5c%5lc\n", ch, ch, wch, wch);

   /* Display strings. */

   printf_s("Strings in field (1):\n%25s\n%25.4hs\n   %S%25.3ls\n",
   string, string, wstring, wstring);
   wprintf_s(L"Strings in field (2):\n%25S\n%25.4hs\n   %s%25.3ls\n",
       string, string, wstring, wstring);

   /* Display real numbers. */
   printf_s( "Real numbers:\n   %f %.2f %e %E\n", fp, fp, fp, fp );

   /* Display pointer. */
   printf_s( "\nAddress as:   %p\n", &count);

}
```

### <a name="sample-output"></a>示例输出

```Output
Integer formats:
   Decimal: -9234  Justified: -009234  Unsigned: 4294958062
Decimal -9234 as:
   Hex: FFFFDBEEh  C hex: 0xffffdbee  Octal: 37777755756
Digits 10 equal:
   Hex: 16  Octal: 8  Decimal: 10
Characters in field (1):
         h    h    w    w
Characters in field (2):
         h    h    w    w
Strings in field (1):
                 computer
                     comp
   Unicode                      Uni
Strings in field (2):
                 computer
                     comp
   Unicode                      Uni
Real numbers:
   251.736600 251.74 2.517366e+002 2.517366E+002

Address as:   0012FF78
```

## <a name="see-also"></a>另请参阅

[浮点支持](../../c-runtime-library/floating-point-support.md)<br/>
[流 I/O](../../c-runtime-library/stream-i-o.md)<br/>
[区域设置](../../c-runtime-library/locale.md)<br/>
[fopen、_wfopen](fopen-wfopen.md)<br/>
[fprintf、_fprintf_l、fwprintf、_fwprintf_l](fprintf-fprintf-l-fwprintf-fwprintf-l.md)<br/>
[scanf、_scanf_l、wscanf、_wscanf_l](scanf-scanf-l-wscanf-wscanf-l.md)<br/>
[sprintf、_sprintf_l、swprintf、_swprintf_l、 \_ _swprintf_l](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)<br/>
[vprintf 函数](../../c-runtime-library/vprintf-functions.md)<br/>
