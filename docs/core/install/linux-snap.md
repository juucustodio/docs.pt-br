---
title: Instalar o .NET no Linux com snap-.NET
description: Demonstra como instalar o SDK do .NET ou o tempo de execução do .NET no Linux com o snap.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 741933b5ca6f01d73b388675fe7f8a43c4efb0f9
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970958"
---
# <a name="install-the-net-sdk-or-the-net-runtime-with-snap"></a>Instalar o SDK do .NET ou o tempo de execução do .NET com snap

Use um pacote de snap para instalar o SDK do .NET ou o tempo de execução do .NET. Os snaps são uma ótima alternativa para o Gerenciador de pacotes incorporado à sua distribuição do Linux. Este artigo descreve como instalar o .NET por meio do [snap](https://snapcraft.io/dotnet-sdk).

Um snap é um pacote de um aplicativo e suas dependências que funcionam sem modificação em várias distribuições do Linux diferentes. Os snaps são detectáveis e instaláveis no repositório de instantâneos. Para obter mais informações sobre o snap, consulte [introdução ao snap](https://snapcraft.io/docs/getting-started).

> [!CAUTION]
> Os pacotes snap não têm suporte no WSL2 no Windows 10. Como alternativa, use o [ `dotnet-install` script](linux-scripted-manual.md#scripted-install) ou o Gerenciador de pacotes para a distribuição WSL2 específica. Não é recomendável, mas você pode tentar habilitar o snap com uma [solução alternativa sem suporte dos fóruns do snapcraft](https://forum.snapcraft.io/t/running-snaps-on-wsl2-insiders-only-for-now/13033).

## <a name="net-releases"></a>Versões do .NET

Somente ✔️ versões com suporte do SDK do .NET estão disponíveis por meio do snap. Todas as versões do tempo de execução do .NET estão disponíveis por meio do snap, começando com a versão 2,1. A tabela a seguir lista as versões do .NET (e do .NET Core):

| ✔️ com suporte | ❌ Sem suporte |
|-------------|---------------|
| 5.0         | 3.0           |
| 3,1 (LTS)   | 2.2           |
| 2,1 (LTS)   | 2,0           |
|             | 1,1           |
|             | 1.0           |

Para obter mais informações sobre o ciclo de vida de versões do .NET, consulte [.NET Core e .NET 5 Support Policy](https://dotnet.microsoft.com/platform/support/policy/dotnet-core).

## <a name="sdk-or-runtime"></a>SDK ou tempo de execução

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

## <a name="install-the-sdk"></a>Instalar o SDK

Pacotes snap para o SDK do .NET são todos publicados sob o mesmo identificador: `dotnet-sdk` . Uma versão específica do SDK pode ser instalada especificando o canal. O SDK inclui o tempo de execução correspondente. A tabela a seguir lista os canais:

| Versão do .NET | Ajustar pacote ou canal  |
|--------------|--------------------------|
| 5.0          | `5.0` ou `latest/stable` |
| 3,1 (LTS)    | `3.1` ou `lts/stable`    |
| 2,1 (LTS)    | `2.1`                    |

Use o `snap install` comando para instalar um pacote de snap do SDK do .net. Use o `--channel` parâmetro para indicar qual versão deve ser instalada. Se esse parâmetro for omitido, `latest/stable` será usado. Neste exemplo, `5.0` é especificado:

```bash
sudo snap install dotnet-sdk --classic --channel=5.0
```

Em seguida, registre o `dotnet` comando para o sistema com o `snap alias` comando:

```bash
sudo snap alias dotnet-sdk.dotnet dotnet
```

Este comando é formatado como: `sudo snap alias {package}.{command} {alias}` . Você pode escolher qualquer `{alias}` nome que desejar. Por exemplo, você pode nomear o comando após a versão específica instalada pelo snap: `sudo snap alias dotnet-sdk.dotnet dotnet50` . Ao usar o comando `dotnet50` , você invocará essa versão específica do .net. Mas a escolha de um alias diferente é incompatível com a maioria dos tutoriais e exemplos, pois eles esperam que um `dotnet` comando seja usado.

## <a name="install-the-runtime"></a>Instalar o runtime

Os pacotes snap para o tempo de execução do .NET são publicados em seu próprio identificador de pacote. A tabela a seguir lista os identificadores de pacote:

| Versão do .NET      | Ajustar pacote        |
|-------------------|---------------------|
| 5.0               | `dotnet-runtime-50` |
| 3,1 (LTS)         | `dotnet-runtime-31` |
| 3.0               | `dotnet-runtime-30` |
| 2.2               | `dotnet-runtime-22` |
| 2,1 (LTS)         | `dotnet-runtime-21` |

Use o `snap install` comando para instalar um pacote de snap do tempo de execução .net. Neste exemplo, o .NET 5,0 está instalado:

```bash
sudo snap install dotnet-runtime-50 --classic
```

Em seguida, registre o `dotnet` comando para o sistema com o `snap alias` comando:

```bash
sudo snap alias dotnet-runtime-50.dotnet dotnet
```

O comando é formatado como: `sudo snap alias {package}.{command} {alias}` . Você pode escolher qualquer `{alias}` nome que desejar. Por exemplo, você pode nomear o comando após a versão específica instalada pelo snap: `sudo snap alias dotnet-runtime-50.dotnet dotnet50` . Ao usar o comando `dotnet50` , você invocará uma versão específica do .net. Mas a escolha de um alias diferente é incompatível com a maioria dos tutoriais e exemplos, pois eles esperam que um `dotnet` comando esteja disponível.

## <a name="tlsssl-certificate-errors"></a>Erros de certificado TLS/SSL

Quando o .NET é instalado por meio do snap, é possível que, em alguns distribuições, os certificados .NET TLS/SSL possam não ser encontrados e você receba um erro durante `restore` :

```bash
Processing post-creation actions...
Running 'dotnet restore' on /home/myhome/test/test.csproj...
  Restoring packages for /home/myhome/test/test.csproj...
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error : Unable to load the service index for source https://api.nuget.org/v3/index.json. [/home/myhome/test/test.csproj]
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error :   The SSL connection could not be established, see inner exception. [/home/myhome/test/test.csproj]
/snap/dotnet-sdk/27/sdk/2.2.103/NuGet.targets(114,5): error :   The remote certificate is invalid according to the validation procedure. [/home/myhome/test/test.csproj]
```

Para resolver esse problema, defina algumas variáveis de ambiente:

```bash
export SSL_CERT_FILE=[path-to-certificate-file]
export SSL_CERT_DIR=/dev/null
```

O local do certificado variará de acordo com distribuição. Aqui estão os locais para o distribuições onde o problema foi experimentado.

| Distribuição | Localização                                            |
|--------------|-----------------------------------------------------|
| **Fedora**   | `/etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem` |
| **OpenSUSE** | `/etc/ssl/ca-bundle.pem`                            |
| **Solus**    | `/etc/ssl/certs/ca-certificates.crt`                |

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
