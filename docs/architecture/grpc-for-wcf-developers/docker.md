---
title: Docker-gRPC para desenvolvedores do WCF
description: Criando imagens do Docker para aplicativos ASP.NET Core gRPC
ms.date: 01/06/2021
ms.openlocfilehash: f59518a28b0a1dee75c792ba03bd4af826638502
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970083"
---
# <a name="create-docker-images"></a>Criar imagens do Docker

Esta seção aborda a criação de imagens do Docker para ASP.NET Core aplicativos gRPC, prontos para execução no Docker, kubernetes ou outros ambientes de contêiner. O aplicativo de exemplo usado, com um ASP.NET Core aplicativo Web MVC e um serviço gRPC, está disponível no repositório [dotnet-Architecture/gRPC-for-WCF-Developers](https://github.com/dotnet-architecture/grpc-for-wcf-developers/tree/master/KubernetesSample) no github.

## <a name="microsoft-base-images-for-aspnet-core-applications"></a>Imagens base da Microsoft para aplicativos ASP.NET Core

A Microsoft fornece uma variedade de imagens básicas para a criação e a execução de aplicativos .NET. Para criar uma imagem ASP.NET Core 5,0, você usa duas imagens base:

- Uma imagem do SDK para compilar e publicar o aplicativo.
- Uma imagem de tempo de execução para implantação.

| Imagem | Descrição |
| ----- | ----------- |
| [mcr.microsoft.com/dotnet/sdk](https://hub.docker.com/_/microsoft-dotnet-sdk/) | Para a criação de aplicativos com o `docker build` . Não deve ser usado na produção. |
| [mcr.microsoft.com/dotnet/aspnet](https://hub.docker.com/_/microsoft-dotnet-aspnet/) | Contém as dependências de tempo de execução e ASP.NET Core. Para produção. |

Para cada imagem, há quatro variantes com base em diferentes distribuições do Linux, diferenciadas por marcas.

| Marca (s) de imagem | Linux | Observações |
| --------- | ----- | ----- |
| 5,0-Buster-Slim, 5,0 | Debian 10 | A imagem padrão se nenhuma variante do sistema operacional for especificada. |
| 5,0 – Alpine Ski | Alpine 3,12 | As imagens da Alpine base são muito menores do que Debian ou Ubuntu. |
| 5,0 – focal| Ubuntu 20.04 | |

A imagem do Alpine base é de cerca de 100 MB, em comparação com 200 MB para as imagens Debian e Ubuntu. Alguns pacotes de software ou bibliotecas podem não estar disponíveis no gerenciamento de pacotes da Alpine Ski. Se você não tiver certeza de qual imagem usar, provavelmente deverá escolher o Debian padrão.

> [!IMPORTANT]
> Certifique-se de usar a mesma variante do Linux para a compilação e o tempo de execução. Os aplicativos criados e publicados em uma variante podem não funcionar em outro.

## <a name="create-a-docker-image"></a>Criar uma imagem do Docker

Uma imagem do Docker é definida por um *Dockerfile*. Esse *Dockerfile* é um arquivo de texto que contém todos os comandos necessários para compilar o aplicativo e instalar quaisquer dependências necessárias para compilar ou executar o aplicativo. O exemplo a seguir mostra a Dockerfile mais simples para um aplicativo ASP.NET Core 5,0:

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:5.0 as build

WORKDIR /src

COPY ./StockKube.sln .
COPY ./src/StockData/StockData.csproj ./src/StockData/
COPY ./src/StockWeb/StockWeb.csproj ./src/StockWeb/

RUN dotnet restore

COPY . .

RUN dotnet publish --no-restore -c Release -o /published src/StockData/StockData.csproj

FROM mcr.microsoft.com/dotnet/aspnet:5.0 as runtime

# Uncomment the line below if running with HTTPS
# ENV ASPNETCORE_URLS=https://+:443

WORKDIR /app

COPY --from=build /published .

ENTRYPOINT [ "dotnet", "StockData.dll" ]
```

O Dockerfile tem duas partes: a primeira usa a `sdk` imagem base para compilar e publicar o aplicativo; a segunda cria uma imagem de tempo de execução a partir da `aspnet` base. Isso ocorre porque a `sdk` imagem está em cerca de 900 MB, em comparação com cerca de 200 MB para a imagem de tempo de execução, e a maior parte de seu conteúdo é desnecessária no tempo de execução.

### <a name="the-build-steps"></a>As etapas de compilação

| Etapa | Descrição |
| ---- | ----------- |
| `FROM ...` | Declara a imagem base e atribui o `builder` alias. |
| `WORKDIR /src` | Cria o `/src` diretório e o define como o diretório de trabalho atual. |
| `COPY . .` | Copia tudo abaixo do diretório atual no host para o diretório atual na imagem. |
| `RUN dotnet restore` | Restaura todos os pacotes externos (ASP.NET Core estrutura 3,0 é pré-instalada com o SDK). |
| `RUN dotnet publish ...` | Compila e publica uma compilação de versão. Observe que o `--runtime` sinalizador não é necessário. |

### <a name="the-runtime-image-steps"></a>As etapas da imagem de tempo de execução

| Etapa | Descrição |
| ---- | ----------- |
| `FROM ...` | Declara uma nova imagem de base. |
| `WORKDIR /app` | Cria o `/app` diretório e o define como o diretório de trabalho atual. |
| `COPY --from=builder ...` | Copia o aplicativo publicado da imagem anterior, usando o `builder` alias da primeira `FROM` linha. |
| `ENTRYPOINT [ ... ]` | Define o comando a ser executado quando o contêiner é iniciado. O `dotnet` comando na imagem de tempo de execução só pode executar arquivos dll. |

### <a name="https-in-docker"></a>HTTPS no Docker

As imagens base da Microsoft para o Docker definem a `ASPNETCORE_URLS` variável de ambiente como `http://+:80` , o que significa que Kestrel é executado sem https nessa porta. Se você estiver usando HTTPS com um certificado personalizado (conforme descrito em [aplicativos gRPC hospedados internamente](self-hosted.md)), deverá substituir essa configuração. Defina a variável de ambiente na parte de criação da imagem de tempo de execução de seu Dockerfile.

```dockerfile
# Runtime image creation
FROM mcr.microsoft.com/dotnet/aspnet:5.0

ENV ASPNETCORE_URLS=https://+:443
```

### <a name="the-dockerignore-file"></a>O arquivo. dockerignore

Assim como `.gitignore` os arquivos que excluem determinados arquivos e diretórios do controle do código-fonte, o `.dockerignore` arquivo pode ser usado para excluir arquivos e diretórios de serem copiados para a imagem durante a compilação. Esse arquivo não apenas poupa tempo de cópia, mas também pode evitar alguns erros que surgem de ter o `obj` diretório do seu PC copiado para a imagem. No mínimo, você deve adicionar entradas para `bin` e `obj` ao seu `.dockerignore` arquivo.

```console
bin/
obj/
```

## <a name="build-the-image"></a>Criar a imagem

Para uma `StockKube.sln` solução que contém dois aplicativos diferentes `StockData` e `StockWeb` , é mais simples colocar o Dockerfile para cada um deles no diretório base. Nesse caso, para criar a imagem, use o comando a seguir `docker build` do mesmo diretório em que o `.sln` arquivo reside.

```console
docker build -t stockdata:1.0.0 -f ./src/StockData/Dockerfile .
```

O `--tag` sinalizador com nome confuso (que pode ser reduzido `-t` ) especifica o nome completo da imagem, incluindo a marca real, se especificado. O `.` no final especifica o contexto no qual a compilação será executada; o diretório de trabalho atual para os `COPY` comandos no Dockerfile.

Se você tiver vários aplicativos em uma única solução, poderá manter o Dockerfile de cada aplicativo em sua própria pasta, ao lado do `.csproj` arquivo. Você ainda deve executar o `docker build` comando do diretório base para garantir que a solução e todos os projetos sejam copiados para a imagem. Você pode especificar um Dockerfile abaixo do diretório atual usando o `--file` sinalizador (ou `-f` ).

```console
docker build -t stockdata:1.0.0 -f ./src/StockData/Dockerfile .
```

## <a name="run-the-image-in-a-container-on-your-machine"></a>Executar a imagem em um contêiner em seu computador

Para executar a imagem em sua instância local do Docker, use o `docker run` comando.

```console
docker run -ti -p 5000:80 stockdata:1.0.0
```

O `-ti` sinalizador conecta o terminal atual ao terminal do contêiner e é executado no modo interativo. A `-p 5000:80` porta de publicação (links) 80 no contêiner para a porta 5000 na interface de rede do localhost.

## <a name="push-the-image-to-a-registry"></a>Efetue o push da imagem para um Registro

Depois de verificar se a imagem funciona, envie-a por push para um registro do Docker para disponibilizá-la em outros sistemas. As redes internas precisarão provisionar um registro do Docker. Essa atividade pode ser tão simples quanto executar a [própria `registry` imagem do Docker](https://docs.docker.com/registry/deploying/) (o registro do Docker é executado em um contêiner do Docker), mas há várias soluções mais abrangentes disponíveis. Para o compartilhamento externo e o uso de nuvem, há vários registros gerenciados disponíveis, como o [registro de contêiner do Azure](/azure/container-registry/) ou o [Hub do Docker](https://docs.docker.com/docker-hub/repos/).

Para enviar por push para o Hub do Docker, Prefixe o nome da imagem com o nome do usuário ou da organização.

```console
docker tag stockdata:1.0.0 <myorg>/stockdata:1.0.0
docker push <myorg>/stockdata:1.0.0
```

Para enviar por push para um registro privado, Prefixe o nome da imagem com o nome do host do registro e o nome da organização.

```console
docker tag stockdata <internal-registry:5000>/<myorg>/stockdata:1.0.0
docker push <internal-registry:5000>/<myorg>/stockdata:1.0.0
```

Depois que a imagem estiver em um registro, você poderá implantá-la em hosts do Docker individuais ou em um mecanismo de orquestração de contêiner, como kubernetes.

>[!div class="step-by-step"]
>[Anterior](self-hosted.md) 
> [Avançar](kubernetes.md)
