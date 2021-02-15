---
description: 'Saiba mais sobre o método: ICLRRuntimeInfo:: BindAsLegacyV2Runtime'
title: Método ICLRRuntimeInfo::BindAsLegacyV2Runtime
ms.date: 03/30/2017
api_name:
- ICLRRuntimeInfo.BindAsLegacyV2Runtime
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRRuntimeInfo::BindAsLegacyV2Runtime
helpviewer_keywords:
- ICLRRuntimeInfo::BindAsLegacyV2Runtime method [.NET Framework hosting]
- BindAsLegacyV2Runtime method [.NET Framework hosting]
ms.assetid: 65fd55ac-4a24-4479-9384-a2e8013bfb2b
topic_type:
- apiref
ms.openlocfilehash: 77b340cba18ea86546e1a8f4a17933f09289b1de
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99637165"
---
# <a name="iclrruntimeinfobindaslegacyv2runtime-method"></a>Método ICLRRuntimeInfo::BindAsLegacyV2Runtime

Associa o tempo de execução atual a todas as decisões de política de ativação da versão 2 do Common Language Runtime herdado (CLR).  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT BindAsLegacyV2Runtime ();  
```  
  
## <a name="return-value"></a>Valor retornado  

 Esse método retorna os HRESULTs específicos a seguir:  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A associação foi bem-sucedida ou esse tempo de execução já estava associado ao tempo de execução da política de ativação do CLR versão 2 herdado.|  
|CLR_E_SHIM_LEGACYRUNTIMEALREADYBOUND|Um tempo de execução diferente já estava associado à política de ativação do CLR versão 2 herdada.|  
  
## <a name="remarks"></a>Comentários  

 Se o tempo de execução atual já estiver associado a todas as decisões da política de ativação do CLR versão 2 herdadas (por exemplo, usando o `useLegacyV2RuntimeActivationPolicy` atributo no [ \<startup> elemento](../../configure-apps/file-schema/startup/startup-element.md) no arquivo de configuração), esse método não retornará um resultado de erro; em vez disso, o resultado será S_OK, assim como seria se o método tivesse associado com êxito a política de ativação herdada.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MetaHost. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRRuntimeInfo](iclrruntimeinfo-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
- [Hospedagem](index.md)
- [\<startup> Elementos](../../configure-apps/file-schema/startup/startup-element.md)
