---
description: 了解详细信息：严重错误 C1090 PDB API 调用失败
title: 错误 C1090
ms.date: 04/01/2021
f1_keywords:
- C1090
helpviewer_keywords:
- C1090
ms.openlocfilehash: 4195fd069aa770593a4ec088286aad7f3ec9e062
ms.sourcegitcommit: be9a1af0b9d3f1d6c2987d8744392170b8dccab0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106232586"
---
# <a name="fatal-error-c1090"></a>错误 C1090

> PDB API 调用失败，错误代码 "*错误号*"： *消息*

处理 PDB 文件时出错。

错误 C1090 是不单独报告的不常见编译器 PDB 文件错误的全部捕获。 我们只提供了解决此问题的一般建议：

- 在生成目录中执行清理操作，然后执行解决方案的完整生成。

- 重新启动计算机，或者在 TaskManager 中检查是否有被或无 mspdbsrv.exe 响应的进程。

- 关闭项目目录中的防病毒检查。

- [`/Zf`](../../build/reference/zf.md)如果使用 [`/MP`](../../build/reference/mp-build-with-multiple-processes.md) with MSBuild 或其他并行生成过程，请使用编译器选项。

- 尝试使用64位托管工具集生成。

有关更多疑难解答或解决方法的信息，请在 [开发人员社区](https://aka.ms/vsfeedback/browsecpp) 或 [Stack Overflow](https://stackoverflow.com/search?q=C1090)上搜索此错误。

你还可以在开发人员社区报告问题。 有关详细信息，请参阅 [如何使用 Microsoft c + + 工具集报告问题](../../overview/how-to-report-a-problem-with-the-visual-cpp-toolset.md)。
