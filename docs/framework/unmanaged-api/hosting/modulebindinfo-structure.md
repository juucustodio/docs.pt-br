---
description: 'Saiba mais sobre: estrutura ModuleBindInfo'
title: Estrutura ModuleBindInfo
ms.date: 03/30/2017
api_name:
- ModuleBindInfo
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ModuleBindInfo
helpviewer_keywords:
- ModuleBindInfo structure [.NET Framework hosting]
ms.assetid: 632d4adc-dbc9-4ce8-9397-abc3285c1c69
topic_type:
- apiref
ms.openlocfilehash: 0969c0ecc459414336800e8e7da5817ac0c1a8ce
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99679596"
---
# <a name="modulebindinfo-structure"></a>Estrutura ModuleBindInfo

Fornece informações detalhadas sobre o módulo referenciado e o assembly que o contém.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp  
typedef struct _ModuleBindInfo {  
    DWORD    dwAppDomainId;  
    LPCWSTR  lpAssemblyIdentity;  
    LPCWSTR  lpModuleName  
} ModuleBindInfo;  
```  
  
## <a name="members"></a>Membros  
  
|Membro|DESCRIÇÃO|  
|------------|-----------------|  
|`dwAppDomainId`|Um identificador exclusivo para o `IStream` que é retornado por uma chamada para o método [IHostAssemblyStore::P rovidemodule](ihostassemblystore-providemodule-method.md) do qual o módulo referenciado deve ser carregado.|  
|`lpAssemblyIdentity`|Um identificador exclusivo para o assembly que contém o módulo referenciado.|  
|`lpModuleName`|O nome do módulo referenciado.|  
  
## <a name="remarks"></a>Comentários  

 `ModuleBindInfo` é passado como um parâmetro para `IHostAssemblyStore::ProvideModule` . O host fornece o identificador exclusivo `dwAppDomainId` para o Common Language Runtime (CLR). Após uma chamada para o método [IHostAssemblyStore::P rovideassembly](ihostassemblystore-provideassembly-method.md) retorna, o tempo de execução usa o identificador para determinar se o conteúdo do `IStream` foi mapeado. Nesse caso, o tempo de execução carrega a cópia existente em vez de remapear o fluxo. O tempo de execução também usa esse identificador como uma chave de pesquisa para fluxos que são retornados de chamadas para o `IHostAssemblyStore::ProvideAssembly` método. Portanto, o identificador deve ser exclusivo para solicitações de módulo, bem como para solicitações de assembly.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. idl  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Estruturas de hospedagem](hosting-structures.md)
- [Estrutura AssemblyBindInfo](assemblybindinfo-structure.md)
- [Interface ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md)
- [Interface ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)
- [Interface IHostAssemblyManager](ihostassemblymanager-interface.md)
