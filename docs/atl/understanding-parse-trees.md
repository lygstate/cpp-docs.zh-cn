---
description: 了解详细信息：了解分析树
title: ATL 注册器和分析树
ms.date: 04/15/2021
helpviewer_keywords:
- parse trees
ms.openlocfilehash: b9442651d8d6e04ee6c309c9d93b76135fe05c57
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539540"
---
# <a name="understanding-parse-trees"></a>了解分析树

你可以在注册器脚本中定义一个或多个分析树，其中每个分析树具有以下形式：

> \<root-key>{\<registry expression>}+

其中：

> *\<root-key>* ::=\
> &emsp;**`HKEY_CLASSES_ROOT`** &vert; **`HKEY_CURRENT_USER`** &vert;\
> &emsp;**`HKEY_LOCAL_MACHINE`** &vert; **`HKEY_USERS`** &vert;\
> &emsp;**`HKEY_PERFORMANCE_DATA`** &vert; **`HKEY_DYN_DATA`** &vert;\
> &emsp;**`HKEY_CURRENT_CONFIG`** &vert; **`HKCR`** &vert; **`HKCU`** &vert;\
> &emsp;**`HKLM`** &vert; **`HKU`** &vert; **`HKPD`** &vert; **`HKDD`** &vert; **`HKCC`**
>
> *\<registry-expression>* ::=\
> &emsp; *\<Add-Key>* &vert; *\<Delete-Key>*
>
> *\<Add-Key>* ::=\
> &emsp; \[**`ForceRemove`** &vert; **`NoRemove`** &vert; **`val`**] *\<Key-Name>* \[*\<Key-Value>*] \[ **`{`** *\<Add-Key>* **`}`** ]
>
> *\<Delete-Key>* ::=\
> &emsp; **`Delete`** *\<Key-Name>*
>
> *\<Key-Name>* ::=\
> &emsp; **`'`**_\<AlphaNumeric>_+**`'`**
>
> *\<AlphaNumeric>* ::=\
> &emsp; 任何非 null 字符。
>
> *\<Key-Value>* ::=\
> &emsp; *\<Key-Type>* *\<Key-Name>*
>
> *\<Key-Type>* ::=\
> &emsp; **`s`** &vert; **`d`**

> [!NOTE]
> **`HKEY_CLASSES_ROOT`** 和 **`HKCR`** 等效; **`HKEY_CURRENT_USER`** 和 **`HKCU`** 等效; 依此类推。

分析树可以向中添加多个键和子项 \<root-key> 。 注册器会保持每个子项句柄处于打开状态，直到分析器完成分析其所有子项。 这比一次对一个键进行操作更为有效。 下面是一个示例：

```rgs
HKEY_CLASSES_ROOT
{
    'MyVeryOwnKey'
    {
        'HasASubKey'
        {
            'PrettyCool'
        }
    }
}
```

此时，注册机构最初会打开 (创建) `HKEY_CLASSES_ROOT\MyVeryOwnKey` 。 然后，它会发现 `MyVeryOwnKey` 具有子项。 `MyVeryOwnKey`注册器会保持句柄并打开 (`HasASubKey` 使用此父句柄创建) ，而不是将键关闭。 如果没有打开父句柄， (系统注册表的速度会较慢。 ) 因此，打开 `HKEY_CLASSES_ROOT\MyVeryOwnKey` 并 `HasASubKey` 打开 `MyVeryOwnKey` 作为父对象的速度比打开 `MyVeryOwnKey` 、关闭 `MyVeryOwnKey` 、然后打开 `MyVeryOwnKey\HasASubKey` 。

## <a name="see-also"></a>另请参阅

[创建注册器脚本](../atl/creating-registrar-scripts.md)
