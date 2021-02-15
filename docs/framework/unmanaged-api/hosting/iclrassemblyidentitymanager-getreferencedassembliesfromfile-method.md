---
description: 'Saiba mais sobre o método: ICLRAssemblyIdentityManager:: GetReferencedAssembliesFromFile'
title: Método ICLRAssemblyIdentityManager::GetReferencedAssembliesFromFile
ms.date: 03/30/2017
api_name:
- ICLRAssemblyIdentityManager.GetReferencedAssembliesFromFile
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRAssemblyIdentityManager::GetReferencedAssembliesFromFile
helpviewer_keywords:
- ICLRAssemblyIdentityManager::GetReferenceAssembliesFromFile method [.NET Framework hosting]
- GetReferenceAssembliesFromFile method [.NET Framework hosting]
ms.assetid: eed63d31-d977-4c7d-9443-f9d37a2a7d81
topic_type:
- apiref
ms.openlocfilehash: 46b2f392746c6e23e2a8a11aded5eacd8f5a597b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99790043"
---
# <a name="iclrassemblyidentitymanagergetreferencedassembliesfromfile-method"></a>Método ICLRAssemblyIdentityManager::GetReferencedAssembliesFromFile

Obtém uma instância de [ICLRReferenceAssemblyEnum](iclrreferenceassemblyenum-interface.md) que contém uma lista de assemblies referenciados pelo assembly no caminho de arquivo especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
HRESULT GetReferencedAssembliesFromFile (  
    [in]  LPCWSTR pwzFilePath,  
    [in]  DWORD   dwFlags,  
    [in]  ICLRAssemblyReferenceList   *pExcludeAssembliesList,  
    [out] ICLRReferenceAssemblyEnum  **ppReferenceEnum  
);  
```  
  
## <a name="parameters"></a>Parâmetros  

 `pwzFilePath`  
 no O caminho para o assembly a ser avaliado.  
  
 `dwFlags`  
 no Fornecido para extensibilidade futura. CLR_ASSEMBLY_IDENTITY_FLAGS_DEFAULT é o único valor para o qual a versão atual do Common Language Runtime (CLR) dá suporte.  
  
 `pExcludeAssembliesList`  
 no Um ponteiro para um objeto [ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md) que representa assemblies que devem ser excluídos do `ppReferenceEnum` .  
  
 `ppReferenceEnum`  
 fora Um ponteiro para o endereço de um `ICLRReferenceAssemblyEnum` objeto que contém dados de identidade de assembly para os assemblies referenciados pelo assembly em `pwzFilePath` , excluindo os assemblies representados por `pExcludeAssembliesList` .  
  
## <a name="return-value"></a>Valor retornado  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi retornado com êxito.|  
|HOST_E_CLRNOTAVAILABLE|O CLR não foi carregado em um processo ou o CLR está em um estado no qual não pode executar código gerenciado ou processar a chamada com êxito.|  
|HOST_E_TIMEOUT|A chamada atingiu o tempo limite.|  
|HOST_E_NOT_OWNER|O chamador não possui o bloqueio.|  
|HOST_E_ABANDONED|Um evento foi cancelado enquanto um thread ou uma fibra bloqueada estava esperando.|  
|E_FAIL|Ocorreu uma falha catastrófica desconhecida. Se um método retornar E_FAIL, o CLR não poderá mais ser usado no processo. As chamadas subsequentes para métodos de hospedagem retornam HOST_E_CLRNOTAVAILABLE.|  
  
## <a name="remarks"></a>Comentários  

 O chamador pode optar por excluir um conjunto de referências de assembly conhecidas da lista retornada. Esse conjunto é definido pelo `pExcludeAssembliesList` parâmetro.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md)
- [Interface ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)
- [Interface ICLRReferenceAssemblyEnum](iclrreferenceassemblyenum-interface.md)
