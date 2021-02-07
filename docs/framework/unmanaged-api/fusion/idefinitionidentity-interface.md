---
description: 'Saiba mais sobre: interface IDefinitionIdentity'
title: Interface IDefinitionIdentity
ms.date: 03/30/2017
api_name:
- IDefinitionIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IDefinitionIdentity
helpviewer_keywords:
- IDefinitionIdentity interface [.NET Framework fusion]
ms.assetid: ce5ba888-5fbe-4efd-91cf-f0ff94d8428b
topic_type:
- apiref
ms.openlocfilehash: 3471879cc822b655b786dd9d8234950cb4b99c1d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760646"
---
# <a name="idefinitionidentity-interface"></a>Interface IDefinitionIdentity

Representa a assinatura exclusiva do código que define o aplicativo no escopo atual.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|`IDefinitionIdentity::Clone`|Obtém um ponteiro de interface para um novo `IDefinitionIdentity` objeto que é idêntico a este `IDefinitionIdentity` , exceto para as alterações de atributo especificadas.|  
|`IDefinitionIdentity::EnumAttributes`|Obtém um ponteiro de interface para um objeto [IEnumIDENTITY_ATTRIBUTE](ienumidentity-attribute-interface.md) que contém os atributos associados a ele `IDefinitionIdentity` .|  
|`IDefinitionIdentity::GetAttribute`|Obtém o valor do atributo com o nome especificado no namespace especificado.|  
|`IDefinitionIdentity::SetAttribute`|Define o atributo que tem o nome especificado no namespace especificado para o valor especificado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Isolamento. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de fusão](fusion-interfaces.md)
