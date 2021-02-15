---
description: 'Saiba mais sobre o método: IHostMemoryManager:: VirtualFree'
title: Método IHostMemoryManager::VirtualFree
ms.date: 03/30/2017
api_name:
- IHostMemoryManager.VirtualFree
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IHostMemoryManager::VirtualFree
helpviewer_keywords:
- IHostMemoryManager::VirtualFree method [.NET Framework hosting]
- VirtualFree method [.NET Framework hosting]
ms.assetid: 1a436e89-eb28-4d15-bcf1-a072f86dbd99
topic_type:
- apiref
ms.openlocfilehash: 987661ce1b7bfd08f757f53082313b8eb60ff282
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99707461"
---
# <a name="ihostmemorymanagervirtualfree-method"></a>Método IHostMemoryManager::VirtualFree

Serve como um wrapper lógico para a função Win32 correspondente. A implementação do Win32 de `VirtualFree` liberações, desconfirma ou libera e desconfirma uma região de páginas dentro do espaço de endereço virtual do processo de chamada.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT VirtualFree (  
    [in] LPVOID  lpAddress,  
    [in] SIZE_T  dwSize,  
    [in] DWORD   dwFreeType  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `lpAddress`  
 no Um ponteiro para o endereço base das páginas de memória virtual a serem liberadas.  
  
 `dwSize`  
 no O tamanho, em bytes, da região a ser liberada.  
  
 `dwFreeType`  
 no O tipo de operação de liberação.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|`VirtualFree` retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Quando um método retorna E_FAIL, o CLR não é mais utilizável no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
|HOST_E_INVALIDOPERATION|Foi feita uma tentativa de liberar memória que não foi alocada por meio do host.|  
  
## <a name="remarks"></a>Comentários  

 `VirtualFree` Libera as páginas de memória virtual associadas ao `lpAddress` parâmetro por meio de uma chamada anterior à função [IHostMemoryManager:: VirtualAlloc](ihostmemorymanager-virtualalloc-method.md) . As tentativas de liberar memória que não foi alocada por meio do host devem retornar HOST_E_INVALIDOPERATION.  
  
 As semânticas são idênticas às da implementação do Win32 do `VirtualFree` . Para obter mais informações, consulte a documentação da plataforma Windows.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IHostMemoryManager](ihostmemorymanager-interface.md)
- [Interface IHostMalloc](ihostmalloc-interface.md)
