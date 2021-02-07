---
description: 'Saiba mais sobre o método: IHostIoCompletionManager:: InitializeHostOverlapped'
title: Método IHostIoCompletionManager::InitializeHostOverlapped
ms.date: 03/30/2017
api_name:
- IHostIoCompletionManager.InitializeHostOverlapped
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped
helpviewer_keywords:
- IHostIoCompletionManager::InitializeHostOverlapped method [.NET Framework hosting]
- InitializeHostOverlapped method [.NET Framework hosting]
ms.assetid: c35199bf-bc47-4901-b467-4e8a37644bbb
topic_type:
- apiref
ms.openlocfilehash: 10be7edb67143937dec6efc6e35466466374d32d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99708457"
---
# <a name="ihostiocompletionmanagerinitializehostoverlapped-method"></a>Método IHostIoCompletionManager::InitializeHostOverlapped

Fornece ao host uma oportunidade de inicializar quaisquer dados personalizados para acrescentar a uma estrutura Win32 `OVERLAPPED` que é usada para solicitações de e/s assíncronas.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT InitializeHostOverlapped (  
    [in] void* pvOverlapped  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pvOverlapped`  
 no Um ponteiro para a estrutura do Win32 `OVERLAPPED` a ser incluído na solicitação de e/s.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`InitializeHostOverlapped` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Não havia memória suficiente disponível para alocar o recurso solicitado.|  
  
## <a name="remarks"></a>Comentários  

 As funções da plataforma Windows usam a `OVERLAPPED` estrutura para armazenar o estado para solicitações de e/s assíncronas. O CLR chama o `InitializeHostOverlapped` método para dar ao host a oportunidade de acrescentar dados personalizados a uma `OVERLAPPED` instância.  
  
> [!IMPORTANT]
> Para chegar ao início do bloco de dados personalizado, os hosts devem definir o deslocamento para o tamanho da `OVERLAPPED` estrutura ( `sizeof(OVERLAPPED)` ).  
  
 Um valor de retorno de E_OUTOFMEMORY indica que o host falhou ao inicializar seus dados personalizados. Nesse caso, o CLR relata um erro e falha na chamada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRIoCompletionManager](iclriocompletionmanager-interface.md)
- [Método GetHostOverlappedSize](ihostiocompletionmanager-gethostoverlappedsize-method.md)
- [Interface IHostIoCompletionManager](ihostiocompletionmanager-interface.md)
