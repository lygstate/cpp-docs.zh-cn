---
title: C + + 标准库头文件
description: C + + 标准库标头文件，已分类
ms.date: 08/31/2020
helpviewer_keywords:
- header files, C++ Standard Library
- C++ Standard Library, header files
ms.assetid: e7bf497a-0f63-48d0-9b54-cb0eef4073c4
ms.openlocfilehash: de4a6a31102c5a4245aeb4600c3e76205c9d195f
ms.sourcegitcommit: 82a0d23b04d0776c00209d885689cbc5be36d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "106099698"
---
# <a name="c-standard-library-header-files"></a>C + + 标准库头文件

C + + 标准库和扩展的头文件（按类别）。

## <a name="headers-by-category"></a>按类别列出的标头

::: moniker range=">=msvc-150"

| 类别 | 标头 |
| - | - |
| [算法](./algorithms.md) | [`<algorithm>`](algorithm.md), [`<cstdlib>`](cstdlib.md), [`<numeric>`](numeric.md) |
| 原子操作 |  [`<atomic>`](atomic.md)<sup>11x17</sup> |
| C 库包装 | [`<cassert>`](cassert.md)， [`<ccomplex>`](ccomplex.md) <sup>11 a b</sup>， [`<cctype>`](cctype.md) ， [`<cerrno>`](cerrno.md) ， [`<cfenv>`](cfenv.md) <sup>11</sup>， [`<cfloat>`](cfloat.md) ， [`<cinttypes>`](cinttypes.md) <sup>11</sup>， [`<ciso646>`](ciso646.md) <sup>b</sup>，，，，，， [`<climits>`](climits.md) [`<clocale>`](clocale.md) [`<cmath>`](cmath.md) [`<csetjmp>`](csetjmp.md) [`<csignal>`](csignal.md) [`<cstdalign>`](cstdalign.md) <sup>11 a b</sup>， [`<cstdarg>`](cstdarg.md) ， [`<cstdbool>`](cstdbool.md) <sup>11 a b</sup>， [`<cstddef>`](cstddef.md) ， [`<cstdint>`](cstdint.md) <sup>11</sup>， [`<cstdio>`](cstdio.md) ，，， [`<cstdlib>`](cstdlib.md) [`<cstring>`](cstring.md) [`<ctgmath>`](ctgmath.md) <sup>11 a b</sup>， [`<ctime>`](ctime.md) ， [`<cuchar>`](cuchar.md) <sup>11</sup>， [`<cwchar>`](cwchar.md) ，[`<cwctype>`](cwctype.md) |
| 概念 | `<concepts>`<sup>0.2</sup> |
| [容器](./stl-containers.md) | |
| 序列容器 | [`<array>`](array.md)<sup>11</sup>、 [`<deque>`](deque.md) 、 [`<forward_list>`](forward-list.md) <sup>11</sup>、 [`<list>`](list.md) 、[`<vector>`](vector.md) |
| 排序关联容器| [`<map>`](map.md), [`<set>`](set.md) |
| 无序关联容器 | [`<unordered_map>`](unordered-map.md)<sup>11</sup>、 [`<unordered_set>`](unordered-set.md) <sup>11</sup> |
| 容器适配器 | [`<queue>`](queue.md), [`<stack>`](stack.md) |
| 容器视图 | [`<span>`](span.md)<sup>0.2</sup> |
| [错误和异常处理](../cpp/errors-and-exception-handling-modern-cpp.md) | [`<cassert>`](cassert.md)， [`<exception>`](exception.md) ， [`<stdexcept>`](stdexcept.md) ， [`<system_error>`](system-error.md) <sup>11</sup> |
| 常规实用工具 | `<any>`<sup>17</sup>， [`<bit>`](bit.md) <sup>20</sup>， [`<bitset>`](bitset.md) ， [`<cstdlib>`](cstdlib.md) ， `<execution>` <sup>17</sup>， [`<functional>`](functional.md) ， [`<memory>`](memory.md) ， `<memory_resource>` <sup>17</sup>， `<optional>` <sup>17</sup>， [`<ratio>`](ratio.md) <sup>11</sup>， [`<scoped_allocator>`](scoped-allocator.md) <sup>11</sup>， [`<tuple>`](tuple.md) <sup>11</sup>， [`<type_traits>`](type-traits.md) <sup>11</sup>， [`<typeindex>`](typeindex.md) <sup>11</sup>， [`<utility>`](utility.md) ， `<variant>` <sup>17</sup> |
| [I/o 和格式设置](../text/string-and-i-o-formatting-modern-cpp.md) | [`<cinttypes>`](cinttypes.md)<sup>11</sup>， [`<cstdio>`](cstdio.md) ， [`<filesystem>`](filesystem.md) <sup>17</sup>，，，，，，，，，， [`<fstream>`](fstream.md) [`<iomanip>`](iomanip.md) [`<ios>`](ios.md) [`<iosfwd>`](iosfwd.md) [`<iostream>`](iostream.md) [`<istream>`](istream.md) [`<ostream>`](ostream.md) [`<sstream>`](sstream.md) [`<streambuf>`](streambuf.md) [`<strstream>`](strstream.md) <sup>c</sup>， `<syncstream>` <sup>20</sup> |
| 迭代器 | [`<iterator>`](iterator.md) |
| 语言支持 | [`<cfloat>`](cfloat.md)， [`<climits>`](climits.md) ， [`<codecvt>`](codecvt.md) <sup>11 a</sup>， `<compare>` <sup>20</sup>， `<contract>` <sup>20</sup>， `<coroutine>` <sup>20</sup>， [`<csetjmp>`](csetjmp.md) ，，， [`<csignal>`](csignal.md) [`<cstdarg>`](cstdarg.md) [`<cstddef>`](cstddef.md) ， [`<cstdint>`](cstdint.md) <sup>11</sup>， [`<cstdlib>`](cstdlib.md) ， [`<exception>`](exception.md) ， [`<initializer_list>`](initializer-list.md) <sup>11</sup>， [`<limits>`](limits.md) ， [`<new>`](new.md) [`<typeinfo>`](typeinfo.md) `<version>` <sup></sup> ，，20 |
| 本地化 | [`<clocale>`](clocale.md)， [`<codecvt>`](codecvt.md) <sup>11 a</sup>， [`<cvt/wbuffer>`](cvt-wbuffer.md) ， [`<cvt/wstring>`](cvt-wstring.md) ，[`<locale>`](locale.md) |
| 数学和数字 | `<bit>`<sup>20</sup>， [`<cfenv>`](cfenv.md) <sup>11</sup>，，，，，， [`<cmath>`](cmath.md) [`<complex>`](complex.md) [`<cstdlib>`](cstdlib.md) [`<limits>`](limits.md) [`<numeric>`](numeric.md) [`<random>`](random.md) <sup>11</sup>， [`<ratio>`](ratio.md) <sup>11</sup>，[`<valarray>`](valarray.md) |
| [内存管理](../cpp/smart-pointers-modern-cpp.md) | [`<allocators>`](allocators-header.md)， [`<memory>`](memory.md) ， `<memory_resource>` <sup>17</sup>， [`<new>`](new.md) ， [`<scoped_allocator>`](scoped-allocator.md) <sup>11</sup> |
| 多线程处理 | [`<atomic>`](atomic.md)<sup>11</sup>、 [`<condition_variable>`](condition-variable.md) <sup>11</sup>、 [`<future>`](future.md) <sup>11</sup>、 [`<mutex>`](mutex.md) <sup>11</sup>、 [`<shared_mutex>`](shared-mutex.md) <sup>14</sup>、 [`<thread>`](thread.md) <sup>11</sup> |
| 范围 | `<ranges>`<sup>0.2</sup> |
| 正则表达式 | [`<regex>`](regex.md)<sup>11x17</sup> |
| 字符串和字符数据 | [`<charconv>`](charconv.md)<sup>17</sup>， [`<cctype>`](cctype.md) ， [`<cstdlib>`](cstdlib.md) ， [`<cstring>`](cstring.md) ， [`<cuchar>`](cuchar.md) <sup>11</sup>， [`<cwchar>`](cwchar.md) ， [`<cwctype>`](cwctype.md) ， [`<regex>`](regex.md) <sup>11</sup>， [`<string>`](string.md) ， [`<string_view>`](string-view.md) <sup>17</sup> |
| 时间 | [`<chrono>`](chrono.md)<sup>11</sup>， [`<ctime>`](ctime.md) |

<sup>11</sup> c + + 11 标准版中添加了11。
c + + 14 标准版中添加了<sup>14</sup>个。
<sup>17</sup> （c + + 17 标准版）。
标准版 c + + 20 标准版中添加了<sup>20</sup> 。 \
c + + 17 标准版中<sup>的</sup>弃用。
<sup>b</sup> 在标准版 c + + 20 标准版中删除。
<sup>c</sup> + + 98 标准版中已弃用。

::: moniker-end

::: moniker range="msvc-140"

|类别|标头|
|-|-|
|[算法](./algorithms.md)|[`<algorithm>`](algorithm.md)|
|C 库包装|[`<cassert>`](cassert.md), [`<cctype>`](cctype.md), [`<cerrno>`](cerrno.md), [`<cfenv>`](cfenv.md), [`<cfloat>`](cfloat.md), [`<cinttypes>`](cinttypes.md), [`<ciso646>`](ciso646.md), [`<climits>`](climits.md), [`<clocale>`](clocale.md), [`<cmath>`](cmath.md), [`<csetjmp>`](csetjmp.md), [`<csignal>`](csignal.md), [`<cstdarg>`](cstdarg.md), [`<cstdbool>`](cstdbool.md), [`<cstddef>`](cstddef.md), [`<cstdint>`](cstdint.md), [`<cstdio>`](cstdio.md), [`<cstdlib>`](cstdlib.md), [`<cstring>`](cstring.md), [`<ctgmath>`](ctgmath.md), [`<ctime>`](ctime.md), [`<cwchar>`](cwchar.md), [`<cwctype>`](cwctype.md)|
|[容器](./stl-containers.md)||
|序列容器|[`<array>`](array.md), [`<deque>`](deque.md), [`<forward_list>`](forward-list.md), [`<list>`](list.md), [`<vector>`](vector.md)|
|排序关联容器| [`<map>`](map.md), [`<set>`](set.md)|
|无序关联容器|[`<unordered_map>`](unordered-map.md), [`<unordered_set>`](unordered-set.md)|
|适配器容器|[`<queue>`](queue.md), [`<stack>`](stack.md)|
|[错误和异常处理](../cpp/errors-and-exception-handling-modern-cpp.md)|[`<exception>`](exception.md), [`<stdexcept>`](stdexcept.md), [`<system_error>`](system-error.md)|
|[I/o 和格式设置](../text/string-and-i-o-formatting-modern-cpp.md)|[`<filesystem>`](filesystem.md), [`<fstream>`](fstream.md), [`<iomanip>`](iomanip.md), [`<ios>`](ios.md), [`<iosfwd>`](iosfwd.md), [`<iostream>`](iostream.md), [`<istream>`](istream.md), [`<ostream>`](ostream.md), [`<sstream>`](sstream.md), [`<streambuf>`](streambuf.md), [`<strstream>`](strstream.md)|
|迭代器|[`<iterator>`](iterator.md)|
|本地化|[`<codecvt>`](codecvt.md), [`<cvt/wbuffer>`](cvt-wbuffer.md), [`<cvt/wstring>`](cvt-wstring.md), [`<locale>`](locale.md)|
|数学和数字|[`<complex>`](complex.md), [`<limits>`](limits.md), [`<numeric>`](numeric.md), [`<random>`](random.md), [`<ratio>`](ratio.md), [`<valarray>`](valarray.md)|
|[内存管理](../cpp/smart-pointers-modern-cpp.md)|[`<allocators>`](allocators-header.md), [`<memory>`](memory.md), [`<new>`](new.md), [`<scoped_allocator>`](scoped-allocator.md)|
|多线程处理|[`<atomic>`](atomic.md), [`<condition_variable>`](condition-variable.md), [`<future>`](future.md), [`<mutex>`](mutex.md), [`<shared_mutex>`](shared-mutex.md), [`<thread>`](thread.md)|
|其他实用工具|[`<bitset>`](bitset.md), [`<chrono>`](chrono.md), [`<functional>`](functional.md), [`<initializer_list>`](initializer-list.md), [`<tuple>`](tuple.md), [`<type_traits>`](type-traits.md), [`<typeinfo>`](typeinfo.md), [`<typeindex>`](typeindex.md), [`<utility>`](utility.md)|
|字符串和字符数据|[`<regex>`](regex.md), [`<string>`](string.md), [`<string_view>`](string-view.md)|

::: moniker-end

## <a name="see-also"></a>另请参阅

[使用 c + + 库标头](using-cpp-library-headers.md)\
[C + + 标准库](cpp-standard-library-reference.md)
