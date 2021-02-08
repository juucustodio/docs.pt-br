---
description: 'Saiba mais sobre: estrutura AssemblyBindInfo'
title: Estrutura AssemblyBindInfo
ms.date: 03/30/2017
api_name:
- AssemblyBindInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- AssemblyBindInfo
helpviewer_keywords:
- AssemblyBindInfo structure [.NET Framework hosting]
ms.assetid: 6fc01e98-c2e7-49de-ab9f-95937cc89017
topic_type:
- apiref
ms.openlocfilehash: 3e11e05924ee6818737f84d9ca92394ee5313292
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99799974"
---
# <a name="assemblybindinfo-structure"></a>Estrutura AssemblyBindInfo

Fornece informações detalhadas sobre o assembly referenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _AssemblyBindInfo {  
    DWORD       dwAppDomainId;  
    LPCWSTR     lpReferencedIdentity;  
    LPCWSTR     lpPostPolicyIdentity;  
    DWORD       ePolicyLevel;  
} AssemblyBindInfo;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`dwAppDomainId`|Um identificador exclusivo para o `IStream` retornado por uma chamada para [IHostAssemblyStore::P rovideassembly](ihostassemblystore-provideassembly-method.md), da qual o assembly referenciado deve ser carregado.|  
|`lpReferencedIdentity`|Um identificador exclusivo para o assembly referenciado.|  
|`lpPostPolicyIdentity`|O identificador para o assembly referenciado após a aplicação de qualquer valor de política de associação.|  
|`ePolicyLevel`|Um dos valores de [EPolicyAction](epolicyaction-enumeration.md) que indicam quais políticas de controle de versão, se houver, deve ser aplicado ao assembly referenciado.|  
  
## <a name="remarks"></a>Comentários  

 O host fornece o identificador exclusivo `dwAppDomainId` para o Common Language Runtime (CLR). Depois de uma chamada para `IHostAssemblyStore::ProvideAssembly` retornar, o tempo de execução usa o identificador para determinar se o conteúdo do `IStream` foi mapeado. Nesse caso, o tempo de execução carrega a cópia existente em vez de remapear o fluxo. O tempo de execução também usa esse identificador como uma chave de pesquisa para fluxos retornados de chamadas para [IHostAssemblyStore::P rovidemodule](ihostassemblystore-providemodule-method.md). Portanto, o identificador deve ser exclusivo para solicitações de módulo e para solicitações de assembly.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. idl  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de hospedagem](hosting-structures.md)
- [Interface ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md)
- [Interface ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)
- [Interface IHostAssemblyManager](ihostassemblymanager-interface.md)
- [Interface IHostAssemblyStore](ihostassemblystore-interface.md)
- [Estrutura ModuleBindInfo](modulebindinfo-structure.md)
