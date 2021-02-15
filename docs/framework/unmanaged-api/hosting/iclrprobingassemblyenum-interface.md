---
description: 'Saiba mais sobre: interface ICLRProbingAssemblyEnum'
title: Interface ICLRProbingAssemblyEnum
ms.date: 03/30/2017
api_name:
- ICLRProbingAssemblyEnum
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- ICLRProbingAssemblyEnum
helpviewer_keywords:
- ICLRProbingAssemblyEnum interface [.NET Framework hosting]
ms.assetid: e7d3ccab-b0f0-4872-8935-0ed72920171b
topic_type:
- apiref
ms.openlocfilehash: 1fd11e237f02bab85ec2b41df49d7d8a2f27e1e1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716491"
---
# <a name="iclrprobingassemblyenum-interface"></a>Interface ICLRProbingAssemblyEnum

Fornece métodos que permitem ao host obter as identidades de investigação de um assembly usando as informações de identidade do assembly que são internas ao Common Language Runtime (CLR), sem a necessidade de criar ou compreender essa identidade.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método Get](iclrprobingassemblyenum-get-method.md)|Obtém a identidade do assembly no índice especificado.|  
  
## <a name="remarks"></a>Comentários  

 Métodos como [ICLRAssemblyIdentityManager:: GetProbingAssembliesFromReference](iclrassemblyidentitymanager-getprobingassembliesfromreference-method.md) retornam uma `ICLRProbingAssemblyEnum` instância.  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** MSCorEE. h  
  
 **Biblioteca:** Incluído como um recurso no MSCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface ICLRAssemblyIdentityManager](iclrassemblyidentitymanager-interface.md)
- [Interface ICLRAssemblyReferenceList](iclrassemblyreferencelist-interface.md)
- [Interfaces de hospedagem](hosting-interfaces.md)
