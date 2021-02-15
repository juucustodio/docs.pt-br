---
description: 'Saiba mais sobre o método: ICLRRuntimeInfo:: GetProcAddress'
title: Método ICLRRuntimeInfo::GetProcAddress
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.GetProcAddress
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::GetProcAddress
helpviewer_keywords:
- GetProcAddress method [.NET Framework hosting]
- ICLRRuntimeInfo::GetProcAddress method [.NET Framework hosting]
ms.assetid: a7732bfc-689a-4926-88fd-4f81e6f9ed78
topic_type:
- apiref
ms.openlocfilehash: 1e5d08ed118930418106b28541b4081d6acad927
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637138"
---
# <a name="iclrruntimeinfogetprocaddress-method"></a>Método ICLRRuntimeInfo::GetProcAddress

Obtém o endereço de uma função especificada que foi exportada do Common Language Runtime (CLR) associado a esta interface.  
  
 Esse método substitui a função [GetRealProcAddress](getrealprocaddress-function.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetProcAddress(  
     [in]  LPCSTR pszProcName,  
     [out, retval] LPVOID *ppProc);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pszProcName`  
 no O nome da função exportada.  
  
 `ppProc`  
 fora O endereço da função exportada.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_POINTER|`pszProcName` ou `ppProc` é nulo.|  
|CLR_E_SHIM_RUNTIMEEXPORT|A função especificada não é uma função exportada.|  
  
## <a name="remarks"></a>Comentários  

 Esse método faz com que o CLR seja carregado, mas não inicializado.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeInfo](iclrruntimeinfo-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
