---
description: 'Saiba mais sobre: correlação de Request-Reply'
title: Correlação resposta/solicitação
ms.date: 03/30/2017
ms.assetid: cf4379bf-2d08-43f3-9584-dfa30ffcb1f6
ms.openlocfilehash: e745c9061f227e08400973f43613da73e68c8d70
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99632835"
---
# <a name="request-reply-correlation"></a>Correlação resposta/solicitação

A correlação de solicitação-resposta é usada com um <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> par para implementar uma operação bidirecional em um serviço de fluxo de trabalho e com um <xref:System.ServiceModel.Activities.Send> / <xref:System.ServiceModel.Activities.ReceiveReply> par que invoca uma operação bidirecional em outro serviço Web. Ao invocar uma operação bidirecional em um serviço WCF, o serviço pode ser um serviço de Windows Communication Foundation (WCF) baseado em código imperativo tradicional ou pode ser um serviço de fluxo de trabalho. Para usar a correlação de solicitação-resposta, é necessário usar uma associação bidirecional, como <xref:System.ServiceModel.BasicHttpBinding> . Se invocar ou implementar uma operação bidirecional, as etapas de inicialização de correlação são semelhantes e são abordadas nesta seção.  
  
## <a name="using-correlation-in-a-two-way-operation-with-receivesendreply"></a>Usando a correlação em uma operação de Two-Way com Receive/SendReply  

 Um <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> par é usado para implementar uma operação bidirecional em um serviço de fluxo de trabalho. O tempo de execução usa a correlação de solicitação-resposta para garantir que a resposta seja expedida para o chamador correto. Quando um fluxo de trabalho é hospedado usando <xref:System.ServiceModel.Activities.WorkflowServiceHost> , que é o caso dos serviços de fluxo de trabalho, a inicialização de correlação padrão é suficiente. Nesse cenário, um <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> par é usado por um fluxo de trabalho e nenhuma configuração de correlação específica é necessária.  
  
```csharp  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
```  
  
### <a name="explicitly-initializing-request-reply-correlation"></a>Inicializando explicitamente Request-Reply correlação  

 Se outras operações de duas vias estiverem em paralelo, a correlação deverá ser configurada explicitamente. Isso pode ser feito especificando um <xref:System.ServiceModel.Activities.CorrelationHandle> e <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> , ou colocando o <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> dentro de um <xref:System.ServiceModel.Activities.CorrelationScope> . Neste exemplo, a correlação de solicitação-resposta é configurada em um <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> par.  
  
```csharp  
Variable<CorrelationHandle> RRHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder",  
    CorrelationInitializers =  
    {  
        new RequestReplyCorrelationInitializer  
        {  
            CorrelationHandle = RRHandle  
        }  
    }  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
// Construct a workflow using StartOrder and ReplyToStartOrder.  
```  
  
 Em vez de configurar explicitamente a correlação, uma <xref:System.ServiceModel.Activities.CorrelationScope> atividade pode ser usada. <xref:System.ServiceModel.Activities.CorrelationScope> fornece um implícito <xref:System.ServiceModel.Activities.CorrelationHandle> para as atividades de mensagens que ele contém. Neste exemplo, um <xref:System.ServiceModel.Activities.Receive> / <xref:System.ServiceModel.Activities.SendReply> par está contido dentro de um <xref:System.ServiceModel.Activities.CorrelationScope> . Nenhuma configuração de correlação explícita é necessária.  
  
```csharp  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = OrderContractName,  
    OperationName = "StartOrder"  
};  
  
SendReply ReplyToStartOrder = new SendReply  
{  
    Request = StartOrder,  
    Content = … // Contains the return value, if any.  
};  
  
CorrelationScope s = new CorrelationScope  
{  
    Body = new Sequence  
    {  
        Activities =
        {  
            StartOrder,  
            // Activities that create the reply.  
            ReplyToStartOrder  
        }  
    }  
};  
  
// Construct a workflow using the CorrelationScope.  
```  
  
 Se correlações adicionais forem necessárias, elas poderão ser configuradas usando a <xref:System.ServiceModel.Activities.Send.CorrelationInitializers%2A> propriedade das respectivas atividades de mensagens usando os tipos desejados `CorrelationInitializer` .  
  
## <a name="using-correlation-in-a-two-way-operation-with-sendreceivereply"></a>Usando a correlação em uma operação de Two-Way com Send/ReceiveReply  

 Embora a <xref:System.ServiceModel.Activities.Receive> atividade só possa ser usada em um serviço de fluxo de trabalho hospedado pelo <xref:System.ServiceModel.Activities.WorkflowServiceHost> , <xref:System.ServiceModel.Activities.Send> e o <xref:System.ServiceModel.Activities.Send> / <xref:System.ServiceModel.Activities.ReceiveReply> par pode ser usado em qualquer fluxo de trabalho que deve invocar um método em um serviço Web. Se o fluxo de trabalho for hospedado usando <xref:System.ServiceModel.Activities.WorkflowServiceHost> , a correlação padrão descrita na seção anterior se aplicará, mas se não, a correlação deverá ser configurada explicitamente usando o desejado <xref:System.ServiceModel.Activities.CorrelationInitializer> e <xref:System.ServiceModel.Activities.CorrelationHandle> , ou usando o gerenciamento de identificador implícito do <xref:System.ServiceModel.Activities.CorrelationScope> .  
  
 Ao usar **Adicionar referência de serviço** em um serviço com operações bidirecionais, são geradas atividades que encapsulam uma <xref:System.ServiceModel.Activities.Send> / <xref:System.ServiceModel.Activities.ReceiveReply> atividade de par internamente com a correlação de solicitação/resposta especificada explicitamente.
