---
title: Instalar o .NET no Debian-.NET
description: Demonstra as várias maneiras de instalar o SDK do .NET e o tempo de execução do .NET no Debian.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 913d8bffdd6c0b5e88a70dae0ec4c8d732e80cc0
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970831"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-debian"></a>Instalar o SDK do .NET ou o tempo de execução do .NET no Debian

Este artigo descreve como instalar o .NET no Debian. Quando uma versão Debian fica sem suporte, o .NET não é mais compatível com essa versão. No entanto, essas instruções podem ajudá-lo a obter o .NET em execução nessas versões, mesmo que não haja suporte.

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a>Distribuições com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento e as versões do Debian nas quais elas têm suporte. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do [Debian atinja o fim da vida útil](https://wiki.debian.org/DebianReleases).

- Um ✔️ indica que a versão do Debian ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do Debian ou do .net não tem suporte nessa versão do Debian.
- Quando uma versão do Debian e uma versão do .NET têm ✔️, essa combinação de so e .NET é suportada.

| Debian                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [10](#debian-10-)     | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [9](#debian-9-)       | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ❌[8](#debian-8-)       | ✔️ 2,1        | ❌ 3,1        | ❌ 5,0 |

Não há mais suporte para as seguintes versões do .NET. Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

## <a name="remove-preview-versions"></a>Remover versões de visualização

[!INCLUDE [package-manager uninstall notice](./includes/linux-uninstall-preview-info.md)]

## <a name="debian-10-"></a>Debian 10 ✔️

[!INCLUDE [linux-prep-intro-apt](includes/linux-prep-intro-apt.md)]

```bash
wget https://packages.microsoft.com/config/debian/10/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
```

[!INCLUDE [linux-apt-install-50](includes/linux-install-50-apt.md)]

## <a name="debian-9-"></a>Debian 9 ✔️

[!INCLUDE [linux-prep-intro-apt](includes/linux-prep-intro-apt.md)]

```bash
wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget https://packages.microsoft.com/config/debian/9/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
```

[!INCLUDE [linux-apt-install-50](includes/linux-install-50-apt.md)]

## <a name="debian-8-"></a>Debian 8 ❌

[!INCLUDE [linux-not-supported](includes/linux-not-supported-debian.md)]

[!INCLUDE [linux-prep-intro-apt](includes/linux-prep-intro-apt.md)]

```bash
wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget https://packages.microsoft.com/config/debian/8/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
```

[!INCLUDE [linux-apt-install-21](includes/linux-install-21-apt.md)]

## <a name="how-to-install-other-versions"></a>Como instalar outras versões

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="use-apt-to-update-net"></a>Usar a APT para atualizar o .NET

Quando uma nova versão de patch estiver disponível para o .NET, você poderá simplesmente atualizá-la por meio de APT com os seguintes comandos:

```bash
sudo apt-get update
sudo apt-get upgrade
```

## <a name="apt-troubleshooting"></a>Solução de problemas da APT

Esta seção fornece informações sobre erros comuns que você pode obter ao usar a APT para instalar o .NET.

### <a name="unable-to-find-package"></a>Não é possível localizar o pacote

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

### <a name="unable-to-locate--some-packages-could-not-be-installed"></a>Não foi possível \\ instalar alguns pacotes

[!INCLUDE [package-manager-failed-to-find-deb](includes/package-manager-failed-to-find-deb.md)]

```bash
sudo apt-get install -y gpg
wget -O - https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor -o microsoft.asc.gpg
sudo mv microsoft.asc.gpg /etc/apt/trusted.gpg.d/
wget https://packages.microsoft.com/config/debian/{os-version}/prod.list
sudo mv prod.list /etc/apt/sources.list.d/microsoft-prod.list
sudo chown root:root /etc/apt/trusted.gpg.d/microsoft.asc.gpg
sudo chown root:root /etc/apt/sources.list.d/microsoft-prod.list
sudo apt-get update; \
  sudo apt-get install -y apt-transport-https && \
  sudo apt-get update && \
  sudo apt-get install -y {dotnet-package}
```

### <a name="failed-to-fetch"></a>Falha ao buscar

[!INCLUDE [package-manager-failed-to-fetch-deb](includes/package-manager-failed-to-fetch-deb.md)]

## <a name="dependencies"></a>Dependências

Quando você instala o com um Gerenciador de pacotes, essas bibliotecas são instaladas para você. Mas, se você instalar manualmente o .NET Core ou publicar um aplicativo independente, precisará verificar se essas bibliotecas estão instaladas:

- libc6
- libgcc1
- libgssapi-krb5-2
- libicu52 (para 8. x)
- libicu57 (para 9. x)
- libicu63 (para 10. x)
- libicu67 (para 11. x)
- libssl 1.0.0 (para 8. x)
- libssl 1.1 (para 9. x-11. x)
- libstdc + + 6
- zlib1g

Para aplicativos .NET Core que usam o assembly *System. Drawing. Common* , você também precisa da seguinte dependência:

- libgdiplus (versão 6.0.1 ou posterior)

  > [!WARNING]
  > Você pode instalar uma versão recente do *libgdiplus* adicionando o repositório do mono ao seu sistema. Para obter mais informações, consulte <https://www.mono-project.com/download/stable/>.

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
