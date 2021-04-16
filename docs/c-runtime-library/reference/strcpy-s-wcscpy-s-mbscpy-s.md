---
description: 了解详细信息： strcpy_s、wcscpy_s、_mbscpy_s、_mbscpy_s_l
title: strcpy_s、wcscpy_s、_mbscpy_s、_mbscpy_s_l
ms.date: 5/28/2020
api_name:
- wcscpy_s
- _mbscpy_s
- _mbscpy_s_l
- strcpy_s
- _o__mbscpy_s
- _o__mbscpy_s_l
- _o_strcpy_s
- _o_wcscpy_s
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
- api-ms-win-crt-multibyte-l1-1-0.dll
- api-ms-win-crt-string-l1-1-0.dll
- ntoskrnl.exe
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- strcpy_s
- _mbscpy_s
- _mbscpy_s_l
- _tcscpy_s
- wcscpy_s
helpviewer_keywords:
- strcpy_s function
- _tcscpy_s function
- _mbscpy_s function
- _mbscpy_s_l function
- copying strings
- strings [C++], copying
- tcscpy_s function
- wcscpy_s function
ms.assetid: 611326f3-7929-4a5d-a465-a4683af3b053
ms.openlocfilehash: 3cbfa2b2f8450adf07b2040fb2be0932377c9e37
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539566"
---
# <a name="strcpy_s-wcscpy_s-_mbscpy_s-_mbscpy_s_l"></a>`strcpy_s`、 `wcscpy_` s、 `_mbscpy_s` 、 `_mbscpy_s_l`

复制字符串。 [ `strcpy` `wcscpy` 的 `_mbscpy` 这些版本具有安全增强功能，如](strcpy-wcscpy-mbscpy.md) [CRT 中的安全功能](../../c-runtime-library/security-features-in-the-crt.md)中所述。

> [!IMPORTANT]
> **`_mbscpy_s`** 和 **`_mbscpy_s_l`** 不能用于在 Windows 运行时中执行的应用程序。 有关详细信息，请参阅[通用 Windows 平台应用中不支持的 CRT 函数](../../cppcx/crt-functions-not-supported-in-universal-windows-platform-apps.md)。

## <a name="syntax"></a>语法

```C
errno_t strcpy_s(
   char *dest,
   rsize_t dest_size,
   const char *src
);
errno_t wcscpy_s(
   wchar_t *dest,
   rsize_t dest_size,
   const wchar_t *src
);
errno_t _mbscpy_s(
   unsigned char *dest,
   rsize_t dest_size,
   const unsigned char *src
);
errno_t _mbscpy_s_l(
   unsigned char *dest,
   rsize_t dest_size,
   const unsigned char *src,
   _locale_t locale
);
```

```cpp
// Template functions are C++ only:
template <size_t size>
errno_t strcpy_s(
   char (&dest)[size],
   const char *src
); // C++ only
template <size_t size>
errno_t wcscpy_s(
   wchar_t (&dest)[size],
   const wchar_t *src
); // C++ only
template <size_t size>
errno_t _mbscpy_s(
   unsigned char (&dest)[size],
   const unsigned char *src
); // C++ only
template <size_t size>
errno_t _mbscpy_s_l(
   unsigned char (&dest)[size],
   const unsigned char *src,
   _locale_t locale
); // C++ only
```

### <a name="parameters"></a>参数

*`dest`*<br/>
目标字符串缓冲区的位置。

*`dest_size`*<br/>
**`char`** 用于窄和多字节函数的目标字符串缓冲区的大小，以及 **`wchar_t`** 宽函数的单位。 此值必须大于零且不大于 **`RSIZE_MAX`** 。 确保该大小的终止 `NULL` 字符串后终止。

*`src`*<br/>
以 null 结尾的源字符串缓冲区。

*`locale`*<br/>
要使用的区域设置。

## <a name="return-value"></a>返回值

如果成功，则为零；否则返回错误。

### <a name="error-conditions"></a>错误条件

|*`dest`*|*`dest_size`*|*`src`*|返回值|内容 *`dest`*|
|----------------------|------------------------|-----------------|------------------|----------------------------------|
|**`NULL`**|any|any|**`EINVAL`**|未修改|
|any|any|**`NULL`**|**`EINVAL`**|*`dest[0]`* 设置为0|
|any|0 或过小|any|**`ERANGE`**|*`dest[0]`* 设置为0|

## <a name="remarks"></a>注解

**`strcpy_s`** 函数将地址中的内容 *`src`* （包括终止 null 字符）复制到指定的位置 *`dest`* 。 目标字符串必须足够大以保存源字符串及其结尾的 null 字符。 **`strcpy_s`** 如果源和目标字符串重叠，则的行为是不确定的。

**`wcscpy_s`** 是的宽字符版本 **`strcpy_s`** ， **`_mbscpy_s`** 是多字节字符版本。 的参数 **`wcscpy_s`** 是宽字符字符串; 和的参数 **`_mbscpy_s`** **`_mbscpy_s_l`** 是多字节字符字符串。 否则这些函数具有相同行为。 **`_mbscpy_s_l`** 与相同， **`_mbscpy_s`** 只不过它使用传入的区域设置参数而不是当前区域设置。 有关详细信息，请参阅 [`locale`](../../c-runtime-library/locale.md)。

如果 *`dest`* 或 *`src`* 为 null 指针，或者如果目标字符串 *`dest_size`* 的大小太小，则调用无效参数处理程序，如 [参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许执行继续，则 **`EINVAL`** 当或为 null 指针时，这些函数将返回并将设置为; 如果 **`errno`** **`EINVAL`** *`dest`* *`src`* **`ERANGE`** **`errno`** **`ERANGE`** 目标字符串过小，则它们将返回并将设置为。

成功执行时，目标字符串始终以 null 结尾。

在 C++ 中，模板重载简化了这些函数的使用；重载可以自动推断缓冲区长度，从而无需指定大小自变量；并且它们可以自动将较旧、不安全的函数替换为更新、更安全的函数。 有关详细信息，请参阅[安全模板重载](../../c-runtime-library/secure-template-overloads.md)。

这些函数的调试库版本首先用0xFE 填充缓冲区。 若要禁用此行为，请使用 [`_CrtSetDebugFillThreshold`](crtsetdebugfillthreshold.md) 。

默认情况下，此函数的全局状态的作用域限定为应用程序。 若要更改此项，请参阅 [CRT 中的全局状态](../global-state.md)。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|`TCHAR.H` 例程|`_UNICODE` & `_MBCS` 未定义|`_MBCS` 明确|`_UNICODE` 明确|
|---------------------|------------------------------------|--------------------|-----------------------|
|**`_tcscpy_s`**|**`strcpy_s`**|**`_mbscpy_s`**|**`wcscpy_s`**|

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**`strcpy_s`**|`<string.h>`|
|**`wcscpy_s`**|`<string.h>` 或 `<wchar.h>`|
|**`_mbscpy_s`**|`<mbstring.h>`|

这些函数是 Microsoft 特定的。 有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

与生产质量代码不同，此示例调用安全字符串函数而不检查错误：

```C
// crt_strcpy_s.c
// Compile by using: cl /W4 crt_strcpy_s.c
// This program uses strcpy_s and strcat_s
// to build a phrase.

#include <string.h>     // for strcpy_s, strcat_s
#include <stdlib.h>     // for _countof
#include <stdio.h>      // for printf
#include <errno.h>      // for return values

int main(void)
{
    char stringBuffer[80];

    strcpy_s(stringBuffer, _countof(stringBuffer), "Hello world from ");
    strcat_s(stringBuffer, _countof(stringBuffer), "strcpy_s ");
    strcat_s(stringBuffer, _countof(stringBuffer), "and ");
    strcat_s(stringBuffer, _countof(stringBuffer), "strcat_s!");

    printf("stringBuffer = %s\n", stringBuffer);
}
```

```Output
stringBuffer = Hello world from strcpy_s and strcat_s!
```

在生成 c + + 代码时，模板版本可能更易于使用。

```cpp
// crt_wcscpy_s.cpp
// Compile by using: cl /EHsc /W4 crt_wcscpy_s.cpp
// This program uses wcscpy_s and wcscat_s
// to build a phrase.

#include <cstring>  // for wcscpy_s, wcscat_s
#include <cstdlib>  // for _countof
#include <iostream> // for cout, includes <cstdlib>, <cstring>
#include <errno.h>  // for return values

int main(void)
{
    wchar_t stringBuffer[80];
    // using template versions of wcscpy_s and wcscat_s:
    wcscpy_s(stringBuffer, L"Hello world from ");
    wcscat_s(stringBuffer, L"wcscpy_s ");
    wcscat_s(stringBuffer, L"and ");
    // of course we can supply the size explicitly if we want to:
    wcscat_s(stringBuffer, _countof(stringBuffer), L"wcscat_s!");

    std::wcout << L"stringBuffer = " << stringBuffer << std::endl;
}
```

```Output
stringBuffer = Hello world from wcscpy_s and wcscat_s!
```

## <a name="see-also"></a>另请参阅

[字符串操作](../../c-runtime-library/string-manipulation-crt.md) <br/>
[`strcat`, `wcscat`, `_mbscat`, `_mbscat_l`](strcat-wcscat-mbscat.md) <br/>
[`strcmp`, `wcscmp`, `_mbscmp`, `_mbscmp_l`](strcmp-wcscmp-mbscmp.md) <br/>
[`strncat_s`, `_strncat_s_l`, `wcsncat_s`, `_wcsncat_s_l`, `_mbsncat_s`, `_mbsncat_s_l`](strncat-s-strncat-s-l-wcsncat-s-wcsncat-s-l-mbsncat-s-mbsncat-s-l.md) <br/>
[`strncmp`, `wcsncmp`, `_mbsncmp`, `_mbsncmp_l`](strncmp-wcsncmp-mbsncmp-mbsncmp-l.md) <br/>
[`strncpy_s`, `_strncpy_s_l`, `wcsncpy_s`, `_wcsncpy_s_l`, `_mbsncpy_s`, `_mbsncpy_s_l`](strncpy-s-strncpy-s-l-wcsncpy-s-wcsncpy-s-l-mbsncpy-s-mbsncpy-s-l.md) <br/>
[`_strnicmp`, `_wcsnicmp`, `_mbsnicmp`, `_strnicmp_l`, `_wcsnicmp_l`, `_mbsnicmp_l`](strnicmp-wcsnicmp-mbsnicmp-strnicmp-l-wcsnicmp-l-mbsnicmp-l.md) <br/>
[`strrchr`, `wcsrchr`, `_mbsrchr`, `_mbsrchr_l`](strrchr-wcsrchr-mbsrchr-mbsrchr-l.md) <br/>
[`strspn`, `wcsspn`, `_mbsspn`, `_mbsspn_l`](strspn-wcsspn-mbsspn-mbsspn-l.md)<br/>
