---
title: ARM64 内部函数
description: Visual Studio 中 Microsoft c + + 编译器支持的 ARM64 内部函数的引用列表。
f1_keywords:
- __break
- __addx18byte
- __addx18word
- __addx18dword
- __addx18qword
- __cas8
- __cas16
- __cas32
- __cas64
- __casa8
- __casa16
- __casa32
- __casa64
- __casl8
- __casl16
- __casl32
- __casl64
- __casal8
- __casal16
- __casal32
- __casal64
- __crc32b
- __crc32h
- __crc32w
- __crc32d
- __crc32cb
- __crc32ch
- __crc32cw
- __crc32cd
- __getReg
- __getRegFp
- __getCallerReg
- __getCallerRegFp
- __hlt
- __incx18byte
- __incx18word
- __incx18dword
- __incx18qword
- __ldar8
- __ldar16
- __ldar32
- __ldar64
- __ldapr8
- __ldapr16
- __ldapr32
- __ldapr64
- __prefetch2
- __readx18byte
- __readx18word
- __readx18dword
- __readx18qword
- __setReg
- __setRegFp
- __setCallerReg
- __setCallerRegFp
- __stlr8
- __stlr16
- __stlr32
- __stlr64
- __swp8
- __swp16
- __swp32
- __swp64
- __swpa8
- __swpa16
- __swpa32
- __swpa64
- __swpl8
- __swpl16
- __swpl32
- __swpl64
- __swpal8
- __swpal16
- __swpal32
- __swpal64
- __sys
- __svc
- __writex18byte
- __writex18word
- __writex18dword
- __writex18qword
helpviewer_keywords:
- __break ARM64 intrinsic
- __addx18byte ARM64 intrinsic
- __addx18word ARM64 intrinsic
- __addx18dword ARM64 intrinsic
- __addx18qword ARM64 intrinsic
- __cas8 ARM64 intrinsic
- __cas16 ARM64 intrinsic
- __cas32 ARM64 intrinsic
- __cas64 ARM64 intrinsic
- __casa8 ARM64 intrinsic
- __casa16 ARM64 intrinsic
- __casa32 ARM64 intrinsic
- __casa64 ARM64 intrinsic
- __casl8 ARM64 intrinsic
- __casl16 ARM64 intrinsic
- __casl32 ARM64 intrinsic
- __casl64 ARM64 intrinsic
- __casal8 ARM64 intrinsic
- __casal16 ARM64 intrinsic
- __casal32 ARM64 intrinsic
- __casal64 ARM64 intrinsic
- __crc32b ARM64 intrinsic
- __crc32h ARM64 intrinsic
- __crc32w ARM64 intrinsic
- __crc32d ARM64 intrinsic
- __crc32cb ARM64 intrinsic
- __crc32ch ARM64 intrinsic
- __crc32cw ARM64 intrinsic
- __crc32cd ARM64 intrinsic
- __getReg ARM64 intrinsic
- __getRegFp ARM64 intrinsic
- __getCallerReg ARM64 intrinsic
- __getCallerRegFp ARM64 intrinsic
- __hlt ARM64 intrinsic
- __incx18byte ARM64 intrinsic
- __incx18word ARM64 intrinsic
- __incx18dword ARM64 intrinsic
- __incx18qword ARM64 intrinsic
- __ldar8 ARM64 intrinsic
- __ldar16 ARM64 intrinsic
- __ldar32 ARM64 intrinsic
- __ldar64 ARM64 intrinsic
- __ldapr8 ARM64 intrinsic
- __ldapr16 ARM64 intrinsic
- __ldapr32 ARM64 intrinsic
- __ldapr64 ARM64 intrinsic
- __prefetch2 ARM64 intrinsic
- __readx18byte ARM64 intrinsic
- __readx18word ARM64 intrinsic
- __readx18dword ARM64 intrinsic
- __readx18qword ARM64 intrinsic
- __setReg ARM64 intrinsic
- __setRegFp ARM64 intrinsic
- __setCallerReg ARM64 intrinsic
- __setCallerRegFp ARM64 intrinsic
- __stlr8 ARM64 intrinsic
- __stlr16 ARM64 intrinsic
- __stlr32 ARM64 intrinsic
- __stlr64 ARM64 intrinsic
- __swp8 ARM64 intrinsic
- __swp16 ARM64 intrinsic
- __swp32 ARM64 intrinsic
- __swp64 ARM64 intrinsic
- __swpa8 ARM64 intrinsic
- __swpa16 ARM64 intrinsic
- __swpa32 ARM64 intrinsic
- __swpa64 ARM64 intrinsic
- __swpl8 ARM64 intrinsic
- __swpl16 ARM64 intrinsic
- __swpl32 ARM64 intrinsic
- __swpl64 ARM64 intrinsic
- __swpal8 ARM64 intrinsic
- __swpal16 ARM64 intrinsic
- __swpal32 ARM64 intrinsic
- __swpal64 ARM64 intrinsic
- __sys ARM64 intrinsic
- __svc ARM64 intrinsic
- __writex18byte ARM64 intrinsic
- __writex18word ARM64 intrinsic
- __writex18dword ARM64 intrinsic
- __writex18qword ARM64 intrinsic
author: sigatrev
ms.author: magardn
ms.date: 11/14/2019
ms.openlocfilehash: 604658dbf4e6ac96b5c2344be5851f3baab3f641
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099490"
---
# <a name="arm64-intrinsics"></a>ARM64 内部函数

Microsoft c + + 编译器 (MSVC) 使以下内部函数可用于 ARM64 体系结构。 有关 ARM 的详细信息，请参阅 [Arm 开发人员文档](https://developer.arm.com/docs) 网站上的体系结构和软件开发工具部分。

## <a name="neon"></a><a name="top"></a> NEON

适用于 ARM64 的霓虹灯矢量指令集扩展提供了 Single Instruction Multiple Data (SIMD) 功能。 它们类似于在 x86 和 x64 体系结构处理器中通用的 MMX 和 SSE 矢量指令集中的内容。

支持霓虹灯内部函数，如标头文件 *arm64_neon* 中所述。 MSVC 对霓虹灯内部函数的支持与 ARM64 编译器的支持相似，后者在 ARM 信息中心网站上的 [ARM 霓虹灯型内部引用](https://developer.arm.com/architectures/instruction-sets/simd-isas/neon/intrinsics) 中进行了介绍。

## <a name="arm64-specific-intrinsics-listing"></a><a name="A"></a> ARM64 特定的内部函数列表

|函数名称|指令|函数原型|
|-------------------|-----------------|------------------------|
|__break|BRK|void __break (int) |
|__addx18byte||void __addx18byte (无符号长、无符号 char) |
|__addx18word||void __addx18word (无符号长、无符号短) |
|__addx18dword||void __addx18dword (无符号长、无符号长) |
|__addx18qword||void __addx18qword (无符号长、无符号 __int64) |
|__cas8|CASB|无符号 __int8 __cas8 (无符号 __int8 volatile * _Target，无符号 __int8 _Comp，无符号 __int8 _Value) |
|__cas16|现金|无符号 __int16 __cas16 (无符号 __int16 volatile * _Target，无符号 __int16 _Comp，无符号 __int16 _Value) |
|__cas32|CAS|无符号 __int32 __cas32 (无符号 __int32 volatile * _Target，无符号 __int32 _Comp，无符号 __int32 _Value) |
|__cas64|CAS|无符号 __int64 __cas64 (无符号 __int64 volatile * _Target，无符号 __int64 _Comp，无符号 __int64 _Value) |
|__casa8|CASAB|无符号 __int8 __casa8 (无符号 __int8 volatile * _Target，无符号 __int8 _Comp，无符号 __int8 _Value) |
|__casa16|CASAH|无符号 __int16 __casa16 (无符号 __int16 volatile * _Target，无符号 __int16 _Comp，无符号 __int16 _Value) |
|__casa32|CASA|无符号 __int32 __casa32 (无符号 __int32 volatile * _Target，无符号 __int32 _Comp，无符号 __int32 _Value) |
|__casa64|CASA|无符号 __int64 __casa64 (无符号 __int64 volatile * _Target，无符号 __int64 _Comp，无符号 __int64 _Value) |
|__casl8|CASLB|无符号 __int8 __casl8 (无符号 __int8 volatile * _Target，无符号 __int8 _Comp，无符号 __int8 _Value) |
|__casl16|CASLH|无符号 __int16 __casl16 (无符号 __int16 volatile * _Target，无符号 __int16 _Comp，无符号 __int16 _Value) |
|__casl32|CASL|无符号 __int32 __casl32 (无符号 __int32 volatile * _Target，无符号 __int32 _Comp，无符号 __int32 _Value) |
|__casl64|CASL|无符号 __int64 __casl64 (无符号 __int64 volatile * _Target，无符号 __int64 _Comp，无符号 __int64 _Value) |
|__casal8|CASALB|无符号 __int8 __casal8 (无符号 __int8 volatile * _Target，无符号 __int8 _Comp，无符号 __int8 _Value) |
|__casal16|CASALH|无符号 __int16 __casal16 (无符号 __int16 volatile * _Target，无符号 __int16 _Comp，无符号 __int16 _Value) |
|__casal32|CASAL|无符号 __int32 __casal32 (无符号 __int32 volatile * _Target，无符号 __int32 _Comp，无符号 __int32 _Value) |
|__casal64|CASAL|无符号 __int64 __casal64 (无符号 __int64 volatile * _Target，无符号 __int64 _Comp，无符号 __int64 _Value) |
|__crc32b|CRC32B|无符号 __int32 __crc32b (无符号的 __int32，未签名的 __int32) |
|__crc32h|CRC32H|无符号 __int32 __crc32h (无符号的 __int32，未签名的 __int32) |
|__crc32w|CRC32W|无符号 __int32 __crc32w (无符号的 __int32，未签名的 __int32) |
|__crc32d|CRC32X|无符号 __int32 __crc32d (无符号的 __int32，未签名的 __int64) |
|__crc32cb|CRC32CB|无符号 __int32 __crc32cb (无符号的 __int32，未签名的 __int32) |
|__crc32ch|CRC32CH|无符号 __int32 __crc32ch (无符号的 __int32，未签名的 __int32) |
|__crc32cw|CRC32CW|无符号 __int32 __crc32cw (无符号的 __int32，未签名的 __int32) |
|__crc32cd|CRC32CX|无符号 __int32 __crc32cd (无符号的 __int32，未签名的 __int64) |
|__dmb|DMB|void __dmb(unsigned int `_Type`)<br /><br /> 将一个内存屏障操作插入指令流中。 参数 `_Type` 指定屏障强制执行的限制类型。<br /><br /> 有关可强制执行的各种限制的详细信息，请参阅 [内存关卡限制](#BarrierRestrictions)。|
|__dsb|DSB|void __dsb(unsigned int _Type)<br /><br /> 将一个内存屏障操作插入指令流中。 参数 `_Type` 指定屏障强制执行的限制类型。<br /><br /> 有关可强制执行的各种限制的详细信息，请参阅 [内存关卡限制](#BarrierRestrictions)。|
|__isb|ISB|void __isb(unsigned int _Type)<br /><br /> 将一个内存屏障操作插入指令流中。 参数 `_Type` 指定屏障强制执行的限制类型。<br /><br /> 有关可强制执行的各种限制的详细信息，请参阅 [内存关卡限制](#BarrierRestrictions)。|
|__getReg|| (int __getReg 无符号 __int64) |
|__getRegFp||double __getRegFp (int) |
|__getCallerReg|| (int __getCallerReg 无符号 __int64) |
|__getCallerRegFp||double __getCallerRegFp (int) |
|__hvc|HVC|unsigned int __hvc(unsigned int, ...)|
|__hlt|HLT|int __hlt (无符号 int，... ) |
|__incx18byte||void __incx18byte (无符号长) |
|__incx18word||void __incx18word (无符号长) |
|__incx18dword||void __incx18dword (无符号长) |
|__incx18qword||void __incx18qword (无符号长) |
|__iso_volatile_load16||__int16 \_ _iso_volatile_load16 (const volatile \_ _int16 \*) <br /><br /> 有关详细信息，请参阅 [__iso_volatile_load/store 内部函数](#IsoVolatileLoadStore)。|
|__iso_volatile_load32||__int32 \_ _iso_volatile_load32 (const volatile \_ _int32 \*) <br /><br /> 有关详细信息，请参阅 [__iso_volatile_load/store 内部函数](#IsoVolatileLoadStore)。|
|__iso_volatile_load64||__int64 \_ _iso_volatile_load64 (const volatile \_ _int64 \*) <br /><br /> 有关详细信息，请参阅 [__iso_volatile_load/store 内部函数](#IsoVolatileLoadStore)。|
|__iso_volatile_load8||__int8 \_ _iso_volatile_load8 (const volatile \_ _int8 \*) <br /><br /> 有关详细信息，请参阅 [__iso_volatile_load/store 内部函数](#IsoVolatileLoadStore)。|
|__iso_volatile_store16||void __iso_volatile_store16 (可变 \_ _int16 \* ， \_ _int16) <br /><br /> 有关详细信息，请参阅 [__iso_volatile_load/store 内部函数](#IsoVolatileLoadStore)。|
|__iso_volatile_store32||void __iso_volatile_store32 (可变 \_ _int32 \* ， \_ _int32) <br /><br /> 有关详细信息，请参阅 [__iso_volatile_load/store 内部函数](#IsoVolatileLoadStore)。|
|__iso_volatile_store64||void __iso_volatile_store64 (可变 \_ _int64 \* ， \_ _int64) <br /><br /> 有关详细信息，请参阅 [__iso_volatile_load/store 内部函数](#IsoVolatileLoadStore)。|
|__iso_volatile_store8||void __iso_volatile_store8 (可变 \_ _int8 \* ， \_ _int8) <br /><br /> 有关详细信息，请参阅 [__iso_volatile_load/store 内部函数](#IsoVolatileLoadStore)。|
|__ldar8|LDARB|无符号 __int8 __ldar8 (无符号 __int8 volatile * _Target) |
|__ldar16|LDARH|无符号 __int16 __ldar16 (无符号 __int16 volatile * _Target) |
|__ldar32|LDAR|无符号 __int32 __ldar32 (无符号 __int32 volatile * _Target) |
|__ldar64|LDAR|无符号 __int64 __ldar64 (无符号 __int64 volatile * _Target) |
|__ldapr8|LDAPRB|无符号 __int8 __ldapr8 (无符号 __int8 volatile * _Target) |
|__ldapr16|LDAPRH|无符号 __int16 __ldapr16 (无符号 __int16 volatile * _Target) |
|__ldapr32|LDAPR|无符号 __int32 __ldapr32 (无符号 __int32 volatile * _Target) |
|__ldapr64|LDAPR|无符号 __int64 __ldapr64 (无符号 __int64 volatile * _Target) |
|__mulh||\__int64 __mulh (\_ _int64， \_ _int64) |
|__prefetch|PRFM|void __cdecl \_ _prefetch (const void \*) <br /><br /> `PRFM`向系统提供一个内存提示，其中包含对系统的预提取操作 `PLDL1KEEP` ，在指定地址附近或附近的内存可能会被访问。 某些系统可能会选择优化此内存访问模式以提高运行时性能。 但是，从 c + + 语言的角度来看，此功能没有明显的影响，可能不执行任何操作。|
|__prefetch2|PRFM|void __cdecl \_ _prefetch (const void \* uint8_t prfop) <br /><br /> `PRFM`向系统提供一个内存提示，其中包含对系统的预取操作，在指定地址附近或附近的内存可能会被访问。 某些系统可能会选择优化此内存访问模式以提高运行时性能。 但是，从 c + + 语言的角度来看，此功能没有明显的影响，可能不执行任何操作。|
|__readx18byte||无符号 char __readx18byte (无符号长) |
|__readx18word||无符号短 __readx18word (无符号长) |
|__readx18dword||无符号长 __readx18dword (无符号长) |
|__readx18qword||无符号 __int64 __readx18qword (无符号长) |
|__setReg||void __setReg (int，未签名的 __int64) |
|__setRegFp||void __setRegFp (int，double) |
|__setCallerReg||void __setCallerReg (int，未签名的 __int64) |
|__setCallerRegFp||void __setCallerRegFp (int，double) |
|__sev|SEV|void __sev(void)|
|__static_assert||void __static_assert (int，const char \*) |
|__stlr8|STLRB|void __stlr8 (无符号 __int8 volatile * _Target，无符号 __int8 _Value) |
|__stlr16|STLRH|void __stlr16 (无符号 __int16 volatile * _Target，无符号 __int16 _Value) |
|__stlr32|STLR|void __stlr32 (无符号 __int32 volatile * _Target，无符号 __int32 _Value) |
|__stlr64|STLR|void __stlr64 (无符号 __int64 volatile * _Target，无符号 __int64 _Value) |
|__swp8|SWPB|无符号 __int8 __swp8 (无符号 __int8 volatile * _Target，无符号 __int8 _Value) |
|__swp16|SWPH|无符号 __int16 __swp16 (无符号 __int16 volatile * _Target，无符号 __int16 _Value) |
|__swp32|SWP|无符号 __int32 __swp32 (无符号 __int32 volatile * _Target，无符号 __int32 _Value) |
|__swp64|SWP|无符号 __int64 __swp64 (无符号 __int64 volatile * _Target，无符号 __int64 _Value) |
|__swpa8|SWPAB|无符号 __int8 __swpa8 (无符号 __int8 volatile * _Target，无符号 __int8 _Value) |
|__swpa16|SWPAH|无符号 __int16 __swpa16 (无符号 __int16 volatile * _Target，无符号 __int16 _Value) |
|__swpa32|SWPA|无符号 __int32 __swpa32 (无符号 __int32 volatile * _Target，无符号 __int32 _Value) |
|__swpa64|SWPA|无符号 __int64 __swpa64 (无符号 __int64 volatile * _Target，无符号 __int64 _Value) |
|__swpl8|SWPLB|无符号 __int8 __swpl8 (无符号 __int8 volatile * _Target，无符号 __int8 _Value) |
|__swpl16|SWPLH|无符号 __int16 __swpl16 (无符号 __int16 volatile * _Target，无符号 __int16 _Value) |
|__swpl32|SWPL|无符号 __int32 __swpl32 (无符号 __int32 volatile * _Target，无符号 __int32 _Value) |
|__swpl64|SWPL|无符号 __int64 __swpl64 (无符号 __int64 volatile * _Target，无符号 __int64 _Value) |
|__swpal8|SWPALB|无符号 __int8 __swpal8 (无符号 __int8 volatile * _Target，无符号 __int8 _Value) |
|__swpal16|SWPALH|无符号 __int16 __swpal16 (无符号 __int16 volatile * _Target，无符号 __int16 _Value) |
|__swpal32|SWPAL|无符号 __int32 __swpal32 (无符号 __int32 volatile * _Target，无符号 __int32 _Value) |
|__swpal64|SWPAL|无符号 __int64 __swpal64 (无符号 __int64 volatile * _Target，无符号 __int64 _Value) |
|__sys|SYS|无符号 int __sys (int，__int64) |
|__svc|SVC|无符号整数 __svc (无符号 int，... ) |
|__wfe|WFE|void __wfe(void)|
|__wfi|WFI|void __wfi(void)|
|__writex18byte||void __writex18byte (无符号长、无符号 char) |
|__writex18word||void __writex18word (无符号长、无符号短) |
|__writex18dword||void __writex18dword (无符号长、无符号长) |
|__writex18qword||void __writex18qword (无符号长、无符号 __int64) |
|__umulh||无符号 \_ _int64 __umulh (无符号 \_ 的 _int64，未签名的 \_ _int64) |
|_CopyDoubleFromInt64||双 _CopyDoubleFromInt64 (\_ _int64) |
|_CopyFloatFromInt32||float _CopyFloatFromInt32 (\_ _int32) |
|_CopyInt32FromFloat||__int32 _CopyInt32FromFloat(float)|
|_CopyInt64FromDouble||__int64 _CopyInt64FromDouble(double)|
|_CountLeadingOnes||unsigned int _CountLeadingOnes(unsigned long)|
|_CountLeadingOnes64||无符号整数 _CountLeadingOnes64 (无符号 \_ _int64) |
|_CountLeadingSigns||unsigned int _CountLeadingSigns(long)|
|_CountLeadingSigns64|| (_int64 的无符号 int _CountLeadingSigns64 \_) |
|_CountLeadingZeros||unsigned int _CountLeadingZeros(unsigned long)|
|_CountLeadingZeros64||无符号整数 _CountLeadingZeros64 (无符号 \_ _int64) |
|_ReadStatusReg|MRS|\_ (int _ReadStatusReg _int64) |
|_WriteStatusReg|MSR|void _WriteStatusReg (int， \_ _int64) |

[[返回页首](#top)]

### <a name="memory-barrier-restrictions"></a><a name="BarrierRestrictions"></a> 内存屏障限制

内部函数 `__dmb` (数据内存关卡) 、 `__dsb` (数据同步关卡) 和 `__isb` (说明同步关卡) 使用以下预定义的值，根据共享域和受操作影响的访问类型指定内存屏障限制。

|限制值|说明|
|-----------------------|-----------------|
|_ARM64_BARRIER_SY|完整系统，读取和写入操作。|
|_ARM64_BARRIER_ST|完整系统，只写操作。|
|_ARM64_BARRIER_LD|完全系统，只读。|
|_ARM64_BARRIER_ISH|内部可共享，读取和写入操作。|
|_ARM64_BARRIER_ISHST|内部可共享，只写操作。|
|_ARM64_BARRIER_ISHLD|内部可共享，只读。|
|_ARM64_BARRIER_NSH|不可共享，读取和写入操作。|
|_ARM64_BARRIER_NSHST|不可共享，只写操作。|
|_ARM64_BARRIER_NSHLD|不可共享，只读。|
|_ARM64_BARRIER_OSH|外部可共享，读取和写入操作。|
|_ARM64_BARRIER_OSHST|外部可共享，只写操作。|
|_ARM64_BARRIER_OSHLD|外部可共享，只读。|

对于 `__isb` 内部函数，当前有效的唯一限制是 _ARM64_BARRIER_SY 的; 所有其他值都由体系结构保留。

### <a name="__iso_volatile_loadstore-intrinsics"></a><a name="IsoVolatileLoadStore"></a> __iso_volatile_load/store 内部函数

这些内部函数显式执行不受编译器优化限制的负载和存储。

```C
__int16 __iso_volatile_load16(const volatile __int16 * Location);
__int32 __iso_volatile_load32(const volatile __int32 * Location);
__int64 __iso_volatile_load64(const volatile __int64 * Location);
__int8 __iso_volatile_load8(const volatile __int8 * Location);

void __iso_volatile_store16(volatile __int16 * Location, __int16 Value);
void __iso_volatile_store32(volatile __int32 * Location, __int32 Value);
void __iso_volatile_store64(volatile __int64 * Location, __int64 Value);
void __iso_volatile_store8(volatile __int8 * Location, __int8 Value);
```

#### <a name="parameters"></a>参数

*定位*\
要从中读取或为其写入的内存位置的地址。

*“值”* \
要写入指定内存位置的值 (仅) 存储内部函数。

#### <a name="return-value-load-intrinsics-only"></a>仅 (加载内部函数的返回值) 

由 *location* 指定的内存位置的值。

#### <a name="remarks"></a>注解

您可以使用 `__iso_volatile_load8/16/32/64` 和 `__iso_volatile_store8/16/32/64` 内部函数显式执行不受编译器优化限制的内存访问。 编译器无法删除、同步或更改这些操作的相对顺序。 但是，它不会产生隐式硬件内存障碍。 因此，硬件仍可能对跨多个线程的可观察内存访问进行重新排序。 更准确地说，这些内部函数等效于在 **/volatile： iso** 下编译的以下表达式。

```cpp
int a = __iso_volatile_load32(p);    // equivalent to: int a = *(const volatile __int32*)p;
__iso_volatile_store32(p, a);        // equivalent to: *(volatile __int32*)p = a;
```

请注意内部函数采用易失性指针来适应易失性变量。 但是，不要求或建议使用可变指针作为参数。 如果使用常规、非易失性类型，则这些操作的语义完全相同。

有关 **/volatile： iso** 命令行参数的详细信息，请参阅 [/volatile (volatile 关键字解读)](../build/reference/volatile-volatile-keyword-interpretation.md)。

## <a name="arm64-support-for-intrinsics-from-other-architectures"></a><a name="I"></a> ARM64 对来自其他体系结构的内部函数的支持

下表列出了 ARM64 平台上支持的其他体系结构的内部函数。 在 ARM64 上，内部函数的行为与其在其他硬件体系结构上的行为不同，还会记下其他详细信息。

|函数名称|函数原型|
|-------------------|------------------------|
|__assume|void __assume(int)|
|__code_seg|void __code_seg (const char \*) |
|__debugbreak|void __cdecl \_ _debugbreak (void) |
|__fastfail|__declspec (noreturn) void \_ _fastfail (无符号 int) |
|__nop|void __nop(void)|
|__yield|void __yield (void) **注意：**  在 ARM64 平台上，此函数生成 yield 指令。 此指令指示线程正在执行可能暂时挂起的任务（例如，旋转锁），但不会对程序产生负面影响。 它使 CPU 可以在执行周期中执行其他任务，否则将会浪费这些任务。|
|_AddressOfReturnAddress|void \* _AddressOfReturnAddress (void) |
|_BitScanForward|无符号 char _BitScanForward (无符号长 \* _Index，无符号长 _Mask) |
|_BitScanForward64|无符号 char _BitScanForward64 (无符号长 \* _Index，未签名的 __int64 _Mask) |
|_BitScanReverse|无符号 char _BitScanReverse (无符号长 \* _Index，无符号长 _Mask) |
|_BitScanReverse64|无符号 char _BitScanReverse64 (无符号长 \* _Index，未签名的 __int64 _Mask) |
|_bittest|无符号 char _bittest (long const \* ，long) |
|_bittest64|无符号 char _bittest64 (__int64 const \* ，__int64) |
|_bittestandcomplement|无符号 char _bittestandcomplement (long \* ，long) |
|_bittestandcomplement64|无符号 char _bittestandcomplement64 (__int64 \* ，__int64) |
|_bittestandreset|无符号 char _bittestandreset (long \* ，long) |
|_bittestandreset64|无符号 char _bittestandreset64 (__int64 \* ，__int64) |
|_bittestandset|无符号 char _bittestandset (long \* ，long) |
|_bittestandset64|无符号 char _bittestandset64 (__int64 \* ，__int64) |
|_byteswap_uint64|未签名的 __int64 \_ _cdecl _byteswap_uint64 (无符号 \_ _int64|
|_byteswap_ulong|unsigned long __cdecl _byteswap_ulong(unsigned long)|
|_byteswap_ushort|unsigned short __cdecl _byteswap_ushort(unsigned short)|
|_disable|void __cdecl _disable (void) **注意：**  在 ARM64 平台上，此函数生成指令 `MSR DAIFCLR,#2` ; 它仅作为内部函数提供。|
|_enable|void __cdecl _enable (void) **注意：**  在 ARM64 平台上，此函数生成指令 `MSR DAIFSET,#2` ; 它仅作为内部函数提供。|
|_lrotl|unsigned long __cdecl _lrotl(unsigned long, int)|
|_lrotr|unsigned long __cdecl _lrotr(unsigned long, int)|
|_ReadBarrier|void _ReadBarrier(void)|
|_ReadWriteBarrier|void _ReadWriteBarrier(void)|
|_ReturnAddress|void \* _ReturnAddress (void) |
|_rotl|unsigned int __cdecl _rotl(unsigned int _Value, int _Shift)|
|_rotl16|unsigned short _rotl16(unsigned short _Value, unsigned char _Shift)|
|_rotl64|未签名 \_ 的 __int64 _cdecl _rotl64 (无符号 \_ _int64 _Value，int _Shift) |
|_rotl8|unsigned char _rotl8(unsigned char _Value, unsigned char _Shift)|
|_rotr|unsigned int __cdecl _rotr(unsigned int _Value, int _Shift)|
|_rotr16|unsigned short _rotr16(unsigned short _Value, unsigned char _Shift)|
|_rotr64|未签名 \_ 的 __int64 _cdecl _rotr64 (无符号 \_ _int64 _Value，int _Shift) |
|_rotr8|unsigned char _rotr8(unsigned char _Value, unsigned char _Shift)|
|_setjmpex|int __cdecl _setjmpex(jmp_buf)|
|_WriteBarrier|void _WriteBarrier(void)|

[[返回页首](#top)]

## <a name="interlocked-intrinsics"></a>联锁内部函数

互锁内部函数是用于执行原子读取-修改-写入操作的一组内部函数。 其中一些互锁内部函数通用于所有平台。 它们是单独列出的，因为它们有很多。 由于它们的定义主要是冗余的，因此更容易考虑它们。 它们的名称可用于派生确切行为。

下表总结了对非 bittest 互锁内部函数的 ARM64 支持。 表中的每个单元格都对应一个名称，这些名称的派生方式是将该行的最左侧单元格中的操作名和该列的最上面单元格中的类型名附加到 `_Interlocked`。 例如，行与列相交处的单元格与 `Xor` `8` `_InterlockedXor8` 和完全支持。 大部分受支持的函数提供以下可选后缀：`_acq`、`_rel` 和 `_nf`。 `_acq` 后缀表示“获取”语义，而 `_rel` 后缀表示“发布”语义。 `_nf`或 "无防护" 后缀对于 ARM 和 ARM64 是唯一的，下一部分将对此进行讨论。

|操作|8|16|32|64|128|P|
|-|-------|--------|--------|--------|-------|-------|
|添加|None|None|完全|完全|None|None|
|且|完全|完全|完全|完全|None|None|
|CompareExchange|完全|完全|完全|完全|完全|完全|
|递减|None|完全|完全|完全|None|None|
|Exchange|完全|完全|完全|完全|None|完全|
|ExchangeAdd|完全|完全|完全|完全|None|None|
|增量|None|完全|完全|完全|None|None|
|或|完全|完全|完全|完全|None|None|
|Xor|完全|完全|完全|完全|None|None|

密钥:

- **Full**：支持无格式、 `_acq` 、 `_rel` 和 `_nf` 窗体。

- **无**：不支持

### <a name="_nf-no-fence-suffix"></a><a name="nf_suffix"></a> _nf (没有防护) 后缀

`_nf`或 "无围墙" 后缀指示操作不会像任何类型的内存屏障一样运行，这与其他三个窗体不同 (纯、 `_acq` 和 `_rel`) ，这一切都作为某种屏障的作用。 窗体的一种可能用途 `_nf` 是维护一个统计信息计数器，该计数器由多个线程同时更新，但其值在多个线程执行时不使用。

### <a name="list-of-interlocked-intrinsics"></a>互锁内部函数的列表

|函数名称|函数原型|
|-------------------|------------------------|
|_InterlockedAdd|长 _InterlockedAdd (长 _volatile \* ，长) |
|_InterlockedAdd64|__int64 _InterlockedAdd64 (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedAdd64_acq|__int64 _InterlockedAdd64_acq (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedAdd64_nf|__int64 _InterlockedAdd64_nf (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedAdd64_rel|__int64 _InterlockedAdd64_rel (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedAdd_acq|长 _InterlockedAdd_acq (长可变 \* ，长整型) |
|_InterlockedAdd_nf|长 _InterlockedAdd_nf (长可变 \* ，长整型) |
|_InterlockedAdd_rel|长 _InterlockedAdd_rel (长可变 \* ，长整型) |
|_InterlockedAnd|长 _InterlockedAnd (长可变 \* ，长整型) |
|_InterlockedAnd16|简短 _InterlockedAnd16 (short volatile \* ，short) |
|_InterlockedAnd16_acq|简短 _InterlockedAnd16_acq (short volatile \* ，short) |
|_InterlockedAnd16_nf|简短 _InterlockedAnd16_nf (short volatile \* ，short) |
|_InterlockedAnd16_rel|简短 _InterlockedAnd16_rel (short volatile \* ，short) |
|_InterlockedAnd64|__int64 _InterlockedAnd64 (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedAnd64_acq|__int64 _InterlockedAnd64_acq (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedAnd64_nf|__int64 _InterlockedAnd64_nf (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedAnd64_rel|__int64 _InterlockedAnd64_rel (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedAnd8|char _InterlockedAnd8 (char volatile \* ，char) |
|_InterlockedAnd8_acq|char _InterlockedAnd8_acq (char volatile \* ，char) |
|_InterlockedAnd8_nf|char _InterlockedAnd8_nf (char volatile \* ，char) |
|_InterlockedAnd8_rel|char _InterlockedAnd8_rel (char volatile \* ，char) |
|_InterlockedAnd_acq|长 _InterlockedAnd_acq (长可变 \* ，长整型) |
|_InterlockedAnd_nf|长 _InterlockedAnd_nf (长可变 \* ，长整型) |
|_InterlockedAnd_rel|长 _InterlockedAnd_rel (长可变 \* ，长整型) |
|_InterlockedCompareExchange|长 __cdecl _InterlockedCompareExchange (长可变 \* 、长、长时间) |
|_InterlockedCompareExchange_acq|长 _InterlockedCompareExchange_acq (长时间可变 \* 、长、长) |
|_InterlockedCompareExchange_nf|长 _InterlockedCompareExchange_nf (长时间可变 \* 、长、长) |
|_InterlockedCompareExchange_rel|长 _InterlockedCompareExchange_rel (长时间可变 \* 、长、长) |
|_InterlockedCompareExchange16|简短 _InterlockedCompareExchange16 (short volatile \* 、short、short) |
|_InterlockedCompareExchange16_acq|简短 _InterlockedCompareExchange16_acq (short volatile \* 、short、short) |
|_InterlockedCompareExchange16_nf|简短 _InterlockedCompareExchange16_nf (short volatile \* 、short、short) |
|_InterlockedCompareExchange16_rel|简短 _InterlockedCompareExchange16_rel (short volatile \* 、short、short) |
|_InterlockedCompareExchange64|__int64 _InterlockedCompareExchange64 (\_ _int64 volatile \* 、 \_ _int64 _int64 \_) |
|_InterlockedCompareExchange64_acq|__int64 _InterlockedCompareExchange64_acq (\_ _int64 volatile \* 、 \_ _int64 _int64 \_) |
|_InterlockedCompareExchange64_nf|__int64 _InterlockedCompareExchange64_nf (\_ _int64 volatile \* 、 \_ _int64 _int64 \_) |
|_InterlockedCompareExchange64_rel|__int64 _InterlockedCompareExchange64_rel (\_ _int64 volatile \* 、 \_ _int64 _int64 \_) |
|_InterlockedCompareExchange8|char _InterlockedCompareExchange8 (char volatile \* 、char、char) |
|_InterlockedCompareExchange8_acq|char _InterlockedCompareExchange8_acq (char volatile \* 、char、char) |
|_InterlockedCompareExchange8_nf|char _InterlockedCompareExchange8_nf (char volatile \* 、char、char) |
|_InterlockedCompareExchange8_rel|char _InterlockedCompareExchange8_rel (char volatile \* 、char、char) |
|_InterlockedCompareExchangePointer|void \* _InterlockedCompareExchangePointer (void \* volatile \* 、void \* 、void \*) |
|_InterlockedCompareExchangePointer_acq|void \* _InterlockedCompareExchangePointer_acq (void \* volatile \* 、void \* 、void \*) |
|_InterlockedCompareExchangePointer_nf|void \* _InterlockedCompareExchangePointer_nf (void \* volatile \* 、void \* 、void \*) |
|_InterlockedCompareExchangePointer_rel|void \* _InterlockedCompareExchangePointer_rel (void \* volatile \* 、void \* 、void \*) |
|_InterlockedCompareExchange128|无符号 char _InterlockedCompareExchange128 (\_ _int64 可变 \* _Destination， \_ _int64 _ExchangeHigh \_ \_ \* _int64 _ExchangeLow _int64 _ComparandResult) |
|_InterlockedCompareExchange128_acq|无符号 char _InterlockedCompareExchange128_acq (\_ _int64 可变 \* _Destination， \_ _int64 _ExchangeHigh \_ \_ \* _int64 _ExchangeLow _int64 _ComparandResult) |
|_InterlockedCompareExchange128_nf|无符号 char _InterlockedCompareExchange128_nf (\_ _int64 可变 \* _Destination， \_ _int64 _ExchangeHigh \_ \_ \* _int64 _ExchangeLow _int64 _ComparandResult) |
|_InterlockedCompareExchange128_rel|无符号 char _InterlockedCompareExchange128_rel (\_ _int64 可变 \* _Destination， \_ _int64 _ExchangeHigh \_ \_ \* _int64 _ExchangeLow _int64 _ComparandResult) |
|_InterlockedDecrement|长 __cdecl _InterlockedDecrement (长可变 \*) |
|_InterlockedDecrement16|简短 _InterlockedDecrement16 (短可变 \*) |
|_InterlockedDecrement16_acq|简短 _InterlockedDecrement16_acq (短可变 \*) |
|_InterlockedDecrement16_nf|简短 _InterlockedDecrement16_nf (短可变 \*) |
|_InterlockedDecrement16_rel|简短 _InterlockedDecrement16_rel (短可变 \*) |
|_InterlockedDecrement64|__int64 _InterlockedDecrement64 (\_ _int64 可变 \*) |
|_InterlockedDecrement64_acq|__int64 _InterlockedDecrement64_acq (\_ _int64 可变 \*) |
|_InterlockedDecrement64_nf|__int64 _InterlockedDecrement64_nf (\_ _int64 可变 \*) |
|_InterlockedDecrement64_rel|__int64 _InterlockedDecrement64_rel (\_ _int64 可变 \*) |
|_InterlockedDecrement_acq|长 _InterlockedDecrement_acq (长可变 \*) |
|_InterlockedDecrement_nf|长 _InterlockedDecrement_nf (长可变 \*) |
|_InterlockedDecrement_rel|长 _InterlockedDecrement_rel (长可变 \*) |
|_InterlockedExchange|长 __cdecl _InterlockedExchange (长可变 \* _Target，long) |
|_InterlockedExchange_acq|长 _InterlockedExchange_acq (长可变 \* _Target，长时间) |
|_InterlockedExchange_nf|长 _InterlockedExchange_nf (长可变 \* _Target，长时间) |
|_InterlockedExchange_rel|长 _InterlockedExchange_rel (长可变 \* _Target，长时间) |
|_InterlockedExchange16|简短 _InterlockedExchange16 (简短 \* 的可变 _Target，short) |
|_InterlockedExchange16_acq|简短 _InterlockedExchange16_acq (简短 \* 的可变 _Target，short) |
|_InterlockedExchange16_nf|简短 _InterlockedExchange16_nf (简短 \* 的可变 _Target，short) |
|_InterlockedExchange16_rel|简短 _InterlockedExchange16_rel (简短 \* 的可变 _Target，short) |
|_InterlockedExchange64|__int64 _InterlockedExchange64 (\_ _int64 可变 \* _Target _int64 \_) |
|_InterlockedExchange64_acq|__int64 _InterlockedExchange64_acq (\_ _int64 可变 \* _Target _int64 \_) |
|_InterlockedExchange64_nf|__int64 _InterlockedExchange64_nf (\_ _int64 可变 \* _Target _int64 \_) |
|_InterlockedExchange64_rel|__int64 _InterlockedExchange64_rel (\_ _int64 可变 \* _Target _int64 \_) |
|_InterlockedExchange8|char _InterlockedExchange8 (char volatile \* _Target，char) |
|_InterlockedExchange8_acq|char _InterlockedExchange8_acq (char volatile \* _Target，char) |
|_InterlockedExchange8_nf|char _InterlockedExchange8_nf (char volatile \* _Target，char) |
|_InterlockedExchange8_rel|char _InterlockedExchange8_rel (char volatile \* _Target，char) |
|_InterlockedExchangeAdd|长 __cdecl _InterlockedExchangeAdd (长可变 \* ，长时间) |
|_InterlockedExchangeAdd16|简短 _InterlockedExchangeAdd16 (short volatile \* ，short) |
|_InterlockedExchangeAdd16_acq|简短 _InterlockedExchangeAdd16_acq (short volatile \* ，short) |
|_InterlockedExchangeAdd16_nf|简短 _InterlockedExchangeAdd16_nf (short volatile \* ，short) |
|_InterlockedExchangeAdd16_rel|简短 _InterlockedExchangeAdd16_rel (short volatile \* ，short) |
|_InterlockedExchangeAdd64|__int64 _InterlockedExchangeAdd64 (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedExchangeAdd64_acq|__int64 _InterlockedExchangeAdd64_acq (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedExchangeAdd64_nf|__int64 _InterlockedExchangeAdd64_nf (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedExchangeAdd64_rel|__int64 _InterlockedExchangeAdd64_rel (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedExchangeAdd8|char _InterlockedExchangeAdd8 (char volatile \* ，char) |
|_InterlockedExchangeAdd8_acq|char _InterlockedExchangeAdd8_acq (char volatile \* ，char) |
|_InterlockedExchangeAdd8_nf|char _InterlockedExchangeAdd8_nf (char volatile \* ，char) |
|_InterlockedExchangeAdd8_rel|char _InterlockedExchangeAdd8_rel (char volatile \* ，char) |
|_InterlockedExchangeAdd_acq|长 _InterlockedExchangeAdd_acq (长可变 \* ，长整型) |
|_InterlockedExchangeAdd_nf|长 _InterlockedExchangeAdd_nf (长可变 \* ，长整型) |
|_InterlockedExchangeAdd_rel|长 _InterlockedExchangeAdd_rel (长可变 \* ，长整型) |
|_InterlockedExchangePointer|void \* _InterlockedExchangePointer (void \* volatile \* _Target void \*) |
|_InterlockedExchangePointer_acq|void \* _InterlockedExchangePointer_acq (void \* volatile \* _Target void \*) |
|_InterlockedExchangePointer_nf|void \* _InterlockedExchangePointer_nf (void \* volatile \* _Target void \*) |
|_InterlockedExchangePointer_rel|void \* _InterlockedExchangePointer_rel (void \* volatile \* _Target void \*) |
|_InterlockedIncrement|长 __cdecl _InterlockedIncrement (长可变 \*) |
|_InterlockedIncrement16|简短 _InterlockedIncrement16 (短可变 \*) |
|_InterlockedIncrement16_acq|简短 _InterlockedIncrement16_acq (短可变 \*) |
|_InterlockedIncrement16_nf|简短 _InterlockedIncrement16_nf (短可变 \*) |
|_InterlockedIncrement16_rel|简短 _InterlockedIncrement16_rel (短可变 \*) |
|_InterlockedIncrement64|__int64 _InterlockedIncrement64 (\_ _int64 可变 \*) |
|_InterlockedIncrement64_acq|__int64 _InterlockedIncrement64_acq (\_ _int64 可变 \*) |
|_InterlockedIncrement64_nf|__int64 _InterlockedIncrement64_nf (\_ _int64 可变 \*) |
|_InterlockedIncrement64_rel|__int64 _InterlockedIncrement64_rel (\_ _int64 可变 \*) |
|_InterlockedIncrement_acq|长 _InterlockedIncrement_acq (长可变 \*) |
|_InterlockedIncrement_nf|长 _InterlockedIncrement_nf (长可变 \*) |
|_InterlockedIncrement_rel|长 _InterlockedIncrement_rel (长可变 \*) |
|_InterlockedOr|长 _InterlockedOr (长可变 \* ，长整型) |
|_InterlockedOr16|简短 _InterlockedOr16 (short volatile \* ，short) |
|_InterlockedOr16_acq|简短 _InterlockedOr16_acq (short volatile \* ，short) |
|_InterlockedOr16_nf|简短 _InterlockedOr16_nf (short volatile \* ，short) |
|_InterlockedOr16_rel|简短 _InterlockedOr16_rel (short volatile \* ，short) |
|_InterlockedOr64|__int64 _InterlockedOr64 (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedOr64_acq|__int64 _InterlockedOr64_acq (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedOr64_nf|__int64 _InterlockedOr64_nf (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedOr64_rel|__int64 _InterlockedOr64_rel (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedOr8|char _InterlockedOr8 (char volatile \* ，char) |
|_InterlockedOr8_acq|char _InterlockedOr8_acq (char volatile \* ，char) |
|_InterlockedOr8_nf|char _InterlockedOr8_nf (char volatile \* ，char) |
|_InterlockedOr8_rel|char _InterlockedOr8_rel (char volatile \* ，char) |
|_InterlockedOr_acq|长 _InterlockedOr_acq (长可变 \* ，长整型) |
|_InterlockedOr_nf|长 _InterlockedOr_nf (长可变 \* ，长整型) |
|_InterlockedOr_rel|长 _InterlockedOr_rel (长可变 \* ，长整型) |
|_InterlockedXor|长 _InterlockedXor (长可变 \* ，长整型) |
|_InterlockedXor16|简短 _InterlockedXor16 (short volatile \* ，short) |
|_InterlockedXor16_acq|简短 _InterlockedXor16_acq (short volatile \* ，short) |
|_InterlockedXor16_nf|简短 _InterlockedXor16_nf (short volatile \* ，short) |
|_InterlockedXor16_rel|简短 _InterlockedXor16_rel (short volatile \* ，short) |
|_InterlockedXor64|__int64 _InterlockedXor64 (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedXor64_acq|__int64 _InterlockedXor64_acq (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedXor64_nf|__int64 _InterlockedXor64_nf (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedXor64_rel|__int64 _InterlockedXor64_rel (\_ _int64 volatile \* 、 \_ _int64) |
|_InterlockedXor8|char _InterlockedXor8 (char volatile \* ，char) |
|_InterlockedXor8_acq|char _InterlockedXor8_acq (char volatile \* ，char) |
|_InterlockedXor8_nf|char _InterlockedXor8_nf (char volatile \* ，char) |
|_InterlockedXor8_rel|char _InterlockedXor8_rel (char volatile \* ，char) |
|_InterlockedXor_acq|长 _InterlockedXor_acq (长可变 \* ，长整型) |
|_InterlockedXor_nf|长 _InterlockedXor_nf (长可变 \* ，长整型) |
|_InterlockedXor_rel|长 _InterlockedXor_rel (长可变 \* ，长整型) |

[[返回页首](#top)]

### <a name="_interlockedbittest-intrinsics"></a>_interlockedbittest 内部函数

普通互锁位测试内部函数对于所有平台都是通用的。 ARM64 添加 `_acq` `_rel` 了、和 `_nf` 变体，只需修改操作的关卡语义，如本文前面 [_nf (没有隔离) 后缀](#nf_suffix) 中所述。

|函数名称|函数原型|
|-------------------|------------------------|
|_interlockedbittestandreset|无符号 char _interlockedbittestandreset (长可变 \* 的长整型) |
|_interlockedbittestandreset_acq|无符号 char _interlockedbittestandreset_acq (长可变 \* 的长整型) |
|_interlockedbittestandreset_nf|无符号 char _interlockedbittestandreset_nf (长可变 \* 的长整型) |
|_interlockedbittestandreset_rel|无符号 char _interlockedbittestandreset_rel (长可变 \* 的长整型) |
|_interlockedbittestandreset64|无符号 char _interlockedbittestandreset64 (__int64 volatile \* ，__int64) |
|_interlockedbittestandreset64_acq|无符号 char _interlockedbittestandreset64_acq (__int64 volatile \* ，__int64) |
|_interlockedbittestandreset64_nf|无符号 char _interlockedbittestandreset64_nf (__int64 volatile \* ，__int64) |
|_interlockedbittestandreset64_rel|无符号 char _interlockedbittestandreset64_rel (__int64 volatile \* ，__int64) |
|_interlockedbittestandset|无符号 char _interlockedbittestandset (长可变 \* 的长整型) |
|_interlockedbittestandset_acq|无符号 char _interlockedbittestandset_acq (长可变 \* 的长整型) |
|_interlockedbittestandset_nf|无符号 char _interlockedbittestandset_nf (长可变 \* 的长整型) |
|_interlockedbittestandset_rel|无符号 char _interlockedbittestandset_rel (长可变 \* 的长整型) |
|_interlockedbittestandset64|无符号 char _interlockedbittestandset64 (__int64 volatile \* ，__int64) |
|_interlockedbittestandset64_acq|无符号 char _interlockedbittestandset64_acq (__int64 volatile \* ，__int64) |
|_interlockedbittestandset64_nf|无符号 char _interlockedbittestandset64_nf (__int64 volatile \* ，__int64) |
|_interlockedbittestandset64_rel|无符号 char _interlockedbittestandset64_rel (__int64 volatile \* ，__int64) |

[[返回页首](#top)]

## <a name="see-also"></a>另请参阅

[编译器内部函数](../intrinsics/compiler-intrinsics.md)\
[ARM 内部函数](arm-intrinsics.md)\
[ARM 汇编程序参考](../assembler/arm/arm-assembler-reference.md)\
[C + + 语言参考](../cpp/cpp-language-reference.md)
