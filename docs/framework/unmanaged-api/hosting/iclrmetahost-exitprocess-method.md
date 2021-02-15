---
description: 'Saiba mais sobre o método: ICLRMetaHost:: ExitProcess'
title: Método ICLRMetaHost::ExitProcess
ms.date: 03/30/2017
api_name:
- ICLRMetaHost.ExitProcess
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRMetaHost::ExitProcess
helpviewer_keywords:
- ICLRMetaHost::ExitProcess method [.NET Framework hosting]
- ExitProcess method, ICLRMetaHost interface [.NET Framework hosting]
ms.assetid: b4df98cc-4e4e-407b-b8f4-e0076afef3a4
topic_type:
- apiref
ms.openlocfilehash: 3bc832538a5ad2b457de758fc35a632b09c02974
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689151"
---
# <a name="iclrmetahostexitprocess-method"></a>Método ICLRMetaHost::ExitProcess

Tenta desligar todos os tempos de execução carregados normalmente e, em seguida, encerra o processo. Substitui a função [CorExitProcess](corexitprocess-function.md) .  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT ExitProcess (  
    [in] INT32 iExitCode);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `iExitCode`  
 no O código de saída do processo.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método nunca retorna, portanto, seu valor de retorno é indefinido.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRMetaHost](iclrmetahost-interface.md)
- [Hospedagem](index.md)
