---
description: 'Saiba mais sobre: método IHostSecurityManager:: GetSecurityContext'
title: Método IHostSecurityManager::GetSecurityContext
ms.date: 03/30/2017
api_name:
- IHostSecurityManager.GetSecurityContext
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostSecurityManager::GetSecurityContext
helpviewer_keywords:
- GetSecurityContext method [.NET Framework hosting]
- IHostSecurityManager::GetSecurityContext method [.NET Framework hosting]
ms.assetid: 958970d6-f6a2-4b84-b32a-f555cbaf8f61
topic_type:
- apiref
ms.openlocfilehash: 0dc9e0380d2fb218b68f6beb85fa1ccba8826d85
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99671554"
---
# <a name="ihostsecuritymanagergetsecuritycontext-method"></a>Método IHostSecurityManager::GetSecurityContext

Obtém o [IHostSecurityContext](ihostsecuritycontext-interface.md) solicitado do host.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetSecurityContext (  
    [in]  EContextType eContextType,
    [out] IHostSecurityContext** ppSecurityContext  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `eContextType`  
 no Um dos valores de [EContextType](econtexttype-enumeration.md) , que indica o tipo de contexto de segurança a ser retornado.  
  
 `ppSecurityContext`  
 fora O endereço de um ponteiro de interface para o `IHostSecurityContext` de `eContextType` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`GetSecurityContext` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 Um host pode controlar todo o acesso ao código para tokens de thread tanto pelo CLR quanto pelo código do usuário. Ele também pode garantir que as informações completas do contexto de segurança sejam passadas entre operações assíncronas ou pontos de código com acesso restrito ao código. `IHostSecurityContext` encapsula essas informações de contexto de segurança, que são opacas para o CLR. O CLR captura essas informações e as move entre a expedição do item de trabalho do pool de threads, a execução do finalizador e a construção de módulo e classe.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Enumeração EContextType](econtexttype-enumeration.md)
- [Interface IHostSecurityContext](ihostsecuritycontext-interface.md)
- [Interface IHostSecurityManager](ihostsecuritymanager-interface.md)
