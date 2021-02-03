---
title: Instalar o .NET em distribuições do Linux
description: Saiba mais sobre o que as distribuições do Linux dão suporte à instalação do .NET no Linux.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 27be7151d95810d8cc607564d5c0ce8dfe5b9ed8
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506273"
---
# <a name="install-net-on-linux"></a>Instalar o .NET no Linux

> [!div class="op_single_selector"]
>
> - [Instalar no Windows](windows.md)
> - [Instalar no macOS](macos.md)
> - [Instalar no Linux](linux.md)

O .NET está disponível em diferentes distribuições do Linux. A maioria das plataformas e distribuições do Linux tem uma versão principal a cada ano, e a maioria fornece um Gerenciador de pacotes que é usado para instalar o .NET. Este artigo descreve o que tem suporte no momento e qual Gerenciador de pacotes é usado.

O restante deste artigo é uma análise de cada grande distribuição do Linux com suporte do .NET. Todas as versões do .NET permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a distribuição do Linux atinja o fim da vida útil.

Para obter a melhor compatibilidade, escolha uma versão de LTS (versão de longo prazo).

## <a name="unsupported-releases"></a>Versões sem suporte

Não há mais suporte para as seguintes versões do .NET ❌ . Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

Essas versões sem suporte não são detalhadas nas seções abaixo e sua quilometragem pode variar se você tentar instalá-las.

## <a name="manual-installation"></a>Instalação manual

Se você não quiser usar um Gerenciador de pacotes para instalar o .NET no Linux, poderá instalar o .NET de uma das seguintes maneiras:

- [Ajustar pacote](linux-snap.md)
- [Instalação com script com _install-dotnet.sh_](linux-scripted-manual.md#scripted-install)
- [Extração binária manual](linux-scripted-manual.md#manual-install)

Certifique-se de verificar a página de distribuição apropriada para obter mais informações sobre as dependências necessárias que podem estar ausentes ao fazer uma instalação manual.

## <a name="alpine"></a>Alpine

A tabela a seguir é uma lista de versões do .NET com suporte no momento e as versões do Alpine para as quais têm suporte. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do [Alpine alcance o fim da vida útil](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Releases).

- Um ✔️ indica que a versão do Alpine ou .NET ainda tem suporte.
- Um ❌ indica que a versão do Alpine ou do .net não tem suporte nessa versão do Alpine.
- Quando uma versão do Alpine e uma versão do .NET têm ✔️, há suporte para essa combinação de so e .NET.

| Alpine                      | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|-----------------------------|---------------|---------------|----------------|
| ✔️ [3,12](linux-alpine.md)  | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [3,11](linux-alpine.md)  | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [3,10](linux-alpine.md)  | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |
| ❌ [3.9](linux-alpine.md)   | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |
| ❌ [3.8](linux-alpine.md)   | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |

Para obter mais informações, consulte [install .net on Alpine](linux-alpine.md).

## <a name="centos"></a>CentOS

O CentOS 7 usa o yum como um Gerenciador de pacotes e o CentOS 8 usa o DNF.

A tabela a seguir é uma lista de versões do .NET com suporte no momento no CentOS 7 e no CentOS 8. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do CentOS não seja mais suportada.

| CentOS                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](linux-centos.md#centos-8-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [7](linux-centos.md#centos-7-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |

Para obter mais informações, consulte [instalar o .net no CentOS](linux-centos.md).

## <a name="debian"></a>Debian

Debian usa APT (ferramenta de pacote avançado) como um Gerenciador de pacotes.

A tabela a seguir é uma lista de versões do .NET com suporte no momento e as versões do Debian nas quais elas têm suporte. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do [Debian atinja o fim da vida útil](https://wiki.debian.org/DebianReleases).

- Um ✔️ indica que a versão do Debian ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do Debian ou do .net não tem suporte nessa versão do Debian.
- Quando uma versão do Debian e uma versão do .NET têm ✔️, essa combinação de so e .NET é suportada.

| Debian                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [10](linux-debian.md#debian-10-)     | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [9](linux-debian.md#debian-9-)       | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ❌[8](linux-debian.md#debian-8-)       | ✔️ 2,1        | ❌ 3,1        | ❌ 5,0 |

Para obter mais informações, consulte [instalar o .net no Debian](linux-debian.md).

## <a name="fedora"></a>Fedora

Fedora usa DNF como seu Gerenciador de pacotes.

A tabela a seguir é uma lista de versões do .NET com suporte no momento e as versões do Fedora em que têm suporte. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do [Fedora atinja o fim da vida útil](https://fedoraproject.org/wiki/End_of_life).

- Um ✔️ indica que a versão do Fedora ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do Fedora ou do .net não tem suporte nessa versão do Fedora.
- Quando uma versão do Fedora e uma versão do .NET têm ✔️, há suporte para essa combinação de so e .NET.

| Fedora                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [33](linux-fedora.md#install-net-50) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [32](linux-fedora.md#install-net-50) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ❌[31](linux-fedora.md#install-on-older-distributions) | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |
| ❌[30](linux-fedora.md#install-on-older-distributions) | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |
| ❌[29](linux-fedora.md#install-on-older-distributions) | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |
| ❌[28](linux-fedora.md#install-on-older-distributions) | ✔️ 2,1        | ❌ 3,1        | ❌ 5,0 |
| ❌[27](linux-fedora.md#install-on-older-distributions) | ✔️ 2,1        | ❌ 3,1        | ❌ 5,0 |

Para obter mais informações, consulte [install .net on Fedora](linux-fedora.md).

## <a name="opensuse"></a>openSUSE

openSUSE usa zypper como o Gerenciador de pacotes.

A tabela a seguir é uma lista de versões do .NET com suporte no momento no openSUSE 15. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do openSUSE não seja mais suportada.

| openSUSE                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|----------------------------|---------------|---------------|----------------|
| ✔️ [15](linux-opensuse.md#opensuse-15-)     | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |

Para obter mais informações, consulte [install .net on openSUSE](linux-opensuse.md).

## <a name="red-hat"></a>Red Hat

Red Hat Enterprise Linux (RHEL) usa yum (RHEL 7) e DNF (RHEL 8) como o Gerenciador de pacotes.

A tabela a seguir é uma lista de versões do .NET com suporte no momento no RHEL 7 e RHEL 8. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do RHEL não seja mais suportada.

- Um ✔️ indica que a versão do RHEL ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do RHEL ou .net não tem suporte nessa versão do RHEL.
- Quando uma versão do RHEL e uma versão do .NET têm ✔️, há suporte para essa combinação de so e .NET.

| RHEL                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [8](linux-rhel.md#rhel-8-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [7](linux-rhel.md#rhel-7--net-50) | ✔️ 2,1        | ✔️ [3,1](linux-rhel.md#rhel-7--net-core-31)        | ✔️ [5,0](linux-rhel.md#rhel-7--net-50) |

Para obter mais informações, consulte [instalar o .net no RHEL](linux-rhel.md).

## <a name="sles"></a>SLES

O SLES usa zypper como o Gerenciador de pacotes.

A tabela a seguir é uma lista de versões do .NET com suporte no momento no SLES 12 SP2 e no SLES 15. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do SLES não seja mais suportada.

- Um ✔️ indica que a versão do SLES ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do SLES ou do .net não tem suporte nessa versão do SLES.
- Quando uma versão do SLES e uma versão do .NET têm ✔️, essa combinação de so e .NET é suportada.

| SLES                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|------------------------|---------------|---------------|----------------|
| ✔️ [15](linux-sles.md#sles-15-)     | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [12 SP2](linux-sles.md#sles-12-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |

Para obter mais informações, consulte [instalar o .net no SLES](linux-sles.md).

## <a name="ubuntu"></a>Ubuntu

O Ubuntu usa a APT (ferramenta de pacote avançado) como um Gerenciador de pacotes.

A tabela a seguir representa o status de suporte do Ubuntu e do .NET.

- Um ✔️ indica que a versão do Ubuntu ou do .NET ainda tem suporte.
- Um ❌ indica que a versão do Ubuntu ou do .net não tem suporte nessa versão do Ubuntu.
- Quando uma versão do Ubuntu e uma versão do .NET têm ✔️, essa combinação de so e .NET é suportada.

| Ubuntu                   | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|--------------------------|---------------|---------------|----------------|
| ✔️ [20,10](linux-ubuntu.md#2010-)       | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ [20, 4 (LTS)](linux-ubuntu.md#2004-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ❌[19,10](linux-ubuntu.md#1910-)       | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ❌[19, 4](linux-ubuntu.md#1904-)       | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |
| ❌[18,10](linux-ubuntu.md#1810-)       | ✔️ 2,1        | ❌ 3,1        | ❌ 5,0 |
| ✔️ [18, 4 (LTS)](linux-ubuntu.md#1804-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ❌ [17.10](linux-ubuntu.md#1710-)       | ✔️ 2,1        | ❌ 3,1        | ❌ 5,0 |
| ❌ [17.04](linux-ubuntu.md#1704-)       | ✔️ 2,1        | ❌ 3,1        | ❌ 5,0 |
| ❌[16,10](linux-ubuntu.md#1610-)       | ❌ 2,1        | ❌ 3,1        | ❌ 5,0 |
| ✔️ [16, 4 (LTS)](linux-ubuntu.md#1604-) | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |

Para obter mais informações, consulte [instalar o .net no Ubuntu](linux-ubuntu.md).

## <a name="next-steps"></a>Próximas etapas

- [Como verificar se o .net já está instalado](how-to-detect-installed-versions.md?pivots=os-linux).
- [Tutorial: criar um novo aplicativo com Visual Studio Code](../tutorials/with-visual-studio-code.md).
- [Tutorial: colocar um aplicativo .net em contêiner](../docker/build-container.md).
