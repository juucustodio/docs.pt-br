---
description: 'Saiba mais sobre: como criar um contrato de One-Way'
title: 'Como: criar um contrato unidirecional'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 85084cd9-31cc-4e95-b667-42ef01336622
ms.openlocfilehash: 465dc2da20288c918a70743fcbe3ed931620b33b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734718"
---
# <a name="how-to-create-a-one-way-contract"></a>Como: criar um contrato unidirecional

Este tópico mostra as etapas básicas para criar métodos que usam um contrato unidirecional. Esses métodos invocam operações em um serviço de Windows Communication Foundation (WCF) de um cliente, mas não esperam uma resposta. Esse tipo de contrato pode ser usado, por exemplo, para publicar notificações para muitos assinantes. Você também pode usar contratos unidirecionais ao criar um contrato duplex (bidirecional), que permite que clientes e servidores se comuniquem entre si de forma independente, de forma que seja possível iniciar chamadas para o outro. Isso pode permitir, em particular, que o servidor faça chamadas unidirecionais para o cliente que o cliente pode tratar como eventos. Para obter informações detalhadas sobre como especificar métodos unidirecionais, consulte a <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> propriedade e a <xref:System.ServiceModel.OperationContractAttribute> classe.  
  
 Para obter mais informações sobre como criar um aplicativo cliente para um contrato duplex, consulte [como acessar serviços com One-Way e contratos de Request-Reply](how-to-access-wcf-services-with-one-way-and-request-reply-contracts.md). Para obter um exemplo funcional, consulte o exemplo [unidirecional](../samples/one-way.md) .  
  
### <a name="to-create-a-one-way-contract"></a>Para criar um contrato unidirecional  
  
1. Crie o contrato de serviço aplicando a <xref:System.ServiceModel.ServiceContractAttribute> classe à interface que define os métodos que o serviço deve implementar.  
  
2. Indique quais métodos na interface um cliente pode invocar aplicando a <xref:System.ServiceModel.OperationContractAttribute> classe a eles.  
  
3. Designe operações que não devem ter nenhuma saída (nenhum valor de retorno e nenhum parâmetro out ou ref) como unidirecional definindo a <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> propriedade como `true` . Observe que as operações que carregam a <xref:System.ServiceModel.OperationContractAttribute> classe atendem a um contrato de solicitação-resposta por padrão, pois a <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> propriedade é `false` por padrão. Portanto, você deve especificar explicitamente o valor da propriedade de atributo como `true` se desejar um contrato unidirecional para o método.  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir define um contrato para um serviço que inclui vários métodos unidirecionais. Todos os métodos têm contratos unidirecionais, exceto `Equals` , que assume a solicitação-Reply e retorna um resultado.  
  
 [!code-csharp[S_Service_Session#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.ServiceContractAttribute>
- <xref:System.ServiceModel.OperationContractAttribute>
- [Serviços de implantação e projeção](../designing-and-implementing-services.md)
- [Como definir um contrato de serviço](../how-to-define-a-wcf-service-contract.md)
- [Sessão](../samples/session.md)
- [Como: criar um contrato duplex](how-to-create-a-duplex-contract.md)
