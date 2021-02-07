---
description: 'Saiba mais sobre o método: ICLRAssemblyIdentityManager:: GetBindingIdentityFromFile'
title: Método ICLRAssemblyIdentityManager::GetBindingIdentityFromFile
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.GetBindingIdentityFromFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::GetBindingIdentityFromFile
helpviewer_keywords:
- GetBindingIdentityFromFile method [.NET Framework hosting]
- ICLRAssemblyIdentityManager::GetBindingIdentifyFromFile method [.NET Framework hosting]
ms.assetid: 7797562d-7b4c-4bd9-8b93-f35e0e2869e4
topic_type:
- apiref
ms.openlocfilehash: 82e72155b38f71fe2c024994f07178638095be9a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99689541"
---
# <a name="iclrassemblyidentitymanagergetbindingidentityfromfile-method"></a>Método ICLRAssemblyIdentityManager::GetBindingIdentityFromFile

Obtém os dados de associação de identidade do assembly para o assembly no caminho de arquivo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetBindingIdentityFromFile(  
    [in] LPCWSTR     pwzFilePath,  
    [in] DWORD       dwFlags,  
    [out, size_is(*pcchBufferSize)] LPWSTR pwzBuffer,  
    [in, out] DWORD *pcchBufferSize  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzFilePath`  
 no O caminho para o arquivo a ser avaliado.  
  
 `dwFlags`  
 no Um valor da enumeração [ECLRAssemblyIdentityFlags](eclrassemblyidentityflags-enumeration.md) que indica o tipo de identidade de um assembly. Fornecido para extensibilidade futura. CLR_ASSEMBLY_IDENTITY_FLAGS_DEFAULT é o único valor ao qual a versão do Common Language Runtime (CLR) 2,0 dá suporte.  
  
 `pwzBuffer`  
 fora Um buffer que contém os dados de identidade do assembly opaco.  
  
 `pcchBufferSize`  
 [entrada, saída] Um ponteiro para o tamanho de `pwzBuffer` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi retornado com êxito.|  
|E_INVALIDARG|O fornecido `pwzFilePath` é nulo.|  
|ERROR_INSUFFICIENT_BUFFER|O tamanho de `pwzBuffer` é muito pequeno.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Se um método retornar E_FAIL, o CLR não poderá mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 `GetBindingIdentityFromFile` normalmente é chamado duas vezes. A primeira chamada fornece um valor nulo para `pwzBuffer` , e o método retorna o tamanho apropriado em `pcchBufferSize` . A segunda chamada fornece um buffer adequadamente alocado e o método retorna com os dados reais do buffer após a conclusão.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md)
- [Interface ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)
- [Interface ICLRHostBindingPolicyManager](iclrhostbindingpolicymanager-interface.md)
