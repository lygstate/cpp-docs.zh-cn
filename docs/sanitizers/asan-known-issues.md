---
title: AddressSanitizer 已知问题
description: 适用于 Microsoft C/c + + 已知问题的 AddressSanitizer 的技术说明。
ms.date: 03/02/2021
helpviewer_keywords:
- AddressSanitizer known issues
ms.openlocfilehash: 0bd8b8cc05265930b8ade514c4d1f8ea162bb304
ms.sourcegitcommit: dc77cf3b5b644d8e2adf595540b98194ab95c6e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377224"
---
# <a name="addresssanitizer-known-issues"></a>AddressSanitizer 已知问题

> [!NOTE]
> 向我们发送有关你希望在未来版本中看到的内容的 [反馈](https://aka.ms/vsfeedback/browsecpp) ，并在遇到问题时 [报告 bug](https://aka.ms/feedback/report?space=62) 。

## <a name="incompatible-options-and-functionality"></a><a name="incompatible-options"></a> 不兼容的选项和功能

这些选项和功能与不兼容 [`/fsanitize=address`](../build/reference/fsanitize.md) ，应禁用或避免这些选项和功能。

- [`/RTC`](../build/reference/rtc-run-time-error-checks.md)选项与 AddressSanitizer 不兼容，应禁用。
- [增量链接](../build/reference/incremental-link-incrementally.md) 不受支持，应禁用。
- 不支持 "[编辑并继续](/visualstudio/debugger/edit-and-continue-visual-cpp)"，应禁用。
- [协同程序](https://devblogs.microsoft.com/cppblog/category/coroutine/) 与 AddressSanitizer 不兼容，可恢复函数不受检测。
- [OpenMP](../build/reference/openmp-enable-openmp-2-0-support.md) 不受支持，应禁用。
- [托管 c + +](../build/reference/clr-common-language-runtime-compilation.md) 不受支持，应禁用。
- [C++ AMP](../parallel/amp/cpp-amp-overview.md) 不受支持，应禁用。
- 不支持[特殊案例列表](https://clang.llvm.org/docs/SanitizerSpecialCaseList.html)文件。

## <a name="standard-library-support"></a>标准库支持

MSVC 标准库 (STL) 不启用理解 AddressSanitizer。 STL 代码中引发的 AddressSanitizer 异常标识真实 bug。 但是，它们并不像它们一样精确。

此示例演示缺少精度：

```cpp
// Compile with: cl /fsanitize=address /Zi
#include <vector>

int main() {   
    // Create a vector of size 10, but with a capacity of 20.    
    std::vector<int> v(10);
    v.reserve(20);

    // Currently, MSVC ASan does NOT raise an exception here.
    // While this is an out-of-bounds write to 'v', MSVC ASan
    // ensures the write is within the heap allocation size (20).
    v[10] = 1;

    // MSVC ASan DOES raise an exception here, as this write
    // is out of bounds from the heap allocation.
    v[20] = 1;
}
```

## <a name="windows-versions"></a>Windows 版本

由于存在与特定 Windows 版本相关的依赖项，因此支持集中于 Windows 10。 MSVC AddressSanitizer 在 10.0.14393 (RS1) 和 10.0.21323 (预发布内部版本) 上进行了测试。 如果遇到问题，请[报告 bug](https://aka.ms/feedback/report?space=62) 。

## <a name="memory-usage"></a>内存使用率

在执行期间，AddressSanitizer 运行时不会将内存释放回操作系统。 从操作系统的角度来看，它可能与内存泄漏有关。 此设计决策是特意的，因此不会提前分配所有所需的内存。

## <a name="addresssanitizer-runtime-dll-locations"></a>AddressSanitizer 运行时 DLL 位置

*`clang_rt.asan*.dll`* 运行时文件安装在中的编译器旁边 *`%VSINSTALLDIR%\VC\Tools\MSVC\<version>\bin\<host-arch>\<target-arch>\`* 。 这些位置位于调试会话和 Visual Studio 开发人员命令提示中的路径上。 永远不会将这些文件放入 *`C:\Windows\System32`* 或 *`C:\Windows\SysWOW64`* 。

## <a name="custom-property-sheet-support"></a>自定义属性表支持

在 Visual Studio IDE 中的 "属性管理器" 窗口中，可以向项目添加自定义 *`.props`* 文件。 即使显示了 **Enable Address Sanitizer** 属性 (`<EnableASAN>`) ，它也不会被生成所遵守。 这是因为自定义 *`.props`* 文件将包含在之后 *`Microsoft.cpp.props`* ，后者使用 `<EnableASAN>` 该值来设置其他属性。

作为一种解决方法，可以 *`Directory.Build.props`* 在项目的根目录中创建一个文件来定义 `<EnableASAN>` 属性。 有关详细信息，请参阅 [自定义 c + + 生成](/visualstudio/msbuild/customize-your-build#customize-c-builds)。

## <a name="see-also"></a>另请参阅

[AddressSanitizer 概述](./asan.md)\
[AddressSanitizer 生成和语言参考](./asan-building.md)\
[AddressSanitizer 运行时引用](./asan-runtime.md)\
[AddressSanitizer 阴影字节数](./asan-shadow-bytes.md)\
[AddressSanitizer 云或分布式测试](./asan-offline-crash-dumps.md)\
[AddressSanitizer 调试器集成](./asan-debugger-integration.md)\
[AddressSanitizer 错误示例](./asan-error-examples.md)
