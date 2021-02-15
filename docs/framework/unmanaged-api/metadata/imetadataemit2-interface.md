---
description: 'Saiba mais sobre: interface IMetaDataEmit2'
title: Interface IMetaDataEmit2
ms.date: 03/30/2017
api_name:
- IMetaDataEmit2
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit2
helpviewer_keywords:
- IMetaDataEmit2 interface [.NET Framework metadata]
ms.assetid: 866dc96b-bbfc-4c0f-80c2-38ce93072106
topic_type:
- apiref
ms.openlocfilehash: db1880d64bf3b1e9084d6745251c174788a4afe7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99745665"
---
# <a name="imetadataemit2-interface"></a>Interface IMetaDataEmit2

Estende a interface [IMetaDataEmit](imetadataemit-interface.md) principalmente para fornecer a capacidade de trabalhar com tipos genéricos.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método DefineGenericParam](imetadataemit2-definegenericparam-method.md)|Cria uma definição para um parâmetro de tipo genérico e Obtém um token para esse parâmetro de tipo genérico.|  
|[Método DefineMethodSpec](imetadataemit2-definemethodspec-method.md)|Cria uma instância genérica de um método e Obtém um token para a definição.|  
|[Método GetDeltaSaveSize](imetadataemit2-getdeltasavesize-method.md)|Obtém um valor que indica a diferença no tamanho dos dados necessários para expressar as alterações da sessão de edição e continuação atual.|  
|[Método ResetENCLog](imetadataemit2-resetenclog-method.md)|Redefine o log de edição e continuação e inicia uma nova sessão.|  
|[Método SaveDelta](imetadataemit2-savedelta-method.md)|Salva as alterações da sessão de edição e continuação atual para o arquivo especificado.|  
|[Método SaveDeltaToMemory](imetadataemit2-savedeltatomemory-method.md)|Salva as alterações da sessão de edição e continuação atual na memória.|  
|[Método SaveDeltaToStream](imetadataemit2-savedeltatostream-method.md)|Salva as alterações da sessão de edição e continuação atual para o fluxo especificado.|  
|[Método SetGenericParamProps](imetadataemit2-setgenericparamprops-method.md)|Define valores de propriedade para a definição de parâmetro genérico referenciada pelo token especificado.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de metadados](metadata-interfaces.md)
- [Interface IMetaDataEmit](imetadataemit-interface.md)
