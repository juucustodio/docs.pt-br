---
description: 'Saiba mais sobre: interface IReferenceAppId'
title: Interface IReferenceAppId
ms.date: 03/30/2017
api_name:
- IReferenceAppId
api_location:
- fusion.dll
api_type:
- COM
f1_keywords:
- IReferenceAppId
helpviewer_keywords:
- IReferenceAppId interface [.NET Framework fusion]
ms.assetid: 8eb9e565-f358-43ce-900e-a8f8a5aa6cfb
topic_type:
- apiref
ms.openlocfilehash: 66838d6ae66aa7de05d899e9fa980308718e2a38
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99800065"
---
# <a name="ireferenceappid-interface"></a>Interface IReferenceAppId

Representa uma referência ao identificador exclusivo para o aplicativo no escopo atual.  
  
## <a name="methods"></a>Métodos  
  
|Método|Descrição|  
|------------|-----------------|  
|`IReferenceAppId::get_CodeBase`|Obtém um ponteiro para uma representação de cadeia de caracteres do identificador de código para o aplicativo referenciado por isso `IReferenceAppId` .|  
|`IReferenceAppId::put_CodeBase`|Define o identificador de código para o aplicativo referenciado por isso `IReferenceAppId` .|  
|`IReferenceAppId::EnumAppPath`|Obtém um ponteiro de interface para uma `IEnumReferenceIdentity` instância que contém as `IReferenceIdentity` instâncias que representam os membros desse `IReferenceAppId` .|  
|`IReferenceAppId::get_SubscriptionId`|Obtém um ponteiro para uma representação de cadeia de caracteres do identificador de token para uma assinatura para isso `IReferenceAppId` .|  
|`IReferenceAppId::put_SubscriptionId`|Define o identificador de token para uma assinatura para `IReferenceAppId` o valor da cadeia de caracteres especificada.|  
  
## <a name="requirements"></a>Requisitos  

 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** Isolamento. h  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v20plus](../../../../includes/net-current-v20plus-md.md)]  
  
## <a name="see-also"></a>Consulte também

- [Interfaces de fusão](fusion-interfaces.md)
- [Interface IEnumReferenceIdentity](ienumreferenceidentity-interface.md)
- [Interface IReferenceIdentity](ireferenceidentity-interface.md)
