---
description: 'Saiba mais sobre o método: ICLRRuntimeHost:: ExecuteInAppDomain'
title: Método ICLRRuntimeHost::ExecuteInAppDomain
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.ExecuteInAppDomain
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::ExecuteInAppDomain
helpviewer_keywords:
- ICLRRuntimeHost::ExecuteInAppDomain method [.NET Framework hosting]
- ExecuteInAppDomain method [.NET Framework hosting]
ms.assetid: e2b0e2db-3fae-4b56-844e-d30a125a660c
topic_type:
- apiref
ms.openlocfilehash: 6640713b55e05817f39af819d5e41ee1f2a10b68
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799733"
---
# <a name="iclrruntimehostexecuteinappdomain-method"></a>Método ICLRRuntimeHost::ExecuteInAppDomain

Especifica o <xref:System.AppDomain> no qual executar o código gerenciado especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ExecuteInAppDomain(  
    [in] DWORD AppDomainId,
    [in] FExecuteInDomainCallback pCallback,
    [in] void* cookie  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `AppDomainId`  
 no A ID numérica do <xref:System.AppDomain> na qual executar o método especificado.  
  
 `pCallback`  
 no Um ponteiro para a função a ser executada dentro do especificado <xref:System.AppDomain> .  
  
 `cookie`  
 no Um ponteiro para uma memória opaca alocada pelo chamador. Esse parâmetro é passado pelo Common Language Runtime (CLR) para o retorno de chamada do domínio. Não é uma memória heap gerenciada pelo tempo de execução; a alocação e o tempo de vida dessa memória são controlados pelo chamador.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`ExecuteInAppDomain` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Se um método retornar E_FAIL, o CLR não poderá mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 `ExecuteInAppDomain` permite que o host assuma o controle sobre qual gerenciado <xref:System.AppDomain> o método gerenciado especificado deve ser executado. Você pode obter o valor do identificador de um domínio de aplicativo, que corresponde ao valor da <xref:System.AppDomain.Id%2A> propriedade, chamando o [método GetCurrentAppDomainId](iclrruntimehost-getcurrentappdomainid-method.md).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeHost](iclrruntimehost-interface.md)
