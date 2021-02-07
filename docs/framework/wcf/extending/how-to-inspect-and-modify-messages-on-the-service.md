---
description: 'Saiba mais sobre: como inspecionar e modificar mensagens no serviço'
title: 'Como: inspecionar e modificar mensagens do serviço'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9c5b1cc7-84f3-45f8-9226-d59c278e8c42
ms.openlocfilehash: 5fd3a5e49bdd35a3095e5855b399533337e133a9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99668871"
---
# <a name="how-to-inspect-and-modify-messages-on-the-service"></a>Como: inspecionar e modificar mensagens do serviço

Você pode inspecionar ou modificar as mensagens de entrada ou saída em um cliente Windows Communication Foundation (WCF) implementando uma <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType> e inserindo-a no tempo de execução do serviço. Para obter mais informações, consulte [estendendo expatchers](extending-dispatchers.md). O recurso equivalente no serviço é o <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType> .  
  
### <a name="to-inspect-or-modify-messages"></a>Para inspecionar ou modificar mensagens  
  
1. Implemente a interface <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType>.  
  
2. Implemente <xref:System.ServiceModel.Description.IServiceBehavior?displayProperty=nameWithType> uma <xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=nameWithType> interface, ou, <xref:System.ServiceModel.Description.IContractBehavior?displayProperty=nameWithType> dependendo do escopo no qual você deseja inserir facilmente seu inspetor de mensagem de serviço.  
  
3. Insira seu comportamento antes de chamar o <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> método no <xref:System.ServiceModel.ServiceHost?displayProperty=nameWithType> . Para obter detalhes, consulte [Configurando e estendendo o tempo de execução com comportamentos](configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="example"></a>Exemplo  

 Os exemplos de código a seguir mostram, em ordem:  
  
- Uma implementação do Inspetor de serviço.  
  
- Um comportamento de serviço que insere o Inspetor.  
  
- Um arquivo de configuração que carrega e executa o comportamento em um aplicativo de serviço.  
  
 [!code-csharp[Interceptors#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/interceptors.cs#7)]
 [!code-vb[Interceptors#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/interceptors.vb#7)]  
  
 [!code-csharp[Interceptors#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/insertingbehaviors.cs#8)]
 [!code-vb[Interceptors#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/interceptors/vb/insertingbehaviors.vb#8)]  
  
 [!code-xml[Interceptors#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/interceptors/cs/hostapplication.exe.config#9)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=nameWithType>
- <xref:System.ServiceModel.Dispatcher.IDispatchMessageInspector?displayProperty=nameWithType>
- [Configurando e estendendo o runtime com comportamentos](configuring-and-extending-the-runtime-with-behaviors.md)
