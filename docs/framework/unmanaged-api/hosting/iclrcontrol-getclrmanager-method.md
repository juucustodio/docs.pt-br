---
description: 'Saiba mais sobre o método: ICLRControl:: GetCLRManager'
title: Método ICLRControl::GetCLRManager
ms.date: 03/30/2017
api_name:
- ICLRControl.GetCLRManager
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRControl::GetCLRManager
helpviewer_keywords:
- GetCLRManager method [.NET Framework hosting]
- ICLRControl::GetCLRManager method [.NET Framework hosting]
ms.assetid: 8a11bfa4-cbb0-4082-82b5-f9fba66c93f5
topic_type:
- apiref
ms.openlocfilehash: fc24cbdfd4bebfff5c2f8d73a9cd6961a8c94e94
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716712"
---
# <a name="iclrcontrolgetclrmanager-method"></a>Método ICLRControl::GetCLRManager

Obtém um ponteiro de interface para uma instância de qualquer um dos tipos de Gerenciador que o host pode usar para configurar o Common Language Runtime (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetCLRManager (  
    [in]  REFIID  riid,  
    [out] void  **ppObject  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `riid`  
 no O `IID` do tipo de Gerenciador a ser retornado. Há `IID` suporte para os valores a seguir.  
  
- IID_ICLRDebugManager: Especifica que `ppObject` será do tipo [ICLRDebugManager](iclrdebugmanager-interface.md).  
  
- IID_ICLRErrorReportingManager: Especifica que `ppObject` será do tipo [ICLRErrorReportingManager](iclrerrorreportingmanager-interface.md).  
  
- IID_ICLRGCManager: Especifica que `ppObject` será do tipo [ICLRGCManager](iclrgcmanager-interface.md).  
  
- IID_ICLRHostProtectionManager: Especifica que `ppObject` será do tipo [ICLRHostProtectionManager](iclrhostprotectionmanager-interface.md).  
  
- IID_ICLROnEventManager: Especifica que `ppObject` será do tipo [ICLROnEventManager](iclroneventmanager-interface.md).  
  
- IID_ICLRPolicyManager: Especifica que `ppObject` será do tipo [ICLRPolicyManager](iclrpolicymanager-interface.md).  
  
- IID_ICLRTaskManager: Especifica que `ppObject` será do tipo [ICLRTaskManager](iclrtaskmanager-interface.md).  
  
 `ppObject`  
 fora Um ponteiro de interface para o Gerenciador solicitado, ou NULL, se um tipo de Gerenciador inválido foi solicitado.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_NOINTERFACE|Não há suporte para o tipo de interface.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRControl](iclrcontrol-interface.md)
- [Interface IHostControl](ihostcontrol-interface.md)
