---
description: 'Saiba mais sobre: enumeração de NOTIFY_FILTER'
title: Enumeração NOTIFY_FILTER
ms.date: 03/30/2017
api_name:
- NOTIFY_FILTER
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- NOTIFY_FILTER
helpviewer_keywords:
- NOTIFY_FILTER enumeration [.NET Framework debugging]
ms.assetid: 4789d08f-8683-45d3-ac30-73d48c61e470
topic_type:
- apiref
ms.openlocfilehash: 0ed09af0af302b08102b7b08fa72a2d255c5b231
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99761480"
---
# <a name="notify_filter-enumeration"></a>Enumeração NOTIFY_FILTER

Identifica retornos de chamada para funções do depurador. Para obter mais informações, consulte o método [INotifySource2:: SetNotifyFilter](inotifysource2-setnotifyfilter-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
enum tagNOTIFY_FILTER  
{  
    NOTIFY_FILTER_ONSYNCCALLOUT    = 0x1,  
    NOTIFY_FILTER_ONSYNCCALLENTER  = 0x2,  
    NOTIFY_FILTER_ONSYNCCALLEXIT   = 0x4,  
    NOTIFY_FILTER_ONSYNCCALLRETURN = 0x8,  
    NOTIFY_FILTER_ALLSYNC = NOTIFY_FILTER_ONSYNCCALLOUT | NOTIFY_FILTER_ONSYNCCALLENTER | NOTIFY_FILTER_ONSYNCCALLEXIT | NOTIFY_FILTER_ONSYNCCALLRETURN,  
    NOTIFY_FILTER_ALL              = 0xffffffff,  
    NOTIFY_FILTER_NONE             = 0  
};  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`NOTIFY_FILTER_ONSYNCCALLOUT`|Indica que o método [INotifySink2:: OnSyncCallOut](inotifysink2-onsynccallout-method.md) deve ser invocado.|  
|`NOTIFY_FILTER_ONSYNCCALLENTER`|Indica que o método [INotifySink2:: OnSyncCallEnter](inotifysink2-onsynccallenter-method.md) deve ser invocado.|  
|`NOTIFY_FILTER_ONSYNCCALLEXIT`|Indica que o método [INotifySink2:: OnSyncCallExit](inotifysink2-onsynccallexit-method.md) deve ser invocado.|  
|`NOTIFY_FILTER_ONSYNCCALLRETURN`|Indica que o método [INotifySink2:: OnSyncCallReturn](inotifysink2-onsynccallreturn-method.md) deve ser invocado.|  
|`NOTIFY_FILTER_ALLSYNC`|Indica que todos os métodos [INotifySink2](inotifysink2-interface.md) devem ser invocados.|  
|`NOTIFY_FILTER_ALL`|Ativa todas as notificações existentes e futuras.|  
|`NOTIFY_FILTER_NONE`|Indica que nenhum método de notificação deve ser invocado.|  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** ProtocolNotify2. idl  
  
## <a name="see-also"></a>Consulte também

- [Enumerações de armazenamento de símbolo de diagnóstico](diagnostics-symbol-store-enumerations.md)
