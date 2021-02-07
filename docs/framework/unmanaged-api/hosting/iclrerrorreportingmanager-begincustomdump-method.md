---
description: 'Saiba mais sobre o método: ICLRErrorReportingManager:: BeginCustomDump'
title: Método ICLRErrorReportingManager::BeginCustomDump
ms.date: 03/30/2017
api_name:
- ICLRErrorReportingManager.BeginCustomDump
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRErrorReportingManager::BeginCustomDump
helpviewer_keywords:
- ICLRErrorReportingManager::BeginCustomDump method [.NET Framework hosting]
- BeginCustomDump method
ms.assetid: 93424a87-ba13-4fa1-b4dc-69d44437b7ae
topic_type:
- apiref
ms.openlocfilehash: 3f8498068d50ffc6ea00cf4f08f969c92f010d6c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689476"
---
# <a name="iclrerrorreportingmanagerbegincustomdump-method"></a>Método ICLRErrorReportingManager::BeginCustomDump

Especifica a configuração de despejos de heap personalizados para o relatório de erros.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT BeginCustomDump (  
    [in] ECustomDumpFlavor dwFlavor,  
    [in] DWORD dwNumItems,  
    [in, size_is(dwNumItems), length_is(dwNumItems)] CustomDumpItem items[],  
    DWORD dwReserved  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwFlavor`  
 no Um valor [ECustomDumpFlavor](ecustomdumpflavor-enumeration.md) que indica o tipo de despejo de heap no qual Compilar o despejo de heap personalizado.  
  
 `dwNumItems`  
 no O comprimento da `items` matriz. Se `dwFlavor` não for DUMP_FLAVOR_Mini, `dwNumItems` deverá ser zero.  
  
 `items`  
 no Uma matriz de instâncias de [CustomDumpItem](customdumpitem-structure.md) , especificando os itens a serem adicionados ao mini-despejo. Se `dwFlavor` não for DUMP_FLAVOR_Mini, `items` deverá ser NULL.  
  
 `dwReserved`  
 no Reservado para uso futuro.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O `BeginCustomDump` método define a configuração de despejo de heap personalizado. O método [EndCustomDump](iclrerrorreportingmanager-endcustomdump-method.md) limpa a configuração de despejo de heap personalizada e libera qualquer estado associado. Ele deve ser chamado após a conclusão do despejo de heap personalizado.  
  
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
