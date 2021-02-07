---
description: 'Saiba mais sobre: uso de pontos de extremidade padrão'
title: Uso de pontos de extremidade padrão
ms.date: 03/30/2017
ms.assetid: ecd6a62f-9619-4778-a497-6f888087a9ea
ms.openlocfilehash: 804fdd84d3f6ff6f961aed81e8bd14cf8c43063c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99685407"
---
# <a name="usage-of-standard-endpoints"></a>Uso de pontos de extremidade padrão

Este exemplo demonstra como usar pontos de extremidade padrão em arquivos de configuração de serviço. Um ponto de extremidade padrão permite que o usuário Simplifique as definições de ponto de extremidade usando uma única propriedade para descrever uma combinação de endereço, associação e contrato com propriedades adicionais associadas a ela. Este exemplo demonstra como definir e implementar um ponto de extremidade padrão personalizado e como definir propriedades específicas no ponto de extremidade.

## <a name="sample-details"></a>Detalhes de exemplo

Os pontos de extremidade de serviço podem ser especificados fornecendo três parâmetros: endereço, associação e contrato. Outros parâmetros que podem ser fornecidos incluem configuração de comportamento, cabeçalhos, URI de escuta e assim por diante. Em alguns casos, qualquer um ou todos os endereços, associações e contratos têm valores que não podem ser alterados. Por esse motivo, é possível usar pontos de extremidade padrão. Alguns exemplos desses pontos de extremidade incluem pontos de extremidade de troca de metadados e pontos de extremidade de descoberta. Os pontos de extremidade padrão também melhoram a usabilidade, permitindo a configuração de pontos de extremidade de serviço sem precisar fornecer informações de natureza fixa ou criar seus próprios pontos de extremidade padrão, por exemplo, para melhorar a usabilidade fornecendo um conjunto razoável de valores padrão e, portanto, reduzindo o detalhamento dos arquivos de configuração.

Este exemplo consiste em dois projetos: o serviço que define dois pontos de extremidade padrão e o cliente que se comunica com o serviço. A maneira como os pontos de extremidade padrão são definidos para o serviço no arquivo de configuração é mostrada no exemplo a seguir.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
  <system.serviceModel>
    <extensions>
      <endpointExtensions>
        <add name="customEndpoint" type="Microsoft.Samples.StandardEndpoints.CustomEndpointCollectionElement, service" />
      </endpointExtensions>
    </extensions>
    <services>
      <service name="Microsoft.Samples.StandardEndpoints.CalculatorService">
        <endpoint address="http://localhost:8000/Samples/Service.svc/customEndpoint" contract="Microsoft.Samples.StandardEndpoints.ICalculator" kind="customEndpoint" />
        <endpoint kind="mexEndpoint" />
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <behavior>
          <serviceMetadata httpGetEnabled="True"/>
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <standardEndpoints>
      <customEndpoint>
        <standardEndpoint property="True" />
      </customEndpoint>
    </standardEndpoints>
  </system.serviceModel>
</configuration>
```

O primeiro ponto de extremidade definido para o serviço é de tipo `customEndpoint` , cuja definição pode ser vista na `<standardEndpoints>` seção, na qual a propriedade `property` recebe o valor `true` . Esse é o caso de um ponto de extremidade personalizado com uma nova propriedade. O segundo ponto de extremidade corresponde a um ponto de extremidade de metadados, no qual os valores de endereço, associação e contrato são corrigidos.

Para definir o elemento de ponto de extremidade padrão, uma classe derivada de `StandardEndpointElement` deve ser criada. No caso deste exemplo, a classe foi `CustomEndpointElement` definida conforme mostrado no exemplo a seguir.

```csharp
public class CustomEndpointElement : StandardEndpointElement
{
    public bool Property
    {
        get { return (bool)base["property"]; }
        set { base["property"] = value; }
    }

    protected override ConfigurationPropertyCollection Properties
    {
        get
        {
            ConfigurationPropertyCollection properties = base.Properties;
            properties.Add(new ConfigurationProperty("property", typeof(bool), false, ConfigurationPropertyOptions.None));
            return properties;
        }
    }

    protected override Type EndpointType
    {
        get { return typeof(CustomEndpoint); }
    }

    protected override ServiceEndpoint CreateServiceEndpoint(ContractDescription contract)
    {
        return new CustomEndpoint();
    }

    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ServiceEndpointElement serviceEndpointElement)
    {
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;
        customEndpoint.Property = this.Property;
    }

    protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ChannelEndpointElement channelEndpointElement)
    {
        CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;
        customEndpoint.Property = this.Property;
    }

    protected override void OnInitializeAndValidate(ServiceEndpointElement serviceEndpointElement)
    {
    }

    protected override void OnInitializeAndValidate(ChannelEndpointElement channelEndpointElement)
    {
    }
}
```

Na `CreateServiceEndpoint` função, um `CustomEndpoint` objeto é criado. Sua definição é mostrada no exemplo a seguir:

```csharp
public class CustomEndpoint : ServiceEndpoint
{
    public CustomEndpoint()
        : this(string.Empty)
    {
    }

    public CustomEndpoint(string address)
        : this(address, ContractDescription.GetContract(typeof(ICalculator)))
    {
    }

    public CustomEndpoint(string address, ContractDescription contract)
        : base(contract)
    {
        this.Binding = new BasicHttpBinding();
        this.IsSystemEndpoint = false;
    }

    public bool Property
    {
        get;
        set;
    }
}
```

 Para executar a comunicação entre o serviço e o cliente, uma referência de serviço é criada no cliente para o serviço. Quando o exemplo é compilado e executado, o serviço é executado e o cliente se comunica com ele. Observe que a referência de serviço deve ser atualizada toda vez que houver alguma alteração no serviço.

#### <a name="to-use-this-sample"></a>Para usar este exemplo

1. Usando o Visual Studio 2012, abra o arquivo StandardEndpoints. sln.

2. Habilite vários projetos para inicialização.

    1. Em **Gerenciador de soluções**, clique com o botão direito do mouse na solução pontos de extremidade padrão e selecione **Propriedades**.

    2. Em **Propriedades comuns**, selecione **projeto de inicialização** e clique em **vários projetos de inicialização**.

    3. Mova o projeto de serviço para o início da lista, com a **ação** definida como **Iniciar**.

    4. Mova o projeto cliente após o projeto de serviço, também com a **ação** definida como **Iniciar**.

         Isso especifica que o projeto do cliente é executado após o projeto de serviço.

3. Para executar a solução, pressione F5.

> [!NOTE]
> Se essas etapas não funcionarem, verifique se o seu ambiente foi configurado corretamente, usando as seguintes etapas:
>
> 1. Verifique se você executou o [procedimento de configuração única para os exemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).
> 2. Para compilar a solução, siga as instruções em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).
> 3. Para executar o exemplo em uma ou várias configurações de computador, siga as instruções em [executando os exemplos de Windows Communication Foundation](running-the-samples.md).

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\StandardEndpoints`
