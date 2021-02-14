---
description: 'Saiba mais sobre: interface IEnumReferenceIdentity'
title: Interface IEnumReferenceIdentity
ms.date: 03/30/2017
api_name:
- IEnumReferenceIdentity
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IEnumReferenceIdentity
helpviewer_keywords:
- IEnumReferenceIdentity interface [.NET Framework fusion]
ms.assetid: a17b3155-7216-4e16-8c9f-abce21f549e7
topic_type:
- apiref
ms.openlocfilehash: a7f17793fd737b5153c27dae59fb2aa87b46cf48
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100465295"
---
# <a name="ienumreferenceidentity-interface"></a>Interface IEnumReferenceIdentity

Serve como um enumerador para uma coleção de `IReferenceIdentity` objetos.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|`IEnumReferenceIdentity::Clone`|Obtém um ponteiro de interface para um novo `IEnumReferenceIdentity` que contém os mesmos membros que isso `IEnumReferenceIdentity` .|  
|`IEnumReferenceIdentity::Next`|Obtém o número especificado de `IReferenceIdentity` objetos, começando na posição atual.|  
|`IEnumReferenceIdentity::Reset`|Move o ponteiro de instrução para o início dele `IEnumReferenceIdentity` .|  
|`IEnumReferenceIdentity::Skip`|Move o ponteiro de instrução para frente pelo número especificado de elementos, começando na posição atual.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Isolamento. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de fusão](fusion-interfaces.md)
- [Interface IReferenceIdentity](ireferenceidentity-interface.md)
