---
title: Instalar manualmente o .NET no Linux-.NET
description: Demonstra como instalar o SDK do .NET e o tempo de execução do .NET sem um Gerenciador de pacotes no Linux. Use o script de instalação ou extraia os binários manualmente.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 14789587a58c7b9d5ef2c9251ed599ce18a48f24
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505570"
---
# <a name="install-the-net-sdk-or-the-net-runtime-manually"></a>Instalar o SDK do .NET ou o tempo de execução do .NET manualmente

O .NET tem suporte no Linux e este artigo descreve como instalar o .NET no Linux usando o script de instalação ou extraindo os binários. Para obter uma lista de distribuições que dão suporte ao Gerenciador de pacotes interno, consulte [instalar o .net no Linux](linux.md).

Você também pode instalar o .NET com snap. Para obter mais informações, consulte [instalar o SDK do .net ou o tempo de execução do .NET com snap](linux-snap.md).

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

## <a name="net-releases"></a>Versões do .NET

A tabela a seguir lista as versões do .NET (e do .NET Core):

| ✔️ com suporte | ❌ Sem suporte |
|-------------|---------------|
| 5.0         | 3.0           |
| 3,1 (LTS)   | 2.2           |
| 2,1 (LTS)   | 2,0           |
|             | 1,1           |
|             | 1.0           |

Para obter mais informações sobre o ciclo de vida de versões do .NET, consulte [.NET Core e .NET 5 Support Policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).

## <a name="dependencies"></a>Dependências

É possível que, ao instalar o .NET, as dependências específicas não sejam instaladas, como durante a [instalação manual](#manual-install)do. A lista a seguir fornece detalhes sobre as distribuições do Linux com suporte da Microsoft e tem dependências que talvez você precise instalar. Verifique a página de distribuição para obter mais informações:

- [Alpine](linux-alpine.md#dependencies)
- [Debian](linux-debian.md#dependencies)
- [CentOS](linux-centos.md#dependencies)
- [Fedora](linux-fedora.md#dependencies)
- [RHEL](linux-rhel.md#dependencies)
- [SLES](linux-sles.md#dependencies)
- [Ubuntu](linux-ubuntu.md#dependencies)

Para obter informações genéricas sobre as dependências, consulte [aplicativos do Linux autocontidos](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md).

### <a name="rpm-dependencies"></a>Dependências de RPM

Se a distribuição não tiver sido listada anteriormente e for baseada em RPM, talvez você precise das seguintes dependências:

- krb5-libs
- libicu
- openssl-libs

Se a versão do OpenSSL do ambiente de tempo de execução de destino for 1,1 ou mais recente, você precisará instalar o **compat-openssl10**.

### <a name="deb-dependencies"></a>Dependências de DEB

Se sua distribuição não foi listada anteriormente e for baseada em Debian, talvez você precise das seguintes dependências:

- libc6
- libgcc1
- libgssapi-krb5-2
- libicu67
- libssl 1.1
- libstdc + + 6
- zlib1g

### <a name="common-dependencies"></a>Dependências comuns

Para aplicativos .NET que usam o assembly *System. Drawing. Common* , você também precisará da seguinte dependência:

- [libgdiplus (versão 6.0.1 ou posterior)](https://www.mono-project.com/docs/gui/libgdiplus/)

  > [!WARNING]
  > Você pode instalar uma versão recente do *libgdiplus* adicionando o repositório do mono ao seu sistema. Para obter mais informações, consulte <https://www.mono-project.com/download/stable/>.

## <a name="scripted-install"></a>Instalação com script

Os [scripts dotnet-install](../tools/dotnet-install-script.md) são usados para instalações de automação e não administrativas do **SDK** e do **tempo de execução**. É possível baixar o script em <https://dot.net/v1/dotnet-install.sh>.

O script assume como padrão a instalação da versão mais recente do [LTS (suporte a longo prazo)](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) do SDK, que é o .net Core 3,1. Para instalar a versão atual, que pode não ser uma versão (LTS), use o `-c Current` parâmetro.

```bash
./dotnet-install.sh -c Current
```

Para instalar o tempo de execução do .NET em vez do SDK, use o `--runtime` parâmetro.

```bash
./dotnet-install.sh -c Current --runtime aspnetcore
```

Você pode instalar uma versão específica alterando o `-c` parâmetro para indicar a versão específica. O comando a seguir instala o SDK do .NET 5,0.

```bash
./dotnet-install.sh -c 5.0
```

Para obter mais informações, consulte [dotnet – referência de scripts de instalação](../tools/dotnet-install-script.md).

## <a name="manual-install"></a>Instalação manual

<!-- Note, this content is copied in macos.md. Any fixes should be applied there too, though content may be different -->

Como alternativa para os gerenciadores de pacotes, você pode baixar e instalar manualmente o SDK e o tempo de execução. A instalação manual é normalmente usada como parte do teste de integração contínua ou em uma distribuição do Linux sem suporte. Para um desenvolvedor ou usuário, é melhor usar um Gerenciador de pacotes.

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

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
