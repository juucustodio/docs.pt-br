---
description: 'Saiba mais sobre: definindo as propriedades de uso e estilo'
title: Definindo as amostras de propriedades de estilo e de uso
ms.date: 03/30/2017
ms.assetid: c09a0600-116f-41cf-900a-1b7e4ea4e300
ms.openlocfilehash: 435ea23e4a34ec91ea764ae9435487c1e1313afd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792993"
---
# <a name="setting-the-use-and-style-properties"></a>Definindo o uso e as propriedades de estilo

Este exemplo demonstra como usar as propriedades de uso e estilo no <xref:System.ServiceModel.XmlSerializerFormatAttribute> e no <xref:System.ServiceModel.DataContractFormatAttribute> . Essas propriedades afetam o modo como as mensagens são formatadas. Por padrão, o corpo da mensagem é formatado com o estilo definido como <xref:System.ServiceModel.OperationFormatStyle.Document> . Essas configurações podem ser especificadas no nível de contrato de serviço ou no nível de contrato de operação.

> [!NOTE]
> O procedimento de instalação e as instruções de Build para este exemplo estão localizados no final deste tópico.

A <xref:System.ServiceModel.DataContractFormatAttribute.Style%2A> Propriedade Style determina como os metadados WSDL para o serviço são formatados. Os valores possíveis são <xref:System.ServiceModel.OperationFormatStyle.Document> e <xref:System.ServiceModel.OperationFormatStyle.Rpc> . RPC significa que a representação WSDL das mensagens trocadas para uma operação contém parâmetros como se fosse uma chamada de procedimento remota. A seguir, é mostrado um exemplo.

```xml
<wsdl:message name="IUseAndStyleCalculator_Add_InputMessage">
  <wsdl:part name="n1" type="xsd:double"/>
  <wsdl:part name="n2" type="xsd:double"/>
</wsdl:message>
```

Definir o estilo como <xref:System.ServiceModel.OperationFormatStyle.Document> significa que a representação WSDL contém um único elemento que representa o documento que é trocado para uma operação, conforme mostrado no exemplo a seguir.

```xml
<wsdl:message name="IUseAndStyleCalculator_Add_InputMessage">
  <wsdl:part name="parameters" element="tns:Add"/>
</wsdl:message>
```

A <xref:System.ServiceModel.XmlSerializerFormatAttribute.Use%2A> propriedade determina o formato da mensagem. Os valores possíveis são <xref:System.ServiceModel.OperationFormatUse.Literal> e <xref:System.ServiceModel.OperationFormatUse.Encoded> ; o valor padrão é <xref:System.ServiceModel.OperationFormatUse.Literal> . Literal significa que a mensagem é uma instância literal do esquema no WSDL, conforme mostrado no exemplo de documento/literal a seguir.

```xml
<Add xmlns="http://Microsoft.ServiceModel.Samples">
  <n1>100</n1>
  <n2>15.99</n2>
</Add>
```

Encoded significa que os esquemas no WSDL são especificações abstratas que são codificadas de acordo com as regras encontradas na seção 5 do SOAP 1,1. Este é um exemplo de RPC/codificado.

```xml
<q1:Add xmlns:q1="http://Microsoft.ServiceModel.Samples">
  <n1 xsi:type="xsd:double" xmlns="">100</n1>
  <n2 xsi:type="xsd:double" xmlns="">15.99</n2>
</q1:Add>
```

O WS-I Basic Profile 1,0 proíbe o uso de <xref:System.ServiceModel.OperationFormatUse.Encoded> e você só deve usá-lo quando exigido pelos serviços herdados. O `Encoded` formato da mensagem só está disponível ao usar o XmlSerializer.

Para permitir que você veja as mensagens que estão sendo enviadas e recebidas, este exemplo é baseado no [rastreamento e no log de mensagens](tracing-and-message-logging.md). A configuração do serviço e o código-fonte foram modificados para habilitar e utilizar rastreamento e log de mensagens. Além disso, o <xref:System.ServiceModel.WSHttpBinding> foi configurado sem segurança, portanto, as mensagens registradas podem ser exibidas em um formato não criptografado. Os logs de rastreamento resultantes (System. ServiceModel. e2e e Message. log) devem ser exibidos usando a [ferramenta do Visualizador de rastreamento de serviço (SvcTraceViewer.exe)](../service-trace-viewer-tool-svctraceviewer-exe.md). Os rastreamentos são configurados para serem criados na pasta C:\LOGS. Crie a pasta antes de executar o exemplo. Para exibir o conteúdo da mensagem na ferramenta Visualizador de rastreamento, selecione **mensagens** nos painéis esquerdo e direito da ferramenta.

O código a seguir mostra o contrato de serviço com a <xref:System.ServiceModel.XmlSerializerFormatAttribute.Use%2A> propriedade definida como <xref:System.ServiceModel.OperationFormatUse> e o formato do corpo da mensagem foi alterado do padrão <xref:System.ServiceModel.OperationFormatStyle> para <xref:System.ServiceModel.OperationFormatStyle.Document> .

```csharp
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples"),
XmlSerializerFormat(Style = OperationFormatStyle.Rpc,
                                 Use = OperationFormatUse.Encoded)]
public interface IUseAndStyleCalculator
{
    [OperationContract]
    double Add(double n1, double n2);
    [OperationContract]
    double Subtract(double n1, double n2);
    [OperationContract]
    double Multiply(double n1, double n2);
    [OperationContract]
    double Divide(double n1, double n2);
}
```

Para ver a diferença entre as diferentes <xref:System.ServiceModel.XmlSerializerFormatAttribute.Use%2A> <xref:System.ServiceModel.XmlSerializerFormatAttribute.Style%2A> configurações, modifique-as no serviço, gere novamente o cliente, execute o exemplo e examine o arquivo c:\logs\message.logs com a ferramenta Visualizador de rastreamento de serviço. Além disso, observe o impacto nos metadados exibindo `http://localhost/ServiceModelSamples/service.svc?wsdl` . Os metadados dos serviços normalmente são divididos em várias páginas. A página WSDL principal contém as associações WSDL, mas a exibição `http://localhost/ServiceModelSamples/service.svc?wsdl=wsdl0` para observar as definições de mensagem.

## <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo

1. Verifique se você executou o [procedimento de configuração única para os exemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).

2. Crie um diretório do C:\LOGS para mensagens de log. Conceda permissões de gravação ao serviço de rede do usuário para esse diretório.

3. Para criar a edição C# ou Visual Basic .NET da solução, siga as instruções em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).

4. Para executar o exemplo em uma configuração de computador único ou cruzado, siga as instruções em [executando os exemplos de Windows Communication Foundation](running-the-samples.md).

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Contract\Message\UseAndStyle`
