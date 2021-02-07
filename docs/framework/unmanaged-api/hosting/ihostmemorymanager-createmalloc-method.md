---
description: 'Saiba mais sobre o método: IHostMemoryManager:: CreateMAlloc'
title: Método IHostMemoryManager::CreateMAlloc
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.CreateMAlloc
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::CreateMAlloc
helpviewer_keywords:
- CreateAlloc method [.NET Framework hosting]
- IHostMemoryManager::CreateMAlloc method [.NET Framework hosting]
ms.assetid: 9ee6e052-bef7-4350-9e4f-edfffd99ad6f
topic_type:
- apiref
ms.openlocfilehash: de73490a5c8b4e1672beb4750bcc617c2371f07b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99707877"
---
# <a name="ihostmemorymanagercreatemalloc-method"></a>Método IHostMemoryManager::CreateMAlloc

Obtém um ponteiro de interface para uma instância de [IHostMAlloc](ihostmalloc-interface.md) que é usada para fazer solicitações de alocação de um heap criado pelo host.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT CreateMalloc (  
    [in]  DWORD         dwMallocType,  
    [out] IHostMalloc **ppMalloc  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `dwMallocType`  
 no Uma combinação de sinalizadores de [MALLOC_TYPE](malloc-type-enumeration.md) que especifica as características da memória que está sendo alocada.  
  
 `ppMAlloc`  
 fora Um ponteiro para o endereço de uma `IHostMAlloc` instância fornecida pelo host.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`CreateMAlloc` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|E_OUTOFMEMORY|Não há memória física suficiente disponível para concluir a solicitação de alocação.|  
  
## <a name="remarks"></a>Comentários  

 `CreateMAlloc` Retorna um objeto que permite que o CLR faça solicitações de alocação por meio do host em vez de usar as funções padrão do Win32.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostMalloc](ihostmalloc-interface.md)
- [Interface IHostMemoryManager](ihostmemorymanager-interface.md)
