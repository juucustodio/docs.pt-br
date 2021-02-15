---
description: 'Saiba mais sobre: como fazer isso: atualização dinâmica'
title: 'Como: Atualização dinâmica'
ms.date: 03/30/2017
ms.assetid: 9b8f6e0d-edab-4a7e-86e3-8c66bebc64bb
ms.openlocfilehash: 877cb58dd271fa70176a4197da273d923ec253f3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704713"
---
# <a name="how-to-dynamic-update"></a>Como: Atualização dinâmica

Este tópico descreve as etapas básicas necessárias para criar e atualizar dinamicamente a configuração de roteamento. Neste exemplo, a configuração de roteamento inicial é obtida do arquivo de configuração e roteia todas as mensagens para o serviço de calculadora regularCalc; no entanto, ele é posteriormente atualizado programaticamente para alterar o ponto de extremidade de destino do serviço roundingCalc.  
  
> [!NOTE]
> Em muitas implementações, a configuração será totalmente dinâmica e não dependerá de uma configuração padrão; no entanto, há alguns cenários, como aquele neste tópico, em que é desejável ter um estado de configuração padrão quando o serviço é iniciado.  
  
> [!NOTE]
> As atualizações dinâmicas ocorrem apenas na memória e não resultam na modificação dos arquivos de configuração.  
  
 RegularCalc e roundingCalc dão suporte às mesmas operações de adicionar, subtrair, multiplicar e dividir; no entanto, roundingCalc arredonda todos os cálculos para o valor inteiro mais próximo antes de retornar. Um arquivo de configuração é usado para configurar o serviço para rotear todas as mensagens para o serviço regularCalc. Depois que o serviço de roteamento foi iniciado, <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> é usado para reconfigurar o serviço para rotear mensagens para o serviço roundingCalc.  
  
### <a name="implement-initial-configuration"></a>Implementar configuração inicial  
  
1. Crie a configuração básica do serviço de roteamento especificando os pontos de extremidade de serviço expostos pelo serviço. O exemplo a seguir define um único ponto de extremidade de serviço, que será usado para receber mensagens. Ele também define um ponto de extremidade de cliente que será usado para enviar mensagens para o regularCalc.  
  
    ```xml  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoint for the Routing Service-->  
        <endpoint address="calculator"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
      </service>  
    </services>  
    <client>  
    <!--set up the destination endpoint-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    ```  
  
2. Defina o filtro usado para rotear mensagens para os pontos de extremidade de destino. Para este exemplo, o filtro filtro matchall é usado para rotear todas as mensagens para o regularCalcEndpoint definido anteriormente. O exemplo a seguir define o filtro e a tabela de filtro.  
  
    ```xml  
    <filters>  
      <!--define the message filter-->  
      <filter name="MatchAllFilter" filterType="MatchAll"/>  
    </filters>  
    <filterTables>  
      <filterTable name="filterTable1">  
          <!--add the filter to the message filter table-->  
          <add filterName="MatchAllFilter" endpointName="regularCalcEndpoint"/>  
      </filterTable>  
    </filterTables>  
    ```  
  
3. Para avaliar as mensagens de entrada em relação aos filtros contidos na tabela de filtros, você deve associar a tabela de filtros aos pontos de extremidade de serviço usando o comportamento de roteamento. O exemplo a seguir demonstra como associar "filterTable1" ao ponto de extremidade de serviço.  
  
    ```xml  
    <behaviors>  
      <!--default routing service behavior definition-->  
      <serviceBehaviors>  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
## <a name="implement-dynamic-configuration"></a>Implementar configuração dinâmica  

 A configuração dinâmica do serviço de roteamento só pode ser executada no código criando um novo <xref:System.ServiceModel.Routing.RoutingConfiguration> e usando <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> para substituir a configuração atual.  Para este exemplo, o serviço de roteamento é hospedado internamente em um aplicativo de console. Depois que o aplicativo for iniciado, você poderá modificar a configuração de roteamento inserindo ' regular ' ou ' arredondando ' na janela do console para configurar o ponto de extremidade de destino para o qual as mensagens são roteadas; regularCalc quando ' regular ' for inserido, caso contrário, roundingCalc quando ' arredondando ' for inserido.  
  
1. As instruções using a seguir devem ser adicionadas para dar suporte ao serviço de roteamento.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.ServiceModel;  
    using System.ServiceModel.Channels;  
    using System.ServiceModel.Description;  
    using System.ServiceModel.Dispatcher;  
    using System.ServiceModel.Routing;  
    ```  
  
2. O código a seguir é usado para hospedar por conta própria o serviço de roteamento como um aplicativo de console. Isso inicializa o serviço de roteamento usando a configuração descrita na etapa anterior, que está contida no arquivo de configuração do aplicativo. O loop while contém o código usado para alterar a configuração de roteamento.  
  
    ```csharp  
    // Host the service within this EXE console application.  
    public static void Main()  
    {  
        // Create a ServiceHost for the CalculatorService type.  
        using (ServiceHost serviceHost =  
            new ServiceHost(typeof(RoutingService)))  
        {  
            // Open the ServiceHost to create listeners
            // and start listening for messages.  
            Console.WriteLine("The Routing Service configured, opening....");  
            serviceHost.Open();  
            Console.WriteLine("The Routing Service is now running.");  
             Console.WriteLine("Type 'quit' to terminate router.");  
             Console.WriteLine("<ENTER> to change routing configuration.");  
             while (Console.ReadLine() != "quit")  
             {  
            ....  
            }  
        }  
    }  
    ```  
  
3. Para atualizar dinamicamente a configuração de roteamento, é necessário criar uma nova configuração de roteamento. Isso deve conter todos os pontos de extremidade, filtros e tabelas de filtro necessários para a nova configuração de roteamento, pois ele substituirá completamente a configuração de roteamento existente. Para usar a nova configuração de roteamento, você deve invocar <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> e passar a nova configuração.  
  
     Adicione o seguinte código ao loop while definido anteriormente para permitir que o serviço seja reconfigurado com base na entrada do usuário.  
  
    ```csharp  
    Console.WriteLine("Enter 'regular' or 'rounding' to set the destination endpoint:");  
    string destEndpoint = Console.ReadLine();  
    // Create a new RoutingConfiguration  
    RoutingConfiguration rc = new RoutingConfiguration();  
    // Determine the endpoint to configure for  
    switch (destEndpoint)  
    {  
        case "regular":  
            // Define the destination endpoint  
            ServiceEndpoint regularCalc = new ServiceEndpoint(  
               ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
               new NetTcpBinding(),  
               new EndpointAddress("net.tcp://localhost:9090/servicemodelsamples/service/"));  
            // Create a MatchAll filter and add to the filter table  
            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { regularCalc });  
            // Use ApplyConfiguration to update the Routing Service  
            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
            Console.WriteLine("Applied new routing configuration.");  
            break;  
        case "rounding":  
            // Define the destination endpoint  
            ServiceEndpoint roundingCalc = new ServiceEndpoint(  
               ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
               new NetTcpBinding(),  
               new EndpointAddress("net.tcp://localhost:8080/servicemodelsamples/service/"));  
            // Create a MatchAll filter and add to the filter table  
            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { roundingCalc });  
            // Use ApplyConfiguration to update the Routing Service  
            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
            Console.WriteLine("Applied new routing configuration.");  
            break;  
        default:  
            Console.WriteLine("Incorrect value entered, no change.");  
            break;  
    }  
    ```  
  
    > [!NOTE]
    > Como o método para fornecer um novo RoutingConfiguration está contido na extensão de serviço RoutingExtension, novos objetos RoutingConfiguration podem ser fornecidos em qualquer lugar no modelo de extensibilidade do WCF que tem ou pode obter uma referência para o ServiceHost ou extensões de serviço (como em outra imextension).
  
## <a name="example"></a>Exemplo  

A seguir está uma lista completa do aplicativo de console usado neste exemplo:
  
```csharp
//-----------------------------------------------------------------  
//  Copyright (c) Microsoft Corporation.  All Rights Reserved.  
//-----------------------------------------------------------------  
  
using System;  
using System.Collections.Generic;  
using System.ServiceModel;  
using System.ServiceModel.Channels;  
using System.ServiceModel.Description;  
using System.ServiceModel.Dispatcher;  
using System.ServiceModel.Routing;  
  
namespace Microsoft.Samples.AdvancedFilters  
{  
    public class Router  
    {  
        // Host the service within this EXE console application.  
        public static void Main()  
        {
            // Create a ServiceHost for the CalculatorService type.  
            using (ServiceHost serviceHost =  
                new ServiceHost(typeof(RoutingService)))  
            {  
                // Open the ServiceHost to create listeners
                // and start listening for messages.  
                Console.WriteLine("The Routing Service configured, opening....");  
                serviceHost.Open();  
                Console.WriteLine("The Routing Service is now running.");  
                Console.WriteLine("Type 'quit' to terminate router.");  
                Console.WriteLine("<ENTER> to change routing configuration.");  
                while (Console.ReadLine() != "quit")  
                {  
                    Console.WriteLine("Enter 'regular' or 'rounding' to set the destination endpoint:");  
                    string destEndpoint = Console.ReadLine();  
                    // Create a new RoutingConfiguration  
                    RoutingConfiguration rc = new RoutingConfiguration();  
                    // Determine the endpoint to configure for  
                    switch (destEndpoint)  
                    {  
                        case "regular":  
                            // Define the destination endpoint  
                            ServiceEndpoint regularCalc = new ServiceEndpoint(  
                            ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
                            new NetTcpBinding(),  
                            new EndpointAddress("net.tcp://localhost:9090/servicemodelsamples/service/"));  
                            // Create a MatchAll filter and add to the filter table  
                            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { regularCalc });  
                            // Use ApplyConfiguration to update the Routing Service  
                            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
                            Console.WriteLine("Applied new routing configuration.");  
                            break;  
                        case "rounding":  
                            // Define the destination endpoint  
                            ServiceEndpoint roundingCalc = new ServiceEndpoint(  
                                ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
                                new NetTcpBinding(),  
                                new EndpointAddress("net.tcp://localhost:8080/servicemodelsamples/service/"));  
                            // Create a MatchAll filter and add to the filter table  
                            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { roundingCalc });  
                            // Use ApplyConfiguration to update the Routing Service  
                            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
                            Console.WriteLine("Applied new routing configuration.");  
                            break;  
                        default:  
                            Console.WriteLine("Incorrect value entered, no change.");  
                            break;  
                    }  
                }  
            }  
        }  
    }  
}  
```  
  
## <a name="example"></a>Exemplo  

A seguir está uma lista completa do arquivo de configuração usado neste exemplo:
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright (c) Microsoft Corporation. All rights reserved -->  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoint for the Routing Service-->  
        <endpoint address="calculator"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
      </service>  
    </services>  
    <behaviors>  
      <!--default routing service behavior definition-->  
      <serviceBehaviors>  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
    <client>  
<!--set up the destination endpoint-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    <routing>  
  
      <filters>  
        <!--define the message filter-->  
        <filter name="MatchAllFilter" filterType="MatchAll"/>  
      </filters>  
      <filterTables>  
        <filterTable name="filterTable1">  
            <!--add the filter to the message filter table-->  
            <add filterName="MatchAllFilter" endpointName="regularCalcEndpoint"/>  
        </filterTable>  
      </filterTables>  
    </routing>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Consulte também

- [Serviços de roteamento](../samples/routing-services.md)
