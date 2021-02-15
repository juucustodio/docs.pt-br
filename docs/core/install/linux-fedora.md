---
title: Instalar o .NET em Fedora-.NET
description: Demonstra as várias maneiras de instalar o SDK do .NET e o tempo de execução do .NET no Fedora.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 9dd8c6264831e2a9382960be505639f1eba95151
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970818"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-fedora"></a>Instalar o SDK do .NET ou o tempo de execução do .NET no Fedora

O .NET tem suporte no Fedora e este artigo descreve como instalar o .NET no Fedora. Quando uma versão do Fedora fica sem suporte, o .NET não é mais compatível com essa versão.

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="install-net-50"></a>Instalar o .NET 5,0

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

**Fedora 32**

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/32/prod.repo
```

**Fedora 33**

```bash
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/33/prod.repo
```

[!INCLUDE [linux-dnf-install-50](includes/linux-install-50-dnf.md)]

## <a name="install-net-core-31"></a>Instalar o .NET Core 3,1

A versão mais recente do .NET disponível nos repositórios de pacotes padrão do Fedora é o .NET Core 3,1.

[!INCLUDE [linux-dnf-install-31](includes/linux-install-31-dnf.md)]

## <a name="supported-distributions"></a>Distribuições com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento e as versões do Fedora em que têm suporte. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do [Fedora atinja o fim da vida útil](https://fedoraproject.org/wiki/End_of_life).

- Um ✔️ indica que a versão do Fedora ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do Fedora ou do .net não tem suporte nessa versão do Fedora.
- Quando uma versão do Fedora e uma versão do .NET têm ✔️, há suporte para essa combinação de so e .NET.

| Versão .NET  | Fedora 33 ✔️ | 32 ✔️ | 31 ❌ | máximo ❌ | 29 ❌ | 38 ❌ | 27 ❌ |
| ------------  | ---------: | --: | --: | --: | --: | --: | --: |
| .NET 5.0      | ✔️        | ✔️ | ❌|❌ |❌ |❌  |❌ |
| .NET Core 3.1 | ✔️        | ✔️ | ✔️|✔️ |✔️ |❌  |❌ |
| .NET Core 2.1 | ✔️        | ✔️ | ✔️|✔️ |✔️ |✔️  |✔️ |

Não há mais suporte para as seguintes versões do .NET. Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

## <a name="remove-preview-versions"></a>Remover versões de visualização

[!INCLUDE [package-manager uninstall notice](./includes/linux-uninstall-preview-info.md)]

## <a name="dependencies"></a>Dependências

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="install-on-older-distributions"></a>Instalar em distribuições mais antigas

As versões mais antigas do Fedora não contêm o .NET Core nos repositórios de pacote padrão. Você pode instalar o .NET com [snap](linux-snap.md), por meio do [script _dotnet-install.sh_](linux-scripted-manual.md#scripted-install), ou usar o repositório da Microsoft para instalar o .net:

01. Primeiro, adicione a chave de assinatura da Microsoft à lista de chaves confiáveis.

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    ```

02. Em seguida, adicione o repositório de pacotes da Microsoft. A origem do repositório é baseada em sua versão do Fedora.

    | Versão do Fedora | Repositório de pacotes |
    | -------------- | ------- |
    | 31             | `https://packages.microsoft.com/config/fedora/31/prod.repo` |
    | 30             | `https://packages.microsoft.com/config/fedora/30/prod.repo` |
    | 29             | `https://packages.microsoft.com/config/fedora/29/prod.repo` |
    | 28             | `https://packages.microsoft.com/config/fedora/28/prod.repo` |
    | 27             | `https://packages.microsoft.com/config/fedora/27/prod.repo` |

    ```bash
    sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/31/prod.repo
    ```

[!INCLUDE [linux-dnf-install-31](./includes/linux-install-31-dnf.md)]

## <a name="how-to-install-other-versions"></a>Como instalar outras versões

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a>Solucionar problemas do Gerenciador de pacotes

Esta seção fornece informações sobre erros comuns que você pode obter ao usar o Gerenciador de pacotes para instalar o .NET ou o .NET Core.

### <a name="unable-to-find-package"></a>Não é possível localizar o pacote

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

### <a name="failed-to-fetch"></a>Falha ao buscar

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
