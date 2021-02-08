---
description: 'Saiba mais sobre: exemplo de WebContentTypeMapper'
title: WebContentTypeMapper Sample
ms.date: 03/30/2017
ms.assetid: a4fe59e7-44d8-43c6-a1f8-40c45223adca
ms.openlocfilehash: 274672bb8db1dc845b1cc1ced58b4c4a92232e9b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798141"
---
# <a name="webcontenttypemapper-sample"></a>WebContentTypeMapper Sample

Este exemplo demonstra como mapear novos tipos de conteúdo para Windows Communication Foundation (WCF) formatos de corpo de mensagem.  
  
 O <xref:System.ServiceModel.Description.WebHttpEndpoint> elemento conecta o codificador de mensagem da Web, que permite que o WCF receba mensagens binárias JSON, XML ou RAW no mesmo ponto de extremidade. O codificador determina o formato do corpo da mensagem observando o tipo de conteúdo HTTP da solicitação. Este exemplo apresenta a <xref:System.ServiceModel.Channels.WebContentTypeMapper> classe, que permite ao usuário controlar o mapeamento entre o tipo de conteúdo e o formato do corpo.  
  
 O WCF fornece um conjunto de mapeamentos padrão para tipos de conteúdo. Por exemplo, `application/json` mapeia para JSON e `text/xml` MAPEIA para XML. Qualquer tipo de conteúdo que não esteja mapeado para JSON ou XML é mapeado para o formato binário bruto.  
  
 Em alguns cenários (por exemplo, APIs de estilo push), o desenvolvedor do serviço não controla o tipo de conteúdo retornado pelo cliente. Por exemplo, os clientes podem retornar JSON como `text/javascript` em vez de `application/json` . Nesse caso, o desenvolvedor do serviço deve fornecer um tipo derivado de <xref:System.ServiceModel.Channels.WebContentTypeMapper> para tratar o tipo de conteúdo fornecido corretamente, conforme mostrado no código de exemplo a seguir.  
  
```csharp  
public class JsonContentTypeMapper : WebContentTypeMapper  
{  
    public override WebContentFormat  
               GetMessageFormatForContentType(string contentType)  
    {  
        if (contentType == "text/javascript")  
        {  
            return WebContentFormat.Json;  
        }  
        else  
        {  
            return WebContentFormat.Default;  
        }  
    }  
}  
```  
  
 O tipo deve substituir o <xref:System.ServiceModel.Channels.WebContentTypeMapper.GetMessageFormatForContentType%28System.String%29> método. O método deve avaliar o `contentType` argumento e retornar um dos seguintes valores: <xref:System.ServiceModel.Channels.WebContentFormat.Json> , <xref:System.ServiceModel.Channels.WebContentFormat.Xml> , <xref:System.ServiceModel.Channels.WebContentFormat.Raw> ou <xref:System.ServiceModel.Channels.WebContentFormat.Default> . Retornando <xref:System.ServiceModel.Channels.WebContentFormat.Default> adiamentos para os mapeamentos de codificador de mensagem da Web padrão. No código de exemplo anterior, o `text/javascript` tipo de conteúdo é mapeado para JSON e todos os outros mapeamentos permanecem inalterados.  
  
 Para usar a `JsonContentTypeMapper` classe, use o seguinte no seu Web.config:  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <standardEndpoint name="" contentTypeMapper="Microsoft.Samples.WebContentTypeMapper.JsonContentTypeMapper, JsonContentTypeMapper, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 Para verificar o requisito para usar o JsonContentTypeMapper, remova o atributo contentTypeMapper do arquivo de configuração acima. Falha ao carregar a página do cliente ao tentar usar o `text/javascript` para enviar conteúdo JSON.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Verifique se você executou o [procedimento de configuração única para os exemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Crie a solução WebContentTypeMapperSample. sln, conforme descrito em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).  
  
3. Navegue até `http://localhost/ServiceModelSamples/JCTMClientPage.htm` (não abra JCTMClientPage.htm no navegador de dentro do diretório do projeto).  
  
> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Extensibility\Ajax\WebContentTypeMapper`  
