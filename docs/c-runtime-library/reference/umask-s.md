---
description: 了解详细信息： _umask_s
title: _umask_s
ms.date: 4/2/2020
api_name:
- _umask_s
- _o__umask_s
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
- unmask_s
- _umask_s
helpviewer_keywords:
- masks, file-permission-setting
- _umask_s function
- masks
- file permissions [C++]
- umask_s function
- files [C++], permission settings for
ms.assetid: 70898f61-bf2b-4d8d-8291-0ccaa6d33145
ms.openlocfilehash: 8a87d924073d5e13d8c5ce0377276cf10a9e0798
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099308"
---
# <a name="_umask_s"></a>_umask_s

设置默认的文件权限掩码。 这是 [_umask](umask.md) 版本，具有 [CRT 中的安全性功能](../../c-runtime-library/security-features-in-the-crt.md)中所述的安全性增强功能。

## <a name="syntax"></a>语法

```C
errno_t _umask_s(
   int mode,
   int * pOldMode
);
```

### <a name="parameters"></a>参数

*mode*<br/>
默认权限设置。

*pOldMode*<br/>
权限设置的上一个值。

## <a name="return-value"></a>返回值

如果 *mode* 未指定有效模式或 *POldMode* 指针为 **NULL**，则返回错误代码。

### <a name="error-conditions"></a>错误条件

|*mode*|*pOldMode*|返回值|*POldMode* 的内容|
|------------|----------------|----------------------|--------------------------------|
|any|**NULL**|**EINVAL**|未修改|
|无效模式|any|**EINVAL**|未修改|

发生上述情况中的任何一个，都会调用无效参数处理程序，如[参数验证](../../c-runtime-library/parameter-validation.md)中所述。 如果允许继续执行， **_umask_s** 将返回 **EINVAL** ，并将 **errno** 设置为 **EINVAL**。

## <a name="remarks"></a>注解

**_Umask_s** 函数将当前进程的文件权限掩码设置为 *mode* 指定的模式。 文件权限掩码修改 **_creat**、 **_open** 或 **_sopen** 创建的新文件的权限设置。 如果掩码中的一位是 1，则将文件的请求权限值中相应的一位设置为 0 (不允许)。 如果掩码中的一位是 0，则相应的一位保留不变。 直至首次关闭新文件时才会设置新文件的权限设置。

整数表达式 *pmode* 包含在 SYS\STAT. 中定义的以下一个或两个清单常量。高

|*pmode*|说明|
|-|-|
|**_S_IWRITE**|允许写入。|
|**_S_IREAD**|允许读取。|
|**_S_IREAD** \|**_S_IWRITE**|允许读取和写入。|

当同时提供两个常量时，它们将与按位 "或" 运算符联接 ( **|** ) 。 如果 _S_IREAD *模式* 参数， 则不允许读取 (文件是只写) 。 如果 _S_IWRITE *模式* 参数， 则不允许写入 (文件为只读) 。 例如，如果掩码中设置了写入位，则任何新文件都将为只读。 请注意在 MS-DOS 和 Windows 操作系统下，所有文件均可读；不可能提供只写权限。 因此，将读取位设置 **_umask_s** 不会影响文件的模式。

如果 *pmode* 不是清单常量之一的组合或包含一组备用常量，则该函数将直接忽略这些常量。

默认情况下，此函数的全局状态的作用域限定为应用程序。 若要更改此项，请参阅 [CRT 中的全局状态](../global-state.md)。

## <a name="requirements"></a>要求

|例程所返回的值|必需的标头|
|-------------|---------------------|
|**_umask_s**|\<io.h> and \<sys/stat.h> 和 \<sys/types.h>|

有关其他兼容性信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="example"></a>示例

```C
// crt_umask_s.c
/* This program uses _umask_s to set
* the file-permission mask so that all future
* files will be created as read-only files.
* It also displays the old mask.
*/

#include <sys/stat.h>
#include <sys/types.h>
#include <io.h>
#include <stdio.h>

int main( void )
{
   int oldmask, err;

   /* Create read-only files: */
   err = _umask_s( _S_IWRITE, &oldmask );
   if (err)
   {
      printf("Error setting the umask.\n");
      exit(1);
   }
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
[_umask](umask.md)<br/>
