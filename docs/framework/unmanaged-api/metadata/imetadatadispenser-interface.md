---
description: 'Saiba mais sobre: interface IMetaDataDispenser'
title: Interface IMetaDataDispenser
ms.date: 03/30/2017
api_name:
- IMetaDataDispenser
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataDispenser
helpviewer_keywords:
- IMetaDataDispenser interface [.NET Framework metadata]
ms.assetid: 989840b3-9822-4ce5-a6c5-b375d3340a7a
topic_type:
- apiref
ms.openlocfilehash: 5ba37fc05a4e1897b100967d32b268f91a0e4402
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99721002"
---
# <a name="imetadatadispenser-interface"></a>Interface IMetaDataDispenser

Fornece métodos para criar um novo escopo de metadados ou abrir um existente.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|[Método DefineScope](imetadatadispenser-definescope-method.md)|Cria uma nova área na memória na qual você pode criar novos metadados.|  
|[Método OpenScope](imetadatadispenser-openscope-method.md)|Abre um arquivo existente em disco e mapeia seus metadados na memória.|  
|[Método OpenScopeOnMemory](imetadatadispenser-openscopeonmemory-method.md)|Abre uma área de memória que contém os metadados existentes. Ou seja, esse método abre uma área especificada de memória na qual os dados existentes são tratados como metadados.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataforma:** Consulte [requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Cor. h  
  
 **Biblioteca:** Usado como um recurso no MsCorEE.dll  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v10plus](../../../../includes/net-current-v10plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interface IMetaDataDispenserEx](imetadatadispenserex-interface.md)
- [Interfaces de metadados](metadata-interfaces.md)
