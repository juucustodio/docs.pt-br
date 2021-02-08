---
description: 'Saiba mais sobre o método: ICLRMemoryNotificationCallback:: OnMemoryNotification'
title: Método ICLRMemoryNotificationCallback::OnMemoryNotification
ms.date: 03/30/2017
api_name:
- ICLRMemoryNotificationCallback.OnMemoryNotification
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMemoryNotificationCallback::OnMemoryNotification
helpviewer_keywords:
- ICLRMemoryNotificationCallback::OnMemoryNotification method [.NET Framework hosting]
- OnMemoryNotification method [.NET Framework hosting]
ms.assetid: 5612a44d-56cc-4f34-af31-8c9809ba9431
topic_type:
- apiref
ms.openlocfilehash: 92041c433fa82bb63afda7968eb8c6e1fa72acb3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789894"
---
# <a name="iclrmemorynotificationcallbackonmemorynotification-method"></a>Método ICLRMemoryNotificationCallback::OnMemoryNotification

Notifica o Common Language Runtime (CLR) da carga de memória no computador.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT OnMemoryNotification (  
    [in] EMemoryAvailable eMemoryAvailable  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `eMemoryAvailable`  
 no Um dos valores de [EMemoryAvailable](ememoryavailable-enumeration.md) , indicando a pressão de memória que o computador está enfrentando no momento.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`OnMemoryNotification` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O CLR registra um retorno de chamada para `OnMemoryNotification` usando uma chamada para o método [IHostMemoryManager:: RegisterMemoryNotificationCallback](ihostmemorymanager-registermemorynotificationcallback-method.md) . O tempo de execução usa as informações retornadas no retorno de chamada para liberar memória adicional quando o host relata que os recursos de memória estão em execução baixa.  
  
> [!NOTE]
> Chamadas para `OnMemoryNotification` nunca bloquear. Eles sempre retornam imediatamente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostMemoryManager](ihostmemorymanager-interface.md)
- [Método RegisterMemoryNotificationCallback](ihostmemorymanager-registermemorynotificationcallback-method.md)
- [Interface ICLRMemoryNotificationCallback](iclrmemorynotificationcallback-interface.md)
