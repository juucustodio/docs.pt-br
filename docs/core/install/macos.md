---
title: Instalar o .NET no macOS
description: Saiba mais sobre quais versões do macOS você pode instalar o .NET.
author: adegeo
ms.author: adegeo
ms.date: 11/10/2020
ms.openlocfilehash: 871263b820aaf4cc04e573dd4aa3022caa401857
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506299"
---
# <a name="install-net-on-macos"></a>Instalar o .NET no macOS

> [!div class="op_single_selector"]
>
> - [Instalar no Windows](windows.md)
> - [Instalar no macOS](macos.md)
> - [Instalar no Linux](linux.md)

Neste artigo, você aprenderá a instalar o .NET no macOS. O .NET é constituído do tempo de execução e do SDK. O tempo de execução é usado para executar um aplicativo .NET e pode ou não ser incluído com o aplicativo. O SDK é usado para criar aplicativos e bibliotecas .NET. O tempo de execução do .NET é sempre instalado com o SDK.

A versão mais recente do .NET é 5,0.

> [!div class="button"]
> [Baixe o .NET Core](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="supported-releases"></a>Versões com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento e as versões do macOS nas quais elas têm suporte. Essas versões permanecem com suporte, ou seja, a versão do [.net atinge o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).

- Um ✔️ indica que a versão do .NET Core ainda tem suporte.
- Um ❌ indica que a versão do .NET Core não tem suporte.

| Sistema operacional          | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|---------------------------|---------------|---------------|----------------|
| macOS 11,0 "Big Sur"        | ✔️ 2,1 ([notas de versão][release-notes-21]) | ✔️ 3,1 ([notas de versão][release-notes-31]) | ✔️ 5,0 ([notas de versão][release-notes-50]) |
| macOS 10.15 "Catalina"    | ✔️ 2,1 ([notas de versão][release-notes-21]) | ✔️ 3,1 ([notas de versão][release-notes-31]) | ✔️ 5,0 ([notas de versão][release-notes-50]) |
| macOS 10.14 "Mojave"      | ✔️ 2,1 ([notas de versão][release-notes-21]) | ✔️ 3,1 ([notas de versão][release-notes-31]) | ✔️ 5,0 ([notas de versão][release-notes-50]) |
| macOS 10.13 "High Sierra" | ✔️ 2,1 ([notas de versão][release-notes-21]) | ✔️ 3,1 ([notas de versão][release-notes-31]) | ✔️ 5,0 ([notas de versão][release-notes-50]) |
| macOS 10.12 "Sierra"      | ✔️ 2,1 ([notas de versão][release-notes-21]) | ❌ 3,1 ([notas de versão][release-notes-31]) | ❌ 5,0 ([notas de versão][release-notes-50]) |

## <a name="unsupported-releases"></a>Versões sem suporte

Não há mais suporte para as seguintes versões do .NET ❌ . Os downloads para eles ainda permanecem publicados:

- 3,0 ([notas de versão][release-notes-30])
- 2,2 ([notas de versão][release-notes-22])
- 2,0 ([notas de versão][release-notes-20])

## <a name="runtime-information"></a>Informações de tempo de execução

O tempo de execução é usado para executar aplicativos criados com o .NET. Quando um autor de aplicativo publica um aplicativo, ele pode incluir o tempo de execução com seu aplicativo. Se eles não incluírem o tempo de execução, cabe ao usuário instalar o tempo de execução.

Há dois tempos de execução diferentes que você pode instalar no macOS:

- *Tempo de execução ASP.NET Core*\
  Executa ASP.NET Core aplicativos. Inclui o tempo de execução do .NET.

- *Tempo de execução do .NET*\
  Esse tempo de execução é o tempo de execução mais simples e não inclui nenhum outro tempo de execução. É altamente recomendável que você instale *ASP.NET Core tempo de execução* para obter a melhor compatibilidade com aplicativos .net.

> [!div class="button"]
> [Baixar o tempo de execução do .NET](https://dotnet.microsoft.com/download/dotnet-core)

## <a name="sdk-information"></a>Informações do SDK

O SDK é usado para compilar e publicar aplicativos e bibliotecas .NET. A instalação do SDK inclui ambos os [tempos de execução](#runtime-information): ASP.NET Core e .net.

## <a name="dependencies"></a>Dependências

O .NET tem suporte nas seguintes versões do macOS:

> [!NOTE]
> Um `+` símbolo representa a versão mínima.

| Versão do .NET Core | macOS                 | Arquiteturas | Mais informações    |
| ----------------- | --------------------- | --------------| --- |
| 5.0               | Alta serra (10.13 +)  | x64 | [Mais informações](https://github.com/dotnet/core/blob/master/release-notes/5.0/5.0-supported-os.md) |
| 3.1               | Alta serra (10.13 +)  | x64 | [Mais informações](https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md) |
| 3.0               | Alta serra (10.13 +)  | x64 | [Mais informações](https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md) |
| 2.2               | Sierra (10.12 +)       | x64 | [Mais informações](https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md) |
| 2.1               | Sierra (10.12 +)       | x64 | [Mais informações](https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md) |

A partir do macOS Catalina (versão 10,15), todo software criado após 1º de junho de 2019 que é distribuído com a ID do desenvolvedor deve ser notarized. Esse requisito se aplica ao tempo de execução do .NET, ao SDK do .NET e ao software criado com o .NET.

Os instaladores de tempo de execução e SDK para .NET 5,0 e .NET Core 3,1, 3,0 e 2,1, foram notarizeddos desde 18 de fevereiro de 2020. Versões anteriores liberadas não são notarized. Se você executar um aplicativo não notarized, verá um erro semelhante à imagem a seguir:

![alerta de notarization Catalina do macOS](media/dependencies/macos-notarized-pkg-warning.png)

Para obter mais informações sobre como o imforced-notarization afeta o .NET (e seus aplicativos .NET), consulte [trabalhando com o MacOS Catalina notarization](macos-notarization-issues.md).

## <a name="libgdiplus"></a>libgdiplus

Os aplicativos .NET que usam o assembly *System. sorteio. Common* exigem que o libgdiplus seja instalado.

Uma maneira fácil de obter o libgdiplus é usando o Gerenciador de pacotes [homebrew ("Brew")](https://brew.sh/) para MacOS. Depois de instalar o *Brew*, instale o libgdiplus executando os seguintes comandos em um prompt de terminal (comando):

```console
brew update
brew install mono-libgdiplus
```

## <a name="install-with-an-installer"></a>Instalar com um instalador

o macOS tem instaladores autônomos que podem ser usados para instalar o SDK do .NET 5,0:

- [CPUs x64 (64 bits)](https://dotnet.microsoft.com/download/dotnet-core/5.0)

## <a name="download-and-manually-install"></a>Baixar e instalar manualmente

<!-- Note, this content is taken from includes/linux-install-manual.md but changed for macOS. Any fixes should be applied there too, though content may be different -->

Como alternativa para os instaladores do macOS para .NET, você pode baixar e instalar manualmente o SDK e o tempo de execução. A instalação manual geralmente é executada como parte do teste de integração contínua. Para um desenvolvedor ou usuário, geralmente é melhor usar um [instalador](https://dotnet.microsoft.com/download/dotnet-core).

Se você instalar o SDK do .NET, não precisará instalar o tempo de execução correspondente. Primeiro, Baixe uma versão **binária** para o SDK ou o tempo de execução de um dos seguintes sites:

- downloads do ✔️ [.net 5,0](https://dotnet.microsoft.com/download/dotnet/5.0)
- downloads do ✔️ [.NET Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1)
- downloads do ✔️ [.NET Core 2,1](https://dotnet.microsoft.com/download/dotnet-core/2.1)
- [Todos os downloads do .NET Core](https://dotnet.microsoft.com/download/dotnet-core)

Em seguida, extraia o arquivo baixado e use o `export` comando para definir as variáveis usadas pelo .net e, em seguida, verifique se o .net está no caminho.

Para extrair o tempo de execução e tornar os comandos da CLI do .NET disponíveis no terminal, primeiro Baixe uma versão binária do .NET. Em seguida, abra um terminal e execute os seguintes comandos no diretório em que o arquivo foi salvo. O nome do arquivo morto pode ser diferente dependendo do que você baixou.

**Use os comandos a seguir para extrair o tempo de execução ou o SDK que você baixou.** Lembre-se de alterar o `DOTNET_FILE` valor para o nome do arquivo:

```bash
DOTNET_FILE=dotnet-sdk-5.0.102-linux-x64.tar.gz
export DOTNET_ROOT=$HOME/dotnet

mkdir -p "$DOTNET_ROOT" && tar zxf "$DOTNET_FILE" -C "$DOTNET_ROOT"

export PATH=$PATH:$DOTNET_ROOT
```

> [!TIP]
> Os `export` comandos anteriores tornam os comandos da CLI do .net disponíveis para a sessão de terminal na qual ele foi executado.
>
> Você pode editar seu perfil de Shell para adicionar os comandos permanentemente. Há vários shells diferentes disponíveis para o Linux e cada um deles tem um perfil diferente. Por exemplo:
>
> - **Shell bash**: *~/.bash_profile*, *~/.bashrc*
> - **Shell Korn**: *~/.Kshrc* ou *. Profile*
> - **Shell Z**: *~/.zshrc* ou *. zprofile*
>
> Edite o arquivo de origem apropriado para o Shell e adicione `:$HOME/dotnet` ao final da `PATH` instrução existente. Se nenhuma `PATH` instrução for incluída, adicione uma nova linha com `export PATH=$PATH:$HOME/dotnet` .
>
> Além disso, adicione `export DOTNET_ROOT=$HOME/dotnet` ao final do arquivo.

Essa abordagem permite que você instale versões diferentes em locais separados e escolha explicitamente qual deles usar por qual aplicativo.

## <a name="install-with-visual-studio-for-mac"></a>Instalar com o Visual Studio para Mac

Visual Studio para Mac instala o SDK do .NET quando a carga de trabalho do **.net** é selecionada. Para começar a usar o desenvolvimento do .NET no macOS, consulte [instalar o Visual Studio 2019 para Mac](/visualstudio/mac/installation).

| Versão do SDK do .NET      | Versão do Visual Studio                      |
| --------------------- | ------------------------------------------ |
| 5.0                   | Visual Studio 2019 para Mac versão 8,8 ou superior. |
| 3.1                   | Visual Studio 2019 para Mac versão 8,4 ou superior. |
| 2.1                   | Visual Studio 2019 para Mac versão 8,0 ou superior. |

[![recurso macOS Visual Studio 2019 para Mac com carga de trabalho .NET](media/install-sdk/mac-install-selection.png)](media/install-sdk/mac-install-selection.png#lightbox)

## <a name="install-alongside-visual-studio-code"></a>Instalar junto com Visual Studio Code

Visual Studio Code é um editor de código-fonte leve e avançado que é executado em sua área de trabalho. Visual Studio Code está disponível para Windows, macOS e Linux.

Embora Visual Studio Code não venha com um instalador .NET automatizado como o Visual Studio, é simples adicionar suporte ao .NET.

01. [Baixe e instale o Visual Studio Code](https://code.visualstudio.com/Download).
01. [Baixe e instale o SDK do .net](https://dotnet.microsoft.com/download/dotnet-core).
01. [Instale a extensão C# do Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp).

## <a name="install-with-bash-automation"></a>Instalar com a automação do bash

Os [scripts dotnet-install](../tools/dotnet-install-script.md) são usados para automação e instalações não administrativas do tempo de execução. Você pode baixar o script na [página de referência de script dotnet-install](../tools/dotnet-install-script.md).

O script assume como padrão a instalação da versão mais recente do [LTS (suporte a longo prazo)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) , que é o .net Core 3,1. Você pode escolher uma versão específica especificando a `current` opção. Inclua a `runtime` opção para instalar um tempo de execução. Caso contrário, o script instalará o [SDK](./windows.md).

```bash
./dotnet-install.sh --channel 5.0 --runtime aspnetcore
```

> [!NOTE]
> O comando anterior instala o tempo de execução de ASP.NET Core para compatibilidade máxima. O tempo de execução de ASP.NET Core também inclui o tempo de execução do .NET padrão.

## <a name="docker"></a>Docker

Os contêineres fornecem uma maneira leve de isolar seu aplicativo do restante do sistema host. Os contêineres no mesmo computador compartilham apenas o kernel e usam os recursos fornecidos ao seu aplicativo.

O .NET pode ser executado em um contêiner do Docker. As imagens oficiais do Docker do .NET são publicadas no MCR (registro de contêiner da Microsoft) e podem ser descobertas no [repositório do Hub do Docker do Microsoft .NET Core](https://hub.docker.com/_/microsoft-dotnet/). Cada repositório contém imagens para diferentes combinações do .NET (SDK ou Runtime) e do sistema operacional que você pode usar.

A Microsoft fornece imagens personalizadas para cenários específicos. Por exemplo, o [repositório do ASP.NET Core](https://hub.docker.com/_/microsoft-dotnet-aspnet) fornece imagens que são criadas para a execução de aplicativos ASP.NET Core na produção.

Para obter mais informações sobre como usar o .NET Core em um contêiner do Docker, consulte [introdução ao .net e ao Docker](../docker/introduction.md) e [amostras](https://github.com/dotnet/dotnet-docker/blob/master/samples/README.md).

## <a name="next-steps"></a>Próximas etapas

- [Como verificar se o .NET Core já está instalado](how-to-detect-installed-versions.md?pivots=os-macos).
- [Trabalhando com o notarization Catalina do MacOS](macos-notarization-issues.md).
- [Tutorial: introdução ao MacOS](../tutorials/with-visual-studio-mac.md).
- [Tutorial: criar um novo aplicativo com Visual Studio Code](../tutorials/with-visual-studio-code.md).
- [Tutorial: colocar em contêiner um aplicativo .NET Core](../docker/build-container.md).

[release-notes-21]: https://github.com/dotnet/core/blob/master/release-notes/2.1/2.1-supported-os.md
[release-notes-31]: https://github.com/dotnet/core/blob/master/release-notes/3.1/3.1-supported-os.md
[release-notes-50]: https://github.com/dotnet/core/blob/master/release-notes/5.0/5.0-supported-os.md
[release-notes-20]: https://github.com/dotnet/core/blob/master/release-notes/2.0/2.0-supported-os.md
[release-notes-22]: https://github.com/dotnet/core/blob/master/release-notes/2.2/2.2-supported-os.md
[release-notes-30]: https://github.com/dotnet/core/blob/master/release-notes/3.0/3.0-supported-os.md
