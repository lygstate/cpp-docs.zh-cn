---
title: _umask
description: _Umask 的 API 参考;这会设置默认的文件权限掩码。
ms.date: 4/2/2020
api_name:
- _umask
- _o__umask
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
- _umask
helpviewer_keywords:
- masks, file-permission-setting
- _umask function
- masks
- umask function
- file permissions [C++]
- files [C++], permission settings for
ms.assetid: 5e9a13ba-5321-4536-8721-6afb6f4c8483
ms.openlocfilehash: 8923e2a9ef489d35d1e7f55b91bfb632c0d22580
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099295"
---
# <a name="_umask"></a>_umask

设置默认的文件权限掩码。 有关此函数的更安全版本，请参阅 [_umask_s](umask-s.md) 。

## <a name="syntax"></a>语法

```C
int _umask( int pmode );
```

### <a name="parameters"></a>参数

*pmode*<br/>
默认权限设置。

## <a name="return-value"></a>返回值

**_umask** 返回 *pmode* 以前的值。 无错误返回。

## <a name="remarks"></a>注解

**_Umask** 函数将当前进程的文件权限掩码设置为 *pmode* 指定的模式。 文件权限掩码修改 **_creat**、 **_open** 或 **_sopen** 创建的新文件的权限设置。 如果掩码中的一位是 1，则将文件的请求权限值中相应的一位设置为 0 (不允许)。 如果掩码中的一位是 0，则相应的一位保留不变。 直至首次关闭新文件时才会设置新文件的权限设置。

整数表达式 *pmode* 包含在 SYS\STAT. 中定义的以下一个或两个清单常量。高

|*pmode*|说明|
|-|-|
| **_S_IWRITE** | 允许写入。 |
| **_S_IREAD** | 允许读取。 |
| **_S_IREAD** &#124; **_S_IWRITE** | 允许读取和写入。 |

当同时提供两个常量时，它们将与按位 "或" 运算符联接 ( **&#124;** ) 。 如果 _S_IREAD *pmode* 参数， 则不允许读取 (文件是只写) 。 如果 _S_IWRITE *pmode* 参数， 则不允许写入 (文件为只读) 。 例如，如果掩码中设置了写入位，则任何新文件都将为只读。 请注意在 MS-DOS 和 Windows 操作系统下，所有文件均可读；不可能提供只写权限。 因此，将读取位设置 **_umask** 不会影响文件的模式。

如果 *pmode* 不是清单常量之一的组合或包含一组备用常量，则该函数将直接忽略这些常量。

默认情况下，此函数的全局状态的作用域限定为应用程序。 若要更改此项，请参阅 [CRT 中的全局状态](../global-state.md)。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**_umask**|\<io.h>, \<sys/stat.h>, \<sys/types.h>|

有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="libraries"></a>库

[C 运行时库](../../c-runtime-library/crt-library-features.md)的所有版本。

## <a name="example"></a>示例

```C
// crt_umask.c
// compile with: /W3
// This program uses _umask to set
// the file-permission mask so that all future
// files will be created as read-only files.
// It also displays the old mask.
#include <sys/stat.h>
#include <sys/types.h>
#include <io.h>
#include <stdio.h>

int main( void )
{
   int oldmask;

   /* Create read-only files: */
   oldmask = _umask( _S_IWRITE ); // C4996
   // Note: _umask is deprecated; consider using _umask_s instead
   printf( "Oldmask = 0x%.4x\n", oldmask );
}
```

```Output
Oldmask = 0x0000
```

## <a name="see-also"></a>另请参阅

[文件处理](../../c-runtime-library/file-handling.md)<br/>
[低级别 i/o](../../c-runtime-library/low-level-i-o.md)<br/>
[_chmod、_wchmod](chmod-wchmod.md)<br/>
[_creat、_wcreat](creat-wcreat.md)<br/>
[_mkdir、_wmkdir](mkdir-wmkdir.md)<br/>
[_open、_wopen](open-wopen.md)<br/>
