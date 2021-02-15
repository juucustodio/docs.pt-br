---
description: 'Saiba mais sobre: pontos de extremidade padrão'
title: Pontos de extremidade padrão
ms.date: 03/30/2017
ms.assetid: 3fcb4225-addc-44f2-935d-30e4943a8812
ms.openlocfilehash: 5879bab5dff4dee8ac574bad1c4452a60cf7c323
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793435"
---
# <a name="standard-endpoints"></a>Pontos de extremidade padrão

Os pontos de extremidade são definidos especificando um endereço, uma associação e um contrato. Outros parâmetros que podem ser definidos em um ponto de extremidade incluem configuração de comportamento, cabeçalhos e URIs de escuta.  Para determinados tipos de pontos de extremidade, esses valores não são alterados. Por exemplo, os pontos de extremidade de troca de metadados sempre usam o <xref:System.ServiceModel.Description.IMetadataExchange> contrato. Outros pontos de extremidade, como <xref:System.ServiceModel.Description.WebHttpEndpoint> sempre requerer um comportamento de Endpoint especificado. A usabilidade de um ponto de extremidade pode ser melhorada com o uso de pontos de extremidade com valores padrão para propriedades de Endpoint mais usadas. Os pontos de extremidade padrão permitem que um desenvolvedor defina um ponto de extremidade que tem valores padrão ou em que uma ou mais propriedades de pontos finais não são alteradas.  Esses pontos de extremidade permitem que você use um deles, sem precisar especificar informações de natureza estática. Os pontos de extremidade padrão podem ser usados para a infraestrutura e os pontos de extremidade do aplicativo.  
  
## <a name="infrastructure-endpoints"></a>Pontos de extremidade de infraestrutura  

 Um serviço pode expor pontos de extremidade com algumas das propriedades não explicitamente implementadas pelo autor do serviço. Por exemplo, o ponto de extremidade de troca de metadados expõe o <xref:System.ServiceModel.Description.IMetadataExchange> contrato, mas como um autor de serviço, você não implementa essa interface, ela é implementada pelo WCF. Esses pontos de extremidade de infraestrutura têm valores padrão para uma ou mais propriedades de ponto de extremidades, alguns dos quais podem não ser alterados. A <xref:System.ServiceModel.Description.ServiceEndpoint.Contract%2A> Propriedade do ponto de extremidade de troca de metadados deve ser <xref:System.ServiceModel.Description.IMetadataExchange> , enquanto outras propriedades, como a associação, podem ser fornecidas pelo desenvolvedor. Os pontos de extremidade de infraestrutura são identificados definindo a <xref:System.ServiceModel.Description.ServiceEndpoint.IsSystemEndpoint%2A> propriedade como `true` .  
  
## <a name="application-endpoints"></a>Pontos de extremidade do aplicativo  

 Os desenvolvedores de aplicativos podem definir seus próprios pontos de extremidade padrão que especificam valores padrão para o endereço, a associação ou o contrato. Você define um ponto de extremidade padrão derivando uma classe de <xref:System.ServiceModel.Description.ServiceEndpoint> e definindo as propriedades apropriadas do ponto de extremidade. Você pode fornecer valores padrão para propriedades que podem ser alteradas. Algumas outras propriedades terão valores estáticos que não podem ser alterados. O exemplo a seguir mostra como implementar um ponto de extremidade padrão.  
  
```csharp
public class CustomEndpoint : ServiceEndpoint
{
    public CustomEndpoint()
        : this(string.Empty)
    { }  

    public CustomEndpoint(string address)
        : this(address, ContractDescription.GetContract(typeof(ICalculator)))
    { }  

    // Create the custom endpoint with a fixed binding
    public CustomEndpoint(string address, ContractDescription contract)
        : base(contract)
    {
        this.Binding = new BasicHttpBinding();
        this.IsSystemEndpoint = false;
    }

    // Definition of the additional property of this endpoint
    public bool Property { get; set; }
}
```
  
 Para usar um ponto de extremidade personalizado definido pelo usuário em um arquivo de configuração, você deve derivar uma classe de <xref:System.ServiceModel.Configuration.StandardEndpointElement> , derivar uma classe de <xref:System.ServiceModel.Configuration.StandardEndpointCollectionElement%602> e registrar o novo ponto de extremidade padrão na seção extensões em app.config ou machine.config.  O <xref:System.ServiceModel.Configuration.StandardEndpointElement> fornece suporte de configuração para o ponto de extremidade padrão, conforme mostrado no exemplo a seguir.  
  
```csharp
public class CustomEndpointElement : StandardEndpointElement
{
    // Definition of the additional property for the standard endpoint element
    public bool Property
    {
        get { return (bool)base["property"]; }
        set { base["property"] = value; }
    }

    // The additional property needs to be added to the properties of the standard endpoint element
    protected override ConfigurationPropertyCollection Properties
    {
        get
        {
            ConfigurationPropertyCollection properties = base.Properties;
            properties.Add(new ConfigurationProperty("property", typeof(bool), false, ConfigurationPropertyOptions.None));
            return properties;
        }
    }

    // Return the type of this standard endpoint
    protected override Type EndpointType
    {
        get { return typeof(CustomEndpoint); }
    }

    // Create the custom service endpoint
    protected override ServiceEndpoint CreateServiceEndpoint(ContractDescription contract)
    {
        return new CustomEndpoint();
    }

    // Read the value given to the property in config and save it
    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ServiceEndpointElement serviceEndpointElement)
    {
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;
        customEndpoint.Property = this.Property;
    }

    // Read the value given to the property in config and save it
    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ChannelEndpointElement channelEndpointElement)
    {
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;
        customEndpoint.Property = this.Property;
    }

    // No validation in this sample
    protected override void OnInitializeAndValidate(ServiceEndpointElement serviceEndpointElement)
    {
    }

    // No validation in this sample
    protected override void OnInitializeAndValidate(ChannelEndpointElement channelEndpointElement)
    {
    }
}
```  
  
 O <xref:System.ServiceModel.Configuration.StandardEndpointCollectionElement%602> fornece o tipo de backup para a coleção que aparece na seção <`standardEndpoints`> na configuração do ponto de extremidade padrão.  O exemplo a seguir mostra como implementar essa classe.  
  
```csharp
public class CustomEndpointCollectionElement : StandardEndpointCollectionElement<CustomEndpoint, CustomEndpointElement>
{
    // ...
}
```

O exemplo a seguir mostra como registrar um ponto de extremidade padrão na seção extensões.

```xml  
<extensions>  
      <standardEndpointExtensions>  
        <add  
          name="customStandardEndpoint"  
          type="CustomEndpointCollectionElement, Example.dll,  
                Version=1.0.0.0, Culture=neutral, PublicKeyToken=ffffffffffffffff"/>  
      </standardEndpointExtensions>
</extensions>  
```  
  
## <a name="configuring-a-standard-endpoint"></a>Configurando um ponto de extremidade padrão  

 Os pontos de extremidade padrão podem ser adicionados no código ou na configuração.  Para adicionar um ponto de extremidade padrão no código, basta instanciar o tipo de ponto de extremidade padrão apropriado e adicioná-lo ao host de serviço, conforme mostrado no exemplo a seguir:  
  
```csharp  
serviceHost.AddServiceEndpoint(new CustomEndpoint());  
```  
  
 Para adicionar um ponto de extremidade padrão na configuração, adicione um `endpoint` elemento <> ao `service` elemento> <e quaisquer definições de configuração necessárias no `standardEndpoints` elemento <>. O exemplo a seguir mostra como adicionar um <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> , um dos pontos de extremidade padrão fornecidos com o [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] .  
  
```xml  
<services>  
  <service>  
    <endpoint isSystemEndpoint="true" kind="udpDiscoveryEndpoint" />  
  </service>  
</services>  
<standardEndpoints>
  <udpDiscoveryEndpoint>  
     <standardEndpoint multicastAddress="soap.udp://239.255.255.250:3702" />
  </udpDiscoveryEndpoint>
</standardEndpoints>
```  
  
 O tipo de ponto de extremidade padrão é especificado usando o atributo Kind no `endpoint` elemento <>. O ponto de extremidade é configurado dentro do `standardEndpoints` elemento <>. No exemplo acima, um <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> ponto de extremidade é adicionado e configurado. O `udpDiscoveryEndpoint` elemento <> contém um> de <`standardEndpoint` que define a <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint.MulticastAddress%2A> Propriedade do <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint> .  
  
## <a name="standard-endpoints-shipped-with-the-net-framework"></a>Pontos de extremidade padrão fornecidos com o .NET Framework  

 A tabela a seguir lista os pontos de extremidade padrão fornecidos com o [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] .  
  
 `Mex Endpoint`  
 Um ponto de extremidade padrão que é usado para expor metadados de serviço.  
  
 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
 Um ponto de extremidade padrão usado pelos serviços para enviar mensagens de comunicado.  
  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
 Um ponto de extremidade padrão que é usado pelos serviços para enviar mensagens de descoberta.  
  
 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
 Um ponto de extremidade padrão pré-configurado para operações de descoberta por meio de uma associação multicast UDP.  
  
 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
 Um ponto de extremidade padrão usado pelos serviços para enviar mensagens de comunicado por meio de uma associação UDP.  
  
 <xref:System.ServiceModel.Discovery.DynamicEndpoint>  
 Um ponto de extremidade padrão que usa WS-Discovery para localizar o endereço do ponto de extremidade dinamicamente no tempo de execução.  
  
 <xref:System.ServiceModel.Description.ServiceMetadataEndpoint>  
 Um ponto de extremidade padrão para troca de metadados.  
  
 <xref:System.ServiceModel.Description.WebHttpEndpoint>  
 Um ponto de extremidade padrão com uma <xref:System.ServiceModel.WebHttpBinding> associação que adiciona automaticamente o <xref:System.ServiceModel.Description.WebHttpBehavior> comportamento  
  
 <xref:System.ServiceModel.Description.WebScriptEndpoint>  
 Um ponto de extremidade padrão com uma <xref:System.ServiceModel.WebHttpBinding> associação que adiciona automaticamente o <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> comportamento.  
  
 <xref:System.ServiceModel.Description.WebServiceEndpoint>  
 Um ponto de extremidade padrão com uma <xref:System.ServiceModel.WebHttpBinding> associação.  
  
 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>  
 Um ponto de extremidade padrão que permite chamar operações de controle em instâncias de fluxo de trabalho.  
  
 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>  
 Um ponto de extremidade padrão que dá suporte à criação de fluxo de trabalho e à continuação de indicador.
