---
description: 'Saiba mais sobre o método: ICLRHostBindingPolicyManager:: EvaluatePolicy'
title: Método ICLRHostBindingPolicyManager::EvaluatePolicy
ms.date: 03/30/2017
api_name:
- ICLRHostBindingPolicyManager.EvaluatePolicy
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRHostBindingPolicyManager::EvaluatePolicy
helpviewer_keywords:
- ICLRHostBindingPolicyManager::EvaluatePolicy method [.NET Framework hosting]
- EvaluatePolicy method [.NET Framework hosting]
ms.assetid: 3a3a9446-7a4e-4836-9b27-5c536c15993d
topic_type:
- apiref
ms.openlocfilehash: e92126a8c12d03ee21e4867754b1a418ef11d463
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789964"
---
# <a name="iclrhostbindingpolicymanagerevaluatepolicy-method"></a>Método ICLRHostBindingPolicyManager::EvaluatePolicy

Avalia a política de associação em nome do host.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT EvaluatePolicy (  
    [in] LPCWSTR     pwzReferenceIdentity,  
    [in] BYTE       *pbApplicationPolicy,  
    [in] DWORD       cbAppPolicySize,  
    [out, size_is(*pcchPostPolicyReferenceIdentity)] LPWSTR pwzPostPolicyReferenceIdentity,  
    [in, out] DWORD *pcchPostPolicyReferenceIdentity,  
    [out] DWORD     *pdwPoliciesApplied  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzReferenceIdentity`  
 no Uma referência ao assembly antes da avaliação da política.  
  
 `pbApplicationPolicy`  
 no Um ponteiro para um buffer que contém os dados da política.  
  
 `cbAppPolicySize`  
 no O tamanho do `pbApplicationPolicy` buffer.  
  
 `pwzPostPolicyReferenceIdentity`  
 fora Uma referência ao assembly após a avaliação dos novos dados de política.  
  
 `pcchPostPolicyReferenceIdentity`  
 [entrada, saída] Um ponteiro para o tamanho do buffer de referência de identidade do assembly após a avaliação dos novos dados de política.  
  
 `pdwPoliciesApplied`  
 fora Um ponteiro para uma combinação lógica ou de valores [EBindPolicyLevels](ebindpolicylevels-enumeration.md) , indicando quais políticas foram aplicadas.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A avaliação foi concluída com êxito.|  
|E_INVALIDARG|`pwzReferenceIdentity`Ou `pbApplicationPolicy` é uma referência nula.|  
|ERROR_INSUFFICIENT_BUFFER|`cbAppPolicySize` é pequeno demais.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O `EvaluatePolicy` método permite que o host influencie a diretiva de associação para manter os requisitos de controle de versão de assembly específicos do host. O próprio mecanismo de política permanece dentro do CLR.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRHostBindingPolicyManager](iclrhostbindingpolicymanager-interface.md)
