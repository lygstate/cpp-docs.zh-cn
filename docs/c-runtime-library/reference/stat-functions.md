---
description: 了解详细信息： _stat、_stat32、_stat64、_stati64、_stat32i64、_stat64i32、_wstat、_wstat32、_wstat64、_wstati64、_wstat32i64、_wstat64i32
title: _stat、_stat32、_stat64、_stati64、_stat32i64、_stat64i32、_wstat、_wstat32、_wstat64、_wstati64、_wstat32i64、_wstat64i32
ms.date: 4/2/2020
api_name:
- _wstat64
- _stati64
- _stat32
- _stat32i64
- _stat
- _wstati64
- _wstat32
- _wstat64i32
- _wstat
- _stat64
- _stat64i32
- _wstat32i64
- _o__stat32
- _o__stat32i64
- _o__stat64
- _o__stat64i32
- _o__wstat32
- _o__wstat32i64
- _o__wstat64
- _o__wstat64i32
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
- api-ms-win-crt-filesystem-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- tstat32
- tstat
- _tstat64i32
- tstati64
- _wstat64
- _wstat32
- wstati64
- tstat64
- _stati64
- _wstat
- wstat64i32
- stat32i64
- tstat32i64
- _tstat
- _wstati64
- _tstati64
- _wstat32i64
- wstat32
- _wstat64i32
- _stat
- _tstat32
- stat64i32
- wstat64
- stat
- _stat32i64
- _stat32
- stati64
- wstat
- _stat64i32
- stat32
- _tstat32i64
- tstat64i32
- _tstat64
- _stat64
- stat/_stat
- stat/_stat32
- stat/_stat64
- stat/_stati64
- stat/_stat32i64
- stat/_stat64i32
- stat/_wstat
- stat/_wstat32
- stat/_wstat64
- stat/_wstati64
- stat/_wstat32i64
- stat/_wstat64i32
helpviewer_keywords:
- files [C++], status information
- _stat function
- _wstat function
- _stat64i32 function
- tstat function
- _tstat64i32 function
- _stati64 function
- _stat64 function
- tstati64 function
- wstati64 function
- wstat64 function
- _wstat64i32 function
- _tstat32i64 function
- _stat32i64 function
- stat function
- status of files
- _tstat32 function
- tstat64 function
- _wstat64 function
- _tstat function
- _stat32 function
- wstat function
- _wstat32i64 function
- _tstati64 function
- _wstat32 function
- stat64 function
- stati64 function
- _wstati64 function
- _tstat64 function
- files [C++], getting status information
ms.assetid: 99a75ae6-ff26-47ad-af70-5ea7e17226a5
ms.openlocfilehash: 572e1d5f2f1c4eadf5f78c696c78630b84b90791
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099217"
---
# <a name="_stat-_stat32-_stat64-_stati64-_stat32i64-_stat64i32-_wstat-_wstat32-_wstat64-_wstati64-_wstat32i64-_wstat64i32"></a>_stat、_stat32、_stat64、_stati64、_stat32i64、_stat64i32、_wstat、_wstat32、_wstat64、_wstati64、_wstat32i64、_wstat64i32

获取文件状态信息。

## <a name="syntax"></a>语法

```C
int _stat(
   const char *path,
   struct _stat *buffer
);
int _stat32(
   const char *path,
   struct __stat32 *buffer
);
int _stat64(
   const char *path,
   struct __stat64 *buffer
);
int _stati64(
   const char *path,
   struct _stati64 *buffer
);
int _stat32i64(
   const char *path,
   struct _stat32i64 *buffer
);
int _stat64i32(
   const char *path,
   struct _stat64i32 *buffer
);
int _wstat(
   const wchar_t *path,
   struct _stat *buffer
);
int _wstat32(
   const wchar_t *path,
   struct __stat32 *buffer
);
int _wstat64(
   const wchar_t *path,
   struct __stat64 *buffer
);
int _wstati64(
   const wchar_t *path,
   struct _stati64 *buffer
);
int _wstat32i64(
   const wchar_t *path,
   struct _stat32i64 *buffer
);
int _wstat64i32(
   const wchar_t *path,
   struct _stat64i32 *buffer
);
```

### <a name="parameters"></a>参数

*路径*<br/>
指向字符串的指针，该字符串包含现有文件或目录的路径。

*宽限*<br/>
指向存储结果的结构的指针。

## <a name="return-value"></a>返回值

如果获取到文件状态信息，则这些函数将返回 0。 返回值-1 表示错误，在这种情况下， **errno** 设置为 **ENOENT**，指示找不到文件名或路径。 **EINVAL** 的返回值指示无效参数;在这种情况下， **errno** 也设置为 **EINVAL** 。

关于此代码以及其他返回代码的详细信息，请参阅 [_doserrno, errno, _sys_errlist, and _sys_nerr](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md) 。

如果文件的日期戳晚于1970年1月1日午夜、23:59:59 到12月 3000 31 日之前的日期戳，则为，除非你使用 **_stat32** 或 **_wstat32**，或者定义了 **_USE_32BIT_TIME_T**，在这种情况下，日期只能在年1月 2038 18 日23:59:59 之前表示。

## <a name="remarks"></a>注解

**_Stat** 函数获取有关 *路径* 指定的文件或目录的信息，并将其存储在 *缓冲区* 指向的结构中。 **_stat** 会根据需要自动处理多字节字符串参数，根据当前使用的多字节代码页识别多字节字符序列。

**_wstat** 是 **_stat** 的宽字符版本;**_wstat** 的 *path* 参数是宽字符字符串。 **_wstat** 和 **_stat** 的行为相同，只是 **_wstat** 不处理多字节字符字符串。

这些函数的变体支持 32 位或 64 位时间类型以及 32 位或 64 位文件长度。 第一个数字后缀 (**32** 或 **64**) 指示所用时间类型的大小;第二个后缀是 **i32** 或 **i64**，指示文件大小是否表示为32位或64位整数。

**_stat** 等效于 **_stat64i32**， **`struct`** **_stat** 包含64位时间。 除非定义 **_USE_32BIT_TIME_T** ，这种情况下旧行为有效; **_stat** 使用32位时间， **`struct`** **_stat** 包含32位时间。 **_Stati64** 也是如此。

> [!NOTE]
> **_wstat** 不适用于 Windows Vista 符号链接。 在这些情况下， **_wstat** 将始终报告文件大小为0。 **_stat** 可以正常使用符号链接。

此函数验证其参数。 如果 *路径* 或 *缓冲区* 为 **NULL**，则将调用无效参数处理程序，如 [参数验证](../../c-runtime-library/parameter-validation.md)中所述。

默认情况下，此函数的全局状态的作用域限定为应用程序。 若要更改此项，请参阅 [CRT 中的全局状态](../global-state.md)。

### <a name="time-type-and-file-length-type-variations-of-_stat"></a>_stat 时间类型和文件长度类型变体

|函数|已定义 _USE_32BIT_TIME_T？|时间类型|文件长度类型|
|---------------|------------------------------------|---------------|----------------------|
|**_stat**， **_wstat**|未定义|64 位|32 位|
|**_stat**， **_wstat**|已定义|32 位|32 位|
|**_stat32**， **_wstat32**|不受宏定义影响|32 位|32 位|
|**_stat64**， **_wstat64**|不受宏定义影响|64 位|64 位|
|**_stati64**， **_wstati64**|未定义|64 位|64 位|
|**_stati64**， **_wstati64**|已定义|32 位|64 位|
|**_stat32i64**， **_wstat32i64**|不受宏定义影响|32 位|64 位|
|**_stat64i32**， **_wstat64i32**|不受宏定义影响|64 位|32 位|

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|------------------------------------|--------------------|-----------------------|
|**_tstat**|**_stat**|**_stat**|**_wstat**|
|**_tstat64**|**_stat64**|**_stat64**|**_wstat64**|
|**_tstati64**|**_stati64**|**_stati64**|**_wstati64**|
|**_tstat32i64**|**_stat32i64**|**_stat32i64**|**_wstat32i64**|
|**_tstat64i32**|**_stat64i32**|**_stat64i32**|**_wstat64i32**|

在 SYS\STAT. 中定义的 **_stat** 结构H 包含以下字段。

|字段|说明|
|-|-|
| **st_gid** | 拥有此文件的组的数字标识符（针对 UNIX）。在 Windows 系统上此字段始终为 0。 重定向的文件分类为 Windows 文件。 |
| **st_atime** | 上次访问文件的时间。 在 NTFS 上有效，但在 FAT 格式的磁盘驱动器上无效。 |
| **st_ctime** | 文件的创建时间。 在 NTFS 上有效，但在 FAT 格式的磁盘驱动器上无效。 |
| **st_dev** | 包含文件的磁盘的驱动器号 (与 **st_rdev**) 相同。 |
| **st_ino** | 信息节点的数目 ( (特定于 UNIX 的) 中的文件的 **inode**) 。 在 UNIX 文件系统上， **inode** 描述文件日期和时间戳、权限和内容。 当文件硬链接到另一文件时，它们共享相同的 **inode**。 **St_ino**， **inode** 在 FAT、HPFS 或 NTFS 文件系统中没有任何意义。 |
| **st_mode** | 文件模式信息的位掩码。 如果 *路径* 指定目录，则设置 **_S_IFDIR** 位;如果 *path* 指定普通文件或设备，则设置 **_S_IFREG** 位。 根据文件的权限模式设置用户读/写位；根据文件扩展名设置用户执行位。 |
| **st_mtime** | 上次修改文件的时间。 |
| **st_nlink** | 在非 NTFS 文件系统上始终为 1。 |
| **st_rdev** | 包含文件的磁盘的驱动器号 (与 **st_dev**) 相同。 |
| **st_size** | 文件大小（以字节为单位）; **i64** 后缀的变体的64位整数。 |
| **st_uid** | 拥有文件的用户的数字标识符（针对 UNIX）。 此字段在 Windows 系统上始终为 0。 重定向的文件分类为 Windows 文件。 |

如果 *path* 引用设备，则 **_stat** 结构中的 **st_size**、各种时间字段、 **st_dev** 和 **st_rdev** 字段没有意义。 因为 STAT.H 使用 TYPES.H 中定义的 [_dev_t](../../c-runtime-library/standard-types.md) 类型，所以必须在代码中的 STAT.H 之前包含 TYPES.H。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|可选标头|
|-------------|---------------------|----------------------|
|**_stat**、 **_stat32**、 **_stat64**、 **_stati64**、 **_stat32i64**、 **_stat64i32**|\<sys/types.h> 后跟 \<sys/stat.h>|\<errno.h>|
|**_wstat**、 **_wstat32**、 **_wstat64**、 **_wstati64**、 **_wstat32i64**、 **_wstat64i32**|\<sys/types.h> 后跟 \<sys/stat.h> 或 \<wchar.h>|\<errno.h>|

有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_stat.c
// This program uses the _stat function to
// report information about the file named crt_stat.c.

#include <time.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <stdio.h>
#include <errno.h>

int main( void )
{
   struct _stat buf;
   int result;
   char timebuf[26];
   char* filename = "crt_stat.c";
   errno_t err;

   // Get data associated with "crt_stat.c":
   result = _stat( filename, &buf );

   // Check if statistics are valid:
   if( result != 0 )
   {
      perror( "Problem getting information" );
      switch (errno)
      {
         case ENOENT:
           printf("File %s not found.\n", filename);
           break;
         case EINVAL:
           printf("Invalid parameter to _stat.\n");
           break;
         default:
           /* Should never be reached. */
           printf("Unexpected error in _stat.\n");
      }
   }
   else
   {
      // Output some of the statistics:
      printf( "File size     : %ld\n", buf.st_size );
      printf( "Drive         : %c:\n", buf.st_dev + 'A' );
      err = ctime_s(timebuf, 26, &buf.st_mtime);
      if (err)
      {
         printf("Invalid arguments to ctime_s.");
         exit(1);
      }
      printf( "Time modified : %s", timebuf );
   }
}
```

```Output
File size     : 732
Drive         : C:
Time modified : Thu Feb 07 14:39:36 2002
```

## <a name="see-also"></a>另请参阅

[文件处理](../../c-runtime-library/file-handling.md)<br/>
[_access、_waccess](access-waccess.md)<br/>
[_fstat、_fstat32、_fstat64、_fstati64、_fstat32i64、_fstat64i32](fstat-fstat32-fstat64-fstati64-fstat32i64-fstat64i32.md)<br/>
[_getmbcp](getmbcp.md)<br/>
[_setmbcp](setmbcp.md)<br/>
