---
description: 了解详细信息： C999 到 C1999 的编译器错误
title: 编译器致命错误 C999 - C1999
ms.date: 04/21/2019
f1_keywords:
- C1034
- C1036
- C1041
- C1048
- C1063
- C1069
- C1101
- C1102
- C1105
- C1110
- C1111
- C1112
- C1114
- C1193
- C1195
- C1300
- C1301
- C1302
- C1306
- C1384
- C1451
- C1505
- C1901
helpviewer_keywords:
- C1034
- C1036
- C1041
- C1048
- C1063
- C1069
- C1101
- C1102
- C1105
- C1110
- C1111
- C1112
- C1114
- C1193
- C1195
- C1300
- C1301
- C1302
- C1306
- C1384
- C1451
- C1505
- C1901
ms.assetid: 6c8df109-7594-48ed-987a-97d9fe2b04af
ms.openlocfilehash: 45a1e5f1a0ab57048d2a40da0f976b5ff7c8d653
ms.sourcegitcommit: be9a1af0b9d3f1d6c2987d8744392170b8dccab0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/02/2021
ms.locfileid: "106232330"
---
# <a name="compiler-fatal-errors-c999-through-c1999"></a>编译器致命错误 C999 - C1999

文档的本节中的文章介绍了由 Microsoft C/c + + 编译器生成的错误消息的子集。

[!INCLUDE[error-boilerplate](../../error-messages/includes/error-boilerplate.md)]

## <a name="error-messages"></a>Error messages

|错误|消息|
|-----------|-------------|
|[错误 C999](../../error-messages/compiler-errors-1/fatal-error-c999.md)|未知消息请在 Visual C++ 帮助菜单上，选择技术支持命令，或打开技术支持帮助文件了解详细信息|
|[错误 C1001](../../error-messages/compiler-errors-1/fatal-error-c1001.md)|编译器中发生了内部错误。<br /> （编译器文件“*file*”中的第 *number* 行）<br /> 若要解决此问题，请尝试简化或更改以上所列出位置附近的程序。 请在 Visual C++ 帮助菜单上，选择技术支持命令，或打开技术支持帮助文件了解详细信息|
|[错误 C1002](../../error-messages/compiler-errors-1/fatal-error-c1002.md)|在第 2 遍中编译器的堆空间不足|
|[错误 C1003](../../error-messages/compiler-errors-1/fatal-error-c1003.md)|错误计数超过 *number*；正在停止编译|
|[错误 C1004](../../error-messages/compiler-errors-1/fatal-error-c1004.md)|发现意外的文件尾|
|[错误 C1005](../../error-messages/compiler-errors-1/fatal-error-c1005.md)|字符串对于缓冲区太大|
|[错误 C1007](../../error-messages/compiler-errors-1/fatal-error-c1007.md)|无法识别的标志“*string*”（在“*option*”中）|
|[错误 C1008](../../error-messages/compiler-errors-1/fatal-error-c1008.md)|没有指定输入文件|
|[错误 C1009](../../error-messages/compiler-errors-1/fatal-error-c1009.md)|编译器限制: 宏嵌套太深|
|[错误 C1010](../../error-messages/compiler-errors-1/fatal-error-c1010.md)|查找预编译头时意外的文件尾。 是否忘记将 "#include" 添加 \<*file*> 到源？|
|[错误 C1012](fatal-error-c1012.md)|括号不匹配：缺少“*character*”|
|[错误 C1013](fatal-error-c1013.md)|编译器限制: 左括号太多|
|[错误 C1014](fatal-error-c1014.md)|包含文件太多：深度 = *number*|
|[错误 C1016](fatal-error-c1016.md)|#ifdef/#ifndef 应输入标识符|
|[错误 C1017](../../error-messages/compiler-errors-1/fatal-error-c1017.md)|无效的整数常量表达式|
|[错误 C1018](fatal-error-c1018.md)|意外的 #elif|
|[错误 C1019](fatal-error-c1019.md)|意外的 #else|
|[错误 C1020](fatal-error-c1020.md)|意外的 #endif|
|[错误 C1021](fatal-error-c1021.md)|无效的预处理器命令“*string*”|
|[错误 C1022](fatal-error-c1022.md)|应输入 #endif|
|[错误 C1023](fatal-error-c1023.md)|“*file*”：pch 存在意外错误，请尝试重新生成 pch|
|[错误 C1026](../../error-messages/compiler-errors-1/fatal-error-c1026.md)|分析器堆栈溢出，程序太复杂|
|[错误 C1033](../../error-messages/compiler-errors-1/fatal-error-c1033.md)|无法打开程序数据库“*file*”|
|错误 C1034|*file*：不包括路径集|
|[错误 C1035](fatal-error-c1035.md)|表达式太复杂；简化表达式|
|错误 C1036|无法覆盖早期的程序数据库格式，请删除“*file*”并重新编译|
|[错误 C1037](fatal-error-c1037.md)|无法打开对象文件“*file*”|
|[错误 C1038](fatal-error-c1038.md)|编译器限制：“*function*”：控制流状态太复杂；请简化函数|
|错误 C1041|无法打开程序数据库“*file*”；如果要将多个 CL.EXE 写入同一个 .PDB 文件，请使用 /FS|
|[错误 C1045](fatal-error-c1045.md)|编译器限制: 链接规范嵌套太深|
|[错误 C1046](../../error-messages/compiler-errors-1/fatal-error-c1046.md)|编译器限制： *structure* 嵌套太深|
|[错误 C1047](fatal-error-c1047.md)|对象或库文件“*file*”是使用比创建其他对象所用编译器旧的编译器创建的；请重新生成旧的对象和库|
|错误 C1048|未知选项“*string*”（在“*option*”中）|
|[错误 C1049](fatal-error-c1049.md)|无效的数值参数“*value*”|
|[错误 C1051](../../error-messages/compiler-errors-1/fatal-error-c1051.md)|程序数据库文件“*file*”具有过时的格式，将其删除并重新编译|
|[错误 C1052](fatal-error-c1052.md)|程序数据库文件 "*filename*" 是使用/debug： fastlink 的链接器生成的。编译器无法更新此类 PDB 文件;请删除它或使用/Fd 来指定不同的 PDB 文件名|
|[错误 C1053](fatal-error-c1053.md)|“*function*”：函数太大|
|[错误 C1054](../../error-messages/compiler-errors-1/fatal-error-c1054.md)|编译器限制: 初始值设定项嵌套太深|
|[错误 C1055](../../error-messages/compiler-errors-1/fatal-error-c1055.md)|编译器限制: 超出键范围|
|[错误 C1057](../../error-messages/compiler-errors-1/fatal-error-c1057.md)|宏扩展中遇到意外的文件结束|
|[错误 C1060](../../error-messages/compiler-errors-1/fatal-error-c1060.md)|编译器的堆空间不足|
|[错误 C1061](../../error-messages/compiler-errors-1/fatal-error-c1061.md)|编译器限制: 块嵌套太深|
|错误 C1063|编译器限制: 编译器堆栈溢出|
|[错误 C1064](../../error-messages/compiler-errors-1/fatal-error-c1064.md)|编译器限制: 标记已溢出内部缓冲区|
|[错误 C1065](../../error-messages/compiler-errors-1/fatal-error-c1065.md)|编译器限制: 超出标记范围|
|[错误 C1067](../../error-messages/compiler-errors-1/fatal-error-c1067.md)|编译器限制: 已超出类型记录的 64K 大小限制|
|[错误 C1068](fatal-error-c1068.md)|无法打开文件“*file*”|
|错误 C1069|无法读取编译器命令行|
|[错误 C1070](fatal-error-c1070.md)|文件“*file*”中的 #if/#endif 对不匹配|
|[错误 C1071](../../error-messages/compiler-errors-1/fatal-error-c1071.md)|在注释中遇到意外的文件结束|
|[错误 C1073](../../error-messages/compiler-errors-1/fatal-error-c1073.md)|涉及增量编译的内部错误（编译器文件“*file*”中的第 *number* 行）|
|[错误 C1074](fatal-error-c1074.md)|“IDB”是 PDB 文件 *file* 的非法扩展名|
|[错误 C1075](../../error-messages/compiler-errors-1/fatal-error-c1075.md)|左侧的 *token* 与文件结尾不匹配|
|[错误 C1076](../../error-messages/compiler-errors-1/fatal-error-c1076.md)|编译器限制: 达到内部堆限制；使用 /Zm 指定更高的限制|
|[错误 C1077](fatal-error-c1077.md)|编译器限制：不能有 *number* 个以上的命令行选项|
|[错误 C1079](../../error-messages/compiler-errors-1/fatal-error-c1079.md)|编译器限制: 超出 PCH 文件大小限制|
|[错误 C1080](../../error-messages/compiler-errors-1/fatal-error-c1080.md)|编译器限制：命令行选项超出 *number* 个字符的限制|
|[错误 C1081](../../error-messages/compiler-errors-1/fatal-error-c1081.md)|“*file*”：文件名太长|
|[错误 C1082](fatal-error-c1082.md)|无法关闭 *type* 文件：“*file*”： *message*|
|[错误 C1083](../../error-messages/compiler-errors-1/fatal-error-c1083.md)|无法打开 *type* 文件：“*file*”： *message*|
|[错误 C1084](../../error-messages/compiler-errors-1/fatal-error-c1084.md)|无法读取 *type* 文件：“*file*”： *message*|
|[错误 C1085](../../error-messages/compiler-errors-1/fatal-error-c1085.md)|无法写入 *type* 文件：“*file*”： *message*|
|[错误 C1086](fatal-error-c1086.md)|无法查找 *type* 文件：“*file*”： *message*|
|[错误 C1087](fatal-error-c1087.md)|无法告知 *type* 文件：“*file*”： *message*|
|[错误 C1088](fatal-error-c1088.md)|无法刷新 *type* 文件：“*file*”： *message*|
|[错误 C1089](fatal-error-c1089.md)|无法截断 *type* 文件：“*file*”： *message*|
|[错误 C1090](fatal-error-c1090.md)|PDB API 调用失败，错误代码“*code*”：“*message*”|
|[错误 C1091](fatal-error-c1091.md)|编译器限制：字符串长度超过 *number* 个字节|
|[错误 C1092](../../error-messages/compiler-errors-1/fatal-error-c1092.md)|“编辑并继续”不支持对数据类型的更改；需要生成|
|[错误 C1093](../../error-messages/compiler-errors-1/fatal-error-c1093.md)|API 调用“*function*”对“*HRESULT*”失败：“*description*”|
|[错误 C1094](../../error-messages/compiler-errors-1/fatal-error-c1094.md)|“-Zm *number*”：命令行选项与用于生成预编译头（“-Zm *number*”）的值不一致|
|[错误 C1098](fatal-error-c1098.md)|版本与“编辑并继续”引擎不匹配|
|[错误 C1099](fatal-error-c1099.md)|“编辑并继续”引擎正在终止编译|
|[错误 C1100](fatal-error-c1100.md)|无法初始化 OLE： *error*|
|错误 C1101|无法创建特性“*identifier*”的处理程序|
|错误 C1102|无法进行初始化： *error*|
|[错误 C1103](fatal-error-c1103.md)|导入 progid 时遇到错误：“*message*”|
|[错误 C1104](fatal-error-c1104.md)|导入 libid 时遇到错误：“*message*”|
|错误 C1105|*message*: *error*|
|[错误 C1107](../../error-messages/compiler-errors-1/fatal-error-c1107.md)|未能找到程序集“*assembly*”：请使用 /AI 或通过设置 LIBPATH 环境变量指定程序集搜索路径|
|[错误 C1108](fatal-error-c1108.md)|无法找到 DLL：“*file*”|
|[错误 C1109](fatal-error-c1109.md)|无法在 DLL“*file*”中找到“*symbol*”|
|错误 C1110|嵌套的模板/泛型定义太多|
|错误 C1111|模板/泛型参数太多|
|错误 C1112|编译器限制： "*number*" 个宏参数太多，只允许使用 *数量*|
|[错误 C1113](../../error-messages/compiler-errors-1/fatal-error-c1113.md)|在“*file*”上 #using 失败|
|错误 C1114|“*file*”：WinRT 不支持托管程序集的 #using|
|[错误 C1120](../../error-messages/compiler-errors-1/fatal-error-c1120.md)|对于“*function*”，调用 GetProcAddress 失败|
|[错误 C1121](../../error-messages/compiler-errors-1/fatal-error-c1121.md)|调用 CryptoAPI 失败|
|[错误 C1126](../../error-messages/compiler-errors-1/fatal-error-c1126.md)|自动分配超过 *size*|
|[错误 C1128](../../error-messages/compiler-errors-1/fatal-error-c1128.md)|节数超过对象文件格式限制: 请使用 /bigobj 进行编译|
|[错误 C1189](../../error-messages/compiler-errors-1/fatal-error-c1189.md)|#error： *消息*|
|[错误 C1190](fatal-error-c1190.md)|托管目标代码需要“/clr”选项|
|[错误 C1191](../../error-messages/compiler-errors-1/fatal-error-c1191.md)|只能在全局范围内导入“*file*”|
|[错误 C1192](../../error-messages/compiler-errors-1/fatal-error-c1192.md)|在“*file*”上 #using 失败|
|错误 C1193|*file*(*line*) 中预期的错误未出现|
|错误 C1195|在同一命令行上使用 /Yu 和 /Yc 与 /clr 选项不兼容|
|[错误 C1196](fatal-error-c1196.md)|"*identifier*"：在类型库 "*typelib*" 中找到的标识符不是有效的 c + + 标识符|
|[错误 C1197](../../error-messages/compiler-errors-1/fatal-error-c1197.md)|无法引用“*file*”，因为程序已经引用了“*file*”|
|[错误 C1201](fatal-error-c1201.md)|类模板定义中出现语法错误后无法继续|
|[错误 C1202](fatal-error-c1202.md)|递归类型或函数依赖项上下文太复杂|
|[错误 C1205](fatal-error-c1205.md)|安装的运行时版本不支持这些泛型|
|[错误 C1206](fatal-error-c1206.md)|安装的运行时版本不支持 per-appdomain 数据|
|[错误 C1207](fatal-error-c1207.md)|安装的运行时版本不支持托管模板|
|[错误 C1208](fatal-error-c1208.md)|安装的运行时版本不支持在堆栈上分配引用类|
|[错误 C1209](fatal-error-c1209.md)|安装的运行时版本不支持友元程序集|
|[错误 C1210](fatal-error-c1210.md)|安装的运行时版本不支持 /clr:pure 和 /clr:safe|
|[错误 C1211](fatal-error-c1211.md)|安装的运行时版本不支持 TypeForwardedTo 自定义特性|
|错误 C1300|访问程序数据库 *file* (*message*) 时出错|
|错误 C1301|访问程序数据库 *file* 时出错，无效的格式，请删除并重新生成|
|错误 C1302|在配置文件数据库“*file*”中没有模块“*module*”的配置文件数据|
|[错误 C1305](../../error-messages/compiler-errors-1/fatal-error-c1305.md)|配置文件数据库“*file*”是用于另一个体系结构的|
|错误 C1306|配置文件数据基“*file*”的上次修改不是优化分析；优化决策可能已经过期|
|[错误 C1307](../../error-messages/compiler-errors-1/fatal-error-c1307.md)|自收集配置文件数据后已编辑了程序|
|[错误 C1308](../../error-messages/compiler-errors-1/fatal-error-c1308.md)|*file*：不支持链接程序集|
|[错误 C1309](../../error-messages/compiler-errors-1/fatal-error-c1309.md)|C2.DLL 和 PGODB *ver*.DLL 的版本不匹配|
|[错误 C1310](fatal-error-c1310.md)|按配置优化不能与 OpenMP 一起使用|
|[错误 C1311](../../error-messages/compiler-errors-1/fatal-error-c1311.md)|COFF 格式无法以静态方式初始化“*symbol*”（地址为 *number* 个字节）|
|[错误 C1312](fatal-error-c1312.md)|函数中的条件分支太多。  简化或重构源代码。|
|[错误 C1313](../../error-messages/compiler-errors-1/fatal-error-c1313.md)|编译器限制： *type* 块的嵌套深度不能深于 *number* 级|
|[错误 C1350](../../error-messages/compiler-errors-1/fatal-error-c1350.md)|加载 dll“*file*”时出错：没有找到 dll|
|[错误 C1351](../../error-messages/compiler-errors-1/fatal-error-c1351.md)|加载 dll“*file*”时出错：版本不兼容|
|[错误 C1352](fatal-error-c1352.md)|函数“*function*”（模块“*module*”中）的 MSIL 无效或已损坏|
|[错误 C1353](fatal-error-c1353.md)|元数据操作失败: 未安装运行时或运行时版本不匹配|
|[错误 C1382](../../error-messages/compiler-errors-1/fatal-error-c1382.md)|“*obj*”生成后，已重新生成 PCH 文件“*file*”。 请重新生成此对象|
|[错误 C1383](fatal-error-c1383.md)|编译器选项 /GL 与安装的公共语言运行时版本不兼容|
|错误 C1384|链接“*file*”时 PGO_PATH_TRANSLATION 的设置不正确|
|错误 C1451|编译以下位置的并发::parallel_for_each 的调用关系图时，未能生成调试信息：“*callsite*”|
|错误 C1505|无法恢复的先行分析错误|
|[错误 C1506](../../error-messages/compiler-errors-1/fatal-error-c1506.md)|无法恢复的块范围错误|
|[错误 C1508](fatal-error-c1508.md)|编译器限制：“*function*”：多于 65535 个参数字节|
|[错误 C1509](../../error-messages/compiler-errors-1/fatal-error-c1509.md)|编译器限制：函数“*function*”中有太多异常处理程序状态；简化函数|
|[错误 C1510](../../error-messages/compiler-errors-1/fatal-error-c1510.md)|无法打开语言资源 clui.dll|
|[错误 C1601](../../error-messages/compiler-errors-1/fatal-error-c1601.md)|不支持的内联程序集操作码|
|[错误 C1602](../../error-messages/compiler-errors-1/fatal-error-c1602.md)|不支持的内部函数|
|[错误 C1603](../../error-messages/compiler-errors-1/fatal-error-c1603.md)|内联程序集分支目标超出范围 *number* 个字节|
|[错误 C1852](fatal-error-c1852.md)|“*file*”不是有效的预编译头文件|
|[错误 C1853](../../error-messages/compiler-errors-1/fatal-error-c1853.md)|“*file*”预编译头文件来自早期版本的编译器，或者预编译头为 C++，却在 C 中使用它（或相反）|
|[错误 C1854](../../error-messages/compiler-errors-1/fatal-error-c1854.md)|无法覆盖在对象文件“*file*”中创建预编译头过程中形成的信息|
|[错误 C1900](../../error-messages/compiler-errors-1/fatal-error-c1900.md)|“*tool*”版本“*number*”和“*tool*”版本“*number*”间的 Il 不匹配|
|错误 C1901|内部内存管理错误|
|[错误 C1902](../../error-messages/compiler-errors-1/fatal-error-c1902.md)|程序数据库管理器不匹配；请检查安装|
|[错误 C1903](fatal-error-c1903.md)|无法从以前的错误中恢复；正在停止编译|
|[错误 C1904](fatal-error-c1904.md)|错误的提供程序交互：“*file*”|
|[错误 C1905](../../error-messages/compiler-errors-1/fatal-error-c1905.md)|前端和后端不兼容(必须以同一处理器为目标)。|

## <a name="see-also"></a>另请参阅

[C/C++ 编译器和生成工具错误与警告](../compiler-errors-1/c-cpp-build-errors.md)
