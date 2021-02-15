---
title: Instalar o .NET no RHEL-.NET
description: Demonstra as várias maneiras de instalar o SDK do .NET e o tempo de execução do .NET no RHEL.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: d585017919507a8fdcbb24778a0ff3ab3d9049c2
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970792"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-rhel"></a>Instalar o SDK do .NET ou o tempo de execução do .NET no RHEL

O .NET tem suporte no RHEL. Este artigo descreve como instalar o .NET no RHEL.

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

## <a name="register-your-red-hat-subscription"></a>Registrar sua assinatura do Red Hat

Para instalar o .NET do Red Hat no RHEL, primeiro você precisa se registrar usando o Gerenciador de assinaturas do Red Hat. Se isso não tiver sido feito em seu sistema ou se você não tiver certeza, consulte a [documentação do produto Red Hat para .net](https://access.redhat.com/documentation/net/5.0/).

## <a name="supported-distributions"></a>Distribuições com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento no RHEL 7 e RHEL 8. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do RHEL não seja mais suportada.

- Um ✔️ indica que a versão do RHEL ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do RHEL ou .net não tem suporte nessa versão do RHEL.
- Quando uma versão do RHEL e uma versão do .NET têm ✔️, há suporte para essa combinação de so e .NET.

| RHEL                     | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](#rhel-8-)        | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [7](#rhel-7--net-50) | ✔️ 2,1        | ✔️ [3,1](#rhel-7--net-core-31)        | ✔️ [5,0](#rhel-7--net-50) |

Não há mais suporte para as seguintes versões do .NET. Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

## <a name="remove-preview-versions"></a>Remover versões de visualização

[!INCLUDE [package-manager uninstall notice](./includes/linux-uninstall-preview-info.md)]

## <a name="rhel-8-"></a>RHEL 8 ✔️

O .NET está incluído nos repositórios do AppStream para RHEL 8.

[!INCLUDE [linux-dnf-install-50](includes/linux-install-50-dnf.md)]

## <a name="rhel-7--net-50"></a>RHEL 7 ✔️ .NET 5,0

O comando a seguir instala o `scl-utils` pacote:

```bash
sudo yum install scl-utils
```

### <a name="install-the-sdk"></a>Instalar o SDK

O SDK do .NET permite que você desenvolva aplicativos com o .NET. Se você instalar o SDK do .NET, não precisará instalar o tempo de execução correspondente. Para instalar o SDK do .NET, execute os seguintes comandos:

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet50 -y
scl enable rh-dotnet50 bash
```

O Red Hat não recomenda a habilitação permanente `rh-dotnet50` porque pode afetar outros programas. Se você quiser habilitar `rh-dotnet` permanentemente, adicione a seguinte linha ao seu arquivo _~/.bashrc_ .

```bash
source scl_source enable rh-dotnet50
```

### <a name="install-the-runtime"></a>Instalar o runtime

O tempo de execução do .NET permite executar aplicativos que foram feitos com o .NET que não incluiu o tempo de execução. Os comandos a seguir instalam o tempo de execução de ASP.NET Core, que é o tempo de execução mais compatível para o .NET Core. Em seu terminal, execute os comandos a seguir.

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet50-aspnetcore-runtime-5.0 -y
scl enable rh-dotnet50 bash
```

O Red Hat não recomenda a habilitação permanente `rh-dotnet50` porque pode afetar outros programas. Se você quiser habilitar `rh-dotnet50` permanentemente, adicione a seguinte linha ao seu arquivo _~/.bashrc_ .

```bash
source scl_source enable rh-dotnet50
```

Como alternativa ao tempo de execução de ASP.NET Core, você pode instalar o tempo de execução do .NET que não inclui suporte a ASP.NET Core: substitua `rh-dotnet50-aspnetcore-runtime-5.0` nos comandos acima por `rh-dotnet50-dotnet-runtime-5.0` .

## <a name="rhel-7--net-core-31"></a>RHEL 7 ✔️ .NET Core 3,1

[!INCLUDE [linux-prep-intro-generic](includes/linux-prep-intro-generic.md)]

O comando a seguir instala o `scl-utils` pacote:

```bash
sudo yum install scl-utils
```

### <a name="install-the-sdk"></a>Instalar o SDK

SDK do .NET Core permite que você desenvolva aplicativos com o .NET Core. Se você instalar SDK do .NET Core, não será necessário instalar o tempo de execução correspondente. Para instalar o SDK do .NET Core, execute os seguintes comandos:

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31 -y
scl enable rh-dotnet31 bash
```

O Red Hat não recomenda a habilitação permanente `rh-dotnet31` porque pode afetar outros programas. Por exemplo, `rh-dotnet31` inclui uma versão do `libcurl` que difere da versão base do RHEL. Isso pode levar a problemas em programas que não esperam uma versão diferente do `libcurl` . Se você quiser habilitar `rh-dotnet` permanentemente, adicione a seguinte linha ao seu arquivo _~/.bashrc_ .

```bash
source scl_source enable rh-dotnet31
```

### <a name="install-the-runtime"></a>Instalar o runtime

O tempo de execução do .NET Core permite executar aplicativos que foram feitos com o .NET Core que não incluiu o tempo de execução. Os comandos a seguir instalam o tempo de execução de ASP.NET Core, que é o tempo de execução mais compatível para o .NET Core. Em seu terminal, execute os comandos a seguir.

```bash
subscription-manager repos --enable=rhel-7-server-dotnet-rpms
yum install rh-dotnet31-aspnetcore-runtime-3.1 -y
scl enable rh-dotnet31 bash
```

O Red Hat não recomenda a habilitação permanente `rh-dotnet31` porque pode afetar outros programas. Por exemplo, `rh-dotnet31` inclui uma versão do `libcurl` que difere da versão base do RHEL. Isso pode levar a problemas em programas que não esperam uma versão diferente do `libcurl` . Se você quiser habilitar `rh-dotnet31` permanentemente, adicione a seguinte linha ao seu arquivo _~/.bashrc_ .

```bash
source scl_source enable rh-dotnet31
```

Como alternativa ao tempo de execução de ASP.NET Core, você pode instalar o tempo de execução do .NET Core que não inclui suporte a ASP.NET Core: substitua `rh-dotnet31-aspnetcore-runtime-3.1` nos comandos acima por `rh-dotnet31-dotnet-runtime-3.1` .

## <a name="dependencies"></a>Dependências

[!INCLUDE [linux-rpm-install-dependencies](includes/linux-rpm-install-dependencies.md)]

## <a name="how-to-install-other-versions"></a>Como instalar outras versões

Consulte a [documentação do Red Hat para .net](https://access.redhat.com/documentation/net/5.0/) nas etapas necessárias para instalar outras versões do .net.

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
