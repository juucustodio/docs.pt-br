---
description: 'Saiba mais sobre o método: ICLRErrorReportingManager:: EndCustomDump'
title: Método ICLRErrorReportingManager::EndCustomDump
ms.date: 03/30/2017
api_name:
- ICLRErrorReportingManager.EndCustomDump
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRErrorReportingManager::EndCustomDump
helpviewer_keywords:
- ICLRErrorReportingManager::EndCustomDump method [.NET Framework hosting]
- EndCustomDump method [.NET Framework hosting]
ms.assetid: 88a5da04-8729-4108-82c4-af206a7d483e
topic_type:
- apiref
ms.openlocfilehash: 406d7d77f4cd63c69fec56acb0819d56c6271630
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689463"
---
# <a name="iclrerrorreportingmanagerendcustomdump-method"></a>Método ICLRErrorReportingManager::EndCustomDump

Remove a configuração de despejo de pilha personalizada que foi especificada em uma chamada anterior para o método [ICLRErrorReportingManager:: BeginCustomDump](iclrerrorreportingmanager-begincustomdump-method.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EndCustomDump ();  
```  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`EndCustomDump` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O `EndCustomDump` método limpa a configuração de despejo de pilha personalizada definida por uma chamada anterior para o `BeginCustomDump` método e libera qualquer estado associado. Ele deve ser chamado após a conclusão do despejo de pilha personalizado.  
  
> [!IMPORTANT]
> Falha ao chamar `EndCustomDump` faz com que a memória seja vazada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estrutura CustomDumpItem](customdumpitem-structure.md)
- [Enumeração ECustomDumpFlavor](ecustomdumpflavor-enumeration.md)
- [Interface ICLRErrorReportingManager](iclrerrorreportingmanager-interface.md)
