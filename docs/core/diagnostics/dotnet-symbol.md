---
title: dotnet-ferramenta de diagnóstico de símbolo-CLI do .NET
description: Saiba como instalar e usar a ferramenta dotnet-Symbol CLI para baixar arquivos necessários para depurar despejos e minidespejos do .NET.
ms.date: 11/17/2020
ms.openlocfilehash: 69c05544e886d9d41113c8a2383f760b85d01124
ms.sourcegitcommit: c0b803bffaf101e12f071faf94ca21b46d04ff30
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/24/2020
ms.locfileid: "97764988"
---
# <a name="symbol-downloader-dotnet-symbol"></a>Downloader de símbolos (dotNet-Symbol)

**Este artigo aplica-se a:** ✔️ SDK do .net Core 2,1 e versões posteriores

## <a name="install"></a>Instalar

Para instalar a versão de lançamento mais recente do `dotnet-symbol` [pacote NuGet](https://www.nuget.org/packages/dotnet-symbol), use o comando de [instalação da ferramenta dotnet](../tools/dotnet-tool-install.md) :

```dotnetcli
dotnet tool install --global dotnet-symbol
```

## <a name="synopsis"></a>Sinopse

```console
dotnet-symbol [-h|--help] [options] <FILES>
```

## <a name="description"></a>Descrição

A `dotnet-symbol` ferramenta global baixa arquivos (símbolos, DAC, módulos, etc.) necessários para depurar dumps principais e minidespejos. Isso pode ser útil ao depurar despejos capturados em outro computador. `dotnet-symbol` pode baixar módulos e símbolos necessários para analisar o despejo.

## <a name="options"></a>Opções

- **`--microsoft-symbol-server`**

  Adicione ' http://msdl.microsoft.com/download/symbols ' caminho do servidor de símbolo (padrão).

- **`--server-path <symbol server path>`**

  Adicione um servidor de símbolos ao caminho do servidor.

- **`authenticated-server-path <pat> <server path>`**

  Adicione um servidor de símbolos autenticado ao caminho do servidor usando um PAT (token de acesso pessoal).

- **`--cache-directory <file cache directory>`**

  Adiciona um diretório de cache.

- **`--recurse-subdirectories`**

  Processar arquivos de entrada em todos os subdiretórios.

- **`--host-only`**

  Baixe apenas o programa host (ou seja, dotnet) que o lldb precisa para carregar os dumps principais.

- **`--symbols`**

  Baixar arquivos de símbolo (. pdb,. dbg,. Dwarf).

- **`--modules`**

  Baixe os arquivos de módulo (. dll,. so,. dylib).

- **`--debugging`**

  Baixe os módulos de depuração especiais (DAC, DBI, SOS).

- **`--windows-pdbs`**

  Force o download dos PDBs do Windows quando PDBs portáteis também estão disponíveis.

- **`-o, --output <output directory>`**

  Defina o diretório de saída. Caso contrário, escreva ao lado do arquivo de entrada (padrão).

- **`-d, --diagnostics`**

  Habilite a saída de diagnóstico.

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

## <a name="download-symbols"></a>Baixar símbolos

`dotnet-symbol`A execução em um arquivo de despejo, por padrão, baixará todos os módulos, símbolos e arquivos DAC/DBI necessários para depurar o despejo, incluindo os assemblies gerenciados. Como o SOS agora pode baixar símbolos quando necessário, a maioria dos despejos de núcleo do Linux pode ser analisada usando lldb apenas com o host (dotnet) e os módulos de depuração. Para obter esses arquivos necessários para diagnosticar um dump principal com lldb, execute:

```console
dotnet-symbol --host-only --debugging <dump file path>
```

## <a name="troubleshoot"></a>Solucionar problemas

- 404 não encontrado ao baixar símbolos.

   O download de símbolo só tem suporte em versões oficiais do .NET Core Runtime adquiridas por meio de canais oficiais, como [o site oficial](https://dotnet.microsoft.com/download/dotnet-core) e as [fontes padrão nos scripts de instalação dotnet](../tools/dotnet-install-script.md). Um erro 404 ao baixar arquivos de depuração pode indicar que o despejo foi criado com um tempo de execução do .NET Core de outra fonte, como um compilado da origem localmente ou para um distribuição Linux específico ou de sites da Comunidade como Archlinux. Nesses casos, o arquivo necessário para depuração (dotNet, libcoreclr.so e libmscordaccore.so) deve ser copiado dessas fontes ou do ambiente no qual o arquivo de despejo foi criado.

## <a name="see-also"></a>Veja também

* [Depurando com símbolos](/windows/win32/dxtecharts/debugging-with-symbols)
* [PDBs portáteis](https://github.com/dotnet/core/blob/master/Documentation/diagnostics/portable_pdb.md)
