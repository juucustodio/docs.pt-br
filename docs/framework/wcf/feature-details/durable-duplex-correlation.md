---
description: 'Saiba mais sobre: correlação de duplex durável'
title: Correlação duplex durável
ms.date: 03/30/2017
ms.assetid: 8eb0e49a-6d3b-4f7e-a054-0d4febee2ffb
ms.openlocfilehash: e30356e03ccb6f8fae7ca735d2ad674bbe2a191d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704947"
---
# <a name="durable-duplex-correlation"></a>Correlação duplex durável

A correlação de duplex durável, também conhecida como correlação de retorno de chamada, é útil quando um serviço de fluxo de trabalho tem um requisito para enviar um retorno de chamada para o chamador inicial. Ao contrário do WCF duplex, o retorno de chamada pode ocorrer a qualquer momento no futuro e não está vinculado ao mesmo canal ou ao tempo de vida do canal; o único requisito é que o chamador tenha um ponto de extremidade ativo ouvindo a mensagem de retorno de chamada. Isso permite que dois serviços de fluxo de trabalho se comuniquem em uma conversa de execução longa. Este tópico fornece uma visão geral da correlação de duplex durável.  
  
## <a name="using-durable-duplex-correlation"></a>Usando a correlação de duplex durável  

 Para usar a correlação de duplex durável, os dois serviços devem usar uma associação habilitada para contexto que dá suporte a operações de duas vias, como <xref:System.ServiceModel.NetTcpContextBinding> ou <xref:System.ServiceModel.WSHttpContextBinding> . O serviço de chamada registra um <xref:System.ServiceModel.WSHttpContextBinding.ClientCallbackAddress%2A> com a associação desejada em seu cliente <xref:System.ServiceModel.Endpoint> . O serviço de recebimento recebe esses dados na chamada inicial e, em seguida, usa-os por conta própria <xref:System.ServiceModel.Endpoint> na <xref:System.ServiceModel.Activities.Send> atividade que faz a chamada de volta para o serviço de chamada. Neste exemplo, dois serviços se comunicam entre si. O primeiro serviço invoca um método no segundo serviço e aguarda uma resposta. O segundo serviço sabe o nome do método de retorno de chamada, mas o ponto de extremidade do serviço que implementa esse método não é conhecido em tempo de design.  
  
> [!NOTE]
> O duplex durável só pode ser usado quando o <xref:System.ServiceModel.Channels.AddressingVersion> do ponto de extremidade está configurado com <xref:System.ServiceModel.Channels.AddressingVersion.WSAddressing10%2A> . Se não for, uma <xref:System.InvalidOperationException> exceção será lançada com a seguinte mensagem: "a mensagem contém um cabeçalho de contexto de retorno de chamada com uma referência de ponto de extremidade para [AddressingVersion](http://schemas.xmlsoap.org/ws/2004/08/addressing). O contexto de retorno de chamada só poderá ser transmitido quando o AddressingVersion estiver configurado com ' WSAddressing10 '.
  
 No exemplo a seguir, um serviço de fluxo de trabalho é hospedado que cria um retorno de chamada <xref:System.ServiceModel.Endpoint> usando <xref:System.ServiceModel.WSHttpContextBinding> .  
  
```csharp  
// Host WF Service 1.  
string baseAddress1 = "http://localhost:8080/Service1";  
WorkflowServiceHost host1 = new WorkflowServiceHost(GetWF1(), new Uri(baseAddress1));  
  
// Add the callback endpoint.  
WSHttpContextBinding Binding1 = new WSHttpContextBinding();  
host1.AddServiceEndpoint("ICallbackItemsReady", Binding1, "ItemsReady");  
  
// Add the service endpoint.  
host1.AddServiceEndpoint("IService1", Binding1, baseAddress1);  
  
// Open the first workflow service.  
host1.Open();  
Console.WriteLine("Service1 waiting at: {0}", baseAddress1);  
```  
  
 O fluxo de trabalho que implementa esse serviço de fluxo de trabalho Inicializa a correlação de retorno de chamada com sua <xref:System.ServiceModel.Activities.Send> atividade e faz referência a esse ponto de extremidade de retorno de chamada da <xref:System.ServiceModel.Activities.Receive> atividade que se correlaciona com o <xref:System.ServiceModel.Activities.Send> . O exemplo a seguir representa o fluxo de trabalho que é retornado do `GetWF1` método.  
  
```csharp  
Variable<CorrelationHandle> CallbackHandle = new Variable<CorrelationHandle>();  
  
Receive StartOrder = new Receive  
{  
    CanCreateInstance = true,  
    ServiceContractName = "IService1",  
    OperationName = "StartOrder"  
};  
  
Send GetItems = new Send  
{  
    CorrelationInitializers =
    {  
        new CallbackCorrelationInitializer  
        {  
            CorrelationHandle = CallbackHandle  
        }  
    },  
    ServiceContractName = "IService2",  
    OperationName = "StartItems",  
    Endpoint = new Endpoint  
    {  
        AddressUri = new Uri("http://localhost:8081/Service2"),  
        Binding = new WSHttpContextBinding  
        {  
            ClientCallbackAddress = new Uri("http://localhost:8080/Service1/ItemsReady")
        }  
    }  
};  
  
Receive ItemsReady = new Receive  
{  
    ServiceContractName = "ICallbackItemsReady",  
    OperationName = "ItemsReady",  
    CorrelatesWith = CallbackHandle,  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        CallbackHandle  
    },  
    Activities =  
    {  
        StartOrder,  
        new WriteLine  
        {  
            Text = "WF1 - Started"  
        },  
        GetItems,  
        new WriteLine  
        {  
            Text = "WF1 - Request Submitted"  
        },  
        ItemsReady,  
        new WriteLine  
        {  
            Text = "WF1 - Items Received"  
        }  
     }  
};  
```  
  
 O segundo serviço de fluxo de trabalho é hospedado usando uma associação baseada em contexto, fornecida pelo sistema.  
  
```csharp  
// Host WF Service 2.  
string baseAddress2 = "http://localhost:8081/Service2";  
WorkflowServiceHost host2 = new WorkflowServiceHost(GetWF2(), new Uri(baseAddress2));  
  
// Add the service endpoint.  
WSHttpContextBinding Binding2 = new WSHttpContextBinding();  
host2.AddServiceEndpoint("IService2", Binding2, baseAddress2);  
  
// Open the second workflow service.  
host2.Open();  
Console.WriteLine("Service2 waiting at: {0}", baseAddress2);  
```  
  
 O fluxo de trabalho que implementa esse serviço de fluxo de trabalho começa com uma <xref:System.ServiceModel.Activities.Receive> atividade. Essa atividade Receive Inicializa a correlação de retorno de chamada para esse serviço, atrasa por um período de tempo para simular o trabalho de execução longa e, em seguida, chama o primeiro serviço usando o contexto de retorno de chamada que foi passado na primeira ligação para o serviço. O exemplo a seguir representa o fluxo de trabalho que é retornado de uma chamada para `GetWF2` . Observe que a <xref:System.ServiceModel.Activities.Send> atividade tem um endereço de espaço reservado de `http://www.contoso.com` ; o endereço real usado em tempo de execução é o endereço de retorno de chamada fornecido.  
  
```csharp  
Variable<CorrelationHandle> ItemsCallbackHandle = new Variable<CorrelationHandle>();  
  
Receive StartItems = new Receive  
{  
    CorrelationInitializers =
    {  
        new CallbackCorrelationInitializer  
        {  
            CorrelationHandle = ItemsCallbackHandle  
        }  
    },  
    CanCreateInstance = true,  
    ServiceContractName = "IService2",  
    OperationName = "StartItems"  
};  
  
Send ItemsReady = new Send  
{  
    CorrelatesWith = ItemsCallbackHandle,  
    Endpoint = new Endpoint  
    {  
        // The callback address on the binding is used  
        // instead of this placeholder address.  
        AddressUri = new Uri("http://www.contoso.com"),  
  
        Binding = new WSHttpContextBinding()  
    },  
    OperationName = "ItemsReady",  
    ServiceContractName = "ICallbackItemsReady"  
};  
  
Activity wf = new Sequence  
{  
    Variables =  
    {  
        ItemsCallbackHandle  
    },  
    Activities =  
    {  
        StartItems,  
        new WriteLine  
        {  
            Text = "WF2 - Request Received"  
        },  
        new Delay  
        {  
            Duration = TimeSpan.FromMinutes(90)  
        },  
        new WriteLine  
        {  
            Text = "WF2 - Sending items"  
        },  
        ItemsReady,  
        new WriteLine  
        {  
            Text = "WF2 - Items sent"  
        }  
     }  
};  
```  
  
 Quando o `StartOrder` método é invocado no primeiro fluxo de trabalho, a saída a seguir é exibida, mostrando o fluxo de execução por meio dos dois fluxos de trabalho.  
  
```output  
Service1 waiting at: http://localhost:8080/Service1  
Service2 waiting at: http://localhost:8081/Service2  
Press enter to exit.
WF1 - Started  
WF2 - Request Received  
WF1 - Request Submitted  
WF2 - Sending items  
WF2 - Items sent  
WF1 - Items Received  
```  
  
 Neste exemplo, os fluxos de trabalho gerenciam explicitamente a correlação usando um <xref:System.ServiceModel.Activities.CallbackCorrelationInitializer> . Como havia apenas uma única correlação nesses fluxos de trabalho de exemplo, o <xref:System.ServiceModel.Activities.CorrelationHandle> Gerenciamento padrão seria suficiente.
