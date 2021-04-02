---
description: 了解详细信息： _utime、_utime32、_utime64、_wutime、_wutime32、_wutime64
title: _utime、_utime32、_utime64、_wutime、_wutime32、_wutime64
ms.date: 4/2/2020
api_name:
- _utime64
- _utime
- _wutime
- _wutime64
- _wutime32
- _utime32
- _o__utime32
- _o__utime64
- _o__wutime32
- _o__wutime64
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
- api-ms-win-crt-time-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- _tutime
- _utime64
- wutime
- utime32
- wutime64
- _utime
- wutime32
- _wutime
- utime
- utime64
- _wutime64
- _utime32
- _tutime64
- _wutime32
helpviewer_keywords:
- tutime function
- utime32 function
- utime64 function
- _utime function
- _tutime32 function
- time [C++], file modification
- wutime function
- _wutime function
- _wutime32 function
- _tutime64 function
- _tutime function
- files [C++], modification time
- _wutime64 function
- _utime32 function
- utime function
- _utime64 function
- wutime64 function
- wutime32 function
- tutime64 function
- tutime32 function
ms.assetid: 8d482d40-19b9-4591-bfee-5d7f601d1a9e
ms.openlocfilehash: 82e8180b21a0de19134673d362989b4ca371dbc2
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099334"
---
# <a name="_utime-_utime32-_utime64-_wutime-_wutime32-_wutime64"></a>_utime、_utime32、_utime64、_wutime、_wutime32、_wutime64

设置文件修改时间。

## <a name="syntax"></a>语法

```C
int _utime(
   const char *filename,
   struct _utimbuf *times
);
int _utime32(
   const char *filename,
   struct __utimbuf32 *times
);
int _utime64(
   const char *filename,
   struct __utimbuf64 *times
);
int _wutime(
   const wchar_t *filename,
   struct _utimbuf *times
);
int _wutime32(
   const wchar_t *filename,
   struct __utimbuf32 *times
);
int _wutime64(
   const wchar_t *filename,
   struct __utimbuf64 *times
);
```

### <a name="parameters"></a>参数

*filename*<br/>
指向包含路径或文件名的字符串的指针。

*times*<br/>
指向存储时间值的指针。

## <a name="return-value"></a>返回值

如果更改了文件修改时间，则这些函数均将返回 0。 返回值-1 表示错误。 如果传递的参数无效，则调用无效参数处理程序，如[参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许执行继续，则这些函数将返回-1，并将 **errno** 设置为以下值之一：

|errno 值|条件|
|-|-|
| **EACCES** | 路径指定目录或只读文件 |
| **EINVAL** | 无效的 *时间* 参数 |
| **EMFILE** | 打开的文件太多（必须打开文件以更改其修改时间） |
| **ENOENT** | 找不到路径或文件名 |

有关这些和其他返回代码的详细信息，请参阅 [_doserrno、errno、_sys_errlist 和 _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md) 。

如果更改日期在 1970 年 1 月 1 日午夜之后且在所使用的函数的结束日期之前，则可以更改文件的日期。 **_utime** 和 **_wutime** 使用64位时间值，因此结束日期为23:59:59，12月31日3000，UTC。 如果 **_USE_32BIT_TIME_T** 定义为强制旧行为，则结束日期为23:59:59 年1月 2038 18 日，UTC。 **_utime32** 或 **_wutime32** 使用32位时间类型，而不管是否定义 **_USE_32BIT_TIME_T** ，并且始终具有更早的结束日期。 **_utime64** 或 **_wutime64** 始终使用64位时间类型，因此这些函数始终支持更晚的结束日期。

## <a name="remarks"></a>注解

**_Utime** 函数为 *filename* 指定的文件设置修改时间。 进程必须拥有文件的写入权限才能更改时间。 在 Windows 操作系统中，可以更改 **_utimbuf** 结构中的访问时间和修改时间。 如果 time 为 **空** 指针 *，则将* 修改时间设置为当前的本地时间。 否则， *时间* 必须指向在 SYS\UTIME.H. 中定义的类型 **_utimbuf** 的结构。

**_Utimbuf** 结构存储 **_utime** 用于更改文件修改日期的文件访问时间和修改时间。 结构具有以下字段，它们均为 **time_t** 类型：

| 字段 | 说明 |
|-------|---|
| **actime** | 文件访问时间 |
| **modtime** | 文件修改时间 |

**_Utimebuf32** 和 **__utimbuf64**) 的特定版本 **_utimbuf** 结构 (使用时间类型的32位和64位版本进行定义。 这些是此函数的 32 位和 64 位特定版本中使用的内容。 默认情况下， **_utimbuf** 默认使用64位时间类型，除非已定义 **_USE_32BIT_TIME_T** 。

**_utime** 与 **_futime** 相同，不同之处在于 **_utime** 的 *filename* 参数是文件的文件名或路径，而不是打开文件的文件描述符。

**_wutime** 是 **_utime** 的宽字符版本;**_wutime** 的 *filename* 参数是宽字符字符串。 否则这些函数具有相同行为。

默认情况下，此函数的全局状态的作用域限定为应用程序。 若要更改此项，请参阅 [CRT 中的全局状态](../global-state.md)。

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tutime**|**_utime**|**_utime**|**_wutime**|
|**_tutime32**|**_utime32**|**_utime32**|**_wutime32**|
|**_tutime64**|**_utime64**|**_utime64**|**_wutime64**|

## <a name="requirements"></a>要求

|例程所返回的值|必需标头|可选标头|
|-------------|----------------------|----------------------|
|**_utime**、 **_utime32** **_utime64**|\<sys/utime.h>|\<errno.h>|
|**_utime64**|\<sys/utime.h>|\<errno.h>|
|**_wutime**|\<utime.h> 或 \<wchar.h>|\<errno.h>|

有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

此程序使用 **_utime** 将文件修改时间设置为当前时间。

```C
// crt_utime.c
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/utime.h>
#include <time.h>

int main( void )
{
   struct tm tma = {0}, tmm = {0};
   struct _utimbuf ut;

   // Fill out the accessed time structure
   tma.tm_hour = 12;
   tma.tm_isdst = 0;
   tma.tm_mday = 15;
   tma.tm_min = 0;
   tma.tm_mon = 0;
   tma.tm_sec = 0;
   tma.tm_year = 103;

   // Fill out the modified time structure
   tmm.tm_hour = 12;
   tmm.tm_isdst = 0;
   tmm.tm_mday = 15;
   tmm.tm_min = 0;
   tmm.tm_mon = 0;
   tmm.tm_sec = 0;
   tmm.tm_year = 102;

   // Convert tm to time_t
   ut.actime = mktime(&tma);
   ut.modtime = mktime(&tmm);

   // Show file time before and after
   system( "dir crt_utime.c" );
   if( _utime( "crt_utime.c", &ut ) == -1 )
      perror( "_utime failed\n" );
   else
      printf( "File time modified\n" );
   system( "dir crt_utime.c" );
}
```

### <a name="sample-output"></a>示例输出

```Output
Volume in drive C has no label.
Volume Serial Number is 9CAC-DE74

Directory of C:\test

01/09/2003  05:38 PM               935 crt_utime.c
               1 File(s)            935 bytes
               0 Dir(s)  20,742,955,008 bytes free
File time modified
Volume in drive C has no label.
Volume Serial Number is 9CAC-DE74

Directory of C:\test

01/15/2002  12:00 PM               935 crt_utime.c
               1 File(s)            935 bytes
               0 Dir(s)  20,742,955,008 bytes free
```

## <a name="see-also"></a>另请参阅

[时间管理](../../c-runtime-library/time-management.md)<br/>
[asctime、_wasctime](asctime-wasctime.md)<br/>
[ctime, _ctime32, _ctime64, _wctime, _wctime32, _wctime64](ctime-ctime32-ctime64-wctime-wctime32-wctime64.md)<br/>
[_fstat、_fstat32、_fstat64、_fstati64、_fstat32i64、_fstat64i32](fstat-fstat32-fstat64-fstati64-fstat32i64-fstat64i32.md)<br/>
[_ftime, _ftime32, _ftime64](ftime-ftime32-ftime64.md)<br/>
[_futime、_futime32、_futime64](futime-futime32-futime64.md)<br/>
[gmtime、_gmtime32、_gmtime64](gmtime-gmtime32-gmtime64.md)<br/>
[localtime、_localtime32、_localtime64](localtime-localtime32-localtime64.md)<br/>
[_stat、_wstat 函数](stat-functions.md)<br/>
[time、_time32、_time64](time-time32-time64.md)<br/>
