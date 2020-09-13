---
title: dotnet-SOS-.NET Core
description: Instalando e usando a ferramenta de linha de comando dotnet-SOS.
ms.date: 08/26/2020
ms.openlocfilehash: 3ce7ca79bbc2c72958d395e9d312e3001ec9fbf8
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598322"
---
# <a name="sos-installer-dotnet-sos"></a>Instalador do SOS (dotNet-SOS)

**Este artigo aplica-se a:** ✔️ SDK do .net Core 2,1 e versões posteriores

## <a name="install-dotnet-sos"></a>Instalar dotnet-SOS

Para instalar a versão de lançamento mais recente do `dotnet-sos` [pacote NuGet](https://www.nuget.org/packages/dotnet-sos), use o comando de [instalação da ferramenta dotnet](../tools/dotnet-tool-install.md) :

```dotnetcli
dotnet tool install -g dotnet-sos
```

## <a name="synopsis"></a>Sinopse

```console
dotnet-sos [-h|--help] [options] [command]]
```

## <a name="description"></a>Descrição

A `dotnet-sos` ferramenta global instala a [extensão do depurador SOS](https://docs.microsoft.com/dotnet/framework/tools/sos-dll-sos-debugging-extension) , permitindo a [inspeção do estado do .NET Core gerenciado](https://github.com/dotnet/diagnostics/blob/master/documentation/sos-debugging-extension.md) por meio de depuradores nativos como WinDbg/CDB no Windows e Lldb no Linux e no MacOS. Observe que as versões recentes do depurador do Windows (>= versão 10.0.18317.1001 do WinDbg ou do CDB) carregarão o SOS automaticamente da Galeria de extensões da Microsoft, portanto, instalar o SOS por meio da `dotnet-sos` ferramenta só será necessário no Linux e no MacOS ou no Windows se estiver usando ferramentas de depuração mais antigas.

## <a name="options"></a>Opções

- **`--version`**

  Exibe informações de versão.

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

## <a name="dotnet-sos-install"></a>dotnet – instalação do SOS

Instala a [extensão SOS localmente](https://docs.microsoft.com/dotnet/framework/tools/sos-dll-sos-debugging-extension) para usar a depuração de processos do .NET Core. No MacOS e Linux, o arquivo. lldbinit será atualizado para que a extensão seja carregada automaticamente na inicialização do lldb. Se estiver instalando o SOS no Windows com as ferramentas de depuração mais antigas (< versão 10.0.18317.1001), será necessário carregar manualmente a extensão no WinDbg ou no CDB executando `.load %USERPROFILE%\.dotnet\sos\sos.dll` no depurador.

### <a name="synopsis"></a>Sinopse

```console
dotnet-sos install
```

## <a name="dotnet-sos-uninstall"></a>dotnet – desinstalação do SOS

Desinstala a [extensão SOS](https://docs.microsoft.com/dotnet/framework/tools/sos-dll-sos-debugging-extension) e, se estiver no Linux ou no MacOS, o removerá da configuração do lldb.

### <a name="synopsis"></a>Sinopse

```console
dotnet-sos uninstall
```
