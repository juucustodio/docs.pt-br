---
description: 'Saiba mais sobre: interface IAssemblyCache'
title: Interface IAssemblyCache
ms.date: 03/30/2017
api_name:
- IAssemblyCache
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IAssemblyCache
helpviewer_keywords:
- IAssemblyCache interface [.NET Framework fusion]
ms.assetid: 71ea170f-872d-4fc5-81b6-27da1dec9b19
topic_type:
- apiref
ms.openlocfilehash: 29c042fc101180085a697e02376b91b0e1ffd19f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99760921"
---
# <a name="iassemblycache-interface"></a>Interface IAssemblyCache

Representa o cache de assembly global para uso pela tecnologia Fusion.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método CreateAssemblyCacheItem](iassemblycache-createassemblycacheitem-method.md)|Obtém uma referência a um novo [IAssemblyCacheItem](iassemblycacheitem-interface.md).|  
|[Método CreateAssemblyScavenger](iassemblycache-createassemblyscavenger-method.md)|Reservado para uso interno pela tecnologia Fusion.|  
|[Método InstallAssembly](iassemblycache-installassembly-method.md)|Instala o assembly especificado no cache de assembly global.|  
|[Método QueryAssemblyInfo](iassemblycache-queryassemblyinfo-method.md)|Obtém os dados solicitados sobre o assembly especificado.|  
|[Método UninstallAssembly](iassemblycache-uninstallassembly-method.md)|Desinstala o assembly especificado do cache de assembly global.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Fusion. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de fusão](fusion-interfaces.md)
- [Cache de assemblies global](../../app-domains/gac.md)
