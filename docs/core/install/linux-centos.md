---
title: Instalar o .NET no CentOS-.NET
description: Demonstra as várias maneiras de instalar o SDK do .NET e o tempo de execução do .NET no CentOS.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 7e73f90a1f1f7e11e592b1b074f243c9f5b32ced
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970857"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-centos"></a>Instalar o SDK do .NET ou o tempo de execução do .NET no CentOS

O .NET tem suporte no CentOS. Este artigo descreve como instalar o .NET no CentOS.

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="supported-distributions"></a>Distribuições com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento no CentOS 7 e no CentOS 8. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do CentOS não seja mais suportada.

- Um ✔️ indica que a versão do CentOS ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do CentOS ou do .net não tem suporte nessa versão do CentOS.
- Quando uma versão do CentOS e uma versão do .NET têm ✔️, essa combinação de so e .NET é suportada.

| CentOS                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](#centos-8-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [7](#centos-7-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |

Não há mais suporte para as seguintes versões do .NET. Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

## <a name="remove-preview-versions"></a>Remover versões de visualização

[!INCLUDE [package-manager uninstall notice](./includes/linux-uninstall-preview-info.md)]

## <a name="centos-8-"></a>CentOS 8 ✔️

O .NET 5,0 está disponível nos repositórios de pacotes padrão do CentOS 8.

[!INCLUDE [linux-dnf-install-50](includes/linux-install-50-dnf.md)]

## <a name="centos-7-"></a>CentOS 7 ✔️

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

```bash
sudo rpm -Uvh https://packages.microsoft.com/config/centos/7/packages-microsoft-prod.rpm
```

[!INCLUDE [linux-yum-install-50](includes/linux-install-50-yum.md)]

## <a name="how-to-install-other-versions"></a>Como instalar outras versões

[!INCLUDE [package-manager-switcher](./includes/package-manager-heading-hack-pkgname.md)]

## <a name="troubleshoot-the-package-manager"></a>Solucionar problemas do Gerenciador de pacotes

Esta seção fornece informações sobre erros comuns que você pode obter ao usar o Gerenciador de pacotes para instalar o .NET.

### <a name="unable-to-find-package"></a>Não é possível localizar o pacote

[!INCLUDE [linux-install-package-manager-x64-vs-arm](includes/linux-install-package-manager-x64-vs-arm.md)]

### <a name="failed-to-fetch"></a>Falha ao buscar

[!INCLUDE [package-manager-failed-to-fetch-rpm](includes/package-manager-failed-to-fetch-rpm.md)]

## <a name="dependencies"></a>Dependências

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
