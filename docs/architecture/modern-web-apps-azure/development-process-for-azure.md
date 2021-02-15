---
title: Processo de desenvolvimento para o Azure
description: Projetar aplicativos Web modernos com o ASP.NET Core e o Azure | Processo de desenvolvimento para o Azure
author: ardalis
ms.author: wiwagn
ms.date: 12/01/2020
ms.openlocfilehash: 2706a4091565e6f3cb795acf031a238ae55a1068
ms.sourcegitcommit: 45c7148f2483db2501c1aa696ab6ed2ed8cb71b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2020
ms.locfileid: "96851621"
---
# <a name="development-process-for-azure"></a>Processo de desenvolvimento para o Azure

> _"Com a nuvem, pessoas e pequenas empresas podem estalar os dedos e configurar serviços de nível empresarial instantaneamente."_  
> _- Roy Stephan_

## <a name="vision"></a>Visão

> *Desenvolva aplicativos ASP.NET Core bem projetados como desejar, usando o Visual Studio ou a CLI do dotnet e o Visual Studio Code ou seu editor escolhido.*

## <a name="development-environment-for-aspnet-core-apps"></a>Ambiente de desenvolvimento para aplicativos ASP.NET Core

### <a name="development-tools-choices-ide-or-editor"></a>Opções de ferramentas de desenvolvimento: IDE ou editor

Seja qual for sua preferência, um IDE avançado e completo ou um editor leve e ágil, a Microsoft oferece as ferramentas que você pode usar para desenvolver aplicativos ASP.NET Core.

**Visual Studio 2019.** O Visual Studio 2019 é o melhor IDE para desenvolver aplicativos para ASP.NET Core. Ele oferece uma série de recursos que aumentam a produtividade do desenvolvedor. Você pode usá-lo para desenvolver o aplicativo e, em seguida, analisar seu desempenho e outras características. O depurador integrado permite pausar a execução de código e avançar e voltar pelo código imediatamente conforme ele está em execução. O executor de teste interno permite organizar seus testes e seus resultados e pode até mesmo executar testes de unidade ao vivo enquanto você está codificando. Usando Live Share, você pode colaborar em tempo real com outros desenvolvedores, compartilhando sua sessão de código diretamente pela rede. E quando estiver pronto, o Visual Studio incluirá tudo o que você precisa para publicar seu aplicativo no Azure ou onde quer que possa hospedá-lo.

[Baixar o Visual Studio 2019](https://aka.ms/vsdownload?utm_source=mscom&utm_campaign=msdocs)

**Visual Studio Code e dotnet CLI** (ferramentas de plataforma cruzada para Mac, Linux e Windows). Se preferir um editor leve e multiplataforma compatível com qualquer linguagem de desenvolvimento, use o Microsoft Visual Studio Code e a CLI do dotnet. Esses produtos fornecem uma experiência simples mas robusta que simplifica o fluxo de trabalho do desenvolvedor. Além disso, o Visual Studio Code é compatível com extensões para o C\# e ao desenvolvimento para a Web, fornecendo o IntelliSense e tarefas de atalho no editor.

[Baixar o SDK do .NET](https://dotnet.microsoft.com/download)

[Baixar o Visual Studio Code](https://code.visualstudio.com/download)

## <a name="development-workflow-for-azure-hosted-aspnet-core-apps"></a>Fluxo de trabalho de desenvolvimento para aplicativos ASP.NET Core hospedados no Azure

O ciclo de vida de desenvolvimento do aplicativo começa no computador de cada desenvolvedor, codificando o aplicativo com sua linguagem preferencial e testando-o localmente. Os desenvolvedores podem escolher seu sistema de controle do código-fonte preferencial e podem configurar a CI (integração contínua) e/ou a CD (implantação/entrega contínua) usando um servidor de build ou com base em recursos internos do Azure.

Para começar a desenvolver um aplicativo ASP.NET Core usando a CI/CD, use o Azure DevOps Services ou o próprio TFS (Team Foundation Server) de sua organização.

### <a name="initial-setup"></a>Instalação inicial

Para criar um pipeline de lançamento para seu aplicativo, você precisa ter o código do aplicativo no controle do código-fonte. Configure um repositório local e conecte-o a um repositório remoto em um projeto de equipe. Siga estas instruções:

- [Compartilhar o código com o GIT e o Visual Studio](/azure/devops/git/share-your-code-in-git-vs) ou

- [Compartilhar o código com o TFVC e o Visual Studio](/azure/devops/tfvc/share-your-code-in-tfvc-vs)

Crie um Serviço de Aplicativo do Azure no qual você implantará o aplicativo. Crie um aplicativo Web acessando a folha Serviços de Aplicativos no Portal do Azure. Clique em +Adicionar, selecione o modelo de Aplicativo Web, clique em Criar e forneça um nome e outros detalhes. O aplicativo Web estará acessível em {name}.azurewebsites.net.

![AzureWebApp](./media/image10-2.png)

**Figura 10-1.** Criando um novo Aplicativo Web do Serviço de Aplicativo do Azure no Portal do Azure.

O processo de build de CI executará um build automatizado sempre que o novo código for confirmado no repositório de controle do código-fonte do projeto. Esse processo fornece comentários imediatos que o código cria (e, idealmente, passa por testes automatizados) e pode potencialmente ser implantado. Esse build de CI produzirá um artefato de pacote de implantação da Web e o publicará para consumo pelo processo de CD.

[Definir o processo de build de CI](/azure/devops/pipelines/ecosystems/dotnet-core)

Lembre-se de habilitar a integração contínua para que o sistema coloque na fila um build sempre que alguém de sua equipe confirmar um novo código. Teste o build e verifique se ele está produzindo um pacote de implantação da Web como um de seus artefatos.

Quando um build for bem-sucedido, o processo de CD implantará os resultados do build de CI no aplicativo Web do Azure. Para configurar essa etapa, você cria e configura uma *versão*, que será implantada em seu serviço de Azure app.

[Implantar um aplicativo Web do Azure](/azure/devops/pipelines/targets/webapp)

Quando o pipeline de CI/CD estiver configurado, você poderá fazer atualizações facilmente em seu aplicativo Web e confirmá-las no controle do código-fonte para que elas sejam implantadas.

### <a name="workflow-for-developing-azure-hosted-aspnet-core-applications"></a>Fluxo de trabalho de desenvolvimento para aplicativos ASP.NET Core hospedados no Azure

Depois de configurar sua conta do Azure e o processo de CI/CD, o desenvolvimento de aplicativos ASP.NET Core hospedados no Azure é simples. A seguir estão as etapas básicas que você geralmente adota ao criar um aplicativo ASP.NET Core, hospedado no serviço Azure App como um aplicativo Web, como ilustrado na Figura 10-2.

![EndToEndDevDeployWorkflow](./media/image10-3.png)

**Figura 10-2.** Fluxo de trabalho passo a passo para a criação de aplicativos ASP.NET Core e sua hospedagem no Azure

#### <a name="step-1-local-dev-environment-inner-loop"></a>Etapa 1. Loop interno do ambiente de desenvolvimento local

O desenvolvimento de seu aplicativo ASP.NET Core para implantação no Azure não é diferente do desenvolvimento do aplicativo de outro modo. Use o ambiente de desenvolvimento local com o qual você está familiarizado, seja ele o Visual Studio 2019 ou a CLI do dotnet e o Visual Studio Code ou o editor preferido. Você pode codificar, executar e depurar as alterações, executar testes automatizados e fazer confirmações locais no controle do código-fonte até que esteja pronto para enviar por push as alterações ao repositório de controle do código-fonte compartilhado.

#### <a name="step-2-application-code-repository"></a>Etapa 2. Repositório de código do aplicativo

Sempre que estiver pronto para compartilhar o código com sua equipe, envie por push as alterações do repositório de origem local para o repositório de origem compartilhado de sua equipe. Se você estiver trabalhando em um branch personalizado, esta etapa geralmente envolverá a mesclagem do código em um branch compartilhado (talvez por meio de uma [solicitação de pull](/azure/devops/git/pull-requests)).

#### <a name="step-3-build-server-continuous-integration-build-test-package"></a>Etapa 3. Servidor de build: integração contínua. compilar, testar, agrupar

Um novo build é disparado no servidor de build sempre que uma nova confirmação é feita no repositório de códigos compartilhados do aplicativo. Como parte do processo de CI, esse build deve compilar o aplicativo por completo e executar testes automatizados para confirmar se tudo está funcionando conforme esperado. O resultado final do processo de CI deve ser uma versão empacotada do aplicativo Web, pronta para implantação.

#### <a name="step-4-build-server-continuous-delivery"></a>Etapa 4. Servidor de build: entrega contínua

Depois que um build for bem-sucedido, o processo de CD selecionará os artefatos de build produzidos. Esse processo incluirá um pacote de implantação da Web. O servidor de build implantará esse pacote no Serviço de Aplicativo do Azure, substituindo o serviço existente pelo recém-criado. Normalmente, esta etapa é direcionada a um ambiente de preparo, mas alguns aplicativos são implantados diretamente em produção por meio de um processo de CD.

#### <a name="step-5-azure-app-service-web-app"></a>Etapa 5. Aplicativo Web do Serviço de Aplicativo do Azure

Depois de implantado, o aplicativo ASP.NET Core é executado dentro do contexto de um Aplicativo Web do Serviço de Aplicativo do Azure. Esse Aplicativo Web pode ser monitorado e configurado em mais detalhes por meio do Portal do Azure.

#### <a name="step-6-production-monitoring-and-diagnostics"></a>Etapa 6. Monitoramento de produção e diagnóstico

Durante a execução do Aplicativo Web, você pode monitorar a integridade do aplicativo e coletar dados de diagnóstico e de comportamento do usuário. O Application Insights é incluído no Visual Studio e oferece instrumentação automática para aplicativos ASP.NET. Ele pode fornecer informações sobre uso, exceções, solicitações, desempenho e logs.

## <a name="references"></a>Referências

**Criar e implantar seu aplicativo ASP.NET Core no Azure**  
<https://docs.microsoft.com/azure/devops/build-release/apps/aspnet/build-aspnet-core>

>[!div class="step-by-step"]
>[Anterior](test-asp-net-core-mvc-apps.md) 
> [Avançar](azure-hosting-recommendations-for-asp-net-web-apps.md)
