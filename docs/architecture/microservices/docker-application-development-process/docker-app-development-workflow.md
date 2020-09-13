---
title: Fluxo de trabalho de desenvolvimento para aplicativos do Docker
description: Entenda os detalhes do fluxo de trabalho para o desenvolvimento de aplicativos baseados no Docker. Comece o passo a passo e obtenha alguns detalhes para otimizar Dockerfiles e concluir com o fluxo de trabalho simplificado disponível ao usar o Visual Studio.
ms.date: 01/30/2020
ms.openlocfilehash: 98dc931e10d5e1a3265ebd6f4e1919a6416e9b27
ms.sourcegitcommit: 6d4ee46871deb9ea1e45bb5f3784474e240bbc26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90022929"
---
# <a name="development-workflow-for-docker-apps"></a>Fluxo de trabalho de desenvolvimento para aplicativos do Docker

O ciclo de vida de desenvolvimento de aplicativo começa em seu computador, como desenvolvedor, onde você pode codificar o aplicativo usando sua linguagem preferida e testá-lo localmente. Com esse fluxo de trabalho, não importa a linguagem, a estrutura e a plataforma escolhidas, você está sempre desenvolvendo e testando contêineres do Docker, mas localmente.

Cada contêiner (uma instância de uma imagem do Docker) inclui os seguintes componentes:

- Uma seleção de sistema operacional, por exemplo, uma distribuição do Linux, o Windows Nano Server ou o Windows Server Core.

- Arquivos adicionados durante o desenvolvimento, por exemplo, os binários e o código-fonte do aplicativo.

- Informações de configuração, como configurações de ambiente e dependências.

## <a name="workflow-for-developing-docker-container-based-applications"></a>Fluxo de trabalho para o desenvolvimento de aplicativos baseados em contêiner do Docker

Esta seção descreve o fluxo de trabalho de desenvolvimento do *loop interno* de aplicativos baseados em contêiner do Docker. O fluxo de trabalho de loop interno significa que ele não está considerando o fluxo de trabalho de DevOps mais amplo, que pode incluir até a implantação de produção e só se concentra na tarefa de desenvolvimento feita no computador do desenvolvedor. As etapas iniciais para configurar o ambiente não são incluídas, pois elas são executadas apenas uma vez.

Um aplicativo é composto de seus próprios serviços e de bibliotecas adicionais (dependências). A figura 5-1 a seguir ilustra as etapas básicas que são normalmente realizadas para criar um aplicativo do Docker.

:::image type="complex" source="./media/docker-app-development-workflow/life-cycle-containerized-apps-docker-cli.png" alt-text="Diagrama mostrando as 7 etapas necessárias para criar um aplicativo em contêineres.":::
O processo de desenvolvimento para aplicativos Docker: 1-codificar seu aplicativo, 2-gravar Dockerfile/s, 3-criar imagens definidas em Dockerfile/s, 4-(opcional) compor serviços no arquivo Docker-Compose. yml, 5-executar o contêiner ou o aplicativo Docker-Compose, 6-testar seu aplicativo ou seus microserviços, 7-enviar para o repositório e repetir
:::image-end:::

**Figura 5-1.** Fluxo de trabalho passo a passo para o desenvolvimento de aplicativos do Docker em contêineres

Nesta seção, todo esse processo é detalhado e cada etapa principal é explicada com base em um ambiente do Visual Studio.

Ao usar uma abordagem de desenvolvimento de editor/CLI (por exemplo, o Visual Studio Code com a CLI do Docker no macOS ou no Windows), você precisará conhecer cada etapa e, na maioria das vezes, com mais detalhes do que ao usar o Visual Studio. Para obter mais informações sobre como trabalhar em um ambiente de CLI, confira o livro eletrônico [Containerized Docker Application lifecycle with Microsoft Platforms and Tools](https://aka.ms/dockerlifecycleebook/) (Ciclo de vida do aplicativo do Docker em contêineres com ferramentas e plataformas da Microsoft).

Quando você está usando o Visual Studio 2019, muitas dessas etapas são tratadas para você, o que melhora drasticamente a sua produtividade. Isso é especialmente verdadeiro quando você está usando o Visual Studio 2019 e direcionando aplicativos de vários contêineres. Por exemplo, com apenas um clique do mouse, o Visual Studio adiciona o `Dockerfile` `docker-compose.yml` arquivo e aos seus projetos com a configuração do seu aplicativo. Ao executar o aplicativo no Visual Studio, ele cria a imagem do Docker e executa o aplicativo de vários contêineres diretamente no Docker; e até mesmo permite que você depure vários contêineres de uma só vez. Esses recursos vão acelerar sua velocidade de desenvolvimento.

No entanto, apenas porque o Visual Studio automatiza essas etapas não significa que você não precisa saber o que está acontecendo nos bastidores com o Docker. Portanto, as diretrizes a seguir detalham cada etapa.

![Imagem da etapa 1.](./media/docker-app-development-workflow/step-1-code-your-app.png)

## <a name="step-1-start-coding-and-create-your-initial-application-or-service-baseline"></a>Etapa 1. Iniciar a codificação e a criação do aplicativo inicial ou da linha de base do serviço

O desenvolvimento de um aplicativo do Docker é semelhante à forma como você desenvolve um aplicativo sem Docker. A diferença é que, durante o desenvolvimento para o Docker, você está implantando e testando o aplicativo ou os serviços executando-os em contêineres do Docker em seu ambiente local (seja em uma VM do Linux configurada pelo Docker ou diretamente no Windows quando está usando contêineres do Windows).

### <a name="set-up-your-local-environment-with-visual-studio"></a>Configurar seu ambiente local com o Visual Studio

Para começar, instale o [Docker CE (Community Edition)](https://docs.docker.com/docker-for-windows/) para Windows, conforme explicado nas instruções a seguir:

[Introdução ao Docker CE for Windows](https://docs.docker.com/docker-for-windows/)

Além disso, você precisa do Visual Studio 2019 versão 16,4 ou posterior, com a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** instalada, conforme mostrado na Figura 5-2.

![Captura de tela da seleção de desenvolvimento de plataforma cruzada do .NET Core.](./media/docker-app-development-workflow/dotnet-core-cross-platform-development.png)

**Figura 5-2**. Selecionando a carga de trabalho de **desenvolvimento de plataforma cruzada do .NET Core** durante a instalação do Visual Studio 2019

Você pode iniciar a codificação do aplicativo no .NET simples (normalmente no .NET Core, se estiver planejando usar contêineres) mesmo antes de habilitar o Docker no aplicativo e antes da implantação e dos testes no Docker. No entanto, é recomendável que você comece a trabalhar no Docker assim que possível, porque que esse será o ambiente real e os problemas poderão ser descobertos o mais rápido possível. Isso é recomendável porque o Visual Studio facilita tanto o trabalho com o Docker parecendo, até mesmo, transparente — o melhor exemplo ao depurar aplicativos de vários contêineres do Visual Studio.

### <a name="additional-resources"></a>Recursos adicionais

- **Introdução ao Docker CE for Windows** \
  <https://docs.docker.com/docker-for-windows/>

- **Visual Studio 2019** \
  [https://visualstudio.microsoft.com/downloads/](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=inline+link&utm_content=download+vs2019)

![Imagem da etapa 2.](./media/docker-app-development-workflow/step-2-write-dockerfile.png)

## <a name="step-2-create-a-dockerfile-related-to-an-existing-net-base-image"></a>Etapa 2. Criar um Dockerfile relacionado a uma imagem base existente do .NET

Você precisa de um Dockerfile para cada imagem personalizada que você deseja criar. Você também precisará de um Dockerfile para cada contêiner a ser implantado automaticamente, por meio do Visual Studio, ou implantado manualmente, usando a CLI do Docker (comandos docker run e docker-compose). Se seu aplicativo contém um único serviço personalizado, é necessário um único Dockerfile. Se seu aplicativo contém vários serviços (como em uma arquitetura de microsserviços), é necessário um Dockerfile para cada serviço.

O Dockerfile é colocado na pasta raiz do seu aplicativo ou serviço. Ele contém os comandos que indicam ao Docker como configurar e executar seu aplicativo ou serviço em um contêiner. Você pode criar manualmente um Dockerfile por meio de código e adicioná-lo ao seu projeto junto com as dependências do .NET.

Com o Visual Studio e suas ferramentas para Docker, esta tarefa requer apenas alguns cliques do mouse. Quando você cria um novo projeto no Visual Studio 2019, há uma opção chamada **habilitar suporte do Docker**, como mostra a Figura 5-3.

![Captura de tela mostrando a caixa de seleção Habilitar suporte ao Docker.](./media/docker-app-development-workflow/enable-docker-support-check-box.png)

**Figura 5-3**. Habilitando o suporte do Docker ao criar um novo projeto de ASP.NET Core no Visual Studio 2019

Você também pode habilitar o suporte do Docker em um projeto de aplicativo Web ASP.NET Core existente clicando com o botão direito do mouse no projeto em **Gerenciador de soluções** e selecionando **Adicionar**  >  **suporte ao Docker...**, conforme mostrado na Figura 5-4.

![Captura de tela mostrando a opção de suporte do Docker no menu Adicionar.](./media/docker-app-development-workflow/add-docker-support-option.png)

**Figura 5-4**. Habilitando o suporte do Docker em um projeto existente do Visual Studio 2019

Essa ação adiciona um *Dockerfile* ao projeto com a configuração necessária e só está disponível em projetos ASP.NET Core.

De maneira semelhante, o Visual Studio também pode adicionar um `docker-compose.yml` arquivo para a solução inteira com a opção **Adicionar > contêiner suporte ao orquestrador...**. Na etapa 4, exploraremos essa opção mais detalhadamente.

### <a name="using-an-existing-official-net-docker-image"></a>Usando uma imagem do Docker do .NET oficial existente

Geralmente, você cria uma imagem personalizada para o contêiner usando uma imagem base que você pode obter de um repositório oficial, como o Registro do [Docker Hub](https://hub.docker.com/). É exatamente isso o que acontece nos bastidores quando você habilita o suporte do Docker no Visual Studio. O Dockerfile usará uma imagem `dotnet/core/aspnet` existente.

Anteriormente, explicamos quais imagens do Docker e quais repositórios você poderia usar, dependendo da estrutura e do sistema operacional que você escolheu. Por exemplo, se você quiser usar o ASP.NET Core (Linux ou Windows), a imagem a ser usada será `mcr.microsoft.com/dotnet/core/aspnet:3.1`. Assim, basta especificar qual imagem base do Docker será usada para o seu contêiner. Você pode fazer isso adicionando `FROM mcr.microsoft.com/dotnet/core/aspnet:3.1` ao seu Dockerfile. Isso será realizado automaticamente pelo Visual Studio, mas se você precisar atualizar a versão, será esse valor que você atualizará.

O uso de um repositório de imagem oficial do .NET do Hub do Docker com um número de versão garante que os mesmos recursos de linguagem estejam disponíveis em todos os computadores (incluindo desenvolvimento, teste e produção).

O exemplo a seguir mostra um Dockerfile de exemplo para um contêiner do ASP.NET Core.

```Dockerfile
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1
ARG source
WORKDIR /app
EXPOSE 80
COPY ${source:-obj/Docker/publish} .
ENTRYPOINT ["dotnet", " MySingleContainerWebApp.dll "]
```

Nesse caso, a imagem é baseada na versão 3,1 do oficial ASP.NET Core imagem do Docker (vários arcos para Linux e Windows). Essa é a configuração `FROM mcr.microsoft.com/dotnet/core/aspnet:3.1`. (Para obter mais informações sobre essa imagem base, consulte a página [imagem do Docker do .NET Core](https://hub.docker.com/_/microsoft-dotnet-core/) .) No Dockerfile, você também precisa instruir o Docker para escutar na porta TCP que será usada no tempo de execução (nesse caso, a porta 80, conforme configurado com a configuração de exposição).

Você pode especificar mais definições de configurações no Dockerfile, dependendo da linguagem e da estrutura usadas. Por exemplo, a linha ENTRYPOINT com `["dotnet", "MySingleContainerWebApp.dll"]` diz ao Docker para executar um aplicativo do .NET Core. Se você estiver usando o SDK e a CLI do .NET Core (CLI do dotnet) para compilar e executar o aplicativo do .NET, essa configuração será diferente. O essencial é que a linha ENTRYPOINT e outras configurações serão diferentes dependendo da linguagem e da plataforma que você escolher para seu aplicativo.

### <a name="additional-resources"></a>Recursos adicionais

- **Criando imagens do Docker para aplicativos .NET Core** \
  [https://docs.microsoft.com/dotnet/core/docker/building-net-docker-images](/aspnet/core/host-and-deploy/docker/building-net-docker-images)

- **Criar sua própria imagem**. Na documentação oficial do Docker.\
  <https://docs.docker.com/engine/tutorials/dockerimages/>

- **Manter-se atualizado com as imagens de contêiner do .NET** \
  <https://devblogs.microsoft.com/dotnet/staying-up-to-date-with-net-container-images/>

- **Usando o .NET e o Docker juntos – atualização do DockerCon 2018** \
  <https://devblogs.microsoft.com/dotnet/using-net-and-docker-together-dockercon-2018-update/>

### <a name="using-multi-arch-image-repositories"></a>Usando repositórios de imagens para várias arquiteturas

Um único repositório pode conter variantes de plataforma, como uma imagem do Linux e uma imagem do Windows. Esse recurso permite que fornecedores, como a Microsoft (criadores de imagem base), criem um único repositório para abranger várias plataformas (ou seja, Linux e Windows). Por exemplo, o repositório [dotnet/core](https://hub.docker.com/_/microsoft-dotnet-core/), disponível no registro do Hub do Docker, é compatível com Linux e Windows Nano Server usando o mesmo nome de repositório.

Ao especificar uma marcação, você direciona a uma plataforma que é explícita, como nos seguintes casos:

- `mcr.microsoft.com/dotnet/core/aspnet:3.1-buster-slim` \
  Destinos: somente em tempo de execução do .NET Core 3,1 no Linux

- `mcr.microsoft.com/dotnet/core/aspnet:3.1-nanoserver-1909` \
  Destinos: somente em tempo de execução do .NET Core 3,1 no Windows nano Server

Mas, se você especificar o mesmo nome de imagem, mesmo com a mesma marca, as imagens para várias arquiteturas (como a imagem `aspnet`) usarão a versão do Linux ou do Windows, dependendo do sistema operacional do host do Docker em que você esteja implantando, conforme mostrado no exemplo a seguir:

- `mcr.microsoft.com/dotnet/core/aspnet:3.1` \
  Vários arcos: tempo de execução do .NET Core 3,1 somente no Linux ou Windows nano Server, dependendo do sistema operacional do host do Docker

Dessa forma, ao efetuar pull de uma imagem de um host do Windows, será efetuado o pull da variante do Windows e, ao efetuar pull do mesmo nome de imagem de um host do Linux, será efetuado pull da variante do Linux.

### <a name="multi-stage-builds-in-dockerfile"></a>Builds de vários estágios no Dockerfile

O Dockerfile é semelhante a um script em lotes. Como o que você faria se tivesse que configurar o computador da linha de comando.

Ele começa com uma imagem base que define o contexto inicial, como o sistema de arquivos de inicialização, que se baseia no sistema operacional do host. Não é um sistema operacional, mas você pode considerá-lo como "o sistema operacional dentro do contêiner.

A execução de cada linha de comando cria uma camada no sistema de arquivos com as alterações em relação à anterior, para que, quando combinadas, produzam o sistema de arquivos resultante.

Como cada nova camada é baseada na anterior e o tamanho da imagem resultante aumenta com cada comando, as imagens poderão ficar muito grandes se precisarem incluir, por exemplo, o SDK necessário para criar e publicar um aplicativo.

É nesse ponto que os builds de vários estágios (do Docker 17.05 e superior) entram em cena para fazer a mágica.

A ideia central é que você pode separar o processo de execução do Dockerfile em estágios, em que um estágio é uma imagem inicial seguida por um ou mais comandos, e o último estágio determina o tamanho da imagem final.

Resumindo, os builds de vários estágios permitem dividir a criação em "fases" diferentes e, em seguida, montar a imagem final usando somente os diretórios relevantes dos estágios intermediários. A estratégia geral para usar esse recurso é:

1. usar uma imagem base do SDK (não importa quão grande), com todos os componentes necessários para criar e publicar o aplicativo em uma pasta e, em seguida,

2. usar uma imagem base pequena, somente em runtime e copiar a pasta de publicação do estágio anterior para produzir uma pequena imagem final.

Provavelmente a melhor maneira de entender os vários estágios é percorrer um Dockerfile detalhadamente, linha por linha, então, vamos começar com o Dockerfile inicial criado pelo Visual Studio ao adicionar o suporte ao Docker a um projeto e entraremos em algumas otimizações mais tarde.

O Dockerfile inicial pode ser como este:

```Dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
 6  WORKDIR /src
 7  COPY src/Services/Catalog/Catalog.API/Catalog.API.csproj …
 8  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.AspNetCore.HealthChecks …
 9  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions.HealthChecks …
10  COPY src/BuildingBlocks/EventBus/IntegrationEventLogEF/ …
11  COPY src/BuildingBlocks/EventBus/EventBus/EventBus.csproj …
12  COPY src/BuildingBlocks/EventBus/EventBusRabbitMQ/EventBusRabbitMQ.csproj …
13  COPY src/BuildingBlocks/EventBus/EventBusServiceBus/EventBusServiceBus.csproj …
14  COPY src/BuildingBlocks/WebHostCustomization/WebHost.Customization …
15  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
16  COPY src/BuildingBlocks/HealthChecks/src/Microsoft.Extensions …
17  RUN dotnet restore src/Services/Catalog/Catalog.API/Catalog.API.csproj
18  COPY . .
19  WORKDIR /src/src/Services/Catalog/Catalog.API
20  RUN dotnet build Catalog.API.csproj -c Release -o /app
21
22  FROM build AS publish
23  RUN dotnet publish Catalog.API.csproj -c Release -o /app
24
25  FROM base AS final
26  WORKDIR /app
27  COPY --from=publish /app .
28  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

E estes são os detalhes, linha por linha:

- **#1 de linha:** Inicie um estágio com uma imagem base somente de tempo de execução "pequeno", chame-a **base** para referência.

- **#2 de linha:** Crie o diretório **/app** na imagem.

- **#3 de linha:** Expor a porta **80**.

- **#5 de linha:** Comece um novo estágio com a imagem "grande" para criação/publicação. Chame-o **Build** para referência.

- **#6 de linha:** Crie o diretório **/src** na imagem.

- **#7 de linha:** Até a linha 16, copie os arquivos de projeto **. csproj** referenciados para poder restaurar pacotes posteriormente.

- **#17 de linha:** Restaure os pacotes para o projeto **Catalog. API** e os projetos referenciados.

- **#18 de linha:** Copie **toda a árvore de diretórios da solução** (exceto os arquivos/diretórios incluídos no arquivo **. dockerignore** ) para o diretório **/src** na imagem.

- **#19 de linha:** Altere a pasta atual para o projeto **Catalog. API** .

- **#20 de linha:** Compile o projeto (e outras dependências do projeto) e a saída para o diretório **/app** na imagem.

- **#22 de linha:** Iniciar um novo estágio continuando a partir da compilação. Chame-o de **publicar** para referência.

- **#23 de linha:** Publique o projeto (e as dependências) e a saída para o diretório **/app** na imagem.

- **#25 de linha:** Inicie um novo estágio continuando da **base** e chame-o **final**.

- **#26 de linha:** Altere o diretório atual para **/app**.

- **#27 de linha:** Copie o diretório **/app** do estágio **Publish** para o diretório atual.

- **#28 de linha:** Defina o comando a ser executado quando o contêiner for iniciado.

Agora vamos explorar algumas otimizações para melhorar o desempenho de todo o processo que, no caso do eShopOnContainers, significa cerca de 22 minutos ou mais para criar a solução completa em contêineres do Linux.

Você aproveitará o recurso de cache de camada do Docker, que é bastante simples: se a imagem base e os comandos forem iguais a outros já executados, ele poderá usar apenas a camada resultante sem precisar executar os comandos, economizando tempo.

Portanto, vamos nos concentrar no estágio **build**. As linhas 5 a 6 são basicamente as mesmas, mas as linhas 7 a 17 são diferentes para cada serviço do eShopOnContainers, portanto precisam ser executadas todas as vezes, no entanto, se você tiver alterado as linhas 7 a 16 para:

```Dockerfile
COPY . .
```

Ele seria igual para cada serviço, ele poderia copiar toda a solução e criar uma camada maior, mas:

1. o processo de cópia seria executado somente na primeira vez (e durante a recriação, se algum arquivo fosse alterado) e usaria o cache para todos os outros serviços e

2. Como a imagem maior ocorre em um estágio intermediário, ela não afeta o tamanho final da imagem.

A próxima otimização significativa envolve o comando `restore` executado na linha 17, que também é diferente para cada serviço do eShopOnContainers. Se você alterar essa linha para apenas:

```Dockerfile
RUN dotnet restore
```

Isso restauraria os pacotes de toda a solução, mas, novamente, isso seria feito apenas uma vez, em vez de 15 vezes com a estratégia atual.

No entanto, `dotnet restore` só será executado se houver um único arquivo de projeto ou de solução na pasta, portanto, isso é um pouco mais complicado e a maneira de resolvê-lo, sem entrar em muitos detalhes, é esta:

1. adicione as seguintes linhas ao **.dockerignore**:

   - `*.sln`, para ignorar todos os arquivos de solução na árvore da pasta principal

   - `!eShopOnContainers-ServicesAndWebApps.sln`, para incluir apenas esse arquivo de solução.

2. inclua o argumento `/ignoreprojectextensions:.dcproj` em `dotnet restore`, para que ele também ignore o projeto docker-compose e só restaure os pacotes da solução eShopOnContainers-ServicesAndWebApps.

Para a otimização final, acontece que a linha 20 é redundante e a linha 23 também compila o aplicativo e vem, naturalmente, logo após a linha 20, o que gera outro comando demorado.

O arquivo resultante é:

```Dockerfile
 1  FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS base
 2  WORKDIR /app
 3  EXPOSE 80
 4
 5  FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS publish
 6  WORKDIR /src
 7  COPY . .
 8  RUN dotnet restore /ignoreprojectextensions:.dcproj
 9  WORKDIR /src/src/Services/Catalog/Catalog.API
10  RUN dotnet publish Catalog.API.csproj -c Release -o /app
11
12  FROM base AS final
13  WORKDIR /app
14  COPY --from=publish /app
15  ENTRYPOINT ["dotnet", "Catalog.API.dll"]
```

### <a name="creating-your-base-image-from-scratch"></a>Criação da imagem base do zero

Você pode criar sua própria imagem base do Docker do zero. Esse cenário não é recomendável para um iniciante no Docker, mas se você desejar definir os bits específicos da sua própria imagem base, isso será possível.

### <a name="additional-resources"></a>Recursos adicionais

- **Imagens do .NET Core em vários arcos**. \
  <https://github.com/dotnet/announcements/issues/14>

- **Criar uma imagem base**. Documentação oficial do Docker.\
  <https://docs.docker.com/develop/develop-images/baseimages/>

![Imagem da etapa 3.](./media/docker-app-development-workflow/step-3-create-dockerfile-defined-images.png)

## <a name="step-3-create-your-custom-docker-images-and-embed-your-application-or-service-in-them"></a>Etapa 3. Criar imagens personalizadas do Docker e inserir seu aplicativo ou serviço nelas

Para cada serviço do seu aplicativo, você precisa criar uma imagem relacionada. Se seu aplicativo é composto de um único serviço ou aplicativo Web, você precisa apenas de uma única imagem.

Observe que as imagens do Docker são criadas automaticamente para você no Visual Studio. As etapas a seguir são necessárias apenas para o fluxo de trabalho de editor/CLI e são explicadas com a finalidade de esclarecer o que acontece nos bastidores.

Você, como desenvolvedor, precisa desenvolver e testar localmente até enviar um recurso concluído por push ou mudar para o sistema de controle do código-fonte (por exemplo, para o GitHub). Isso significa que você precisa criar as imagens do Docker e implantar contêineres em um host do Docker local (VM do Windows ou Linux) e executar, testar e depurar nesses contêineres locais.

Para criar uma imagem personalizada no seu ambiente local, usando a CLI do Docker e o Dockerfile, você pode usar o comando docker build, como na Figura 5-5.

![Captura de tela mostrando a saída do console do comando de Build do Docker.](./media/docker-app-development-workflow/run-docker-build-command.png)

**Figura 5-5**. Criando uma imagem personalizada do Docker

Opcionalmente, em vez de executar diretamente o comando docker build na pasta do projeto, você pode, primeiro, gerar uma pasta implantável com as bibliotecas e os binários do .NET necessários, executando `dotnet publish` e, em seguida, usar o comando `docker build`.

Isso criará uma imagem do Docker com o nome `cesardl/netcore-webapi-microservice-docker:first`. Nesse caso, :first é uma marcação que representa uma versão específica. Você poderá repetir esta etapa para cada imagem personalizada que tiver que criar para o seu aplicativo composto do Docker.

Quando um aplicativo é composto de vários contêineres (ou seja, ele é um aplicativo multicontêineres), você também pode usar o comando `docker-compose up --build` para compilar todas as imagens relacionadas com um único comando usando os metadados expostos nos arquivos docker-compose.yml relacionados.

Você pode encontrar as imagens existentes no seu repositório local usando o comando docker images, conforme mostrado na Figura 5-6.

![Saída do console do comando docker images, mostrando as imagens existentes.](./media/docker-app-development-workflow/view-existing-images-with-docker-images.png)

**Figura 5-6.** Exibição de imagens existentes usando o comando docker images

### <a name="creating-docker-images-with-visual-studio"></a>Criação de imagens do Docker com o Visual Studio

Ao usar o Visual Studio para criar um projeto com suporte ao Docker, você não cria explicitamente uma imagem. Em vez disso, a imagem é criada quando você pressiona **F5** (ou **Ctrl+F5**) para executar o aplicativo ou o serviço convertido para Docker. Esta etapa é automática no Visual Studio e você não verá ela ocorrer, mas é importante que você saiba o que está acontecendo nos bastidores.

![Imagem para a etapa 4 opcional.](./media/docker-app-development-workflow/step-4-define-services-docker-compose-yml.png)

## <a name="step-4-define-your-services-in-docker-composeyml-when-building-a-multi-container-docker-application"></a>Etapa 4. Definir os serviços no docker-compose.yml ao compilar um aplicativo de vários contêineres do Docker

O arquivo [docker-compose.yml](https://docs.docker.com/compose/compose-file/) permite que você defina um conjunto de serviços relacionados para que sejam implantados como um aplicativo composto com comandos de implantação. Ele também configura as relações de dependência e a configuração de tempo de execução.

Para usar um arquivo docker-compose.yml, você precisa criar o arquivo na pasta principal ou raiz da sua solução, com conteúdo semelhante ao do exemplo a seguir:

```yml
version: '3.4'

services:

  webmvc:
    image: eshop/web
    environment:
      - CatalogUrl=http://catalog-api
      - OrderingUrl=http://ordering-api
    ports:
      - "80:80"
    depends_on:
      - catalog-api
      - ordering-api

  catalog-api:
    image: eshop/catalog-api
    environment:
      - ConnectionString=Server=sqldata;Port=1433;Database=CatalogDB;…
    ports:
      - "81:80"
    depends_on:
      - sqldata

  ordering-api:
    image: eshop/ordering-api
    environment:
      - ConnectionString=Server=sqldata;Database=OrderingDb;…
    ports:
      - "82:80"
    extra_hosts:
      - "CESARDLBOOKVHD:10.0.75.1"
    depends_on:
      - sqldata

  sqldata:
    image: mcr.microsoft.com/mssql/server:latest
    environment:
      - SA_PASSWORD=Pass@word
      - ACCEPT_EULA=Y
    ports:
      - "5433:1433"
```

Esse arquivo docker-compose.yml é uma versão simplificada e mesclada. Ele contém dados de configuração estáticos para cada contêiner (como o nome da imagem personalizada), o que é sempre necessário, além das informações de configuração que poderão depender do ambiente de implantação, como a cadeia de conexão. Nas próximas seções, você aprenderá como dividir a configuração do docker-compose.yml em vários arquivos docker-compose e substituir valores dependendo do ambiente e do tipo de execução (depuração ou lançamento).

O arquivo docker-compose.yml de exemplo define quatro serviços: o serviço `webmvc` (um aplicativo Web), dois microsserviços (`ordering-api` e `basket-api`) e um contêiner de fonte de dados, `sqldata`, com base no SQL Server para Linux, em execução como um contêiner. Cada serviço será implantado como um contêiner, portanto, uma imagem do Docker é necessária para cada um.

O arquivo docker-compose.yml não apenas especifica quais contêineres estão sendo usados, mas também como eles são configurados individualmente. Por exemplo, a definição de contêiner `webmvc` no arquivo .yml:

- usa uma imagem `eshop/web:latest` predefinida. Entretanto, você também poderia definir a imagem para ser compilada como parte da execução do docker-compose, com uma configuração adicional baseada em uma seção build: no arquivo docker-compose.

- Inicializa duas variáveis de ambiente (CatalogUrl e OrderingUrl).

- Encaminha a porta 80, exposta no contêiner, para a porta 80 externa, no computador host.

- vincula o aplicativo Web ao catálogo e ao serviço de pedidos com a configuração depends_on. Isso faz com que o serviço aguarde até que esses serviços sejam iniciados.

Vamos abordar novamente o arquivo docker-compose.yml em uma seção posterior, ao explicar como implementar microsserviços e aplicativos de vários contêineres.

### <a name="working-with-docker-composeyml-in-visual-studio-2019"></a>Trabalhando com Docker-Compose. yml no Visual Studio 2019

Além de adicionar um Dockerfile a um projeto, como mencionamos anteriormente, o Visual Studio 2017 (da versão 15,8 em) pode adicionar suporte do Orchestrator para Docker Compose a uma solução.

Quando você adiciona o suporte ao orquestrador de contêineres, conforme mostrado na Figura 5-7, pela primeira vez, o Visual Studio cria o Dockerfile para o projeto e cria um projeto (seção de serviço) na solução com vários arquivos `docker-compose*.yml` globais e, em seguida, adiciona o projeto nesses arquivos. Depois, você pode abrir os arquivos docker-compose.yml e atualizá-los com mais recursos.

Você precisa repetir essa forma de operação para cada projeto que deseja incluir no arquivo docker-compose.yml.

No momento da redação deste artigo, o Visual Studio dá suporte aos orquestradores **Docker Compose** e **kubernetes/Helm** .

![Captura de tela mostrando a opção de suporte do orquestrador de contêiner no menu de contexto do projeto.](./media/docker-app-development-workflow/add-container-orchestrator-support-option.png)

**Figura 5-7**. Adicionando suporte ao Docker no Visual Studio 2019 clicando com o botão direito do mouse em um projeto ASP.NET Core

Depois de adicionar suporte ao orquestrador à solução no Visual Studio, você também verá um novo nó (no arquivo de projeto `docker-compose.dcproj`) no Gerenciador de Soluções contendo os arquivos docker-compose.yml adicionados, conforme mostrado na Figura 5-8.

![Captura de tela do nó Docker-Compose no Gerenciador de Soluções.](./media/docker-app-development-workflow/docker-compose-tree-node.png)

**Figura 5-8**. O nó da árvore **Docker-Compose** adicionado ao Visual Studio 2019 Gerenciador de soluções

Você pode implantar um aplicativo de vários contêineres com um único arquivo docker-compose.yml usando o comando `docker-compose up`. No entanto, o Visual Studio adiciona um grupo desses arquivos, para que você possa substituir os valores de acordo com o ambiente (desenvolvimento ou produção) e o tipo de execução (lançamento ou depuração). Essa funcionalidade será explicada nas seções posteriores.

![Imagem da etapa 5.](./media/docker-app-development-workflow/step-5-run-containers-compose-app.png)

## <a name="step-5-build-and-run-your-docker-application"></a>Etapa 5. Compilar e executar seu aplicativo do Docker

Se seu aplicativo tem apenas um contêiner, você pode executá-lo implantando-o no host do Docker (VM ou servidor físico). No entanto, se seu aplicativo contiver vários serviços, você poderá implantá-lo como um aplicativo composto, usando um único comando da CLI ( `docker-compose up)` ou com o Visual Studio, que usará esse comando nos bastidores. Vamos examinar as diferentes opções.

### <a name="option-a-running-a-single-container-application"></a>Opção A: executar um aplicativo de contêiner único

#### <a name="using-docker-cli"></a>Usando a CLI do Docker

Você pode executar um contêiner do Docker usando o comando `docker run`, conforme mostrado na Figura 5-9:

```console
docker run -t -d -p 80:5000 cesardl/netcore-webapi-microservice-docker:first
```

O comando acima criará uma instância de contêiner da imagem especificada, cada vez que for executado. Você pode usar o `--name` parâmetro para dar um nome ao contêiner e, em seguida, usar `docker start {name}` (ou usar a ID do contêiner ou o nome automático) para executar uma instância de contêiner existente.

![Captura de tela executando um contêiner do Docker usando o comando Docker Run.](./media/docker-app-development-workflow/use-docker-run-command.png)

**Figura 5-9**. Executando um contêiner do Docker usando o comando docker run

Nesse caso, o comando associa a porta interna 5000 do contêiner à porta 80 do computador host. Isso significa que o host está escutando na porta 80 e encaminhando para a porta 5000 no contêiner.

O hash mostrado é a ID do contêiner e também é atribuído um nome legível aleatório se a `--name` opção não for usada.

#### <a name="using-visual-studio"></a>Como usar o Visual Studio

Se ainda não adicionou o suporte ao orquestrador de contêineres, você também poderá executar um aplicativo de contêiner único no Visual Studio pressionando **Ctrl+F5** e usar **F5** para depurar o aplicativo dentro do contêiner. O contêiner é executado localmente usando o docker run.

### <a name="option-b-running-a-multi-container-application"></a>Opção B: executando um aplicativo de vários contêineres

Na maioria dos cenários empresariais, um aplicativo do Docker será ser composto de vários serviços, o que significa que você precisará executar um aplicativo de vários contêineres, conforme mostrado na Figura 5-10.

![VM com vários contêineres do Docker](./media/docker-app-development-workflow/vm-with-docker-containers-deployed.png)

**Figura 5-10**. VM com contêineres do Docker implantados

#### <a name="using-docker-cli"></a>Usando a CLI do Docker

Para executar um aplicativo de vários contêineres com a CLI do Docker, use o comando `docker-compose up`. Esse comando usa o arquivo **docker-compose.yml**, que existe no nível da solução, para implantar um aplicativo de vários contêineres. A figura 5-11 mostra os resultados da execução do comando no diretório principal da solução, que contém o arquivo docker-compose.yml.

![Exibição da tela ao executar o comando docker-compose up](./media/docker-app-development-workflow/results-docker-compose-up.png)

**Figura 5-11**. Resultados de exemplo ao executar o comando docker-compose up

Depois que o comando docker-compose up é executado, o aplicativo e os contêineres relacionados são implantados no host do Docker, como é mostrado na Figura 5-10.

#### <a name="using-visual-studio"></a>Como usar o Visual Studio

A execução de um aplicativo de vários contêineres usando o Visual Studio 2019 não pode ser mais simples. Basta pressionar **Ctrl+F5** para executar ou **F5** para depuração, como de costume, configurando o projeto **docker-compose** como o projeto de inicialização.  O Visual Studio lida com toda a instalação necessária, para que você possa criar pontos de interrupção como de costume e depurar o que finalmente se torna processos independentes em execução em "servidores remotos", com o depurador já anexado, assim como esse.

Conforme mencionado anteriormente, sempre que você adiciona suporte à solução do Docker a um projeto de uma solução, esse projeto é configurado no arquivo global (nível da solução) docker-compose.yml, o que permite que você execute ou depure toda a solução de uma só vez. O Visual Studio iniciará um contêiner para cada projeto que tenha suporte habilitado à solução do Docker e executará todas as etapas internas para você (dotnet publish, docker build, etc.).

Se você quiser dar uma olhada na parte chata do trabalho, confira o arquivo:

`{root solution folder}\obj\Docker\docker-compose.vs.debug.g.yml`

O ponto importante aqui é que, como mostrado na Figura 5-12, no Visual Studio 2019, há um comando **Docker** adicional para a ação de tecla F5. Essa opção permite que você execute ou depure um aplicativo de vários contêineres executando todos os contêineres que estão definidos nos arquivos docker-compose.yml no nível da solução. A capacidade de depurar soluções de vários contêineres significa que você poderá definir vários pontos de interrupção, cada ponto de interrupção em um projeto (contêiner) diferente e que, durante a depuração no Visual Studio, você vai parar nos pontos de interrupção definidos em diferentes projetos e em execução em diferentes contêineres.

![Captura de tela da barra de ferramentas de depuração que executa um projeto Docker-Compose.](./media/docker-app-development-workflow/debug-toolbar-docker-compose-project.png)

**Figura 5-12**. Executando aplicativos de vários contêineres no Visual Studio 2019

### <a name="additional-resources"></a>Recursos adicionais

- **Implantar um contêiner ASP.NET em um host remoto do Docker** \
  <https://docs.microsoft.com/azure/vs-azure-tools-docker-hosting-web-apps-in-docker>

### <a name="a-note-about-testing-and-deploying-with-orchestrators"></a>Uma observação sobre teste e implantação com orquestradores

Os comandos docker-compose up e docker run (ou executar e depurar os contêineres no Visual Studio) são adequados para contêineres de teste em seu ambiente de desenvolvimento. Mas você não deve usar essa abordagem para implantações de produção, com orquestradores de destino como [Kubernetes](https://kubernetes.io/) ou [Service Fabric](https://azure.microsoft.com/services/service-fabric/). Se você estiver usando o kubernetes, precisará usar [pods](https://kubernetes.io/docs/concepts/workloads/pods/pod/) para organizar contêineres e [Serviços](https://kubernetes.io/docs/concepts/services-networking/service/) para agrupá-los. Você também pode usar [implantações](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/) para organizar a criação e a modificação de pods.

![Imagem da etapa 6.](./media/docker-app-development-workflow/step-6-test-app-microservices.png)

## <a name="step-6-test-your-docker-application-using-your-local-docker-host"></a>Etapa 6. Testar seu aplicativo do Docker usando o host local do Docker

Esta etapa varia de acordo com o que seu aplicativo está fazendo. Em um aplicativo Web .NET Core simples implantado como um único contêiner ou serviço, você pode acessar o serviço abrindo um navegador no host do Docker e navegando até o site, conforme mostrado na Figura 5-13. (Se a configuração do Dockerfile mapear o contêiner para uma porta no host que seja diferente de 80, inclua a porta do host na URL).

![Captura de tela da resposta de localhost/API/Values.](./media/docker-app-development-workflow/test-docker-app-locally-localhost.png)

**Figura 5-13**. Exemplo de teste do seu aplicativo do Docker localmente usando localhost

Se o localhost não estiver apontando para o IP do host do Docker (por padrão, obrigatório ao usar o Docker CE), use o endereço IP da placa de rede do computador para navegar até o serviço.

Observe que a URL no navegador usa a porta 80 para o exemplo de contêiner específico que está sendo discutido. No entanto, internamente as solicitações estão sendo redirecionadas para a porta 5000, pois é assim que ele foi implantado com o comando docker run, conforme explicado em uma etapa anterior.

Você também pode testar o aplicativo usando o comando curl no terminal, conforme mostrado na Figura 5-14. Em uma instalação do Docker no Windows, o IP padrão do host do Docker é sempre 10.0.75.1, além do endereço IP real do computador.

![Saída do console de obter a http://10.0.75.1/API/values ondulação.](./media/docker-app-development-workflow/test-docker-app-locally-curl.png)

**Figura 5-14**. Exemplo de teste do seu aplicativo do Docker localmente usando curl

### <a name="testing-and-debugging-containers-with-visual-studio-2019"></a>Testando e Depurando contêineres com o Visual Studio 2019

Ao executar e depurar os contêineres com o Visual Studio 2019, você pode depurar o aplicativo .NET da mesma forma como faria ao executar sem contêineres.

### <a name="testing-and-debugging-without-visual-studio"></a>Testando e depurando sem o Visual Studio

Se você estiver desenvolvendo usando a abordagem do editor/CLI, os contêineres de depuração serão mais difíceis e você provavelmente desejará depurar gerando rastreamentos.

### <a name="additional-resources"></a>Recursos adicionais

- **Depurando aplicativos em um contêiner do Docker local** \
  [https://docs.microsoft.com/visualstudio/containers/edit-and-refresh](/visualstudio/containers/edit-and-refresh)

- **Steve Lasker. Crie, depure, implante aplicativos ASP.NET Core com o Docker.** Vídeo. \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T115>

## <a name="simplified-workflow-when-developing-containers-with-visual-studio"></a>Fluxo de trabalho simplificado ao desenvolver contêineres com o Visual Studio

Efetivamente, o fluxo de trabalho ao usar o Visual Studio é muito mais simples do que ao usar a abordagem de editor/CLI. A maioria das etapas necessárias pelo Docker, relacionadas ao Dockerfile e aos arquivos docker-compose.yml, são ocultas ou simplificadas pelo Visual Studio, conforme mostrado na Figura 5-15.

:::image type="complex" source="./media/docker-app-development-workflow/simplified-life-cycle-containerized-apps-docker-cli.png" alt-text="Diagrama mostrando as cinco etapas simplificadas necessárias para criar um aplicativo.":::
O processo de desenvolvimento para aplicativos Docker: 1-codificar seu aplicativo, 2-gravar Dockerfile/s, 3-criar imagens definidas em Dockerfile/s, 4-(opcional) compor serviços no arquivo Docker-Compose. yml, 5-executar o contêiner ou o aplicativo Docker-Compose, 6-testar seu aplicativo ou seus microserviços, 7-enviar para o repositório e repetir
:::image-end:::

**Figura 5-15**. Fluxo de trabalho simplificado ao desenvolver com o Visual Studio

Além disso, será necessário executar a etapa 2 (adicionar suporte do Docker aos seus projetos) apenas uma vez. Portanto, o fluxo de trabalho é semelhante às suas tarefas de desenvolvimento regulares, quando utiliza o .NET para qualquer outro desenvolvimento. É necessário saber o que está acontecendo nos bastidores (o processo de build da imagem, quais imagens base você está usando, a implantação de contêineres, etc.) e, às vezes, você também precisará editar o Dockerfile ou o arquivo docker-compose.yml para personalizar comportamentos. Mas a maior parte do trabalho é bastante simplificada com o uso do Visual Studio, o que o torna muito mais produtivo.

### <a name="additional-resources"></a>Recursos adicionais

- **Steve Lasker. Desenvolvimento do Docker do .NET com o Visual Studio (2017)** \
  <https://channel9.msdn.com/Events/Visual-Studio/Visual-Studio-2017-Launch/T111>

## <a name="using-powershell-commands-in-a-dockerfile-to-set-up-windows-containers"></a>Usando comandos do PowerShell em um DockerFile para configurar contêineres do Windows

Os [contêineres do Windows](https://docs.microsoft.com/virtualization/windowscontainers/about/index) permitem converter seus aplicativos existentes do Windows em imagens do Docker e implantá-los com as mesmas ferramentas que o resto do ecossistema do Docker. Para usar contêineres do Windows, você executa comandos do PowerShell no Dockerfile, conforme mostrado no exemplo a seguir:

```Dockerfile
FROM mcr.microsoft.com/windows/servercore
LABEL Description="IIS" Vendor="Microsoft" Version="10"
RUN powershell -Command Add-WindowsFeature Web-Server
CMD [ "ping", "localhost", "-t" ]
```

Nesse caso, estamos usando uma imagem base do Windows Server Core (a configuração FROM) e instalando IIS com um comando do PowerShell (a configuração RUN). Da mesma forma, você também pode usar comandos do PowerShell para configurar outros componentes, como ASP.NET 4.x, .NET 4.6 ou qualquer outro software do Windows. Por exemplo, o seguinte comando, em um Dockerfile, configura o ASP.NET 4.5:

```Dockerfile
RUN powershell add-windowsfeature web-asp-net45
```

### <a name="additional-resources"></a>Recursos adicionais

- **aspnet-docker/Dockerfile.** Comandos do PowerShell de exemplo a serem executados em Dockerfiles para incluir recursos do Windows.\
  <https://github.com/Microsoft/aspnet-docker/blob/master/4.7.1-windowsservercore-ltsc2016/runtime/Dockerfile>

>[!div class="step-by-step"]
>[Anterior](index.md) 
> [Avançar](../multi-container-microservice-net-applications/index.md)
