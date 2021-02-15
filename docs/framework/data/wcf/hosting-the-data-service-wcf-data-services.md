---
description: 'Saiba mais sobre: hospedando o serviço de dados (WCF Data Services)'
title: Hospedando o serviço de dados (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, configuring
- WCF Data Services, Windows Communication Foundation
ms.assetid: b48f42ce-22ce-4f8d-8f0d-f7ddac9125ee
ms.openlocfilehash: 519adde3a3e054d68ff9a1b7acf7ff06c0ca7532
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765783"
---
# <a name="hosting-the-data-service-wcf-data-services"></a>Hospedando o serviço de dados (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Usando WCF Data Services, você pode criar um serviço que expõe dados como um feed Protocolo Open Data (OData). Esse serviço de dados é definido como uma classe que herda de <xref:System.Data.Services.DataService%601> . Essa classe fornece a funcionalidade necessária para processar mensagens de solicitação, executar atualizações na fonte de dados e gerar mensagens de respostas, conforme exigido pelo OData. No entanto, um serviço de dados não pode se associar a e escutar em um soquete de rede para solicitações HTTP de entrada. Para essa funcionalidade necessária, o serviço de dados depende de um componente de hospedagem.

 O host do serviço de dados executa as seguintes tarefas em nome do serviço de dados:

- Escuta solicitações e roteia essas solicitações para o serviço de dados.

- Cria uma instância do serviço de dados para cada solicitação.

- Solicita que o serviço de dados processe a solicitação de entrada.

- Envia a resposta em nome do serviço de dados.

 Para simplificar a hospedagem de um serviço de dados, WCF Data Services é projetada para integrar com o Windows Communication Foundation (WCF). O serviço de dados fornece uma implementação padrão do WCF que serve como o host do serviço de dados em um aplicativo ASP.NET. Portanto, você pode hospedar um serviço de dados do de uma das seguintes maneiras:

- Em um aplicativo ASP.NET.

- Em um aplicativo gerenciado que dá suporte a serviços WCF hospedados internamente.

- Em algum outro host de serviço de dados personalizado.

## <a name="hosting-a-data-service-in-an-aspnet-application"></a>Hospedando um serviço de dados em um aplicativo ASP.NET

Quando você usa a caixa de diálogo **Adicionar novo item** no Visual Studio 2015 para definir um serviço de dados em um aplicativo ASP.net, a ferramenta gera dois novos arquivos no projeto. O primeiro arquivo tem uma `.svc` extensão e instrui o tempo de execução do WCF a criar uma instância do serviço de dados. Este é um exemplo desse arquivo para o serviço de dados de exemplo Northwind criado quando você conclui o [início rápido](quickstart-wcf-data-services.md):

```aspx-csharp
<%@ ServiceHost Language="C#"
    Factory="System.Data.Services.DataServiceHostFactory,
            System.Data.Services, Version=4.0.0.0,
            Culture=neutral, PublicKeyToken=b77a5c561934e089"
    Service="NorthwindService.Northwind" %>
```

 Essa diretiva informa o aplicativo para criar o host de serviço para a classe de serviço de dados nomeada usando a <xref:System.Data.Services.DataServiceHostFactory> classe.

 A página code-behind do `.svc` arquivo contém a classe que é a implementação do próprio serviço de dados, que é definida da seguinte maneira para o serviço de dados de exemplo Northwind:

 [!code-csharp[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#servicedefinition)]
 [!code-vb[Astoria Quickstart Service#ServiceDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#servicedefinition)]

 Como um serviço de dados se comporta como um serviço WCF, o serviço de dados integra-se ao ASP.NET e segue o modelo de programação Web do WCF. Para obter mais informações, consulte [Serviços WCF e](../../wcf/feature-details/wcf-services-and-aspnet.md) [modelo de programação Web http](../../wcf/feature-details/wcf-web-http-programming-model.md)do ASP.net e WCF.

## <a name="self-hosted-wcf-services"></a>Self-Hosted serviços WCF

 Como ele incorpora uma implementação do WCF, WCF Data Services dá suporte à hospedagem interna de um serviço de dados como um serviço WCF. Um serviço pode ser hospedado automaticamente em qualquer aplicativo .NET Framework, como um aplicativo de console. A <xref:System.Data.Services.DataServiceHost> classe, que é herdada de <xref:System.ServiceModel.Web.WebServiceHost> , é usada para instanciar o serviço de dados em um endereço específico.

 A hospedagem interna pode ser usada para desenvolvimento e teste porque pode facilitar a implantação e a solução de problemas do serviço. No entanto, esse tipo de hospedagem não fornece recursos avançados de hospedagem e gerenciamento fornecidos pelo ASP.NET ou pelo Serviços de Informações da Internet (IIS). Para obter mais informações, consulte [hospedagem em um aplicativo gerenciado](../../wcf/feature-details/hosting-in-a-managed-application.md).

## <a name="defining-a-custom-data-service-host"></a>Definindo um host de serviço de dados personalizado

 Para casos em que a implementação do host do WCF é muito restritiva, você também pode definir um host personalizado para um serviço de dados. Qualquer classe que implemente <xref:System.Data.Services.IDataServiceHost> a interface pode ser usada como o host de rede para um serviço de dados. Um host personalizado deve implementar a <xref:System.Data.Services.IDataServiceHost> interface e ser capaz de lidar com as seguintes responsabilidades básicas do host do serviço de dados:

- Forneça o serviço de dados com o caminho raiz do serviço.

- Processar informações de cabeçalhos de solicitação e resposta para a <xref:System.Data.Services.IDataServiceHost> implementação de membro apropriada.

- Tratar exceções geradas pelo serviço de dados.

- Valide os parâmetros na cadeia de caracteres de consulta.

## <a name="see-also"></a>Consulte também

- [Configurando WCF Data Services](defining-wcf-data-services.md)
- [Expor seus dados como um serviço](exposing-your-data-as-a-service-wcf-data-services.md)
- [Configurar o serviço de dados](configuring-the-data-service-wcf-data-services.md)
