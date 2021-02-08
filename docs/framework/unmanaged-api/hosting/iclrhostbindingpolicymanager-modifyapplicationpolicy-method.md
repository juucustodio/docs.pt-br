---
description: 'Saiba mais sobre o método: ICLRHostBindingPolicyManager:: ModifyApplicationPolicy'
title: Método ICLRHostBindingPolicyManager::ModifyApplicationPolicy
ms.date: 03/30/2017
api_name:
- ICLRHostBindingPolicyManager.ModifyApplicationPolicy
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRHostBindingPolicyManager::ModifyApplicationPolicy
helpviewer_keywords:
- ICLRHostBindingPolicyManager::ModifyApplicationPolicy method [.NET Framework hosting]
- ModifyApplicationPolicy method [.NET Framework hosting]
ms.assetid: d82d633e-cce6-427c-8b02-8227e34e12ba
topic_type:
- apiref
ms.openlocfilehash: 3f7d992f4b7d24233da175814f991106bb97a937
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99789925"
---
# <a name="iclrhostbindingpolicymanagermodifyapplicationpolicy-method"></a>Método ICLRHostBindingPolicyManager::ModifyApplicationPolicy

Modifica a política de associação para o assembly especificado e cria uma nova versão da política.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT  ModifyApplicationPolicy (  
    [in] LPCWSTR     pwzSourceAssemblyIdentity,
    [in] LPCWSTR     pwzTargetAssemblyIdentity,  
    [in] BYTE       *pbApplicationPolicy,  
    [in] DWORD       cbAppPolicySize,  
    [in] DWORD       dwPolicyModifyFlags,  
    [out, size_is(*pcbNewAppPolicySize)] BYTE *pbNewApplicationPolicy,
    [in, out] DWORD *pcbNewAppPolicySize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzSourceAssemblyIdentity`  
 no A identidade do assembly a ser modificada.  
  
 `pwzTargetAssemblyIdentity`  
 no A nova identidade do assembly modificado.  
  
 `pbApplicationPolicy`  
 no Um ponteiro para um buffer que contém os dados da política de associação para o assembly modificar.  
  
 `cbAppPolicySize`  
 no O tamanho da política de associação a ser substituída.  
  
 `dwPolicyModifyFlags`  
 no Uma combinação lógica ou de valores [EHostBindingPolicyModifyFlags](ehostbindingpolicymodifyflags-enumeration.md) , indicando o controle do redirecionamento.  
  
 `pbNewApplicationPolicy`  
 fora Um ponteiro para um buffer que contém os novos dados de diretiva de associação.  
  
 `pcbNewAppPolicySize`  
 [entrada, saída] Um ponteiro para o tamanho do novo buffer de diretiva de associação.  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|A política foi modificada com êxito.|  
|E_INVALIDARG|`pwzSourceAssemblyIdentity` ou `pwzTargetAssemblyIdentity` era uma referência nula.|  
|ERROR_INSUFFICIENT_BUFFER|`pbNewApplicationPolicy` é pequeno demais.|  
|HOST_E_CLRNOTAVAILABLE|O Common Language Runtime (CLR) não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Depois que um método retorna E_FAIL, o CLR não pode mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O `ModifyApplicationPolicy` método pode ser chamado duas vezes. A primeira chamada deve fornecer um valor nulo para o `pbNewApplicationPolicy` parâmetro. Essa chamada retornará com o valor necessário para `pcbNewAppPolicySize` . A segunda chamada deve fornecer esse valor para `pcbNewAppPolicySize` e apontar para um buffer desse tamanho para `pbNewApplicationPolicy` .  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRHostBindingPolicyManager](iclrhostbindingpolicymanager-interface.md)
