---
title: /clr（公共语言运行时编译）
description: 使用 Microsoft c + + 编译器选项/clr 将 c + +/CLI 和 c + + 代码编译为托管代码。
ms.date: 10/27/2020
f1_keywords:
- /CLR
- VC.Project.VCNMakeTool.CompileAsManaged
- VC.Project.VCCLCompilerTool.CompileAsManaged
helpviewer_keywords:
- cl.exe compiler, common language runtime option
- -clr compiler option [C++]
- clr compiler option [C++]
- /clr compiler option [C++]
- Managed Extensions for C++, compiling
- common language runtime, /clr compiler option
ms.assetid: fec5a8c0-40ec-484c-a213-8dec918c1d6c
ms.openlocfilehash: 1e0e0ac42316f7d76ea478d9666018e5855ceec6
ms.sourcegitcommit: dc77cf3b5b644d8e2adf595540b98194ab95c6e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106377250"
---
# <a name="clr-common-language-runtime-compilation"></a>`/clr` (公共语言运行时编译) 

允许应用程序和组件使用公共语言运行时中的功能 (CLR) 并启用 c + +/CLI 编译。

## <a name="syntax"></a>语法

> **`/clr`**\[**`:`**_options_]

## <a name="arguments"></a>参数

options\
以下一个或多个以逗号分隔的参数。

- 无

   如果没有选项， **`/clr`** 则会为组件创建元数据。 元数据可由其他 CLR 应用程序使用，并使组件可以使用其他 CLR 组件的元数据中的类型和数据。 有关详细信息，请参阅[混合（本机和托管）程序集](../../dotnet/mixed-native-and-managed-assemblies.md)。

::: moniker range="msvc-160"

- **`netcore`**

   从 Visual Studio 2019 版本16.4 开始提供， **`/clr:netcore`** 使用最新的跨平台 .net framework （也称为 .Net Core）创建组件的元数据和代码。 元数据可由其他 .NET Core 应用程序使用。 而且，选项使组件能够使用其他 .NET Core 组件的元数据中的类型和数据。

::: moniker-end

- **`nostdlib`**

   指示编译器忽略默认 *`\clr`* 目录。 如果包含 DLL 的多个版本，则编译器会生成错误，如 System.dll。 使用此选项可以指定编译过程中要使用的特定框架。

- **`pure`**

   **`/clr:pure` 已弃用**。 在 Visual Studio 2017 及更高版本中，该选项已删除。 建议移植对 C# 来说必须是纯 MSIL 的代码。

- **`safe`**

   **`/clr:safe` 已弃用**。 在 Visual Studio 2017 及更高版本中，该选项已删除。 建议移植对 C# 来说必须是安全 MSIL 的代码。

- **`noAssembly`**

   **`/clr:noAssembly` 已弃用**。 改用[ `/LN` (创建 MSIL 模块) ](ln-create-msil-module.md) 。

   告诉编译器不要将程序集清单插入输出文件中。 默认情况下，该 **`noAssembly`** 选项不起作用。

   清单中不具有程序集元数据的托管程序称为 " *模块*"。 **`noAssembly`** 选项只能用于生成模块。 如果使用和进行编译 [`/c`](c-compile-without-linking.md) **`/clr:noAssembly`** ，则在 [`/NOASSEMBLY`](noassembly-create-a-msil-module.md) 链接器阶段指定选项以创建模块。

   在 Visual Studio 2005 之前， **`/clr:noAssembly`** 需要 **`/LD`** 。 **`/LD`** 当前在指定时是隐含的 **`/clr:noAssembly`** 。

- **`initialAppDomain`**

   **`initialAppDomain` 已过时**。 允许 c + +/CLI 应用程序在 CLR 版本1上运行。  使用 ASP.NET 编译的应用程序 **`initialAppDomain`** 不应由使用的应用程序使用，因为它在 CLR 版本1中不受支持。

## <a name="remarks"></a>备注

*托管代码* 是可以由 CLR 检查和管理的代码。 托管代码可以访问托管对象。 有关详细信息，请参阅[ `/clr` 限制](clr-restrictions.md)。

有关如何开发用于在 c + + 中定义和使用托管类型的应用程序的信息，请参阅 [运行时平台的组件扩展](../../extensions/component-extensions-for-runtime-platforms.md)。

使用编译的应用程序 **`/clr`** 可能包含也可能不包含托管数据。

若要在托管应用程序上启用调试，请参阅[ `/ASSEMBLYDEBUG` (Add DebuggableAttribute) ](assemblydebug-add-debuggableattribute.md)。

只有 CLR 类型会在垃圾回收堆上实例化。 有关更多信息，请参阅[类和结构](../../extensions/classes-and-structs-cpp-component-extensions.md)。 若要将函数编译为本机代码，请使用 `unmanaged` 杂注。 有关详细[信息，请参阅 `managed` `unmanaged` 。 ](../../preprocessor/managed-unmanaged.md)

默认情况下， **`/clr`** 不起作用。 当 **`/clr`** 有效时， **`/MD`** 也会生效。 有关详细信息，请参阅[ `/MD` 、 `/MT` 、 `/LD` (使用 Run-Time 库) ](md-mt-ld-use-run-time-library.md)。 **`/MD`** 确保从标准头文件中选择运行时例程的动态链接的多线程版本。 托管编程必须进行多线程处理，因为 CLR 垃圾回收器将在辅助线程中运行终结器。

如果使用进行编译 **`/c`** ，则可以使用链接器选项指定生成输出文件的 CLR 类型 [`/CLRIMAGETYPE`](clrimagetype-specify-type-of-clr-image.md) 。

**`/clr`** 隐含 **`/EHa`** ，不支持其他任何 **`/EH`** 选项 **`/clr`** 。 有关详细信息，请参阅[ `/EH` (异常处理模型) ](eh-exception-handling-model.md)。

有关如何确定文件的 CLR 映像类型的信息，请参阅 [`/CLRHEADER`](clrheader.md) 。

传递给链接器的给定调用的所有模块都必须使用相同的运行时库编译器选项 (或) 来进行编译 **`/MD`** **`/LD`** 。

使用 [`/ASSEMBLYRESOURCE`](assemblyresource-embed-a-managed-resource.md) 链接器选项将资源嵌入程序集。 [`/DELAYSIGN`](delaysign-partially-sign-an-assembly.md)、 [`/KEYCONTAINER`](keycontainer-specify-a-key-container-to-sign-an-assembly.md) 和 [`/KEYFILE`](keyfile-specify-key-or-key-pair-to-sign-an-assembly.md) 链接器选项还允许您自定义程序集的创建方式。

**`/clr`** 使用时， `_MANAGED` 符号定义为1。 有关详细信息，请参阅 [预定义的宏](../../preprocessor/predefined-macros.md)。

如果可执行文件是 DLL) ，则会先初始化本机对象文件中的全局变量 `DllMain` ，然后在运行任何托管代码) 之前，初始化托管节中的全局变量 ( (。 [`#pragma init_seg`](../../preprocessor/init-seg.md) 仅影响托管和非托管类别中的初始化顺序。

### <a name="metadata-and-unnamed-classes"></a>元数据和未命名类

命名类出现在名称下的元数据中（例如  `$UnnamedClass$<crc-of-current-file-name>$<index>$` ），其中 `<index>` 是编译中未命名类的顺序计数。 例如，下面的代码示例将在元数据中生成一个未命名类。

```cpp
// clr_unnamed_class.cpp
// compile by using: /clr /LD
class {} x;
```

使用 ildasm.exe 查看元数据。

### <a name="to-set-this-compiler-option-in-the-visual-studio-development-environment"></a>在 Visual Studio 开发环境中设置此编译器选项

1. 打开项目的“属性页”  对话框。 有关详细信息，请参阅[在 Visual Studio 中设置 C++ 编译器和生成属性](../working-with-project-properties.md)。

1. 将 **配置** 下拉列表设置为 " **所有配置**"，并将 " **平台** " 下拉列表设置为 " **所有平台**"。

1. 选择 "**配置属性**" "  >  **c/c + +**" "  >  **常规**" 页。

1. 修改 " **公共语言运行时支持** " 属性。 选择“确定”以保存更改  。

> [!NOTE]
> 在 Visual Studio IDE 中， **`/clr`** 可以在 "属性页" 对话框的 "**配置属性**" "  >  **c/c + +**" "  >  **常规**" 页上单独设置编译器选项。 但是，我们建议使用 CLR 模板来创建项目。 它设置成功创建 CLR 组件所需的所有属性。 设置这些属性的另一种方法是使用 "属性页" 对话框的 "**配置属性**" "高级" 页上的 "**公共语言运行时支持**" 属性  >   。 此属性一次设置与 CLR 相关的其他所有工具选项。

### <a name="to-set-this-compiler-option-programmatically"></a>以编程方式设置此编译器选项

- 请参阅 <xref:Microsoft.VisualStudio.VCProjectEngine.VCCLCompilerTool.CompileAsManaged>。

## <a name="see-also"></a>另请参阅

[MSVC 编译器选项](compiler-options.md)\
[MSVC 编译器命令行语法](compiler-command-line-syntax.md)
