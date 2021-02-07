---
description: 'Saiba mais sobre: exemplo de integração do SystemWebRouting'
title: Exemplo de integração de SystemWebRouting
ms.date: 03/30/2017
ms.assetid: f1c94802-95c4-49e4-b1e2-ee9dd126ff93
ms.openlocfilehash: 84b442dfb7f0e5877f742fb055aea49a5625bb78
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99668637"
---
# <a name="systemwebrouting-integration-sample"></a>Exemplo de integração de SystemWebRouting

Este exemplo demonstra a integração da camada de hospedagem com as classes no <xref:System.Web.Routing> namespace. As classes no <xref:System.Web.Routing> namespace permitem que um aplicativo use URLs que não correspondem diretamente a um recurso físico. Usar o roteamento da Web permite que o desenvolvedor crie endereços virtuais para HTTP que são então mapeados de volta para os serviços reais do WCF. Isso é útil quando um serviço WCF deve ser hospedado sem a necessidade de um arquivo ou recurso físico, ou quando os serviços devem ser acessados com URLs que não contêm arquivos como. html ou. aspx. Este exemplo demonstra como utilizar a <xref:System.Web.Routing.RouteTable> classe para criar URIs virtuais que mapeiam para serviços em execução definidos em global. asax.

> [!NOTE]
> As classes no <xref:System.Web.Routing> namespace só funcionam para serviços hospedados via http.  
  
Este exemplo usa o WCF para criar dois RSS feeds: um `movies` feed e um `channels` feed. As URLs para ativar os serviços não contêm uma extensão e são registradas no `Application_Start` método da `Global` classe derivada da <xref:System.Web.HttpApplication> classe.  
  
> [!NOTE]
> Este exemplo só funciona no Serviços de Informações da Internet (IIS) 7,0 e posterior, pois o IIS 6,0 usa um método diferente para dar suporte a URLs sem extensão.  

#### <a name="to-download-this-sample"></a>Para baixar este exemplo
  
Este exemplo pode já estar instalado em seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  

`<InstallDrive>:\WF_WCF_Samples`  

 Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  

`<InstallDrive>:\WF_WCF_Samples\WCF\Basic\Services\Hosting\WebRoutingIntegration`  
  
#### <a name="to-use-this-sample"></a>Para usar este exemplo  
  
1. Usando o Visual Studio, abra o arquivo WebRoutingIntegration. sln.  
  
2. Para executar a solução e iniciar o servidor de desenvolvimento da Web, pressione F5.  
  
     Uma listagem de diretório para o exemplo é exibida. Observe que não há arquivos com uma extensão de arquivo. svc.  
  
3. Na barra de endereços, adicione `movies` à URL, para que ela leia `http://localhost:[port]/movies` e pressione Enter.  
  
     O feed de filmes aparece no navegador.  
  
4. Na barra de endereços, adicione `channels` à URL, para que seja leituras `http://localhost:[port]/channels` e pressione Enter.  
  
     O feed canais é exibido no navegador.  
  
5. Feche o navegador da Web, pressionando ALT + F4.  
  
     Se o servidor de desenvolvimento não tiver sido encerrado, clique com o botão direito do mouse no ícone da área de notificação e selecione **parar**.  
  
#### <a name="to-use-this-sample-when-hosted-in-iis"></a>Para usar este exemplo quando hospedado no IIS  
  
1. Usando o Visual Studio, abra o arquivo WebRoutingIntegration. sln.  
  
2. Crie o projeto pressionando CTRL + SHIFT + B.  
  
3. Crie um aplicativo Web no Gerenciador do Serviços de Informações da Internet (IIS).  
  
    1. No Gerenciador do IIS, clique com o botão direito do mouse no **site padrão** e selecione **Adicionar um aplicativo**.  
  
    2. Para o **alias**, digite `WebRoutingIntegration` .  
  
    3. Para o **caminho físico**, selecione a pasta de serviço dentro do projeto.  
  
    4. Pressione **OK**.  
  
4. Inicie o aplicativo clicando com o botão direito do mouse no aplicativo Web e selecionando **gerenciar aplicativo** e, em seguida, **procurar**.  
  
5. Na barra de endereços, adicione `movies` à URL, para que seja leituras `http://localhost:[port]/movies` e pressione Enter.  
  
     O feed de filmes aparece no navegador.  
  
6. Na barra de endereços, adicione `channels` à URL, para que seja leituras `http://localhost:[port]/channels` e pressione Enter.  
  
     O feed canais é exibido no navegador.  
  
7. Feche o navegador da Web, pressionando ALT + F4.  
  
 Este exemplo demonstra que a camada de hospedagem é capaz de compor com as classes no <xref:System.Web.Routing> namespace para rotear as solicitações de serviços hospedados via http.  
  
> [!NOTE]
> Você deve atualizar a versão padrão do pool de aplicativos para .NET Framework 4 se ela estiver definida para a versão 2.  
  
## <a name="see-also"></a>Consulte também

- [Hospedagem de AppFabric e persistência Exemplos](/previous-versions/appfabric/ff383418(v=azure.10))
