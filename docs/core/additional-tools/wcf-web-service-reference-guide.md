---
title: Adicionar WCF Web Service Reference
description: Uma visão geral da ferramenta Microsoft WCF Web Service Reference Provider que adiciona funcionalidade a projetos do .NET Core e ASP.NET Core, semelhante à ferramenta Adicionar Referência de Serviço para projetos do .NET Framework.
author: dasetser
ms.date: 10/29/2019
ms.custom: mvc
ms.openlocfilehash: 1f7b1831a956553dbef26f58f4f257c2f3914ede
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400598"
---
# <a name="use-the-wcf-web-service-reference-provider-tool"></a>Usar a ferramenta WCF Web Service Reference Provider

Ao longo dos anos, muitos desenvolvedores do Visual Studio têm apreciado a produtividade que a ferramenta [**Adicionar Referência de Serviço**](/visualstudio/data-tools/how-to-add-update-or-remove-a-wcf-data-service-reference) fornecida quando seus projetos do .NET Framework precisam acessar serviços Web.  A ferramenta **WCF Web Service Reference** é uma extensão de serviço conectado do Visual Studio que fornece uma experiência semelhante à funcionalidade Adicionar Referência de Serviço para projetos do .NET Core e ASP.NET Core. Essa ferramenta recupera metadados de um serviço Web na solução atual, em um local de rede ou de um arquivo WSDL e gera um arquivo de fonte compatível com o .NET Core que contém o código de proxy de cliente do Windows Communication Foundation (WCF) que você pode usar para acessar esse serviço Web.

> [!IMPORTANT]
> Você só deve fazer referência a serviços de uma fonte confiável. A adição de referências de uma fonte não confiável pode comprometer a segurança.

## <a name="prerequisites"></a>Pré-requisitos

- [Visual Studio 2017 versão 15,5](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs) ou versões posteriores

## <a name="how-to-use-the-extension"></a>Como usar a extensão

> [!NOTE]
> A opção **WCF Web Service Reference** é aplicável a projetos criados com o uso dos seguintes modelos de projeto:
>
> - **Visual C#**  >  **.NET Core**
> - **Visual C#**  >  **.Net Standard**
> - **Visual C#**  >  **Web**  >  do **ASP.NET Core aplicativo Web**

Ao usar o modelo de projeto **Aplicativo Web ASP.NET Core** como um exemplo, este artigo o orienta na adição de uma referência de serviço WCF ao projeto:

1. No Gerenciador de Soluções, clique duas vezes no nó **Serviços Conectados** do projeto (para um projeto do .NET Core ou .NET Standard, essa opção está disponível quando você clica com o botão direito do mouse no nó **Dependências** do projeto no Gerenciador de Soluções).

    A página **Serviços Conectados** é exibida, conforme mostrado na imagem a seguir:

    ![Guia Serviços Conectados do Visual Studio para .NET Core](./media/wcf-web-service-reference-guide/wcfcs-ConnectedServicesPage.png)

2. Na página **Serviços Conectados** , clique em **Microsoft WCF Web Service Reference Provider**. Isso apresenta o assistente **Configurar a WCF Web Service Reference** :

    ![Guia Ponto de Extremidade do Serviço do Visual Studio para .NET Core](./media/wcf-web-service-reference-guide/wcfcs-ServiceEndpointPage.png)

3. Selecione um serviço.

    3a. Há várias opções de pesquisa de serviços disponíveis no assistente **Configurar a WCF Web Service Reference** :

     * Para pesquisar serviços definidos na solução atual, clique no botão **Descobrir**.
     * Para pesquisar serviços hospedados em um endereço especificado, insira uma URL de serviço na caixa **Endereço** e clique no botão **Ir**.
     * Para selecionar um arquivo WSDL que contenha as informações de metadados do serviço Web, clique no botão **Procurar**.

    3b. Selecione o serviço na lista de resultados da pesquisa na caixa **Serviços**. Se necessário, insira o namespace para o código gerado na caixa de texto **Namespace** correspondente.

    3c. Clique no botão **Avançar** para abrir as páginas **Opções de Tipo de Dados** e **Opções do Cliente**. Como alternativa, clique no botão **Concluir** para usar as opções padrão.

4. O formulário **Opções de Tipo de Dados** permite que você refine as definições de configuração de referência do serviço gerado:

    ![Guia Opções de tipo de dados do Visual Studio para .NET Core](./media/wcf-web-service-reference-guide/wcfcs-DataTypesPage.png)

    > [!NOTE]
    > A opção da caixa de seleção **Usar novamente os tipos em assemblies consultados** é útil quando os tipos de dados necessários para a geração de código da referência de serviço são definidos em um dos assemblies referenciados do seu projeto.  É importante reutilizar esses tipos de dados existentes para evitar problemas de conflito de tipo de tempo de compilação ou problemas de runtime.

    Pode haver um atraso enquanto as informações de tipo são carregadas, dependendo do número de dependências do projeto e de outros fatores de desempenho do sistema. O botão **Concluir** será desabilitado durante o carregamento, a menos que a caixa de seleção **Usar novamente os tipos em assemblies consultados** esteja desmarcada.

5. Clique em **Concluir** quando terminar.

Enquanto exibe o andamento, a ferramenta:

- Baixa metadados do serviço WCF.
- Gera o código de referência de serviço em um arquivo chamado *reference.cs* e o adiciona ao seu projeto no nó **Serviços Conectados**.
- Atualiza o arquivo de projeto (.csproj) com as referências de pacote NuGet necessárias para compilar e executar na plataforma de destino.

![Janela Progresso do Studio Visual](./media/wcf-web-service-reference-guide/wcfcs-ProgressWindow.png)

Quando esses processos forem concluídos, você poderá criar uma instância do tipo de cliente do WCF gerado e invocar as operações de serviço.

## <a name="see-also"></a>Confira também

- [Introdução aos aplicativos Windows Communication Foundation](../../framework/wcf/getting-started-tutorial.md)
- [Serviços de Windows Communication Foundation e WCF Data Services no Visual Studio](/visualstudio/data-tools/windows-communication-foundation-services-and-wcf-data-services-in-visual-studio)
- [Recursos com suporte do WCF no .NET Core](https://github.com/dotnet/wcf/blob/master/release-notes/SupportedFeatures-v2.1.0.md)

## <a name="feedback--questions"></a>Perguntas e comentários

Se você tiver algum comentário sobre o produto, denuncie-o na [comunidade de desenvolvedores](https://aka.ms/feedback/report?space=61) usando o [relatório uma ferramenta problemática](/visualstudio/ide/how-to-report-a-problem-with-visual-studio) .

## <a name="release-notes"></a>Notas de versão

- Consulte as [Notas de versão](https://github.com/dotnet/wcf/blob/master/release-notes/WCF-Web-Service-Reference-notes.md) para obter informações de versão atualizadas, incluindo problemas conhecidos.
