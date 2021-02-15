---
title: Instalar o .NET no SLES-.NET
description: Demonstra as várias maneiras de instalar o SDK do .NET e o tempo de execução do .NET no SLES.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 80da69616dd1507b809ef56d439645d569a6a805
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970779"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-sles"></a>Instalar o SDK do .NET ou o tempo de execução do .NET no SLES

O .NET tem suporte no SLES. Este artigo descreve como instalar o .NET no SLES.

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

## <a name="supported-distributions"></a>Distribuições com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento no SLES 12 SP2 e no SLES 15. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do SLES não seja mais suportada.

- Um ✔️ indica que a versão do SLES ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do SLES ou do .net não tem suporte nessa versão do SLES.
- Quando uma versão do SLES e uma versão do .NET têm ✔️, essa combinação de so e .NET é suportada.

| SLES                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|------------------------|---------------|---------------|----------------|
| ✔️ [15](#sles-15-)     | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [12 SP2](#sles-12-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |

Não há mais suporte para as seguintes versões do .NET Core. Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

## <a name="remove-preview-versions"></a>Remover versões de visualização

[!INCLUDE [package-manager uninstall notice](./includes/linux-uninstall-preview-info.md)]

## <a name="sles-15-"></a>✔️ SLES 15

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/sles/15/packages-microsoft-prod.rpm
```

Atualmente, o pacote de instalação do repositório do SLES 15 da Microsoft instala o arquivo *Microsoft-prod. repositório* no diretório errado, impedindo que o Zypper Localize os pacotes .net. Para corrigir esse problema, crie um symlink no diretório correto.

```bash
sudo ln -s /etc/yum.repos.d/microsoft-prod.repo /etc/zypp/repos.d/microsoft-prod.repo
```

[!INCLUDE [linux-zyp-install-50](includes/linux-install-50-zyp.md)]

## <a name="sles-12-"></a>✔️ SLES 12

O .NET requer o SP2 como um mínimo para a família SLES 12.

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/sles/12/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-zyp-install-50](includes/linux-install-50-zyp.md)]

## <a name="how-to-install-other-versions"></a>Como instalar outras versões

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a>Solucionar problemas do Gerenciador de pacotes

Esta seção fornece informações sobre erros comuns que você pode obter ao usar o Gerenciador de pacotes para instalar o .NET.

### <a name="failed-to-fetch"></a>Falha ao buscar

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="dependencies"></a>Dependências

Quando você instala o com um Gerenciador de pacotes, essas bibliotecas são instaladas para você. Mas, se você instalar o .NET manualmente ou publicar um aplicativo independente, precisará verificar se essas bibliotecas estão instaladas:

- krb5
- libicu
- libopenssl1_1

Se a versão do OpenSSL do ambiente de tempo de execução de destino for 1,1 ou mais recente, você precisará instalar o **compat-openssl10**.

Para obter mais informações sobre as dependências, consulte [aplicativos do Linux autocontidos](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md).

Para aplicativos .NET que usam o assembly *System. Drawing. Common* , você também precisará da seguinte dependência:

- [libgdiplus (versão 6.0.1 ou posterior)](https://www.mono-project.com/docs/gui/libgdiplus/)

  > [!WARNING]
  > Você pode instalar uma versão recente do *libgdiplus* adicionando o repositório do mono ao seu sistema. Para obter mais informações, consulte <https://www.mono-project.com/download/stable/>.

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
