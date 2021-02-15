---
title: Instalar o .NET no Alpine-.NET
description: Demonstra as várias maneiras de instalar o SDK do .NET e o tempo de execução do .NET na Alpine.
author: adegeo
ms.author: adegeo
ms.date: 01/06/2021
ms.openlocfilehash: 6adaa905c400b45526ebbc3d8e2606522863eec3
ms.sourcegitcommit: 7ef96827b161ef3fcde75f79d839885632e26ef1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/07/2021
ms.locfileid: "97970844"
---
# <a name="install-the-net-sdk-or-the-net-runtime-on-alpine"></a>Instalar o SDK do .NET ou o tempo de execução do .NET em Alpine Ski

Este artigo descreve como instalar o .NET em Alpine Ski. Quando uma versão do Alpineio ficar sem suporte, o .NET não terá mais suporte com essa versão. No entanto, essas instruções podem ajudá-lo a obter o .NET em execução nessas versões, mesmo que não haja suporte.

[!INCLUDE [linux-intro-sdk-vs-runtime](includes/linux-intro-sdk-vs-runtime.md)]

## <a name="install"></a>Instalar

Instaladores não estão disponíveis para o Alpine Linux. Você deve instalar o .NET de uma das seguintes maneiras:

- [Ajustar pacote](linux-snap.md)
- [Instalação com script com _install-dotnet.sh_](linux-scripted-manual.md#scripted-install)
- [Extração binária manual](linux-scripted-manual.md#manual-install)

## <a name="supported-distributions"></a>Distribuições com suporte

A tabela a seguir é uma lista de versões do .NET com suporte no momento e as versões do Alpine para as quais têm suporte. Essas versões permanecem com suporte até que a versão do [.net atinja o fim do suporte](https://dotnet.microsoft.com/platform/support/policy/dotnet-core) ou a versão do [Alpine alcance o fim da vida útil](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Releases).

- Um ✔️ indica que a versão do Alpine ou .NET ainda tem suporte.
- Um ❌ indica que a versão do Alpine ou do .net não tem suporte nessa versão do Alpine.
- Quando uma versão do Alpine e uma versão do .NET têm ✔️, há suporte para essa combinação de so e .NET.

| Alpine  | .NET Core 2.1 | .NET Core 3.1 | .NET 5.0 |
|-------- |---------------|---------------|----------------|
| ✔️ 3,12 | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ 3,11 | ✔️ 2,1        | ✔️ 3,1        | ✔️ 5,0 |
| ✔️ 3,10 | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |
| ❌ 3,9  | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |
| ❌ 3,8  | ✔️ 2,1        | ✔️ 3,1        | ❌ 5,0 |

Não há mais suporte para as seguintes versões do .NET. Os downloads para eles ainda permanecem publicados:

- 3.0
- 2.2
- 2,0

## <a name="dependencies"></a>Dependências

O .NET no Alpineum Linux requer as seguintes dependências instaladas:

- ICU-bibliotecas
- krb5-libs
- libgcc
- libintl
- libssl 1.1 (Alpine v 3.9 ou superior)
- libssl 1.0 (Alpine v 3.8 ou inferior)
- libstdc++
- zlib

## <a name="next-steps"></a>Próximas etapas

- [Como habilitar o preenchimento com TAB para a CLI do .NET](../tools/enable-tab-autocomplete.md)
- [Tutorial: criar um aplicativo de console com o SDK do .NET usando o Visual Studio Code](../tutorials/with-visual-studio-code.md)
