---
title: Instalar o .NET em openSUSE-.NET
description: Demonstra as várias maneiras de instalar o SDK do .NET e o tempo de execução do .NET no openSUSE.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 7a519f19f708e1f12af1e9715bad4f38a607f9c3
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970805"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-opensuse"></a>Instalar o SDK do .NET ou o tempo de execução do .NET no openSUSE

O .NET tem suporte no openSUSE. Este artigo descreve como instalar o .NET no openSUSE.

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a>Distribuições com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento no openSUSE 15. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do openSUSE não seja mais suportada.

- Um ✔️ indica que a versão do openSUSE ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do openSUSE ou do .net não tem suporte nessa versão do openSUSE.
- Quando uma versão do openSUSE e uma versão do .NET têm ✔️, há suporte para essa combinação de so e .NET.

| openSUSE                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|----------------------------|---------------|---------------|----------------|
| ✔️ [15](#opensuse-15-)     | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |

Não há mais suporte para as seguintes versões do .NET. Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

## <a name="remove-preview-versions"></a>Remover versões de visualização

[!INCLUDE [package-manager uninstall notice](./includes/linux-uninstall-preview-info.md)]

## <a name="opensuse-15-"></a>openSUSE 15 ✔️

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo zypper install libicu
sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
wget https://packages.microsoft.com/config/opensuse/15/prod.repo
sudo mv prod.repo /etc/zypp/repos.d/microsoft-prod.repo
sudo chown root:root /etc/zypp/repos.d/microsoft-prod.repo
```

[!INCLUDE [linux-zyp-install-50](includes/linux-install-50-zyp.md)]

## <a name="how-to-install-other-versions"></a>Como instalar outras versões

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a>Solucionar problemas do Gerenciador de pacotes

Esta seção fornece informações sobre erros comuns que você pode obter ao usar o Gerenciador de pacotes para instalar o .NET.

### <a name="unable-to-find-package"></a>Não é possível localizar o pacote

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

### <a name="failed-to-fetch"></a>Falha ao buscar

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="dependencies"></a>Dependências

Quando você instala o com um Gerenciador de pacotes, essas bibliotecas são instaladas para você. Mas, se você instalar o .NET manualmente ou publicar um aplicativo independente, precisará verificar se essas bibliotecas estão instaladas:

- krb5
- libicu
- libopenssl1_0_0

Se a versão do OpenSSL do ambiente de tempo de execução de destino for 1,1 ou mais recente, você precisará instalar o **compat-openssl10**.

Para obter mais informações sobre as dependências, consulte [aplicativos do Linux autocontidos](https://github.com/dotnet/core/blob/master/Documentation/self-contained-linux-apps.md).

Para aplicativos .NET que usam o assembly *System. Drawing. Common* , você também precisará da seguinte dependência:

- [libgdiplus (versão 6.0.1 ou posterior)](https://www.mono-project.com/docs/gui/libgdiplus/)

  > [!WARNING]
  > Você pode instalar uma versão recente do *libgdiplus* adicionando o repositório do mono ao seu sistema. Para obter mais informações, consulte <https://www.mono-project.com/download/stable/>.

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
