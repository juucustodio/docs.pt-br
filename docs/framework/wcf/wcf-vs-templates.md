---
description: 'Saiba mais sobre: modelos do WCF do Visual Studio'
title: Modelos do Visual Studio do WCF
ms.date: 03/30/2017
ms.assetid: 6a608575-3535-4190-89da-911e24c8374f
ms.openlocfilehash: 95d320b2a425ddef7e48f915c8f66d759702ccce
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99676359"
---
# <a name="wcf-visual-studio-templates"></a>Modelos do Visual Studio do WCF

Os modelos do Windows Communication Foundation (WCF) do Visual Studio são modelos de projeto e item predefinidos que você pode usar no Visual Studio para criar rapidamente serviços WCF e aplicativos adjacentes.  
  
## <a name="using-the-wcf-templates"></a>Usando os modelos do WCF  

 Os modelos do WCF Visual Studio fornecem uma estrutura de classe básica para o desenvolvimento de serviços. Especificamente, esses modelos fornecem as definições básicas para contrato de serviço, contrato de dados, implementação de serviço e configuração. Você pode usar esses modelos para criar um serviço simples com interação mínima de código, bem como um bloco de construção para serviços mais avançados.  
  
### <a name="wcf-service-library-project-template"></a>Modelo de projeto da biblioteca de serviços WCF  

 O modelo de projeto da biblioteca de serviços WCF está disponível na caixa de diálogo novo projeto em **Visual C# \WCF** e **Visual Basic\WCF**.  
  
 Quando você cria um novo projeto usando o modelo de **serviço do WCF** , o novo projeto inclui automaticamente os três arquivos a seguir:  
  
- Arquivo de contrato de serviço (IService1.cs ou IService1. vb). O arquivo de contrato de serviço é uma interface que tem atributos de serviço WCF aplicados. Esse arquivo fornece uma definição de um serviço simples para mostrar como definir seus serviços e inclui operações baseadas em parâmetros e um exemplo de contrato de dados simples. Esse é o arquivo padrão exibido no editor de código após a criação de um projeto de serviço WCF.  
  
- Arquivo de implementação de serviço (Service1.cs ou Service1. vb). O arquivo de implementação de serviço implementa o contrato definido no arquivo de contrato de serviço.  
  
- Arquivo de configuração de aplicativo (App.config). O arquivo de configuração fornece os elementos básicos de um modelo de serviço WCF com uma associação HTTP segura. Ele também inclui um ponto de extremidade para o serviço e habilita a troca de metadados.  
  
> [!NOTE]
> O Visual Studio é configurado para reconhecer o arquivo de App.config como o arquivo de configuração do projeto quando ele é executado usando o [host de serviço do WCF (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md), que é a configuração padrão. Se você hospedar a biblioteca de serviços em um executável, precisará mover o código de configuração para o arquivo de configuração do executável, pois os arquivos de configuração para DLLs não são válidos.  
  
### <a name="wcf-service-application-template"></a>Modelo de aplicativo de serviço WCF  

 O modelo de aplicativo de serviço WCF está disponível na caixa de diálogo novo projeto em **Visual C# \WCF** e **Visual Basic\WCF**.  
  
 Quando você cria um novo projeto usando o modelo de **serviço de aplicativo Web WCF** , o projeto inclui os quatro arquivos a seguir:  
  
- Arquivo de host de serviço (Service1. svc).  
  
- Arquivo de contrato de serviço (IService1.cs ou IService1. vb).  
  
- Arquivo de implementação de serviço (Service1.svc.cs ou Service1. svc. vb).  
  
- Arquivo de configuração da Web (Web.config).  
  
 O modelo cria automaticamente um site (para ser implantado em um diretório virtual) e hospeda um serviço nele.  
  
### <a name="wcf-web-site-template"></a>Modelo de site da Web do WCF  

 O modelo site da Web do WCF está disponível na caixa de diálogo novo projeto em **Visual C# \Servidor Site\WCF Service** e **Visual Basic\Web Site\WCF Service**. Isso cria os mesmos arquivos que o modelo de aplicativo de serviço WCF, mas os organiza como se fosse um site ASP.NET. As pastas App_Code e App_Data são criadas.  
  
### <a name="wcf-service-item-template"></a>Modelo de item de serviço do WCF  

 O modelo de item de serviço do WCF é um modelo personalizado que fornece uma maneira rápida de adicionar serviços WCF aos seus projetos existentes do Visual Studio.  
  
 Para usar este modelo, vá para o painel de **Gerenciador de soluções** , clique com o botão direito do mouse no nome do projeto, aponte para **Adicionar** e clique em **novo item** para iniciar a caixa de diálogo **Adicionar novo item** .  
  
 A interface de serviço e os arquivos de implementação são colocados na pasta raiz do projeto.  
  
 O modelo tenta mesclar a seção de configuração do novo serviço para o arquivo de configuração existente, se eles forem tipos compatíveis.  
  
 Um arquivo de host de serviço (Service1. svc) também será criado se o projeto existente for um projeto Web.  
  
### <a name="wcf-wf-service-project-and-item-template"></a>Modelo de item e projeto de serviço WCF WF.  

 Esses modelos criam serviços WCF que hospedam um serviço de fluxo de trabalho, que é um fluxo de trabalho que pode ser acessado como um serviço Web. Existem modelos separados para modelos de programação XAML ou imperativos. Usando os modelos, você pode criar um fluxo de trabalho Sequencial ou de máquina de estado. Para obter mais informações sobre esses tipos de fluxo de trabalho, consulte [como: criar um fluxo de trabalho](../windows-workflow-foundation/how-to-create-a-workflow.md). Para obter mais informações sobre como criar projetos de fluxo de trabalho, consulte [criando projetos de fluxo de trabalho herdados](/visualstudio/workflow-designer/developing-applications-with-the-workflow-designer).  
  
 O Visual Studio designer é mais responsivo quando os fluxos de trabalho do tipo XOML são usados em vez de códigos baseados em código. Fluxo de trabalho de XOML é o tipo de fluxo de trabalho padrão a ser criado.  
  
### <a name="wcf-syndication-service-library-template"></a>Modelo de biblioteca de serviço de distribuição do WCF  

 Este modelo permite que você exponha seu feed no formato RSS ou ATOM como um serviço WCF. Para obter mais informações, consulte [agregação do WCF](./feature-details/wcf-syndication.md).  
  
#### <a name="changing-the-address-of-the-feed"></a>Alterando o endereço do feed  

 O modelo de distribuição usa o Internet Explorer durante a execução. Ao clicar com o botão direito do mouse em seu projeto no **Gerenciador de soluções** no Visual Studio, selecione **Propriedades** e, em seguida, selecione a guia **depurar** e você poderá ver o endereço padrão do modelo. O Internet Explorer tenta abrir o feed neste endereço.  
  
 Se você alterar o endereço do feed, também deverá alterar o endereço na guia **depurar** . Se você não fizer isso, o Internet Explorer tentará abrir o feed no endereço padrão e falhará.  
  
### <a name="ajax-enabled-wcf-service-item-template"></a>Modelo de item de serviço WCF habilitado para AJAX  

 Esse modelo expõe um controle AJAX como um serviço WCF. Para obter mais informações sobre controles AJAX, consulte a [documentação do controle Ajax](/aspnet/ajax/).  
  
### <a name="silverlight-enabled-wcf-service-item-template"></a>Modelo de item de serviço WCF habilitado para Silverlight  

 Este modelo cria um serviço Web que fornece dados para um cliente Silverlight ou front-end. O modelo pode ser adicionado a um site da Web ou a um projeto de aplicativo Web para criar um serviço WCF, que inclui o código de serviço e a configuração que dão suporte à comunicação com um cliente do Silverlight. Você pode usar **Adicionar referência de serviço** para adicionar um proxy de cliente do serviço ao cliente e trocar dados entre o cliente Silverlight e o serviço WCF habilitado para Silverlight.  
  
 Para acessar esse modelo, clique com o botão direito do mouse em um site da Web ou em um projeto de aplicativo Web no **Gerenciador de soluções**, clique em **Adicionar um novo item** e clique em **serviço WCF habilitado para Silverlight**.  
  
> [!NOTE]
> O serviço WCF habilitado para Silverlight expõe um `basicHttpBinding` ponto de extremidade sem habilitar nenhuma configuração de segurança. Portanto, as informações sobre o serviço podem ser obtidas por todos os clientes que se conectam a esse serviço. As mensagens trocadas entre o serviço e o cliente também não são assinadas ou criptografadas. Para proteger o ponto de extremidade corretamente, você deve usar a autenticação ASP.NET, HTTPS ou outros mecanismos.  
  
## <a name="see-also"></a>Consulte também

- [Host de serviço do WCF (WcfSvcHost.exe)](wcf-service-host-wcfsvchost-exe.md)
- [Cliente de Teste do WCF (WcfTestClient.exe)](wcf-test-client-wcftestclient-exe.md)
