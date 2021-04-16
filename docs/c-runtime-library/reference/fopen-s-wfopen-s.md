---
title: fopen_s、_wfopen_s
description: 介绍用于和的 API `fopen_s``_wfopen_s`
ms.date: 2/24/2021
api_name:
- _wfopen_s
- fopen_s
- _o__wfopen_s
- _o_fopen_s
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
- api-ms-win-crt-stdio-l1-1-0.dll
- api-ms-win-crt-private-l1-1-0.dll
api_type:
- DLLExport
topic_type:
- apiref
f1_keywords:
- fopen_s
- _tfopen_s
- _wfopen_s
helpviewer_keywords:
- _wfopen_s function
- opening files, for file I/O
- _tfopen_s function
- tfopen_s function
- wfopen_s function
- fopen_s function
- Unicode [C++], creating files
- Unicode [C++], writing files
- files [C++], opening
- Unicode [C++], files
ms.openlocfilehash: e3526df036711d7c6319dfa582dcefcf7b7d0818
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539794"
---
# <a name="fopen_s-_wfopen_s"></a>`fopen_s`, `_wfopen_s`

打开文件。 [ `fopen` 的 `_wfopen` 这些版本具有安全性增强功能，如](fopen-wfopen.md) [CRT 中的安全功能](../../c-runtime-library/security-features-in-the-crt.md)中所述。

## <a name="syntax"></a>语法

```C
errno_t fopen_s(
   FILE** pFile,
   const char *filename,
   const char *mode
);
errno_t _wfopen_s(
   FILE** pFile,
   const wchar_t *filename,
   const wchar_t *mode
);
```

### <a name="parameters"></a>参数

*`pFile`*\
指向文件指针的指针，文件指针将接收指向已打开文件的指针。

*`filename`*\
文件名。

*`mode`*\
允许的访问类型。

## <a name="return-value"></a>返回值

如果成功，则为零；如果失败，则为错误代码。 有关这些错误代码的详细信息，请参阅[ `errno` 、、 `_doserrno` `_sys_errlist` 和 `_sys_nerr` ](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

### <a name="error-conditions"></a>错误条件

|*`pFile`*|*`filename`*|*`mode`*|返回值|内容 *`pFile`*|
|-------------|----------------|------------|------------------|------------------------|
|**`NULL`**|any|any|**`EINVAL`**|未更改|
|any|**`NULL`**|any|**`EINVAL`**|未更改|
|any|any|**`NULL`**|**`EINVAL`**|未更改|

## <a name="remarks"></a>注解

由打开 **`fopen_s`** 且 **`_wfopen_s`** 不能共享的文件。 如果要求文件可共享，请使用 [ `_fsopen` ， `_wfsopen`](fsopen-wfsopen.md)并使用适当的共享模式常量（例如 **`_SH_DENYNO`** 用于读/写共享）。

**`fopen_s`** 函数打开 *文件名* 指定的文件。 **`_wfopen_s`** 是的宽字符版本 **`fopen_s`** ; 的参数 **`_wfopen_s`** 是宽字符字符串。 **`_wfopen_s`** 和的 **`fopen_s`** 行为方式相同。

**`fopen_s`** 接受执行时在文件系统上有效的路径; **`fopen_s`** 只要执行代码的系统在执行时能够访问共享或映射的网络驱动器，则会接受 UNC 路径和包含映射的网络驱动器的路径。 为构造路径时 **`fopen_s`** ，不要对执行环境中驱动器、路径或网络共享的可用性进行假设。 可使用斜杠 (/) 或反斜杠 (\\) 作为路径中的目录分隔符。

这些函数验证其参数。 如果 *`pFile`* 、 *`filename`* 或 *`mode`* 为 null 指针，则这些函数将生成无效的参数异常，如 [参数验证](../../c-runtime-library/parameter-validation.md)中所述。

在对文件执行任何进一步操作之前，请始终检查返回值以查看函数是否成功。 如果发生错误，将返回错误代码并设置全局变量 **`errno`** 。 有关详细信息，请参阅[ `errno` 、、 `_doserrno` `_sys_errlist` 和 `_sys_nerr` ](../../c-runtime-library/errno-doserrno-sys-errlist-and-sys-nerr.md)。

默认情况下，此函数的全局状态的作用域限定为应用程序。 若要更改此项，请参阅 [CRT 中的全局状态](../global-state.md)。

## <a name="unicode-support"></a>Unicode 支持

**`fopen_s`** 支持 Unicode 文件流。 若要打开新的或现有的 Unicode 文件，请将指定所需编码的 *ccs* 标志传递给 **`fopen_s`** ：

**`fopen_s(&fp, "newfile.txt", "rw, ccs=**_encoding_**");`**

允许的 *编码* 值为 **`UNICODE`** 、 **`UTF-8`** 和 **`UTF-16LE`** 。 如果没有为指定值，将 *`encoding`* **`fopen_s`** 使用 ANSI 编码。

如果文件已存在并已打开以进行读取或追加，则字节顺序标记 (BOM)（如果文件中存在）将确定编码。 BOM 编码优先于标志指定的编码 *`ccs`* 。 *`ccs`* 仅在不存在 BOM 或文件是新文件时，才使用编码。

> [!NOTE]
> BOM 检测仅适用于在 Unicode 模式下打开的文件;也就是说，传递 *`ccs`* 标志。

下表汇总了为指定的各种 *`ccs`* 标志的模式 **`fopen_s`** 以及文件中的字节顺序标记。

### <a name="encodings-used-based-on-ccs-flag-and-bom"></a>基于 ccs 标志和 BOM 使用的编码

|ccs 标志|无 BOM（或新文件）|BOM：UTF-8|BOM：UTF-16|
|----------------|----------------------------|-----------------|------------------|
|**`UNICODE`**|**`UTF-16LE`**|**`UTF-8`**|**`UTF-16LE`**|
|**`UTF-8`**|**`UTF-8`**|**`UTF-8`**|**`UTF-16LE`**|
|**`UTF-16LE`**|**`UTF-16LE`**|**`UTF-8`**|**`UTF-16LE`**|

在 Unicode 模式下打开用于写入的文件将自动在其中写入 BOM。

如果 *`mode`* 是 **`"a, ccs=` 编码 `"`**， **`fopen_s`** 首先会尝试打开具有读取访问权限和写入访问权限的文件。 如果成功，此函数将读取 BOM 以确定文件的编码；如果失败，此函数将使用文件的默认编码。 在任一情况下，都将 **`fopen_s`** 使用只写访问权限重新打开文件。  (仅适用于 **`a`** 模式，而不是 **`a+`** 。 ) 

### <a name="generic-text-routine-mappings"></a>一般文本例程映射

|TCHAR.H 例程|未定义 _UNICODE 和 _MBCS|已定义 _MBCS|已定义 _UNICODE|
|---------------------|------------------------------------|--------------------|-----------------------|
|**`_tfopen_s`**|**`fopen_s`**|**`fopen_s`**|**`_wfopen_s`**|

字符串指定为 *`mode`* 文件请求的访问类型，如下所示。

|*`mode`*|Access|
|-|-|
| **`"r"`** | 打开以便读取。 如果文件不存在或找不到，调用将 **`fopen_s`** 失败。 |
| **`"w"`** | 打开用于写入的空文件。 如果给定文件存在，则其内容会被销毁。 |
| **`"a"`** | 在文件末尾打开以进行写入（追加），在新数据写入到文件之前不移除文件末尾 (EOF) 标记。 如果文件不存在，则创建文件。 |
| **`"r+"`** | 打开以便读取和写入。 文件必须存在。 |
| **"w +"** | 打开用于读取和写入的空文件。 如果文件存在，则其内容会被销毁。 |
| **`"a+"`** | 打开以进行读取和追加。 追加操作包括在新数据写入文件之前移除 EOF 标记。 写入完成后，EOF 标记不会还原。 如果文件不存在，则创建文件。 |

使用 **`"a"`** 或访问类型打开文件时 **`"a+"`** ，所有写入操作都将在文件末尾进行。 可以使用或重定位文件指针 [`fseek`](fseek-fseeki64.md) [`rewind`](rewind.md) ，但在执行任何写入操作之前，将始终将其移回文件末尾，以便不会覆盖现有数据。

在 **`"a"`** 追加到文件之前，模式不会删除 EOF 标记。 在追加后，MS-DOS `TYPE` 命令只显示原始 EOF 标记中的数据，而不显示追加到文件的任何数据。 **`"a+"`** 模式会在将 EOF 标记追加到文件之前将其删除。 追加后，MS-DOS `TYPE` 命令显示文件中的所有数据。 **`"a+"`** 若要追加到以 **CTRL** + **Z** EOF 标记终止的流文件，则需要模式。

**`"r+"`** **`"w+"`** 指定、或 **`"a+"`** 访问类型时，允许读取和写入。  (该文件被称为 "更新"。 ) 不过，当你从读取切换到写入时，输入操作必须跨越 EOF 标记。 如果没有 EOF 标记，则必须使用对文件定位函数的干预调用。 文件定位函数是 **`fsetpos`** 、 [`fseek`](fseek-fseeki64.md) 和 [`rewind`](rewind.md) 。 当从写入切换到读取时，必须使用对 **`fflush`** 或文件定位函数的干预调用。

从 C11 开始， **`"x"`** 如果文件存在，你可以将添加到 **`"w"`** 或 **`"w+"`** 以导致函数失败，而不是覆盖它。

除了以上值之外，还可以在中包含以下字符 *`mode`* 以指定换行符的转换模式：

|*`mode`* 组合键|转换模式|
|-|-|
| **`t`** | 在文本（转换）模式下打开。 |
| **`b`** | 在二进制 (未翻译的) 模式下打开;将禁止涉及回车符和换行符的翻译。 |

在文本 (平移) 模式下，在输入时将 **CTRL** + **Z** 解释为文件尾字符。 在使用打开以进行读取/写入的文件中 **`"a+"`** ， **`fopen_s`** 将检查文件末尾的 **CTRL +** + **Z** 并将其删除（如果可能）。 这是因为使用 [`fseek`](fseek-fseeki64.md) 和 **`ftell`** 在以 **CTRL** Z 结尾的文件中移动时 + ，可能会导致 [`fseek`](fseek-fseeki64.md) 在文件末尾附近运行不当。

此外，在文本模式中，回车符/换行符的组合在输入时转换为单行馈送，换行符转换为输出时的回车换行符组合。 当 Unicode 流 I/O 函数在文本模式（默认设置）下运行时，源或目标流将假定为一系列多字节字符。 Unicode 流输入函数将多字节字符转换为宽字符 (就像通过调用 **`mbtowc`** 函数) 。 出于同一原因，Unicode 流输出函数将宽字符转换为多字节字符， (就像通过调用 **`wctomb`** 函数) 。

如果 **`t`** **`b`** 在中未指定或 *`mode`* ，则默认转换模式由全局变量 [_fmode](../../c-runtime-library/fmode.md)定义。 如果 **`t`** 或 **`b`** 是参数的前缀，则函数将失败并返回 **`NULL`** 。

有关在 Unicode 和多字节流 I/O 中使用文本和二进制模式的详细信息，请参阅[文本和二进制模式文件 I/O](../../c-runtime-library/text-and-binary-mode-file-i-o.md) 和[文本和二进制模式下的 Unicode 流 I/O](../../c-runtime-library/unicode-stream-i-o-in-text-and-binary-modes.md)。

|*`mode`* 组合键|行为|
|-|-|
| **`c`** | 启用关联 *文件名* 的提交标志，以便在 **`fflush`** 调用或时将文件缓冲区的内容直接写入磁盘 **`_flushall`** 。 |
| **`n`** | 将关联的 *文件名* 的提交标志重置为 "无提交"。 这是默认值。 如果将程序显式链接到 COMMODE.OBJ，它还将重写全局提交标志。 除非将程序显式链接到 COMMODE.OBJ，否则全局提交标志默认为“no-commit”（请参阅 [Link Options](../../c-runtime-library/link-options.md)）。 |
| **`n`** | 指定文件不由子进程继承。 |
| **`S`** | 指定缓存针对（但不限于）从磁盘的顺序访问进行优化。 |
| **`R`** | 指定缓存针对（但不限于）从磁盘的随机访问进行优化。 |
| **`t`** | 将文件指定为临时。 如果可能，它不会刷新到磁盘。 |
| **`D`** | 将文件指定为临时。 当最后一个文件指针关闭时，它将被删除。 |
| **`ccs=`**_编码器_ | 指定要使用的编码字符集 **`UTF-8`** ， (**`UTF-16LE`** 该文件的、或 **`UNICODE`**) 之一。 如果需要 ANSI 编码，请不要指定此字符集。 |

和中使用的字符串的有效字符 *`mode`* **`fopen_s`** [`_fdopen`](fdopen-wfdopen.md) 与 *`oflag`* 和中使用的参数对应 [`_open`](open-wopen.md) ，如下所示 [`_sopen`](sopen-wsopen.md) 。

|字符串中的字符 *`mode`*|等效 *`oflag`* 值 `_open`/`_sopen`|
|-------------------------------|----------------------------------------------------|
|**`a`**|**`_O_WRONLY`** &#124; **`_O_APPEND`** (通常 **`_O_WRONLY`** &#124; **`_O_CREAT`** &#124; **`_O_APPEND`**) |
|**`a+`**|**`_O_RDWR`** &#124; **`_O_APPEND`** (通常 **`_O_RDWR`** &#124; **`_O_APPEND`** &#124; **`_O_CREAT`**) |
|**`R`**|**`_O_RDONLY`**|
|**`r+`**|**`_O_RDWR`**|
|**`w`**|**`_O_WRONLY`** (通常 **`_O_WRONLY`** &#124; **`_O_CREAT`** &#124; **_O_TRUNC**) |
|**`w+`**|**`_O_RDWR`** (通常 **`_O_RDWR`** &#124; **`_O_CREAT`** &#124; **_O_TRUNC**) |
|**`b`**|**`_O_BINARY`**|
|**`t`**|**`_O_TEXT`**|
|**`c`**|无|
|**`n`**|无|
|**`S`**|**`_O_SEQUENTIAL`**|
|**`R`**|**`_O_RANDOM`**|
|**`t`**|**`_O_SHORTLIVED`**|
|**`D`**|**`_O_TEMPORARY`**|
|**`ccs=UNICODE`**|**`_O_WTEXT`**|
|**`ccs=UTF-8`**|**`_O_UTF8`**|
|**`ccs=UTF-16LE`**|**`_O_UTF16`**|

如果你使用 **`rb`** 的是模式，如果不需要移植代码，则内存映射的 Win32 文件可能也是一个选项，你希望读取很多文件，或者不关心网络性能。

## <a name="requirements"></a>要求

|函数|必需的标头|
|--------------|---------------------|
|**`fopen_s`**|`<stdio.h>`|
|**`_wfopen_s`**|`<stdio.h>` 或 `<wchar.h>`|

有关兼容性的详细信息，请参阅[兼容性](../../c-runtime-library/compatibility.md)。

## <a name="libraries"></a>库

[C 运行时库](../../c-runtime-library/crt-library-features.md)的所有版本。

**`c`**、和 **`n`** **`t`** *`mode`* 选项是适用于和的 Microsoft 扩展，不 **`fopen_s`** 应在 [`_fdopen`](fdopen-wfdopen.md) 需要 ANSI 可移植性的地方使用。

## <a name="example"></a>示例

```C
// crt_fopen_s.c
// This program opens two files. It uses
// fclose to close the first file and
// _fcloseall to close all remaining files.

#include <stdio.h>

FILE *stream, *stream2;

int main( void )
{
   errno_t err;

   // Open for read (will fail if file "crt_fopen_s.c" doesn't exist)
   err  = fopen_s( &stream, "crt_fopen_s.c", "r" );
   if( err == 0 )
   {
      printf( "The file 'crt_fopen_s.c' was opened\n" );
   }
   else
   {
      printf( "The file 'crt_fopen_s.c' was not opened\n" );
   }

   // Open for write
   err = fopen_s( &stream2, "data2", "w+" );
   if( err == 0 )
   {
      printf( "The file 'data2' was opened\n" );
   }
   else
   {
      printf( "The file 'data2' was not opened\n" );
   }

   // Close stream if it isn't NULL
   if( stream )
   {
      err = fclose( stream );
      if ( err == 0 )
      {
         printf( "The file 'crt_fopen_s.c' was closed\n" );
      }
      else
      {
         printf( "The file 'crt_fopen_s.c' was not closed\n" );
      }
   }

   // All other files are closed:
   int numclosed = _fcloseall( );
   printf( "Number of files closed by _fcloseall: %u\n", numclosed );
}
```

```Output
The file 'crt_fopen_s.c' was opened
The file 'data2' was opened
Number of files closed by _fcloseall: 1
```

## <a name="see-also"></a>另请参阅

[流 i/o](../../c-runtime-library/stream-i-o.md)\
[`fclose`, `_fcloseall`](fclose-fcloseall.md)\
[`_fdopen`, `_wfdopen`](fdopen-wfdopen.md)\
[`ferror`](ferror.md)\
[`_fileno`](fileno.md)\
[`freopen`, `_wfreopen`](freopen-wfreopen.md)\
[`_open`, `_wopen`](open-wopen.md)\
[`_setmode`](setmode.md)
