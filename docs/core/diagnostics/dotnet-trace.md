---
title: dotnet-ferramenta de diagnóstico de rastreamento-CLI do .NET
description: Saiba como instalar e usar a ferramenta de CLI de rastreamento dotnet para coletar rastreamentos do .NET de um processo em execução sem o criador de perfil nativo, usando o .NET EventPipe.
ms.date: 11/17/2020
ms.openlocfilehash: 93698882e94f58eda84abebc277e1eacfe22a3da
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98189692"
---
# <a name="dotnet-trace-performance-analysis-utility"></a>dotnet-utilitário de análise de desempenho de rastreamento

**Este artigo aplica-se a:** ✔️ SDK do .net Core 3,0 e versões posteriores

## <a name="install"></a>Instalar

Há duas maneiras de baixar e instalar `dotnet-trace` :

- **ferramenta global dotnet:**

  Para instalar a versão de lançamento mais recente do `dotnet-trace` [pacote NuGet](https://www.nuget.org/packages/dotnet-trace), use o comando de [instalação da ferramenta dotnet](../tools/dotnet-tool-install.md) :

  ```dotnetcli
  dotnet tool install --global dotnet-trace
  ```

- **Download direto:**

  Baixe o executável da ferramenta que corresponde à sua plataforma:

  | Sistema operacional  | Plataforma |
  | --- | -------- |
  | Windows | [x86](https://aka.ms/dotnet-trace/win-x86) \| [x64](https://aka.ms/dotnet-trace/win-x64) \| [ARM](https://aka.ms/dotnet-trace/win-arm) \| [ARM-x64](https://aka.ms/dotnet-trace/win-arm64) |
  | macOS   | [x64](https://aka.ms/dotnet-trace/osx-x64) |
  | Linux   | [x64](https://aka.ms/dotnet-trace/linux-x64) \| [ARM](https://aka.ms/dotnet-trace/linux-arm) \| [arm64](https://aka.ms/dotnet-trace/linux-arm64) \| [MUSL-x64](https://aka.ms/dotnet-trace/linux-musl-x64) \| [MUSL-arm64](https://aka.ms/dotnet-trace/linux-musl-arm64) |

> [!NOTE]
> Para usar `dotnet-trace` o em um aplicativo x86, você precisa de uma versão x86 correspondente da ferramenta.

## <a name="synopsis"></a>Sinopse

```console
dotnet-trace [-h, --help] [--version] <command>
```

## <a name="description"></a>Descrição

A `dotnet-trace` ferramenta:

* É uma ferramenta .NET Core de plataforma cruzada.
* Habilita a coleção de rastreamentos do .NET Core de um processo em execução sem um criador de perfil nativo.
* É criado [`EventPipe`](./eventpipe.md) a partir do tempo de execução do .NET Core.
* Oferece a mesma experiência no Windows, Linux ou macOS.

## <a name="options"></a>Opções

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

- **`--version`**

  Exibe a versão do utilitário dotnet-Trace.

## <a name="commands"></a>Comandos

| Comando                                                   |
|-----------------------------------------------------------|
| [dotnet-coleta de rastreamento](#dotnet-trace-collect)             |
| [dotnet-conversão de rastreamento](#dotnet-trace-convert)             |
| [dotnet-rastrear PS](#dotnet-trace-ps)                       |
| [dotnet-lista de rastreamento-perfis](#dotnet-trace-list-profiles) |

## <a name="dotnet-trace-collect"></a>dotnet-coleta de rastreamento

Coleta um rastreamento de diagnóstico de um processo em execução.

### <a name="synopsis"></a>Sinopse

```console
dotnet-trace collect [--buffersize <size>] [--clreventlevel <clreventlevel>] [--clrevents <clrevents>]
    [--format <Chromium|NetTrace|Speedscope>] [-h|--help]
    [-n, --name <name>] [--diagnostic-port] [-o|--output <trace-file-path>] [-p|--process-id <pid>]
    [--profile <profile-name>] [--providers <list-of-comma-separated-providers>]
    [-- <command>] (for target applications running .NET 5.0 or later)
```

### <a name="options"></a>Opções

- **`--buffersize <size>`**

  Define o tamanho do buffer circular na memória, em megabytes. 256 MB padrão.

- **`--clreventlevel <clreventlevel>`**

  Detalhes dos eventos CLR a serem emitidos.

- **`--clrevents <clrevents>`**

  Uma lista de palavras-chave do provedor de tempo de execução do CLR para habilitar a separação por `+` sinais. Esse é um mapeamento simples que permite especificar palavras-chave de evento por meio de aliases de cadeia de caracteres em vez de seus valores hexadecimais. Por exemplo, `dotnet-trace collect --providers Microsoft-Windows-DotNETRuntime:3:4` solicita o mesmo conjunto de eventos que `dotnet-trace collect --clrevents gc+gchandle --clreventlevel informational` . A tabela a seguir mostra a lista de palavras-chave disponíveis:

  | Alias de cadeia de palavra-chave | Valor hexadecimal da palavra-chave |
  | ------------ | ------------------- |
  | `gc` | `0x1` |
  | `gchandle` | `0x2` |
  | `fusion` | `0x4` |
  | `loader` | `0x8` |
  | `jit` | `0x10` |
  | `ngen` | `0x20` |
  | `startenumeration` | `0x40` |
  | `endenumeration` | `0x80` |
  | `security` | `0x400` |
  | `appdomainresourcemanagement` | `0x800` |
  | `jittracing` | `0x1000` |
  | `interop` | `0x2000` |
  | `contention` | `0x4000` |
  | `exception` | `0x8000` |
  | `threading` | `0x10000` |
  | `jittedmethodiltonativemap` | `0x20000` |
  | `overrideandsuppressngenevents` | `0x40000` |
  | `type` | `0x80000` |
  | `gcheapdump` | `0x100000` |
  | `gcsampledobjectallocationhigh` | `0x200000` |
  | `gcheapsurvivalandmovement` | `0x400000` |
  | `gcheapcollect` | `0x800000` |
  | `gcheapandtypenames` | `0x1000000` |
  | `gcsampledobjectallocationlow` | `0x2000000` |
  | `perftrack` | `0x20000000` |
  | `stack` | `0x40000000` |
  | `threadtransfer` | `0x80000000` |
  | `debugger` | `0x100000000` |
  | `monitoring` | `0x200000000` |
  | `codesymbols` | `0x400000000` |
  | `eventsource` | `0x800000000` |
  | `compilation` | `0x1000000000` |
  | `compilationdiagnostic` | `0x2000000000` |
  | `methoddiagnostic` | `0x4000000000` |
  | `typediagnostic` | `0x8000000000` |

  Você pode ler sobre o provedor CLR mais detalhadamente na [documentação de referência do provedor de tempo de execução do .net](../../fundamentals/diagnostics/runtime-events.md).

- **`--format {Chromium|NetTrace|Speedscope}`**

  Define o formato de saída para a conversão do arquivo de rastreamento. O padrão é `NetTrace`.

- **`-n, --name <name>`**

  O nome do processo do qual coletar o rastreamento.

- **`--diagnostic-port <path-to-port>`**

  O nome da porta de diagnóstico a ser criada. Consulte [usar a porta de diagnóstico para coletar um rastreamento da inicialização do aplicativo](#use-diagnostic-port-to-collect-a-trace-from-app-startup) para saber como usar essa opção para coletar um rastreamento da inicialização do aplicativo.

- **`-o|--output <trace-file-path>`**

  O caminho de saída para os dados de rastreamento coletados. Se não for especificado, o padrão será `trace.nettrace` .

- **`-p|--process-id <PID>`**

  A ID do processo da qual coletar o rastreamento.

- **`--profile <profile-name>`**

  Um conjunto nomeado predefinido de configurações de provedor que permite que cenários de rastreamento comuns sejam especificados de forma sucinta. Os seguintes perfis estão disponíveis:

 | Perfil | Descrição |
 |---------|-------------|
 |`cpu-sampling`|Útil para controlar o uso da CPU e informações gerais de tempo de execução do .NET. Essa será a opção padrão se nenhum perfil ou provedor for especificado.|
 |`gc-verbose`|Rastreia coleções de GC e as alocações de objeto de exemplos.|
 |`gc-collect`|Rastreia coleções de GC somente em sobrecarga muito baixa.|

- **`--providers <list-of-comma-separated-providers>`**

  Uma lista separada por vírgulas de `EventPipe` provedores a serem habilitados. Esses provedores complementam todos os provedores implícitos pelo `--profile <profile-name>` . Se houver alguma inconsistência para um provedor específico, essa configuração terá precedência sobre a configuração implícita do perfil.

  Esta lista de provedores está no formato:

  - `Provider[,Provider]`
  - `Provider` está no formato: `KnownProviderName[:Flags[:Level][:KeyValueArgs]]` .
  - `KeyValueArgs` está no formato: `[key1=value1][;key2=value2]` .

- **`-- <command>` (somente para aplicativos de destino que executam o .NET 5,0)**

  Após os parâmetros de configuração da coleção, o usuário pode acrescentar `--` seguido por um comando para iniciar um aplicativo .NET com pelo menos um tempo de execução de 5,0. Isso pode ser útil ao diagnosticar problemas que ocorrem no início do processo, como problemas de desempenho de inicialização ou carregador de assembly e erros de fichário.

  > [!NOTE]
  > O uso dessa opção monitora o primeiro processo do .NET 5,0 que se comunica de volta à ferramenta, o que significa que, se o comando iniciar vários aplicativos .NET, ele só coletará o primeiro aplicativo. Portanto, é recomendável usar essa opção em aplicativos independentes ou usando a `dotnet exec <app.dll>` opção.

> [!NOTE]
> Parar o rastreamento pode levar muito tempo (até minutos) para aplicativos grandes. O tempo de execução precisa enviar pelo cache de tipo para todo o código gerenciado que foi capturado no rastreamento.

> [!NOTE]
> No Linux e no macOS, esse comando espera o aplicativo de destino e `dotnet-trace` compartilha a mesma `TMPDIR` variável de ambiente. Caso contrário, o comando atingirá o tempo limite.

> [!NOTE]
> Para coletar um rastreamento usando o `dotnet-trace` , ele precisa ser executado como o mesmo usuário que o usuário que está executando o processo de destino ou como raiz. Caso contrário, a ferramenta não conseguirá estabelecer uma conexão com o processo de destino.

## <a name="dotnet-trace-convert"></a>dotnet-conversão de rastreamento

Converte `nettrace` rastreamentos em formatos alternativos para uso com ferramentas de análise de rastreamento alternativas.

### <a name="synopsis"></a>Sinopse

```console
dotnet-trace convert [<input-filename>] [--format <Chromium|NetTrace|Speedscope>] [-h|--help] [-o|--output <output-filename>]
```

### <a name="arguments"></a>Argumentos

- **`<input-filename>`**

  Arquivo de rastreamento de entrada a ser convertido. O padrão é *trace. NetTrace*.

### <a name="options"></a>Opções

- **`--format <Chromium|NetTrace|Speedscope>`**

  Define o formato de saída para a conversão do arquivo de rastreamento.

- **`-o|--output <output-filename>`**

  Nome de arquivo de saída. A extensão do formato de destino será adicionada.

> [!NOTE]
> `nettrace`A conversão de arquivos em `chromium` ou `speedscope` arquivos é irreversível. `speedscope` e `chromium` os arquivos não têm todas as informações necessárias para reconstruir os `nettrace` arquivos. No entanto, o `convert` comando preserva o `nettrace` arquivo original, portanto, não exclua esse arquivo se você planeja abri-lo no futuro.

## <a name="dotnet-trace-ps"></a>dotnet-rastrear PS

 Lista os processos dotnet dos quais os rastreamentos podem ser coletados.

### <a name="synopsis"></a>Sinopse

```console
dotnet-trace ps [-h|--help]
```

## <a name="dotnet-trace-list-profiles"></a>dotnet-lista de rastreamento-perfis

Lista os perfis de rastreamento pré-criados com uma descrição de quais provedores e filtros estão em cada perfil.

### <a name="synopsis"></a>Sinopse

```console
dotnet-trace list-profiles [-h|--help]
```

## <a name="collect-a-trace-with-dotnet-trace"></a>Coletar um rastreamento com dotnet-Trace

Para coletar rastreamentos usando `dotnet-trace` :

- Obtenha o identificador do processo (PID) do aplicativo .NET Core do qual coletar rastreamentos.

  - No Windows, você pode usar o Gerenciador de tarefas ou o `tasklist` comando, por exemplo.
  - No Linux, por exemplo, o `ps` comando.
  - [dotnet-rastrear PS](#dotnet-trace-ps)

- Execute o comando a seguir:

  ```console
  dotnet-trace collect --process-id <PID>
  ```

  O comando anterior gera uma saída semelhante à seguinte:

  ```console
  Press <Enter> to exit...
  Connecting to process: <Full-Path-To-Process-Being-Profiled>/dotnet.exe
  Collecting to file: <Full-Path-To-Trace>/trace.nettrace
  Session Id: <SessionId>
  Recording trace 721.025 (KB)
  ```

- Pare a coleta pressionando a `<Enter>` tecla. `dotnet-trace` encerrará eventos de log no arquivo *trace. NetTrace* .

## <a name="launch-a-child-application-and-collect-a-trace-from-its-startup-using-dotnet-trace"></a>Iniciar um aplicativo filho e coletar um rastreamento de sua inicialização usando dotNet-Trace

> [!IMPORTANT]
> Isso funciona somente para aplicativos que executam o .NET 5,0 ou posterior.

Às vezes, pode ser útil coletar um rastreamento de um processo a partir de sua inicialização. Para aplicativos que executam o .NET 5,0 ou posterior, é possível fazer isso usando o rastreamento dotnet.

Isso será iniciado `hello.exe` com `arg1` e `arg2` como seus argumentos de linha de comando e coletará um rastreamento de sua inicialização de tempo de execução:

```console
dotnet-trace collect -- hello.exe arg1 arg2
```

O comando anterior gera uma saída semelhante à seguinte:

```console
No profile or providers specified, defaulting to trace profile 'cpu-sampling'

Provider Name                           Keywords            Level               Enabled By
Microsoft-DotNETCore-SampleProfiler     0x0000F00000000000  Informational(4)    --profile
Microsoft-Windows-DotNETRuntime         0x00000014C14FCCBD  Informational(4)    --profile

Process        : E:\temp\gcperfsim\bin\Debug\net5.0\gcperfsim.exe
Output File    : E:\temp\gcperfsim\trace.nettrace


[00:00:00:05]   Recording trace 122.244  (KB)
Press <Enter> or <Ctrl+C> to exit...
```

Você pode parar de coletar o rastreamento pressionando `<Enter>` ou `<Ctrl + C>` tecla. Isso também será encerrado `hello.exe` .

> [!NOTE]
> `hello.exe`A inicialização por meio de dotnet-Trace fará com que sua entrada/saída seja redirecionada e você não conseguirá interagir com seu STDIN/STDOUT.
> Sair da ferramenta por meio de CTRL + C ou SIGTERM irá encerrar com segurança a ferramenta e o processo filho.
> Se o processo filho for encerrado antes da ferramenta, a ferramenta também será encerrada e o rastreamento deverá ser visível com segurança.

## <a name="use-diagnostic-port-to-collect-a-trace-from-app-startup"></a>Usar a porta de diagnóstico para coletar um rastreamento da inicialização do aplicativo

  > [!IMPORTANT]
  > Isso funciona somente para aplicativos que executam o .NET 5,0 ou posterior.

A porta de diagnóstico é um novo recurso de tempo de execução que foi adicionado no .NET 5 que permite iniciar o rastreamento da inicialização do aplicativo. Para fazer isso usando o `dotnet-trace` , você pode usar o `dotnet-trace collect -- <command>` conforme descrito nos exemplos acima ou usar a `--diagnostic-port` opção.

Usar o `dotnet-trace <collect|monitor> -- <command>` para iniciar o aplicativo como um processo filho é a maneira mais simples de rastreá-lo rapidamente a partir de sua inicialização.

No entanto, quando você quiser obter um controle mais preciso sobre o tempo de vida do aplicativo que está sendo rastreado (por exemplo, monitorar o aplicativo pelos primeiros 10 minutos apenas e continuar executando) ou se precisar interagir com o aplicativo usando a CLI, o uso da `--diagnostic-port` opção permitirá que você controle o aplicativo de destino que está sendo monitorado e `dotnet-trace` .

1. O comando a seguir `dotnet-trace` cria um soquete de diagnóstico chamado `myport.sock` e aguarda uma conexão.

    > ```dotnet-cli
    > dotnet-trace collect --diagnostic-port myport.sock
    > ```

    Saída:

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ```

2. Em um console separado, inicie o aplicativo de destino com a variável de ambiente `DOTNET_DiagnosticPorts` definida como o valor na `dotnet-trace` saída.

    > ```bash
    > export DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ./my-dotnet-app arg1 arg2
    > ```

    Isso deve, então, habilitar `dotnet-trace` para iniciar o rastreamento `my-dotnet-app` :

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=myport.sock
    > Starting a counter session. Press Q to quit.
    > ```

    > [!IMPORTANT]
    > Iniciar seu aplicativo com `dotnet run` pode ser problemático porque a CLI dotnet pode gerar muitos processos filho que não são seu aplicativo e podem se conectar `dotnet-trace` antes do seu aplicativo, deixando seu aplicativo para ser suspenso em tempo de execução. É recomendável que você use diretamente uma versão independente do aplicativo ou use `dotnet exec` para iniciar o aplicativo.

## <a name="view-the-trace-captured-from-dotnet-trace"></a>Exibir o rastreamento capturado de dotnet-Trace

No Windows, os arquivos *. NetTrace* podem ser exibidos em [Perfview](https://github.com/microsoft/perfview) para análise: para rastreamentos coletados em outras plataformas, o arquivo de rastreamento pode ser movido para um computador Windows para ser exibido em Perfview.

No Linux, o rastreamento pode ser exibido alterando o formato de saída de `dotnet-trace` para `speedscope` . O formato do arquivo de saída pode ser alterado usando a `-f|--format` opção- `-f speedscope` fará com que o `dotnet-trace` produza um `speedscope` arquivo. Você pode escolher entre `nettrace` (a opção padrão) e `speedscope` . `Speedscope` os arquivos podem ser abertos em <https://www.speedscope.app> .

> [!NOTE]
> O tempo de execução do .NET Core gera rastreamentos no `nettrace` formato. Os rastreamentos são convertidos em speedscope (se especificado) após a conclusão do rastreamento. Como algumas conversões podem resultar em perda de dados, o arquivo original `nettrace` é preservado ao lado do arquivo convertido.

## <a name="use-dotnet-trace-to-collect-counter-values-over-time"></a>Usar o rastreamento dotnet para coletar valores de contador ao longo do tempo

`dotnet-trace` podem

* Use `EventCounter` para o monitoramento de integridade básico em ambientes sensíveis ao desempenho. Por exemplo, em produção.
* Colete rastreamentos para que eles não precisem ser exibidos em tempo real.

Por exemplo, para coletar valores de contador de desempenho de tempo de execução, use o seguinte comando:

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1
```

O comando anterior informa os contadores de tempo de execução para relatar uma vez a cada segundo para monitoramento de integridade leve. Substituir `EventCounterIntervalSec=1` por um valor mais alto (por exemplo, 60) permite a coleta de um rastreamento menor com menos granularidade nos dados do contador.

O comando a seguir reduz a sobrecarga e o tamanho do rastreamento mais do que o anterior:

```console
dotnet-trace collect --process-id <PID> --providers System.Runtime:0:1:EventCounterIntervalSec=1,Microsoft-Windows-DotNETRuntime:0:1,Microsoft-DotNETCore-SampleProfiler:0:1
```

O comando anterior desabilita os eventos de tempo de execução e o profiler de pilha gerenciado.

## <a name="use-rsp-file-to-avoid-typing-long-commands"></a>Use o arquivo. rsp para evitar a digitação de comandos longos

Você pode iniciar `dotnet-trace` com um `.rsp` arquivo que contém os argumentos a serem aprovados. Isso pode ser útil ao habilitar provedores que esperam argumentos longos ou ao usar um ambiente de shell que retira caracteres.

Por exemplo, o provedor a seguir pode ser trabalhoso para digitar cada vez que você quiser rastrear:

```cmd
dotnet-trace collect --providers Microsoft-Diagnostics-DiagnosticSource:0x3:5:FilterAndPayloadSpecs="SqlClientDiagnosticListener/System.Data.SqlClient.WriteCommandBefore@Activity1Start:-Command;Command.CommandText;ConnectionId;Operation;Command.Connection.ServerVersion;Command.CommandTimeout;Command.CommandType;Command.Connection.ConnectionString;Command.Connection.Database;Command.Connection.DataSource;Command.Connection.PacketSize\r\nSqlClientDiagnosticListener/System.Data.SqlClient.WriteCommandAfter@Activity1Stop:\r\nMicrosoft.EntityFrameworkCore/Microsoft.EntityFrameworkCore.Database.Command.CommandExecuting@Activity2Start:-Command;Command.CommandText;ConnectionId;IsAsync;Command.Connection.ClientConnectionId;Command.Connection.ServerVersion;Command.CommandTimeout;Command.CommandType;Command.Connection.ConnectionString;Command.Connection.Database;Command.Connection.DataSource;Command.Connection.PacketSize\r\nMicrosoft.EntityFrameworkCore/Microsoft.EntityFrameworkCore.Database.Command.CommandExecuted@Activity2Stop:",OtherProvider,AnotherProvider
```

Além disso, o exemplo anterior contém `"` como parte do argumento. Como as aspas não são manipuladas igualmente por cada shell, você pode enfrentar vários problemas ao usar shells diferentes. Por exemplo, o comando a ser inserido `zsh` é diferente do comando no `cmd` .

Em vez de digitar isso todas as vezes, você pode salvar o texto a seguir em um arquivo chamado `myprofile.rsp` .

```txt
--providers
Microsoft-Diagnostics-DiagnosticSource:0x3:5:FilterAndPayloadSpecs="SqlClientDiagnosticListener/System.Data.SqlClient.WriteCommandBefore@Activity1Start:-Command;Command.CommandText;ConnectionId;Operation;Command.Connection.ServerVersion;Command.CommandTimeout;Command.CommandType;Command.Connection.ConnectionString;Command.Connection.Database;Command.Connection.DataSource;Command.Connection.PacketSize\r\nSqlClientDiagnosticListener/System.Data.SqlClient.WriteCommandAfter@Activity1Stop:\r\nMicrosoft.EntityFrameworkCore/Microsoft.EntityFrameworkCore.Database.Command.CommandExecuting@Activity2Start:-Command;Command.CommandText;ConnectionId;IsAsync;Command.Connection.ClientConnectionId;Command.Connection.ServerVersion;Command.CommandTimeout;Command.CommandType;Command.Connection.ConnectionString;Command.Connection.Database;Command.Connection.DataSource;Command.Connection.PacketSize\r\nMicrosoft.EntityFrameworkCore/Microsoft.EntityFrameworkCore.Database.Command.CommandExecuted@Activity2Stop:",OtherProvider,AnotherProvider
```

Depois `myprofile.rsp` de salvar, você pode iniciar `dotnet-trace` com essa configuração usando o seguinte comando:

```bash
dotnet-trace @myprofile.rsp
```

## <a name="see-also"></a>Confira também

- [Provedores de eventos bem conhecidos do .NET](well-known-event-providers.md)
