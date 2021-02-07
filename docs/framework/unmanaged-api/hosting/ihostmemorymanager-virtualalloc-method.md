---
description: 'Saiba mais sobre: método IHostMemoryManager:: VirtualAlloc'
title: Método IHostMemoryManager::VirtualAlloc
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualAlloc
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualAlloc
helpviewer_keywords:
- VirtualAlloc method [.NET Framework hosting]
- IHostMemoryManager::VirtualAlloc method [.NET Framework hosting]
ms.assetid: 4dff3646-a050-4bd9-ac31-fe307e8637ec
topic_type:
- apiref
ms.openlocfilehash: 28682aea5e6e7951b3b8f0a9af946a3f3828601b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99707833"
---
# <a name="ihostmemorymanagervirtualalloc-method"></a>Método IHostMemoryManager::VirtualAlloc

Serve como um wrapper lógico para a função Win32 correspondente. A implementação do Win32 de `VirtualAlloc` reserva ou confirma uma região de páginas no espaço de endereço virtual do processo de chamada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT VirtualAlloc (  
    [in]  void*   pAddress,  
    [in]  SIZE_T  dwSize,  
    [in]  DWORD   flAllocationType,  
    [in]  DWORD   flProtect,  
    [in]  EMemoryCriticalLevel dwCriticalLevel,  
    [out] void**  ppMem  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pAddress`  
 no Um ponteiro para o endereço inicial da região a ser alocada.  
  
 `dwSize`  
 no O tamanho, em bytes, da região.  
  
 `flAllocationType`  
 no O tipo de alocação de memória.  
  
 `flProtect`  
 no Proteção de memória para a região de páginas a ser alocada.  
  
 `dwCriticalLevel`  
 no Um valor de [EMemoryCriticalLevel](ememorycriticallevel-enumeration.md) que indica o impacto de uma falha de alocação.  
  
 `ppMem`  
 fora Ponteiro para o endereço inicial da memória alocada, ou NULL se a solicitação não puder ser atendida.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`VirtualAlloc` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Não havia memória suficiente disponível para concluir a solicitação de alocação|  
  
## <a name="remarks"></a>Comentários  

 Você reserva uma região no espaço de endereço do processo chamando `VirtualAlloc` . O `pAddress` parâmetro contém o endereço inicial do bloco de memória desejado. Esse parâmetro é normalmente definido como nulo. O sistema operacional mantém um registro de intervalos de endereços livres disponíveis para seu processo. Um `pAddress` valor de NULL instrui o sistema a reservar a região onde quer que ela se ajuste. Como alternativa, você pode fornecer um endereço inicial específico para o bloco de memória. Em ambos os casos, o parâmetro de saída `ppMem` é retornado como um ponteiro para a memória alocada. A função em si retorna um valor HRESULT.  
  
 A `VirtualAlloc` função Win32 não tem um `ppMem` parâmetro e, em vez disso, retorna o ponteiro para a memória alocada. Para obter mais informações, consulte a documentação da plataforma Windows.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostMemoryManager](ihostmemorymanager-interface.md)
