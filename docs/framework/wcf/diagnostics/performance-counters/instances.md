---
description: 'Saiba mais sobre: instâncias'
title: Instâncias
ms.date: 03/30/2017
ms.assetid: c8cf3460-0ca1-4411-8262-e9ecaf7f0a31
ms.openlocfilehash: 9cd602164816a419b481ff600a7537593d4f500e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99655260"
---
# <a name="instances"></a>Instâncias

Nome do contador: instâncias.  
  
## <a name="description"></a>Descrição  

 Número de contextos de instância que o serviço contém atualmente.  
  
 Na maioria das vezes, o número de contextos de instância é idêntico ao número de instâncias. No entanto, os cenários a seguir são uma exceção a essa regra.  
  
- Um método de serviço chama o <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A> método explicitamente.  
  
- Um <xref:System.ServiceModel.ReleaseInstanceMode> é aplicado a uma <xref:System.ServiceModel.OperationBehaviorAttribute> instância do.  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.OperationBehaviorAttribute>
