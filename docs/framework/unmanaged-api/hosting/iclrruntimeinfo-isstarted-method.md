---
description: 'Saiba mais sobre: ICLRRuntimeInfo:: método IsStarted'
title: Método ICLRRuntimeInfo::IsStarted
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.IsStarted
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::IsStarted
helpviewer_keywords:
- IsStarted method [.NET Framework hosting]
- ICLRRuntimeInfo::IsStarted method [.NET Framework hosting]
ms.assetid: ef6f2662-323b-4534-aa82-6d1afb7b9309
ms.openlocfilehash: 22059ecbded9eae9659cdaae8b9b92f2d7df0650
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753842"
---
# <a name="iclrruntimeinfoisstarted-method"></a>Método ICLRRuntimeInfo::IsStarted

Indica se o tempo de execução foi iniciado (ou seja, se o [Método ICLRRuntimeHost:: Start](iclrruntimehost-start-method.md) foi chamado e teve êxito).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT IsStarted(  
        [out] BOOL     *pbStarted,  
        [out] DWORD    *pdwStartupFlags);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pbStarted`  
 [fora] `true` Se esse tempo de execução for iniciado; caso contrário, `false` .  
  
 `pdwStartupFlags`  
 fora Retorna os sinalizadores que foram usados para iniciar o tempo de execução.  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir, bem como os erros de HRESULT que indicam falha de método.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito.|  
|E_NOTIMPL|A versão Common Language Runtime (CLR) é anterior à versão do CLR no .NET Framework 4.|  
  
## <a name="remarks"></a>Comentários  

 Esse método não funciona com versões do CLR anteriores à versão do CLR no .NET Framework 4.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeInfo](iclrruntimeinfo-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
