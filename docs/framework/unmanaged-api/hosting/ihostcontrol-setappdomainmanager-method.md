---
description: 'Saiba mais sobre o método: IHostControl:: SetAppDomainManager'
title: Método IHostControl::SetAppDomainManager
ms.date: 03/30/2017
api_name:
- IHostControl.SetAppDomainManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostControl::SetAppDomainManager
helpviewer_keywords:
- IHostControl::SetAppDomainManager method [.NET Framework hosting]
- SetAppDomainManager method [.NET Framework hosting]
ms.assetid: 6562bbe7-0d67-4c50-a958-3a18cf680375
topic_type:
- apiref
ms.openlocfilehash: 1fc5efc0afad73d1805338140f186a50913ca542
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99708886"
---
# <a name="ihostcontrolsetappdomainmanager-method"></a>Método IHostControl::SetAppDomainManager

Notifica o host de que um domínio de aplicativo foi criado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT SetAppDomainManager (  
    [in] DWORD     dwAppDomainID,  
    [in] IUnknown* pUnkAppDomainManager  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwAppDomainID`  
 no O identificador numérico do selecionado <xref:System.AppDomain> .  
  
 `pUnkAppDomainManager`  
 no Um ponteiro para o <xref:System.AppDomainManager> objeto que o host implementa como `IUnknown` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`SetAppDomainManager` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O <xref:System.AppDomainManager> fornece ao host um mecanismo para inicializar em código gerenciado e controlar a criação e as configurações de cada um <xref:System.AppDomain> . O <xref:System.AppDomainManager> é carregado em cada um <xref:System.AppDomain> quando <xref:System.AppDomain> é criado. Se escolher, o CLR notifica o host de que o domínio do aplicativo foi criado definindo o valor do `pUnkAppDomainManager` parâmetro.  
  
 Em sua implementação do `SetAppDomainManager` método, o host pode definir o nome do assembly e o tipo para o Gerenciador de domínio do aplicativo.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.AppDomain>
- <xref:System.AppDomainManager>
- [Interface IHostControl](ihostcontrol-interface.md)
