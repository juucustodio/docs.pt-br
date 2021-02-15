---
description: 'Saiba mais sobre: interface IAssemblyCacheItem'
title: Interface IAssemblyCacheItem
ms.date: 03/30/2017
api_name:
- IAssemblyCacheItem
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCacheItem
helpviewer_keywords:
- IAssemblyCacheItem interface [.NET Framework fusion]
ms.assetid: ccc9387a-9f44-4f4f-bf8f-0ea6d2afa21b
topic_type:
- apiref
ms.openlocfilehash: 2dcb721f6b65ecca93262f9af2ba355d94bb774d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760843"
---
# <a name="iassemblycacheitem-interface"></a>Interface IAssemblyCacheItem

Representa um único assembly no cache de assembly global.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método AbortItem](iassemblycacheitem-abortitem-method.md)|Permite que o assembly no cache de assembly global execute operações de limpeza antes que ele seja liberado.|  
|[Método Commit](iassemblycacheitem-commit-method.md)|Confirma a referência de assembly armazenada em cache para a memória.|  
|[Método CreateStream](iassemblycacheitem-createstream-method.md)|Cria um fluxo com o nome e o formato especificados.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de fusão](fusion-interfaces.md)
- [Cache de assemblies global](../../app-domains/gac.md)
- [Interface IAssemblyCache](iassemblycache-interface.md)
