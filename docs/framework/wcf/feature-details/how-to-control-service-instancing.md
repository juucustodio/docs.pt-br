---
description: 'Saiba mais sobre: como controlar a instanciação de serviço'
title: 'Como: controlar instanciação de serviço'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e0b12b34-8004-443a-a46d-83a5c00f2601
ms.openlocfilehash: 014d7fb4b054a1b52c1fea671cd099267fba468c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99779914"
---
# <a name="how-to-control-service-instancing"></a>Como: controlar instanciação de serviço

Definir o modo de instância de um serviço permite que você especifique quando um <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType> (e seu objeto de serviço associado definido pelo usuário) são criados. Consulte a <xref:System.ServiceModel.InstanceContextMode> enumeração para os modos possíveis. Para obter mais informações sobre comportamentos, consulte [Configurando e estendendo o tempo de execução com comportamentos](../extending/configuring-and-extending-the-runtime-with-behaviors.md). Para obter exemplos de funcionamento, consulte [comportamentos](../samples/behaviors.md).  
  
### <a name="to-control-the-service-instance-lifetime-using-code"></a>Para controlar o tempo de vida da instância de serviço usando código  
  
1. Aplique o <xref:System.ServiceModel.ServiceBehaviorAttribute> à classe de serviço.  
  
2. Defina a <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> propriedade como um dos seguintes valores: <xref:System.ServiceModel.InstanceContextMode.PerCall> , <xref:System.ServiceModel.InstanceContextMode.PerSession> ou <xref:System.ServiceModel.InstanceContextMode.Single> .  
  
     [!code-csharp[C_ControlServiceInstancing#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#1)]
     [!code-vb[C_ControlServiceInstancing#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#1)]  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir define a <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> Propriedade do <xref:System.ServiceModel.ServiceBehaviorAttribute> atributo como <xref:System.ServiceModel.InstanceContextMode.PerCall> .  
  
 [!code-csharp[c_ControlServiceInstancing#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_controlserviceinstancing/cs/source.cs#2)]
 [!code-vb[c_ControlServiceInstancing#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_controlserviceinstancing/vb/source.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.ServiceBehaviorAttribute>
- <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>
- <xref:System.ServiceModel.InstanceContextMode>
- [Serviço: exemplos de comportamentos](../samples/behaviors.md)
