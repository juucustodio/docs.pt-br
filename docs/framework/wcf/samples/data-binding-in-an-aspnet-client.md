---
description: 'Saiba mais sobre: Associação de dados em um cliente ASP.NET'
title: Associação de dados em um cliente do ASP.NET
ms.date: 03/30/2017
ms.assetid: 68b49fa6-94e7-4d4c-a34e-902a2b3770b6
ms.openlocfilehash: 9615c34805d406bb382ab252f317156e1750bed1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755857"
---
# <a name="data-binding-in-an-aspnet-client"></a>Associação de dados em um cliente do ASP.NET

Este exemplo demonstra como associar dados retornados por um serviço de Windows Communication Foundation típico (WCF) em um aplicativo Web Forms.  
  
> [!NOTE]
> O procedimento de instalação e as instruções de Build para este exemplo estão localizados no final deste tópico.  
  
 Este exemplo demonstra um serviço que implementa um contrato que define um padrão de comunicação de solicitação-resposta. O exemplo consiste em um cliente Web Forms aplicativo acessível de um navegador e um serviço WCF hospedado pelo Serviços de Informações da Internet (IIS).  
  
 O serviço implementa um contrato que define um padrão de comunicação de solicitação-resposta. O contrato é definido pela `IWeatherService` interface, que expõe uma operação chamada `GetWeatherData` . Esta operação aceita uma matriz de cidades e retorna uma matriz de `WeatherData` objetos que representam a temperatura alta e baixa prevista para uma cidade.  
  
 Na página ASP.NET Client. aspx, um controle Web DataGrid é definido, que contém a representação gráfica dos dados retornados pelo serviço. O código na página. aspx chama o serviço WCF para dados meteorológicos e retorna os dados para uma matriz de `WeatherData` objetos. O DataGrid especifica para onde obter seus dados definindo sua `DataSource` propriedade para essa matriz. A vinculação de dados ocorre com uma chamada para o método do DataGrid `DataBind` . Todo esse código está contido no.`aspx` o método da página `Page_Load` , portanto, sempre que o usuário atualiza a página do navegador, os dados são atualizados no DataGrid.  
  
### <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo  
  
1. Verifique se você executou o [procedimento de configuração única para os exemplos de Windows Communication Foundation](one-time-setup-procedure-for-the-wcf-samples.md).  
  
2. Para criar a edição C# ou Visual Basic .NET da solução, siga as instruções em [criando os exemplos de Windows Communication Foundation](building-the-samples.md).  
  
3. O cliente deste exemplo é um site da Web que é executado em um servidor Web de desenvolvimento. Para iniciar o servidor Web de desenvolvimento, digite o seguinte no prompt de comando: `%SystemDrive%\Program Files\Common Files\Microsoft Shared\DevServer\9.0\WebDev.WebServer.EXE" /port:8000 /path:<WebFormsSamplePath>\CS\client /vpath:/client` . Em seguida, navegue até `http://localhost:8000/client` . Para executar esse exemplo entre computadores, substitua todas as referências `localhost` no arquivo de Web.config do cliente pelo nome do computador do servidor.  
  
> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WCF\Scenario\DataBinding\WebForms`
