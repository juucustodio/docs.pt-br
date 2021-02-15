---
description: 'Saiba mais sobre o método: ICLRRuntimeHost:: GetCLRControl'
title: Método ICLRRuntimeHost::GetCLRControl
ms.date: 03/30/2017
api_name:
- ICLRRuntimeHost.GetCLRControl
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeHost::GetCLRControl
helpviewer_keywords:
- ICLRRuntimeHost::GetCLRControl method [.NET Framework hosting]
- GetCLRControl method [.NET Framework hosting]
ms.assetid: e47e3655-efd5-4572-a1dc-50c69bf2a468
topic_type:
- apiref
ms.openlocfilehash: 832ae03c0126f0c08afa9b5c0312a636ec1de294
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753920"
---
# <a name="iclrruntimehostgetclrcontrol-method"></a>Método ICLRRuntimeHost::GetCLRControl

Obtém um ponteiro de interface do tipo [interface ICLRControl](iclrcontrol-interface.md) que os hosts podem usar para personalizar aspectos do Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCLRControl(  
    [out] ICLRControl** pCLRControl  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pCLRControl`  
 fora Um ponteiro de interface do tipo [interface ICLRControl](iclrcontrol-interface.md) que permite que os hosts configurem aspectos adicionais do CLR.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`GetCLRControl` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Se um método retornar E_FAIL, o CLR não poderá mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_INVALIDOPERATION|O CLR já foi iniciado.|  
  
## <a name="remarks"></a>Comentários  

 `ICLRControl` fornece o método de [método GetCLRManager](iclrcontrol-getclrmanager-method.md) , que permite que o host obtenha um ponteiro de interface para um dos tipos de gerente.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRControl](iclrcontrol-interface.md)
- [Interface ICLRRuntimeHost](iclrruntimehost-interface.md)
