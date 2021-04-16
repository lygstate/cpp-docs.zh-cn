---
description: 了解详细信息： scanf_s、_scanf_s_l、wscanf_s、_wscanf_s_l
title: scanf_s、_scanf_s_l、wscanf_s、_wscanf_s_l
ms.date: 03/26/2019
api_name:
- wscanf_s
- _wscanf_s_l
- scanf_s
- _scanf_s_l
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
- wscanf_s
- _tscanf_s_l
- _wscanf_s_l
- scanf_s
- _tscanf_s
- _scanf_s_l
helpviewer_keywords:
- reading data [C++], from input streams
- buffers [C++], buffer overruns
- _scanf_s_l function
- _wscanf_s_l function
- tscanf_s_l function
- tscanf_s function
- scanf_s function
- data [C++], reading from input stream
- wscanf_s function
- _tscanf_s_l function
- _tscanf_s function
- scanf_s_l function
- formatted data [C++], from input streams
- wscanf_s_l function
- buffers [C++], avoiding overruns
ms.assetid: 42cafcf7-52d6-404a-80e4-b056a7faf2e5
ms.openlocfilehash: 0a23ed2958f29c8027fdd2530cbcb215cbb54ffa
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539341"
---
# <a name="scanf_s-_scanf_s_l-wscanf_s-_wscanf_s_l"></a>`scanf_s`, `_scanf_s_l`, `wscanf_s`, `_wscanf_s_l`

读取标准输入流中的格式化数据。 [ `scanf` `_scanf_l` `wscanf` 的 `_wscanf_l` 这些版本具有安全增强功能，如](scanf-scanf-l-wscanf-wscanf-l.md) [CRT 中的安全功能](../../c-runtime-library/security-features-in-the-crt.md)中所述。

## <a name="syntax"></a>语法

```C
int scanf_s(
   const char *format [,
   argument]...
);
int _scanf_s_l(
   const char *format,
   locale_t locale [,
   argument]...
);
int wscanf_s(
   const wchar_t *format [,
   argument]...
);
int _wscanf_s_l(
   const wchar_t *format,
   locale_t locale [,
   argument]...
);
```

### <a name="parameters"></a>参数

*`format`*<br/>
格式控制字符串。

*`argument`*<br/>
可选参数。

*`locale`*<br/>
要使用的区域设置。

## <a name="return-value"></a>返回值

返回已成功转换和分配的字段数。 返回值不包括已读取但未分配的字段。 如果返回值为0，则表示未分配任何字段。 对于错误，返回值为 **EOF** ; 或者，如果在第一次尝试读取字符时找到文件尾字符或字符串末尾字符，则为。 如果 *format* 是 **`NULL`** 指针，则会调用无效参数处理程序，如 [参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许执行继续，则 **`scanf_s`** **`wscanf_s`** 返回 **EOF** 并将设置 **`errno`** 为 **`EINVAL`** 。

有关这些错误代码及其他错误代码的信息，请参阅[ `errno` 、、 `_doserrno` `_sys_errlist` 和 `_sys_nerr` ](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

## <a name="remarks"></a>注解

**`scanf_s`** 函数从标准输入流中读取数据， **`stdin`** 并将其写入到中 *`argument`* 。 每个都 *`argument`* 必须是指向与中的类型说明符相对应的变量类型的指针 *`format`* 。 如果在重叠的字符串之间发生复制，则此行为不确定。

**`wscanf_s`** 是的宽字符版本 **`scanf_s`** ; 的 *格式* 参数 **`wscanf_s`** 是宽字符字符串。 **`wscanf_s`****`scanf_s`** 如果在 ANSI 模式下打开流，则和的行为相同。 **`scanf_s`** 当前不支持 UNICODE 流的输入。

这些具有 **_l** 后缀的函数的版本相同，只不过它们使用 *`locale`* 参数而不是当前线程区域设置。

与 **`scanf`** 和不同 **`wscanf`** ， **`scanf_s`** 和 **`wscanf_s`** 要求你为一些参数指定缓冲区大小。 指定所有、、、 **`c`** **`C`** **`s`** **`S`** 或字符串控制集参数的大小 **`[]`** 。 以字符作为附加参数传递的缓冲区大小。 它紧跟在指向缓冲区或变量的指针后面。 例如，如果您正在读取一个字符串，则将传递该字符串的缓冲区大小，如下所示：

```C
char s[10];
scanf_s("%9s", s, (unsigned)_countof(s)); // buffer size is 10, width specification is 9
```

缓冲区大小包括终端 null。 您可以使用宽度规范字段来确保读入的令牌适合缓冲区。 如果某个令牌太大而无法容纳，则不会向该缓冲区写入任何内容，除非存在宽度规范。

> [!NOTE]
> 大小参数的类型为 **`unsigned`** ，而不是 **`size_t`** 。 使用静态强制转换将值转换为 **`size_t`** **`unsigned`** 64 位生成配置。

Buffer size 参数描述了最大字符数，而不是字节数。 在此示例中，缓冲区类型的宽度与格式说明符的宽度不匹配。

```C
wchar_t ws[10];
wscanf_s(L"%9S", ws, (unsigned)_countof(ws));
```

**`S`** 格式说明符表示使用该函数支持的默认宽度的 "相反" 字符宽度。 字符宽度是单字节，而函数支持双字节字符。 此示例读取一个最多包含9个单字节宽度字符的字符串，并将其放入一个双字节宽度字符缓冲区。 这些字符被视为单字节值；头两个字符存储在 `ws[0]` 中，紧接着的两个字符存储在 `ws[1]` 中，依此类推。

此示例读取单个字符：

```C
char c;
scanf_s("%c", &c, 1);
```

读取非 null 终止的字符串的多个字符时，将同时使用整数规范和缓冲区大小。

```C
char c[4];
scanf_s("%4c", c, (unsigned)_countof(c)); // not null terminated
```

有关详细信息，请参阅[ `scanf` 宽度规范](../../c-runtime-library/scanf-width-specification.md)。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|`TCHAR.H` 例程|`_UNICODE` & `_MBCS` 未定义|`_MBCS` 明确|`_UNICODE` 明确|
|---------------------|------------------------------------|--------------------|-----------------------|
|**`_tscanf_s`**|**`scanf_s`**|**`scanf_s`**|**`wscanf_s`**|
|**`_tscanf_s_l`**|**`_scanf_s_l`**|**`_scanf_s_l`**|**`_wscanf_s_l`**|

有关详细信息，请参阅 [格式规范字段： `scanf` 和 `wscanf` 函数](../../c-runtime-library/format-specification-fields-scanf-and-wscanf-functions.md)。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**`scanf_s`**, **`_scanf_s_l`**|`<stdio.h>`|
|**`wscanf_s`**, **`_wscanf_s_l`**|`<stdio.h>` 或 `<wchar.h>`|

通用 Windows 平台 (UWP) 应用中不支持控制台。 标准流处理 **`stdin`** 、 **`stdout`** 和时， **`stderr`** 必须重定向，然后 C 运行时函数才能在 UWP 应用中使用它们。 有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_scanf_s.c
// This program uses the scanf_s and wscanf_s functions
// to read formatted input.

#include <stdio.h>
#include <stdlib.h>

int main( void )
{
   int      i,
            result;
   float    fp;
   char     c,
            s[80];
   wchar_t  wc,
            ws[80];

   result = scanf_s( "%d %f %c %C %s %S", &i, &fp, &c, 1,
                     &wc, 1, s, (unsigned)_countof(s), ws, (unsigned)_countof(ws) );
   printf( "The number of fields input is %d\n", result );
   printf( "The contents are: %d %f %c %C %s %S\n", i, fp, c,
           wc, s, ws);
   result = wscanf_s( L"%d %f %hc %lc %S %ls", &i, &fp, &c, 2,
                      &wc, 1, s, (unsigned)_countof(s), ws, (unsigned)_countof(ws) );
   wprintf( L"The number of fields input is %d\n", result );
   wprintf( L"The contents are: %d %f %C %c %hs %s\n", i, fp,
            c, wc, s, ws);
}
```

当提供此输入时，该程序将生成以下输出：

```Input
71 98.6 h z Byte characters
36 92.3 y n Wide characters
```

```Output
The number of fields input is 6
The contents are: 71 98.599998 h z Byte characters
The number of fields input is 6
The contents are: 36 92.300003 y n Wide characters
```

## <a name="see-also"></a>另请参阅

[浮点支持](../../c-runtime-library/floating-point-support.md)<br/>
[流 I/O](../../c-runtime-library/stream-i-o.md)<br/>
[区域设置](../../c-runtime-library/locale.md)<br/>
[`fscanf`, `_fscanf_l`, `fwscanf`, `_fwscanf_l`](fscanf-fscanf-l-fwscanf-fwscanf-l.md)<br/>
[`printf`, `_printf_l`, `wprintf`, `_wprintf_l`](printf-printf-l-wprintf-wprintf-l.md)<br/>
[`sprintf`, `_sprintf_l`, `swprintf`, `_swprintf_l`, `__swprintf_l`](sprintf-sprintf-l-swprintf-swprintf-l-swprintf-l.md)<br/>
[`sscanf`, `_sscanf_l`, `swscanf`, `_swscanf_l`](sscanf-sscanf-l-swscanf-swscanf-l.md)<br/>
