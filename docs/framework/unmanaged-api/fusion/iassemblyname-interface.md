---
description: 'Saiba mais sobre: Interface IAssemblyName'
title: Interface IAssemblyName
ms.date: 03/30/2017
api_name:
- IAssemblyName
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyName
helpviewer_keywords:
- IAssemblyName interface [.NET Framework fusion]
ms.assetid: f7f8e605-6b67-4151-936f-f04ecd671d90
topic_type:
- apiref
ms.openlocfilehash: fb5949572adc533bab5ed26ee969267f430f36ba
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760700"
---
# <a name="iassemblyname-interface"></a>Interface IAssemblyName

Fornece métodos para descrever e trabalhar com a identidade exclusiva de um assembly.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Clone](iassemblyname-clone-method.md)|Cria uma cópia superficial desse `IAssemblyName` objeto.|  
|[Método Finalize](iassemblyname-finalize-method.md)|Permite que este `IAssemblyName` objeto libere recursos e execute outras operações de limpeza antes que seu destruidor seja chamado.|  
|[Método GetDisplayName](iassemblyname-getdisplayname-method.md)|Obtém o nome legível do assembly referenciado por este `IAssemblyName` objeto.|  
|[Método GetName](iassemblyname-getname-method.md)|Obtém o nome simples e não criptografado do assembly referenciado por esse `IAssemblyName` objeto.|  
|[Método GetProperty](iassemblyname-getproperty-method.md)|Obtém um ponteiro para a propriedade referenciada pelo especificado `PropertyId` .|  
|[Método GetVersion](iassemblyname-getversion-method.md)|Obtém as informações de versão do assembly referenciado por este `IAssemblyName` objeto.|  
|[Método IsEqual](iassemblyname-isequal-method.md)|Determina se um `IAssemblyName` objeto especificado é igual a este `IAssemblyName` , com base nos sinalizadores de comparação especificados.|  
|[Método SetProperty](iassemblyname-setproperty-method.md)|Define o valor da propriedade referenciada pelo especificado `PropertyId` .|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de fusão](fusion-interfaces.md)
- [Interface IAssemblyEnum](iassemblyenum-interface.md)
