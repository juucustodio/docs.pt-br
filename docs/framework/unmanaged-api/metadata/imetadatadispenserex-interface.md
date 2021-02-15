---
description: 'Saiba mais sobre: interface IMetaDataDispenserEx'
title: Interface IMetaDataDispenserEx
ms.date: 03/30/2017
api_name:
- IMetaDataDispenserEx
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenserEx
helpviewer_keywords:
- IMetaDataDispenserEx interface [.NET Framework metadata]
ms.assetid: 78b3629e-77a2-4406-89c3-56b5cc2c4594
topic_type:
- apiref
ms.openlocfilehash: d940ac20eaad4b930ab17fb2d194d3b03bd4cf3c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99753530"
---
# <a name="imetadatadispenserex-interface"></a>Interface IMetaDataDispenserEx

Estende a interface de [interface IMetaDataDispenser](imetadatadispenser-interface.md) para fornecer a capacidade de controlar como as APIs de metadados operam no escopo de metadados atual.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método FindAssembly](imetadatadispenserex-findassembly-method.md)|Este método não está implementado. Se chamado, ele retornará E_NOTIMPL.|  
|[Método FindAssemblyModule](imetadatadispenserex-findassemblymodule-method.md)|Este método não está implementado. Se chamado, ele retornará E_NOTIMPL.|  
|[Método GetCORSystemDirectory](imetadatadispenserex-getcorsystemdirectory-method.md)|Obtém o diretório que contém o Common Language Runtime atual (CLR). Esse método só tem suporte para uso por depuradores fora do processo. Se for chamado de outro componente, ele retornará E_NOTIMPL.|  
|[Método GetOption](imetadatadispenserex-getoption-method.md)|Obtém o valor da opção especificada para o escopo de metadados atual. A opção controla como as chamadas para o escopo de metadados atual são tratadas.|  
|[Método OpenScopeOnITypeInfo](imetadatadispenserex-openscopeonitypeinfo-method.md)|Este método não está implementado. Se chamado, ele retornará E_NOTIMPL.|  
|[Método SetOption](imetadatadispenserex-setoption-method.md)|Define a opção especificada para um determinado valor para o escopo de metadados atual. A opção controla como as chamadas para o escopo de metadados atual são tratadas.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de metadados](metadata-interfaces.md)
- [Interface IMetaDataDispenser](imetadatadispenser-interface.md)
- [Interface IMetaDataEmit](imetadataemit-interface.md)
- [Interface IMetaDataImport](imetadataimport-interface.md)
