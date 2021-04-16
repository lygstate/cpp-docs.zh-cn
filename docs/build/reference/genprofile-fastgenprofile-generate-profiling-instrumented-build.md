---
description: '了解详细信息：/GENPROFILE、/FASTGENPROFILE (生成分析检测的生成) '
title: /GENPROFILE, /FASTGENPROFILE（生成经分析检测的生成）
ms.date: 04/14/2021
f1_keywords:
- GENPROFILE
- FASTGENPROFILE
- /GENPROFILE
- /FASTGENPROFILE
helpviewer_keywords:
- GENPROFILE
- FASTGENPROFILE
ms.openlocfilehash: 3b966148525fc470d53e2af9052a666aa39d7d99
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539484"
---
# <a name="genprofile-fastgenprofile-generate-profiling-instrumented-build"></a>`/GENPROFILE`， `/FASTGENPROFILE` (生成分析检测的生成) 

*`.pgd`* 通过链接器指定文件的生成，以支持按配置文件优化 (PGO) 。 **`/GENPROFILE`** 和 **`/FASTGENPROFILE`** 使用不同的默认参数。 **`/GENPROFILE`** 在分析期间使用来优选速度和内存使用情况。 使用 **`/FASTGENPROFILE`** 来支持更小的内存使用情况和更快的精度。

## <a name="syntax"></a>语法

> **`/GENPROFILE`**\[**`:`**_`profile-argument`_\[**`,`**_`profile-argument`_ ...]]\
> **`/FASTGENPROFILE`**\[**`:`**_`profile-argument`_\[**`,`**_`profile-argument`_ ...]]\

> *`profile-argument`*\
> &emsp;{ **`COUNTER32`** &vert; **`COUNTER64`** }\
> &emsp;{ **`EXACT`** &vert; **`NOEXACT`** }\
> &emsp;**`MEMMAX=`**_负值_\
> &emsp;**`MEMMIN=`**_负值_\
> &emsp;{ **`PATH`** &vert; **`NOPATH`** }\
> &emsp;{ **`TRACKEH`** &vert; **`NOTRACKEH`** }\
> &emsp;**`PGD=`**_名字_

### <a name="arguments"></a>参数

*`profile-argument`* 可以将任何参数指定为 **`/GENPROFILE`** 或 **`/FASTGENPROFILE`** 。 此处列出的由管道字符分隔的参数 (**`|`**) 是互斥的。 使用逗号字符 (**`,`**) 分隔参数。 不要在参数、逗号或冒号之后 (**`:`**) 。

**`COUNTER32`** &vert; **`COUNTER64`**\
使用 **`COUNTER32`** 指定32位探测计数器的使用，并 **`COUNTER64`** 指定64位探测计数器。 指定时 **`/GENPROFILE`** ，默认值为 **`COUNTER64`** 。 指定时 **`/FASTGENPROFILE`** ，默认值为 **`COUNTER32`** 。

**`EXACT`** &vert; **`NOEXACT`**\
用于 **`EXACT`** 指定探测器的线程安全互锁增量。 **`NOEXACT`** 指定探测器的未受保护增量操作。 默认值为 **`NOEXACT`** 。

**`MEMMAX`**=*值*、 **`MEMMIN`** = *值*\
使用 **`MEMMAX`** 和 **`MEMMIN`** 指定在内存中训练数据的最大和最小预留大小。 该值为要保留的内存量（以字节为单位）。 默认情况下，这些值由内部启发式确定。

**`PATH`**  &vert; **`NOPATH`**\
使用 **`PATH`**  为函数的每个唯一路径指定一组单独的 PGO 计数器。 **`NOPATH`** 仅用于为每个函数指定一组计数器。 指定时 **`/GENPROFILE`** ，默认值为 **`PATH`** 。 指定时 **`/FASTGENPROFILE`** ，默认值为 **`NOPATH`** 。

**`TRACKEH`**  &vert; **`NOTRACKEH`**\
指定是否使用额外计数器以便在训练期间引发异常时保持准确计数。 用于为 **`TRACKEH`**  确切计数指定额外的计数器。 用于为 **`NOTRACKEH`**  不使用异常处理或在定型方案中不会遇到异常的代码指定单个计数器。  指定时 **`/GENPROFILE`** ，默认值为 **`TRACKEH`** 。 指定时 **`/FASTGENPROFILE`** ，默认值为 **`NOTRACKEH`** 。

**`PGD`**=*名字*\
指定文件的基文件名 *`.pgd`* 。 默认情况下，链接器使用带扩展名的基本可执行映像文件名 *`.pgd`* 。

## <a name="remarks"></a>注解

**`/GENPROFILE`** 和 **`/FASTGENPROFILE`** 选项通知链接器生成支持按配置优化 (PGO) 的应用程序定型所需的分析检测文件。 这些选项是 Visual Studio 2015 中的新增选项。 首选这些选项到不推荐使用的 **`/LTCG:PGINSTRUMENT`** 、 **`/PGD`** 、和 **`/POGOSAFEMODE`** 选项，以及 **`PogoSafeMode`** 、和 **`VCPROFILE_ALLOC_SCALE`** **`VCPROFILE_PATH`** 环境变量。 在生成过程中，应用程序定型生成的分析信息用作目标全程序优化的输入。 还可以设置其他选项来控制各种性能分析功能，以便在应用培训和生成期间提高性能。 指定的默认选项 **`/GENPROFILE`** 提供最准确的结果，尤其是对于大型的复杂多线程应用。 在 **`/FASTGENPROFILE`** 定型期间，选项使用不同的默认值来实现更低的内存占用量和更快的性能，代价是准确性。

使用创建后，当你运行已检测应用时，将捕获分析 **`/GENPROFILE`** 信息 **`/FASTGENPROFILE`** 。 当你指定 [`/USEPROFILE`](useprofile.md) 链接器选项来执行分析步骤，然后使用该选项来引导优化生成步骤时，将捕获此信息。 若要详细了解如何培训您的应用程序和有关所收集数据的详细信息，请参阅 [按配置文件优化](../profile-guided-optimizations.md)。

**`/LTCG`** 指定或时，始终 **`/GENPROFILE`** 指定 **`/FASTGENPROFILE`** 。

### <a name="to-set-this-linker-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此链接器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 选择“配置属性” > “链接器” > “命令行”属性页    。

1. **`/GENPROFILE`** **`/FASTGENPROFILE`** 在 "**附加选项**" 框中输入或选项和参数。 选择 **`OK`** 保存更改。

### <a name="to-set-this-linker-option-programmatically"></a>以编程方式设置此链接器选项

- 请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCLinkerTool.AdditionalOptions%2A>。

## <a name="see-also"></a>另请参阅

[MSVC 链接器参考](linking.md)\
[MSVC 链接器选项](linker-options.md)\
[`/LTCG` (的链接时间代码生成) ](ltcg-link-time-code-generation.md)
