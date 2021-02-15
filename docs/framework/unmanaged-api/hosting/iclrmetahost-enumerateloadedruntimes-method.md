---
description: 'Saiba mais sobre o método: ICLRMetaHost:: EnumerateLoadedRuntimes'
title: Método ICLRMetaHost::EnumerateLoadedRuntimes
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.EnumerateLoadedRuntimes
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::EnumerateLoadedRuntimes
helpviewer_keywords:
- EnumerateLoadedRuntimes method [.NET Framework hosting]
- ICLRMetaHost::EnumerateLoadedRuntimes method [.NET Framework hosting]
ms.assetid: 22fc0a3f-dce4-4766-9a3c-9fab15f4b4ca
topic_type:
- apiref
ms.openlocfilehash: 508c4daca7e34366e0da35591f4e7a780301e823
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789860"
---
# <a name="iclrmetahostenumerateloadedruntimes-method"></a>Método ICLRMetaHost::EnumerateLoadedRuntimes

Retorna uma enumeração que inclui um ponteiro de interface [ICLRRuntimeInfo](iclrruntimeinfo-interface.md) válido para cada versão do Common Language Runtime (CLR) que é carregado em um determinado processo. Esse método substitui a função [GetVersionFromProcess](getversionfromprocess-function.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EnumerateLoadedRuntimes (  
    [in] HANDLE hndProcess,  
    [out, retval] IEnumUnknown **ppEnumerator  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `hndProcess`  
 no O identificador do processo para inspecionar os tempos de execução carregados.  
  
 `ppEnumerator`  
 fora Uma <xref:Microsoft.VisualStudio.OLE.Interop.IEnumUnknown> enumeração de interfaces [ICLRRuntimeInfo](iclrruntimeinfo-interface.md) correspondentes a cada CLR que é carregado pelo processo.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_POINTER|`ppEnumerator` é nulo.|  
  
## <a name="remarks"></a>Comentários  

 Esse método lista todos os tempos de execução carregados, mesmo que eles tenham sido carregados com funções preteridas, como [CorBindToRuntime](corbindtoruntime-function.md).  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRMetaHost](iclrmetahost-interface.md)
- [Hospedagem](index.md)
