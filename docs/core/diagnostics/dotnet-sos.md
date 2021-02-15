---
title: dotnet – ferramenta de diagnóstico do SOS-CLI do .NET
description: Saiba como instalar e usar a ferramenta dotnet-SOS CLI para gerenciar a extensão do depurador SOS, que é usada com depuradores nativos no Windows e no Linux.
ms.date: 11/17/2020
ms.openlocfilehash: 09e8228c47bdc632bccf3c9ad2296d55fe420060
ms.sourcegitcommit: c0b803bffaf101e12f071faf94ca21b46d04ff30
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97765001"
---
# <a name="sos-installer-dotnet-sos"></a>Instalador do SOS (dotNet-SOS)

**Este artigo aplica-se a:** ✔️ SDK do .net Core 2,1 e versões posteriores

## <a name="install"></a>Instalar

Há duas maneiras de baixar e instalar `dotnet-sos` :

- **ferramenta global dotnet:**

  Para instalar a versão de lançamento mais recente do `dotnet-sos` [pacote NuGet](https://www.nuget.org/packages/dotnet-sos), use o comando de [instalação da ferramenta dotnet](../tools/dotnet-tool-install.md) :

  ```dotnetcli
  dotnet tool install --global dotnet-sos
  ```

- **Download direto:**

  Baixe o executável da ferramenta que corresponde à sua plataforma:

  | Sistema operacional  | Plataforma |
  | --- | -------- |
  | Windows | [x86](https://aka.ms/dotnet-sos/win-x86) \| [x64](https://aka.ms/dotnet-sos/win-x64) \| [ARM](https://aka.ms/dotnet-sos/win-arm) \| [ARM-x64](https://aka.ms/dotnet-sos/win-arm64) |
  | macOS   | [x64](https://aka.ms/dotnet-sos/osx-x64) |
  | Linux   | [x64](https://aka.ms/dotnet-sos/linux-x64) \| [ARM](https://aka.ms/dotnet-sos/linux-arm) \| [arm64](https://aka.ms/dotnet-sos/linux-arm64) \| [MUSL-x64](https://aka.ms/dotnet-sos/linux-musl-x64) \| [MUSL-arm64](https://aka.ms/dotnet-sos/linux-musl-arm64) |

## <a name="synopsis"></a>Sinopse

```console
dotnet-sos [-h|--help] [options] [command]]
```

## <a name="description"></a>Descrição

A `dotnet-sos` ferramenta global instala a [extensão do depurador SOS](sos-debugging-extension.md). Essa extensão permite inspecionar o estado do .NET Core gerenciado a partir de depuradores nativos, como lldb e WinDbg.

> [!NOTE]
> A instalação do SOS por meio da `dotnet-sos` ferramenta só é necessária no Linux ou no MacOS.  Ele também pode ser necessário no Windows se você estiver usando ferramentas de depuração mais antigas. As versões recentes do [depurador do Windows](/windows-hardware/drivers/debugger/debugger-download-tools) (>= versão 10.0.18317.1001 do WinDbg ou do CDB) carregam o SOS automaticamente da Galeria de extensões da Microsoft.  

## <a name="options"></a>Opções

- **`--version`**

  Exibe informações de versão.

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

## <a name="dotnet-sos-install"></a>dotnet – instalação do SOS

Instala a [extensão SOS](sos-debugging-extension.md) localmente para depurar processos do .NET Core. No macOS e Linux, o arquivo *. lldbinit* será atualizado para que a extensão seja carregada automaticamente na inicialização do lldb. Se você estiver instalando o SOS no Windows com as ferramentas de depuração mais antigas (antes da versão 10.0.18317.1001), será necessário carregar manualmente a extensão no WinDbg ou no CDB executando `.load %USERPROFILE%\.dotnet\sos\sos.dll` no depurador.

### <a name="synopsis"></a>Sinopse

```console
dotnet-sos install [--architecture <arch>]
```

### <a name="options"></a>Opções

- **`--architecture <arch>`**

  Especifica a arquitetura do processador dos binários SOS a serem instalados. Por padrão, `dotnet-sos` o instala a arquitetura do computador host. Use essa opção quando quiser instalar o SOS para uma arquitetura diferente da arquitetura de host dotnet. Por exemplo, se você estiver executando binários Arm32 de um host Arm64, será necessário instalar o SOS com o `dotnet-sos install --architecture Arm` .

  As arquiteturas a seguir estão disponíveis:

  - `Arm`
  - `Arm64`
  - `X86`
  - `X64`

## <a name="dotnet-sos-uninstall"></a>dotnet – desinstalação do SOS

Desinstala a [extensão SOS](sos-debugging-extension.md) e, no Linux e MacOS, remove-a da configuração do lldb.

### <a name="synopsis"></a>Sinopse

```console
dotnet-sos uninstall
```
