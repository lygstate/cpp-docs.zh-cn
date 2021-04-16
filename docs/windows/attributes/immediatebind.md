---
description: '了解详细信息： immediatebind (c + + COM 特性) '
title: 'immediatebind (c + + COM 特性) '
ms.date: 04/15/2021
f1_keywords:
- vc-attr.immediatebind
helpviewer_keywords:
- immediatebind attribute
ms.assetid: 186d40e6-9166-4d0c-9853-4e7e4d25226f
ms.openlocfilehash: b4bd8ddd61de7bc249fef2e6b0a140f4ee5cff95
ms.sourcegitcommit: d531c567c268b676b44abbc8416ba7e20d22044b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2021
ms.locfileid: "107539751"
---
# `immediatebind`

指示将立即通知数据库对数据绑定对象的属性所做的所有更改。

## <a name="syntax"></a>语法

```cpp
[immediatebind]
```

## <a name="remarks"></a>备注

**`immediatebind`** C + + 特性具有与 MIDL 特性相同的功能 [`immediatebind`](/windows/win32/Midl/immediatebind) 。

## <a name="example"></a>示例

[`bindable`](bindable.md)有关如何使用 **immediatebind** 的示例，请参阅。

## <a name="requirements"></a>要求

| 特性上下文 | 值 |
|-|-|
|**适用于**|接口方法|
|**可重复**|否|
|**必需属性**|无|
|**无效的特性**|无|

有关详细信息，请参见 [特性上下文](cpp-attributes-com-net.md#contexts)。

## <a name="see-also"></a>另请参阅

[IDL 特性](idl-attributes.md)<br/>
[方法特性](method-attributes.md)<br/>
[`defaultbind`](defaultbind.md)<br/>
[`displaybind`](displaybind.md)<br/>
[`requestedit`](requestedit.md)
