---
title: 按字母顺序列出的编译器选项
description: Microsoft C/c + + 编译器命令行选项的按字母顺序排列的引用列表。
ms.date: 04/13/2021
helpviewer_keywords:
- compiler options, C++
ms.openlocfilehash: 78366537d0ff0599951d4ba528cfae2bdcc2c3e0
ms.sourcegitcommit: bac5dde649d5b0447de1d26a73365e36d74595f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "107381215"
---
# <a name="compiler-options-listed-alphabetically"></a>按字母顺序列出的编译器选项

此表包含编译器选项的按字母顺序排序的列表。 有关按类别列出的编译器选项的列表，请参阅 [按类别列出的编译器选项](compiler-options-listed-by-category.md) 一文。

## <a name="compiler-options"></a>编译器选项

| 选项 | 目标 |
|--|--|
| [`@`](at-specify-a-compiler-response-file.md) | 指定响应文件。 |
| [`/?`](help-compiler-command-line-help.md) | 列出编译器选项。 |
| [`/AI`](ai-specify-metadata-directories.md) | 指定要搜索以解析传递到指令的文件引用的目录 [`#using`](../../preprocessor/hash-using-directive-cpp.md) 。 |
| [`/analyze`](analyze-code-analysis.md) | 启用代码分析。 |
| [`/arch`](arch-minimum-cpu-architecture.md) | 为代码生成指定体系结构。 |
| [`/await`](await-enable-coroutine-support.md) | ) 扩展启用协同程序 (可恢复的函数。 |
| [`/bigobj`](bigobj-increase-number-of-sections-in-dot-obj-file.md) | 增加 .obj 文件中可寻址节的数目。 |
| [`/C`](c-preserve-comments-during-preprocessing.md) | 在预处理期间保留注释。 |
| [`/c`](c-compile-without-linking.md) | 编译但不链接。 |
| [`/cgthreads`](cgthreads-code-generation-threads.md) | 指定 cl.exe 线程数以用于优化和代码生成。 |
| [`/clr`](clr-common-language-runtime-compilation.md) | 生成要在公共语言运行时上运行的输出文件。 |
| [`/constexpr`](constexpr-control-constexpr-evaluation.md) | **`constexpr`** 在编译时控制计算。 |
| [`/D`](d-preprocessor-definitions.md) | 定义常数和宏。 |
| [`/diagnostics`](diagnostics-compiler-diagnostic-options.md) | 控制诊断消息的格式。 |
| [`/doc`](doc-process-documentation-comments-c-cpp.md) | 处理 XML 文件的文档注释。 |
| [`/E`](e-preprocess-to-stdout.md) | 将预处理器输出复制到标准输出。 |
| [`/EH`](eh-exception-handling-model.md) | 指定异常处理模型。 |
| [`/EP`](ep-preprocess-to-stdout-without-hash-line-directives.md) | 将预处理器输出复制到标准输出。 |
| [`/errorReport`](errorreport-report-internal-compiler-errors.md) | 已弃用。 错误报告由 [Windows 错误报告 (WER) ](/windows/win32/wer/windows-error-reporting) 设置控制。 |
| [`/execution-charset`](execution-charset-set-execution-character-set.md) | 设置执行字符集。 |
| [`/experimental:module`](experimental-module.md) | 启用实验性模块支持。 |
| [`/experimental:preprocessor`](experimental-preprocessor.md) | 已弃用。 启用实验相容预处理器支持。 使用 [`/Zc:preprocessor`](zc-preprocessor.md) |
| [`/exportHeader`](module-exportheader.md) | 创建标头单元 (*`.ifc`* 由输入参数指定的) 文件。 |
| [`/F`](f-set-stack-size.md) | 设置堆栈大小。 |
| [`/favor`](favor-optimize-for-architecture-specifics.md) | 生成针对特定 x64 体系结构进行了优化的代码。 或者，适用于 AMD64 和 EM64T 体系结构中的特定微体系结构。 |
| [`/FA`](fa-fa-listing-file.md) | 创建列表文件。 |
| [`/Fa`](fa-fa-listing-file.md) | 设置列表文件名。 |
| [`/FC`](fc-full-path-of-source-code-file-in-diagnostics.md) | 在诊断文本中显示传递给 cl.exe 的源代码文件的完整路径。 |
| [`/Fd`](fd-program-database-file-name.md) | 重命名程序数据库文件。 |
| [`/Fe`](fe-name-exe-file.md) | 重命名可执行文件。 |
| [`/FI`](fi-name-forced-include-file.md) | 预处理指定的包含文件。 |
| [`/Fi`](fi-preprocess-output-file-name.md) | 设置预处理输出文件名。 |
| [`/Fm`](fm-name-mapfile.md) | 创建映射文件。 |
| [`/Fo`](fo-object-file-name.md) | 创建对象文件。 |
| [`/fp`](fp-specify-floating-point-behavior.md) | 指定浮点行为。 |
| [`/Fp`](fp-name-dot-pch-file.md) | 指定预编译头文件名。 |
| [`/FR`](fr-fr-create-dot-sbr-file.md)<br /><br /> [`/Fr`](fr-fr-create-dot-sbr-file.md) | 生成浏览器文件。 **`/Fr`** 已弃用。 |
| [`/FS`](fs-force-synchronous-pdb-writes.md) | 通过 MSPDBSRV.EXE (PDB) 文件强制对程序数据库执行所有写入操作的序列化。 |
| [`/fsanitize`](fsanitize.md) | 启用 sanitizer 检测的编译，如 AddressSanitizer。 |
| [`/FU`](fu-name-forced-hash-using-file.md) | 强制使用文件名，就像它已被传递到 [`#using`](../../preprocessor/hash-using-directive-cpp.md) 指令一样。 |
| [`/Fx`](fx-merge-injected-code.md) | 将插入的代码与源文件合并。 |
| [`/GA`](ga-optimize-for-windows-application.md) | 优化 Windows 应用程序的代码。 |
| [`/Gd`](gd-gr-gv-gz-calling-convention.md) | **`__cdecl`** 仅 (x86) 使用调用约定。 |
| [`/Ge`](ge-enable-stack-probes.md) | 已弃用。 激活堆栈探测。 |
| [`/GF`](gf-eliminate-duplicate-strings.md) | 启用字符串池。 |
| [`/GH`](gh-enable-pexit-hook-function.md) | 调用挂钩函数 `_pexit`。 |
| [`/Gh`](gh-enable-penter-hook-function.md) | 调用挂钩函数 `_penter`。 |
| [`/GL`](gl-whole-program-optimization.md) | 启用全程序优化。 |
| [`/Gm`](gm-enable-minimal-rebuild.md) | 已弃用。 启用最小重新生成。 |
| [`/GR`](gr-enable-run-time-type-information.md) | 启用运行时类型信息 (RTTI)。 |
| [`/Gr`](gd-gr-gv-gz-calling-convention.md) | **`__fastcall`** 仅 (x86) 使用调用约定。 |
| [`/GS`](gs-buffer-security-check.md) | 缓冲区安全检查。 |
| [`/Gs`](gs-control-stack-checking-calls.md) | 控制堆栈探测。 |
| [`/GT`](gt-support-fiber-safe-thread-local-storage.md) | 支持使用静态线程本地存储区分配的数据的纤程安全。 |
| [`/guard:cf`](guard-enable-control-flow-guard.md) | 添加控制流防护安全检查。 |
| [`/guard:ehcont`](guard-enable-eh-continuation-metadata.md) | 启用 EH 继续元数据。 |
| [`/Gv`](gd-gr-gv-gz-calling-convention.md) | 使用 **`__vectorcall`** 调用约定。 （仅限 x86 和 x64） |
| [`/Gw`](gw-optimize-global-data.md) | 启用全程序全局数据优化。 |
| [`/GX`](gx-enable-exception-handling.md) | 已弃用。 启用同步异常处理。 改为使用 [`/EH`](eh-exception-handling-model.md) 。 |
| [`/Gy`](gy-enable-function-level-linking.md) | 启用函数级链接。 |
| [`/GZ`](gz-enable-stack-frame-run-time-error-checking.md) | 已弃用。 与 `/RTC1` 相同。 |
| [`/Gz`](gd-gr-gv-gz-calling-convention.md) | **`__stdcall`** 仅 (x86) 使用调用约定。 |
| [`/H`](h-restrict-length-of-external-names.md) | 已弃用。 限制外部（公共）名称的长度。 |
| [`/headerName`](headername.md) | 从指定的标头生成标题单元。 |
| [`/headerUnit`](headerunit.md) | 指定在何处查找指定标头 () 的标头单元文件 `.ifc` 。 |
| [`/HELP`](help-compiler-command-line-help.md) | 列出编译器选项。 |
| [`/homeparams`](homeparams-copy-register-parameters-to-stack.md) | 强制将传入寄存器的参数写入其在函数入口的堆栈上的位置。 此编译器选项仅适用于 x64 编译器 (本机编译和跨平台编译) 。 |
| [`/hotpatch`](hotpatch-create-hotpatchable-image.md) | 创建热可修补映像。 |
| [`/I`](i-additional-include-directories.md) | 在目录中搜索包含文件。 |
| [`/J`](j-default-char-type-is-unsigned.md) | 更改默认 **`char`** 类型。 |
| [`/JMC`](jmc.md) | 支持本机 c + + 仅我的代码调试。 |
| [`/kernel`](kernel-create-kernel-mode-binary.md) | 编译器和链接器将创建可在 Windows 内核中执行的二进制文件。 |
| [`/LD`](md-mt-ld-use-run-time-library.md) | 创建动态链接库。 |
| [`/LDd`](md-mt-ld-use-run-time-library.md) | 创建调试动态链接库。 |
| [`/link`](link-pass-options-to-linker.md) | 将指定的选项传递给 LINK。 |
| [`/LN`](ln-create-msil-module.md) | 创建 MSIL 模块。 |
| [`/MD`](md-mt-ld-use-run-time-library.md) | 使用 MSVCRT.lib 创建多线程 DLL。 |
| [`/MDd`](md-mt-ld-use-run-time-library.md) | 使用 MSVCRTD.lib 创建调试多线程 DLL。 |
| [`/MP`](mp-build-with-multiple-processes.md) | 使用多个进程编译多个源文件。 |
| [`/MT`](md-mt-ld-use-run-time-library.md) | 使用 LIBCMT.lib 创建多线程可执行文件。 |
| [`/MTd`](md-mt-ld-use-run-time-library.md) | 使用 LIBCMTD.lib 创建调试多线程可执行文件。 |
| [`/nologo`](nologo-suppress-startup-banner-c-cpp.md) | 取消显示登录版权标志。 |
| [`/O1`](o1-o2-minimize-size-maximize-speed.md) | 创建小代码。 |
| [`/O2`](o1-o2-minimize-size-maximize-speed.md) | 创建快速代码。 |
| [`/Ob`](ob-inline-function-expansion.md) | 控制内联展开。 |
| [`/Od`](od-disable-debug.md) | 禁用优化。 |
| [`/Og`](og-global-optimizations.md) | 已弃用。 使用全局优化。 |
| [`/Oi`](oi-generate-intrinsic-functions.md) | 生成内部函数。 |
| [`/openmp`](openmp-enable-openmp-2-0-support.md) | 启用 [`#pragma omp`](../../preprocessor/omp.md) 源代码中的指令。 |
| [`/Os`](os-ot-favor-small-code-favor-fast-code.md) | 代码大小优先。 |
| [`/Ot`](os-ot-favor-small-code-favor-fast-code.md) | 代码速度优先。 |
| [`/Ox`](ox-full-optimization.md) | 不包含/GF 或/Gy. 的/O2 子集 |
| [`/Oy`](oy-frame-pointer-omission.md) | 省略帧指针（仅限 x86）。 |
| [`/P`](p-preprocess-to-a-file.md) | 将预处理器输出写入文件。 |
| [`/permissive-`](permissive-standards-conformance.md) | 设置标准一致性模式。 |
| [`/Qfast_transcendentals`](qfast-transcendentals-force-fast-transcendentals.md) | 生成快速先验。 |
| [`/QIfist`](qifist-suppress-ftol.md) | 已弃用。 当需要从浮点类型转换为整型时（仅限 x86）取消 `_ftol` 。 |
| [`/Qimprecise_fwaits`](qimprecise-fwaits-remove-fwaits-inside-try-blocks.md) | 删除 `fwait` 块内 **`try`** 的命令。 |
| [`/QIntel-jcc-erratum`](qintel-jcc-erratum.md) | 缓解 Intel JCC 错误微代码更新对性能的影响。 |
| [/Qpar (自动并行) ](qpar-auto-parallelizer.md) | 对标记有 [#pragma loop()](../../preprocessor/loop.md) 指令的循环启用自动并行化。 |
| [`/Qsafe_fp_loads`](qsafe-fp-loads.md) | 将整数移动指令用于浮点值，并禁用特定浮点加载优化。 |
| [`/Qspectre`](qspectre.md) | 指定编译器生成指令以缓解某些 Spectre 变体 1 安全漏洞。 |
| [`/Qspectre-load`](qspectre-load.md) | 指定编译器生成序列化说明，以根据负载说明减少 Spectre 的安全漏洞。 |
| [`/Qspectre-load-cf`](qspectre-load-cf.md) | 指定编译器的序列化说明的生成，以根据加载内存的控制流指令来减少 Spectre 的安全漏洞。 |
| [`/Qvec-report` (自动向量化报表级别) ](qvec-report-auto-vectorizer-reporting-level.md) | 启用自动矢量化的报告级别。 |
| [`/reference`](module-reference.md) | 使用命名模块 IFC。 |
| [`/RTC`](rtc-run-time-error-checks.md) | 启用运行时错误检查。 |
| [`/sdl`](sdl-enable-additional-security-checks.md) | 启用更多安全功能和警告。 |
| [`/showIncludes`](showincludes-list-include-files.md) | 在编译期间显示包含文件的列表。 |
| [`/source-charset`](source-charset-set-source-character-set.md) | 设置源字符集。 |
| [`/sourceDependencies`](sourcedependencies.md) | 列出所有源级别的依赖关系。 |
| [`/sourceDependencies:directives`](sourcedependencies-directives.md) |列出模块和标头单元依赖关系。 |
| [`/std`](std-specify-language-standard-version.md) | C + + 标准版本兼容性选择器。 |
| [`/Tc`](tc-tp-tc-tp-specify-source-file-type.md) | 指定 C 源文件。 |
| [`/TC`](tc-tp-tc-tp-specify-source-file-type.md) | 指定所有源文件均为 C。 |
| [`/Tp`](tc-tp-tc-tp-specify-source-file-type.md) | 指定 C++ 源文件。 |
| [`/TP`](tc-tp-tc-tp-specify-source-file-type.md) | 指定所有源文件均为 c + +。 |
| [`/translateInclude`](translateinclude.md) | 视为 `#include` `import` 。 |
| [`/U`](u-u-undefine-symbols.md) | 移除预定义宏。 |
| [`/u`](u-u-undefine-symbols.md) | 移除所有的预定义宏。 |
| [`/utf-8`](utf-8-set-source-and-executable-character-sets-to-utf-8.md) | 将源和执行字符集设置为 UTF-8。 |
| [`/V`](v-version-number.md) | 已弃用。 设置 .obj 文件版本字符串。 |
| [`/validate-charset`](validate-charset-validate-for-compatible-characters.md) | 仅验证 UTF-8 文件的兼容字符。 |
| [`/vd`](vd-disable-construction-displacements.md) | 取消或启用隐藏的 vtordisp 类成员。 |
| [`/vmb`](vmb-vmg-representation-method.md) | 对指向成员的指针使用最佳的基。 |
| [`/vmg`](vmb-vmg-representation-method.md) | 对指向成员的指针使用完全一般性。 |
| [`/vmm`](vmm-vms-vmv-general-purpose-representation.md) | 声明多重继承。 |
| [`/vms`](vmm-vms-vmv-general-purpose-representation.md) | 声明单一继承。 |
| [`/vmv`](vmm-vms-vmv-general-purpose-representation.md) | 声明虚拟继承。 |
| [`/volatile`](volatile-volatile-keyword-interpretation.md) | 选择如何解释 volatile 关键字。 |
| [`/w`](compiler-option-warning-level.md) | 禁用所有警告。 |
| [`/W0`, `/W1`, `/W2`, `/W3`, `/W4`](compiler-option-warning-level.md) | 设置要输出的警告级别。 |
| [`/w1`, `/w2`, `/w3`, `/w4`](compiler-option-warning-level.md) | 针对指定的警告设置警告级别。 |
| [`/Wall`](compiler-option-warning-level.md) | 启用所有警告，包括默认情况下禁用的警告。 |
| [`/wd`](compiler-option-warning-level.md) | 禁用指定的警告。 |
| [`/we`](compiler-option-warning-level.md) | 将指定的警告视为错误。 |
| [`/WL`](wl-enable-one-line-diagnostics.md) | 在从命令行编译 C++ 源代码时启用错误消息和警告消息的单行诊断。 |
| [`/wo`](compiler-option-warning-level.md) | 仅显示指定的警告一次。 |
| [`/Wp64`](wp64-detect-64-bit-portability-issues.md) | 已过时。 检测 64 位可移植性问题。 |
| [`/Wv`](compiler-option-warning-level.md) | 不显示编辑器的指定版本后引入的警告。 |
| [`/WX`](compiler-option-warning-level.md) | 将所有警告视为错误。 |
| [`/X`](x-ignore-standard-include-paths.md) | 忽略标准包含目录。 |
| [`/Y-`](y-ignore-precompiled-header-options.md) | 忽略当前生成中的所有其他预编译头编译器选项。 |
| [`/Yc`](yc-create-precompiled-header-file.md) | 创建预编译头文件。 |
| [`/Yd`](yd-place-debug-information-in-object-file.md) | 已弃用。 将完整的调试信息放在所有对象文件中。 改为使用 [`/Zi`](z7-zi-zi-debug-information-format.md) 。 |
| [`/Yl`](yl-inject-pch-reference-for-debug-library.md) | 创建调试库时插入 PCH 引用 |
| [`/Yu`](yu-use-precompiled-header-file.md) | 在生成期间使用预编译头文件。 |
| [`/Z7`](z7-zi-zi-debug-information-format.md) | 生成与 C 7.0 兼容的调试信息。 |
| [`/Za`](za-ze-disable-language-extensions.md) | 禁用语言扩展。 |
| [`/Zc`](zc-conformance.md) | 指定标准行为。 |
| [`/Ze`](za-ze-disable-language-extensions.md) | 已弃用。 启用语言扩展。 |
| [`/Zf`](zf.md) | 在并行生成中改善 PDB 生成时间。 |
| [`/Zg`](zg-generate-function-prototypes.md) | 在 Visual Studio 2015 中移除。 生成函数原型。 |
| [`/ZH`](zh.md) | 为调试信息中的校验和指定 MD5、SHA-1 或 SHA-256。 |
| [`/ZI`](z7-zi-zi-debug-information-format.md) | 将调试信息包含在与“编辑并继续”兼容的程序数据库中。 |
| [`/Zi`](z7-zi-zi-debug-information-format.md) | 生成完整的调试信息。 |
| [`/Zl`](zl-omit-default-library-name.md) | 从 .obj 文件中移除默认库名（仅限 x86）。 |
| [`/Zm`](zm-specify-precompiled-header-memory-allocation-limit.md) | 指定预编译头内存分配限制。 |
| [`/Zo`](zo-enhance-optimized-debugging.md) | 为优化代码生成增强的调试信息。 |
| [`/Zp`](zp-struct-member-alignment.md) | 封装结构成员。 |
| [`/Zs`](zs-syntax-check-only.md) | 只检查语法。 |
| [`/ZW`](zw-windows-runtime-compilation.md) | 生成要在 Windows 运行时上运行的输出文件。 |

## <a name="see-also"></a>请参阅

[MSVC 编译器选项](compiler-options.md)\
[MSVC 编译器命令行语法](compiler-command-line-syntax.md)
