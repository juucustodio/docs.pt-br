---
title: dotnet-ferramenta de diagnóstico do gcdump – CLI do .NET
description: Saiba como instalar e usar a ferramenta de CLI do dotnet-gcdump para coletar despejos de GC (coletor de lixo) de processos do .NET em tempo real usando o .NET EventPipe.
ms.date: 11/17/2020
ms.openlocfilehash: fe7772eed642daadbd1754627751f58d0ab57b8e
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188563"
---
# <a name="heap-analysis-tool-dotnet-gcdump"></a>Ferramenta de análise de heap (dotNet-gcdump)

**Este artigo aplica-se a:** ✔️ SDK do .net Core 3,1 e versões posteriores

## <a name="install"></a>Instalar

Há duas maneiras de baixar e instalar `dotnet-gcdump` :

- **ferramenta global dotnet:**

  Para instalar a versão de lançamento mais recente do `dotnet-gcdump` [pacote NuGet](https://www.nuget.org/packages/dotnet-gcdump), use o comando de [instalação da ferramenta dotnet](../tools/dotnet-tool-install.md) :

  ```dotnetcli
  dotnet tool install --global dotnet-gcdump
  ```

- **Download direto:**

  Baixe o executável da ferramenta que corresponde à sua plataforma:

  | Sistema operacional  | Plataforma |
  | --- | -------- |
  | Windows | [x86](https://aka.ms/dotnet-gcdump/win-x86) \| [x64](https://aka.ms/dotnet-gcdump/win-x64) \| [ARM](https://aka.ms/dotnet-gcdump/win-arm) \| [ARM-x64](https://aka.ms/dotnet-gcdump/win-arm64) |
  | macOS   | [x64](https://aka.ms/dotnet-gcdump/osx-x64) |
  | Linux   | [x64](https://aka.ms/dotnet-gcdump/linux-x64) \| [ARM](https://aka.ms/dotnet-gcdump/linux-arm) \| [arm64](https://aka.ms/dotnet-gcdump/linux-arm64) \| [MUSL-x64](https://aka.ms/dotnet-gcdump/linux-musl-x64) \| [MUSL-arm64](https://aka.ms/dotnet-gcdump/linux-musl-arm64) |

> [!NOTE]
> Para usar `dotnet-gcdump` o em um aplicativo x86, você precisa de uma versão x86 correspondente da ferramenta.

## <a name="synopsis"></a>Sinopse

```console
dotnet-gcdump [-h|--help] [--version] <command>
```

## <a name="description"></a>Descrição

A `dotnet-gcdump` ferramenta global coleta despejos GC (coletor de lixo) de processos do Live .NET usando o [EventPipe](./eventpipe.md). Os despejos de GC são criados disparando um GC no processo de destino, ativando eventos especiais e regenerando o grafo de raízes de objeto a partir do fluxo de eventos. Esse processo permite que os despejos de GC sejam coletados enquanto o processo está em execução e com sobrecarga mínima. Esses despejos são úteis para vários cenários:

- Comparando o número de objetos no heap em vários pontos no tempo.
- Análise de raízes de objetos (respondendo a perguntas como "o que ainda tem uma referência a esse tipo?").
- Coletando estatísticas gerais sobre as contagens de objetos no heap.

### <a name="view-the-gc-dump-captured-from-dotnet-gcdump"></a>Exibir o despejo de GC capturado de dotnet-gcdump

No Windows, `.gcdump` os arquivos podem ser exibidos no [Perfview](https://github.com/microsoft/perfview) para análise ou no Visual Studio. Atualmente, não há nenhuma maneira de abrir um `.gcdump` em plataformas não Windows.

Você pode coletar vários `.gcdump` s e abri-los simultaneamente no Visual Studio para obter uma experiência de comparação.

## <a name="options"></a>Opções

- **`--version`**

  Exibe a versão do `dotnet-gcdump` Utilitário do.

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

## `dotnet-gcdump collect`

Coleta um despejo de GC de um processo em execução no momento.

> [!WARNING]
> Para percorrer o heap de GC, esse comando dispara uma coleta de lixo de geração 2 (completa), que pode suspender o tempo de execução por um longo tempo, especialmente quando o heap de GC for grande. Não use esse comando em ambientes sensíveis ao desempenho quando o heap de GC for grande.

### <a name="synopsis"></a>Sinopse

```console
dotnet-gcdump collect [-h|--help] [-p|--process-id <pid>] [-o|--output <gcdump-file-path>] [-v|--verbose] [-t|--timeout <timeout>] [-n|--name <name>]
```

### <a name="options"></a>Opções

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

- **`-p|--process-id <pid>`**

  A ID do processo para coletar o despejo do GC.

- **`-o|--output <gcdump-file-path>`**

  O caminho onde os despejos de GC coletados devem ser gravados. O padrão é *. \\ AAAAMMDD \_ HHMMSS \_ \<pid> . gcdump*.

- **`-v|--verbose`**

  Gere o log durante a coleta do despejo do GC.

- **`-t|--timeout <timeout>`**

  Desistir da coleta do despejo do GC se levar mais tempo do que esse número de segundos. O valor padrão é 30.

- **`-n|--name <name>`**

  O nome do processo do qual coletar o despejo do GC.

> [!NOTE]
> No Linux e no macOS, esse comando espera o aplicativo de destino e `dotnet-gcdump` compartilha a mesma `TMPDIR` variável de ambiente. Caso contrário, o comando atingirá o tempo limite.

> [!NOTE]
> Para coletar um despejo de GC usando `dotnet-gcdump` o, ele precisa ser executado como o mesmo usuário que o usuário que está executando o processo de destino ou como raiz. Caso contrário, a ferramenta não conseguirá estabelecer uma conexão com o processo de destino.

## `dotnet-gcdump ps`

Lista os processos dotnet para os quais os despejos de GC podem ser coletados.

### <a name="synopsis"></a>Sinopse

```console
dotnet-gcdump ps
```

## `dotnet-gcdump report <gcdump_filename>`

Gere um relatório de um despejo GC gerado anteriormente ou de um processo em execução e grave no `stdout` .

### <a name="synopsis"></a>Sinopse

```console
dotnet-gcdump report [-h|--help] [-p|--process-id <pid>] [-t|--report-type <HeapStat>]
```

### <a name="options"></a>Opções

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

- **`-p|--process-id <pid>`**

  A ID do processo para coletar o despejo do GC.

- **`-t|--report-type <HeapStat>`**

  O tipo de relatório a ser gerado. Opções disponíveis: heapstat (padrão).

## <a name="troubleshoot"></a>Solução de problemas

- Não há nenhuma informação de tipo no gcdump.

   Antes do .NET Core 3,1, houve um problema em que um cache de tipo não foi limpo entre gcdumps quando eles eram invocados com EventPipe. Isso resultou nos eventos necessários para determinar as informações de tipo que não estão sendo enviadas para o segundo e o gcdumps subsequente. Isso foi corrigido no .NET Core 3,1-Preview2.

- Os tipos COM e estáticos não estão no despejo de GC.

   Antes do .NET Core 3,1-Preview2, houve um problema em que os tipos static e COM não eram enviados quando o despejo de GC era invocado via EventPipe. Isso foi corrigido no .NET Core 3,1-Preview2.
