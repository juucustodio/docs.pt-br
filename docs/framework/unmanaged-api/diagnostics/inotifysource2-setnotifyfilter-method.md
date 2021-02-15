---
description: 'Saiba mais sobre o método: INotifySource2:: SetNotifyFilter'
title: Método INotifySource2::SetNotifyFilter
ms.date: 03/30/2017
api_name:
- INotifySource2.SetNotifyFilter
api_location:
- diasymreader.dll
api_type:
- COM
f1_keywords:
- INotifySource2::SetNotifyFilter
helpviewer_keywords:
- INotifySource2::SetNotifyFilter method [.NET Framework debugging]
- SetNotifyFilter method [.NET Framework debugging]
ms.assetid: 6351fc92-b126-4af6-9bf3-0a8ce92845fc
topic_type:
- apiref
ms.openlocfilehash: 2aaf2a5253f8a9acb67c4b538f109a7a62559d12
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800221"
---
# <a name="inotifysource2setnotifyfilter-method"></a>Método INotifySource2::SetNotifyFilter

Atribui um filtro de notificação para uso com esta origem.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetNotifyFilter  
(  
    [in]  NOTIFY_FILTER   in_NotifyFilter,  
    [in]  USER_THREAD*    in_pUserThreadFilter  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `in_NotifyFilter`  
 no Uma combinação de bits bit a [NOTIFY_FILTER](notify-filter-enumeration.md) valores de enumeração que identificam retornos de chamada para a API do depurador.  
  
 `in_pUserThreadFilter`  
 no Um ponteiro para uma estrutura de [USER_THREAD](user-thread-structure.md) que identifica threads para a API do depurador.  
  
## <a name="return-value"></a>Valor retornado  

 S_OK se o método tiver sucesso.  
  
## <a name="requirements"></a>Requisitos  

 **Cabeçalho:** ProtocolNotify2. idl  
  
## <a name="see-also"></a>Consulte também

- [Interface INotifySource2](inotifysource2-interface.md)
- [Interface INotifyConnection2](inotifyconnection2-interface.md)
- [Interface INotifySink2](inotifysink2-interface.md)
