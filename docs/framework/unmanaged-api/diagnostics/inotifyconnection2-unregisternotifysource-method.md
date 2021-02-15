---
description: 'Saiba mais sobre o método: INotifyConnection2:: UnregisterNotifySource'
title: Método INotifyConnection2::UnregisterNotifySource
ms.date: 03/30/2017
api_name:
- INotifyConnection2.UnregisterNotifySource
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifyConnection2::UnregisterNotifySource
helpviewer_keywords:
- INotifyConnection2::UnregisterNotifySource method [.NET Framework debugging]
- UnregisterNotifySource method [.NET Framework debugging]
ms.assetid: 2fc6c715-646f-41fd-9c12-c59b40575269
topic_type:
- apiref
ms.openlocfilehash: d3b82665375f54d33b6a5581241788d828060a83
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800299"
---
# <a name="inotifyconnection2unregisternotifysource-method"></a>Método INotifyConnection2::UnregisterNotifySource

Remove um objeto de origem de notificação especificado da conexão.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT UnregisterNotifySource  
(  
    [in]  INotifySource2*  in_pNotifySource  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `in_pNotifySource`  
 no Objeto de notificação a ser cancelado.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** ProtocolNotify2. idl  
  
## <a name="see-also"></a>Consulte também

- [Interface INotifyConnection2](inotifyconnection2-interface.md)
- [Interface INotifySource2](inotifysource2-interface.md)
- [Interface INotifySink2](inotifysink2-interface.md)
- [Método RegisterNotifySource](inotifyconnection2-registernotifysource-method.md)
