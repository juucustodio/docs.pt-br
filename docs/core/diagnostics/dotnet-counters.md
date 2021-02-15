---
title: dotnet – ferramenta de diagnóstico de contadores – CLI do .NET
description: Saiba como instalar e usar a ferramenta dotnet-Counter CLI para monitoramento de integridade ad hoc e investigação de desempenho de primeiro nível.
ms.date: 11/17/2020
ms.openlocfilehash: 1842b1fb9cde0e0b7a570456766cbfdeb64c5896
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188576"
---
# <a name="investigate-performance-counters-dotnet-counters"></a>Investigar contadores de desempenho (dotNet-contadores)

**Este artigo aplica-se a:** ✔️ SDK do .net Core 3,0 e versões posteriores

## <a name="install"></a>Instalar

Há duas maneiras de baixar e instalar `dotnet-counters` :

- **ferramenta global dotnet:**

  Para instalar a versão de lançamento mais recente do `dotnet-counters` [pacote NuGet](https://www.nuget.org/packages/dotnet-counters), use o comando de [instalação da ferramenta dotnet](../tools/dotnet-tool-install.md) :

  ```dotnetcli
  dotnet tool install --global dotnet-counters
  ```

- **Download direto:**

  Baixe o executável da ferramenta que corresponde à sua plataforma:

  | Sistema operacional  | Plataforma |
  | --- | -------- |
  | Windows | [x86](https://aka.ms/dotnet-counters/win-x86) \| [x64](https://aka.ms/dotnet-counters/win-x64) \| [ARM](https://aka.ms/dotnet-counters/win-arm) \| [ARM-x64](https://aka.ms/dotnet-counters/win-arm64) |
  | macOS   | [x64](https://aka.ms/dotnet-counters/osx-x64) |
  | Linux   | [x64](https://aka.ms/dotnet-counters/linux-x64) \| [ARM](https://aka.ms/dotnet-counters/linux-arm) \| [arm64](https://aka.ms/dotnet-counters/linux-arm64) \| [MUSL-x64](https://aka.ms/dotnet-counters/linux-musl-x64) \| [MUSL-arm64](https://aka.ms/dotnet-counters/linux-musl-arm64) |

> [!NOTE]
> Para usar `dotnet-counters` o em um aplicativo x86, você precisa de uma versão x86 correspondente da ferramenta.

## <a name="synopsis"></a>Sinopse

```console
dotnet-counters [-h|--help] [--version] <command>
```

## <a name="description"></a>Descrição

`dotnet-counters` é uma ferramenta de monitoramento de desempenho para monitoramento de integridade ad hoc e investigação de desempenho de primeiro nível. Ele pode observar os valores do contador de desempenho que são publicados por meio da <xref:System.Diagnostics.Tracing.EventCounter> API. Por exemplo, você pode monitorar rapidamente coisas como o uso da CPU ou a taxa de exceções que estão sendo geradas em seu aplicativo .NET Core para ver se há algo suspeito antes de mergulhar em uma investigação de desempenho mais séria usando o `PerfView` ou o `dotnet-trace` .

## <a name="options"></a>Opções

- **`--version`**

  Exibe a versão do utilitário dotnet-Counters.

- **`-h|--help`**

  Mostra a ajuda da linha de comando.

## <a name="commands"></a>Comandos

| Comando                                             |
|-----------------------------------------------------|
| [dotnet – coleta de contadores](#dotnet-counters-collect) |
| [dotnet – lista de contadores](#dotnet-counters-list)       |
| [dotnet – monitor de contadores](#dotnet-counters-monitor) |
| [dotnet-contadores PS](#dotnet-counters-ps)           |

## <a name="dotnet-counters-collect"></a>dotnet – coleta de contadores

Coletar periodicamente os valores de contador selecionados e exportá-los para um formato de arquivo especificado para o pós-processamento.

### <a name="synopsis"></a>Sinopse

```console
dotnet-counters collect [-h|--help] [-p|--process-id] [-n|--name] [--diagnostic-port] [--refresh-interval] [--counters <COUNTERS>] [--format] [-o|--output] [-- <command>]
```

### <a name="options"></a>Opções

- **`-p|--process-id <PID>`**

  A ID do processo do qual coletar dados do contador.

- **`-n|--name <name>`**

  O nome do processo do qual coletar dados do contador.

- **`--diagnostic-port`**

  O nome da porta de diagnóstico a ser criada. Consulte [usando a porta de diagnóstico](#using-diagnostic-port) para saber como usar essa opção para iniciar o monitoramento de contadores da inicialização do aplicativo.

- **`--refresh-interval <SECONDS>`**

  O número de segundos de atraso entre a atualização dos contadores exibidos

- **`--counters <COUNTERS>`**

  Uma lista separada por vírgulas de contadores. Os contadores podem ser especificados `provider_name[:counter_name]` . Se o `provider_name` for usado sem uma lista de contadores de qualificação, todos os contadores do provedor serão mostrados. Para descobrir os nomes de provedor e contador, use o comando [dotnet-Counters List](#dotnet-counters-list) .

- **`--format <csv|json>`**

  O formato a ser exportado. Atualmente disponível: CSV, JSON.

- **`-o|--output <output>`**

  O nome do arquivo de saída.

- **`-- <command>` (para aplicativos de destino que executam o .NET 5,0 ou posterior somente)**

  Após os parâmetros de configuração da coleção, o usuário pode acrescentar `--` seguido por um comando para iniciar um aplicativo .NET com pelo menos um tempo de execução de 5,0. `dotnet-counters` o iniciará um processo com o comando fornecido e coletará as métricas solicitadas. Isso geralmente é útil para coletar métricas para o caminho de inicialização do aplicativo e pode ser usado para diagnosticar ou monitorar problemas que ocorrem antes ou logo após o ponto de entrada principal.

  > [!NOTE]
  > O uso dessa opção monitora o primeiro processo do .NET 5,0 que se comunica de volta à ferramenta, o que significa que, se o comando iniciar vários aplicativos .NET, ele só coletará o primeiro aplicativo. Portanto, é recomendável usar essa opção em aplicativos independentes ou usando a `dotnet exec <app.dll>` opção.

  > [!NOTE]
  > Iniciar um executável .NET por meio de dotnet-Counters fará com que sua entrada/saída seja redirecionada e você não poderá interagir com seu STDIN/STDOUT. Sair da ferramenta por meio de CTRL + C ou SIGTERM irá encerrar com segurança a ferramenta e o processo filho. Se o processo filho for encerrado antes da ferramenta, a ferramenta também será encerrada e o rastreamento deverá ser visível com segurança. Se você precisar usar stdin/stdout, poderá usar a `--diagnostic-port` opção. Consulte [usando a porta de diagnóstico](#using-diagnostic-port) para obter mais informações.

> [!NOTE]
> No Linux e no macOS, esse comando espera o aplicativo de destino e `dotnet-counters` compartilha a mesma `TMPDIR` variável de ambiente. Caso contrário, o comando atingirá o tempo limite.

> [!NOTE]
> Para coletar métricas usando o `dotnet-counters` , ele precisa ser executado como o mesmo usuário que o usuário que está executando o processo de destino ou como raiz. Caso contrário, a ferramenta não conseguirá estabelecer uma conexão com o processo de destino.

### <a name="examples"></a>Exemplos

- Colete todos os contadores em um intervalo de atualização de 3 segundos e gere um CSV como saída:

  ```console
  > dotnet-counters collect --process-id 1902 --refresh-interval 3 --format csv

  counter_list is unspecified. Monitoring all counters by default.
  Starting a counter session. Press Q to quit.
  ```

- Inicie `dotnet mvc.dll` o como um processo filho e comece a coletar contadores de tempo de execução e ASP.NET Core contadores de hospedagem da inicialização e salve-os como uma saída JSON:

  ```console
  > dotnet-counters collect --format json --counters System.Runtime,Microsoft.AspNetCore.Hosting -- dotnet mvc.dll
  Starting a counter session. Press Q to quit.
  File saved to counter.json
  ```

## <a name="dotnet-counters-list"></a>dotnet – lista de contadores

Exibe uma lista de nomes e descrições de contadores, agrupados por provedor.

### <a name="synopsis"></a>Sinopse

```console
dotnet-counters list [-h|--help]
```

### <a name="example"></a>Exemplo

```console
> dotnet-counters list
Showing well-known counters only. Specific processes may support additional counters.

System.Runtime
    cpu-usage                                    Amount of time the process has utilized the CPU (ms)
    working-set                                  Amount of working set used by the process (MB)
    gc-heap-size                                 Total heap size reported by the GC (MB)
    gen-0-gc-count                               Number of Gen 0 GCs per interval
    gen-1-gc-count                               Number of Gen 1 GCs per interval
    gen-2-gc-count                               Number of Gen 2 GCs per interval
    time-in-gc                                   % time in GC since the last GC
    gen-0-size                                   Gen 0 Heap Size
    gen-1-size                                   Gen 1 Heap Size
    gen-2-size                                   Gen 2 Heap Size
    loh-size                                     LOH Heap Size
    alloc-rate                                   Allocation Rate
    assembly-count                               Number of Assemblies Loaded
    exception-count                              Number of Exceptions per interval
    threadpool-thread-count                      Number of ThreadPool Threads
    monitor-lock-contention-count                Monitor Lock Contention Count
    threadpool-queue-length                      ThreadPool Work Items Queue Length
    threadpool-completed-items-count             ThreadPool Completed Work Items Count
    active-timer-count                           Active Timers Count

Microsoft.AspNetCore.Hosting
    requests-per-second                  Request rate
    total-requests                       Total number of requests
    current-requests                     Current number of requests
    failed-requests                      Failed number of requests
```

> [!NOTE]
> Os `Microsoft.AspNetCore.Hosting` contadores são exibidos quando há processos identificados que dão suporte a esses contadores, por exemplo, quando um aplicativo ASP.NET Core está em execução no computador host.

## <a name="dotnet-counters-monitor"></a>dotnet – monitor de contadores

Exibe a atualização periódica de valores dos contadores selecionados.

### <a name="synopsis"></a>Sinopse

```console
dotnet-counters monitor [-h|--help] [-p|--process-id] [-n|--name] [--diagnostic-port] [--refresh-interval] [--counters] [-- <command>]
```

### <a name="options"></a>Opções

- **`-p|--process-id <PID>`**

  A ID do processo a ser monitorado.

- **`-n|--name <name>`**

  O nome do processo a ser monitorado.

- **`--diagnostic-port`**

  O nome da porta de diagnóstico a ser criada. Consulte [usando a porta de diagnóstico](#using-diagnostic-port) para saber como usar essa opção para iniciar o monitoramento de contadores da inicialização do aplicativo.

- **`--refresh-interval <SECONDS>`**

  O número de segundos de atraso entre a atualização dos contadores exibidos

- **`--counters <COUNTERS>`**

  Uma lista separada por vírgulas de contadores. Os contadores podem ser especificados `provider_name[:counter_name]` . Se o `provider_name` for usado sem uma lista de contadores de qualificação, todos os contadores do provedor serão mostrados. Para descobrir os nomes de provedor e contador, use o comando [dotnet-Counters List](#dotnet-counters-list) .

 **`-- <command>` (para aplicativos de destino que executam o .NET 5,0 ou posterior somente)**

  Após os parâmetros de configuração da coleção, o usuário pode acrescentar `--` seguido por um comando para iniciar um aplicativo .NET com pelo menos um tempo de execução de 5,0. `dotnet-counters` o iniciará um processo com o comando fornecido e monitorará as métricas solicitadas. Isso geralmente é útil para coletar métricas para o caminho de inicialização do aplicativo e pode ser usado para diagnosticar ou monitorar problemas que ocorrem antes ou logo após o ponto de entrada principal.

  > [!NOTE]
  > O uso dessa opção monitora o primeiro processo do .NET 5,0 que se comunica de volta à ferramenta, o que significa que, se o comando iniciar vários aplicativos .NET, ele só coletará o primeiro aplicativo. Portanto, é recomendável usar essa opção em aplicativos independentes ou usando a `dotnet exec <app.dll>` opção.

  > [!NOTE]
  > Iniciar um executável .NET por meio de dotnet-Counters fará com que sua entrada/saída seja redirecionada e você não poderá interagir com seu STDIN/STDOUT. Sair da ferramenta por meio de CTRL + C ou SIGTERM irá encerrar com segurança a ferramenta e o processo filho. Se o processo filho for encerrado antes da ferramenta, a ferramenta também será encerrada. Se você precisar usar stdin/stdout, poderá usar a `--diagnostic-port` opção. Consulte [usando a porta de diagnóstico](#using-diagnostic-port) para obter mais informações.

> [!NOTE]
> No Linux e no macOS, esse comando espera o aplicativo de destino e `dotnet-counters` compartilha a mesma `TMPDIR` variável de ambiente.

> [!NOTE]
> Para monitorar as métricas usando o `dotnet-counters` , ele precisa ser executado como o mesmo usuário que o usuário que está executando o processo de destino ou como raiz.

### <a name="examples"></a>Exemplos

- Monitorar todos os contadores de `System.Runtime` em um intervalo de atualização de 3 segundos:

  ```console
  > dotnet-counters monitor --process-id 1902  --refresh-interval 3 --counters System.Runtime
  Press p to pause, r to resume, q to quit.
      Status: Running

  [System.Runtime]
      % Time in GC since last GC (%)                                 0
      Allocation Rate (B / 1 sec)                                5,376
      CPU Usage (%)                                                  0
      Exception Count (Count / 1 sec)                                0
      GC Fragmentation (%)                                          48.467
      GC Heap Size (MB)                                              0
      Gen 0 GC Count (Count / 1 sec)                                 1
      Gen 0 Size (B)                                                24
      Gen 1 GC Count (Count / 1 sec)                                 1
      Gen 1 Size (B)                                                24
      Gen 2 GC Count (Count / 1 sec)                                 1
      Gen 2 Size (B)                                           272,000
      IL Bytes Jitted (B)                                       19,449
      LOH Size (B)                                              19,640
      Monitor Lock Contention Count (Count / 1 sec)                  0
      Number of Active Timers                                        0
      Number of Assemblies Loaded                                    7
      Number of Methods Jitted                                     166
      POH (Pinned Object Heap) Size (B)                             24
      ThreadPool Completed Work Item Count (Count / 1 sec)           0
      ThreadPool Queue Length                                        0
      ThreadPool Thread Count                                        2
      Working Set (MB)                                              19
  ```

- Monitorar apenas o uso da CPU e o tamanho do heap do GC de `System.Runtime` :

  ```console
  > dotnet-counters monitor --process-id 1902 --counters System.Runtime[cpu-usage,gc-heap-size]

  Press p to pause, r to resume, q to quit.
    Status: Running

  [System.Runtime]
      CPU Usage (%)                                 24
      GC Heap Size (MB)                            811
  ```

- Monitorar `EventCounter` valores de definidos pelo usuário `EventSource` . Para obter mais informações, consulte [tutorial: medir o desempenho usando o EventCounters no .NET Core](event-counter-perf.md).

  ```console
  > dotnet-counters monitor --process-id 1902 --counters Samples-EventCounterDemos-Minimal

  Press p to pause, r to resume, q to quit.
      request                                      100
  ```

- Exiba todos os contadores conhecidos que estão disponíveis no `dotnet-counters` :

  ```console
  > dotnet-counters list

  Showing well-known counters for .NET (Core) version 3.1 only. Specific processes may support additional counters.
  System.Runtime
      cpu-usage                          The percent of process' CPU usage relative to all of the system CPU resources [0-100]
      working-set                        Amount of working set used by the process (MB)
      gc-heap-size                       Total heap size reported by the GC (MB)
      gen-0-gc-count                     Number of Gen 0 GCs between update intervals
      gen-1-gc-count                     Number of Gen 1 GCs between update intervals
      gen-2-gc-count                     Number of Gen 2 GCs between update intervals
      time-in-gc                         % time in GC since the last GC
      gen-0-size                         Gen 0 Heap Size
      gen-1-size                         Gen 1 Heap Size
      gen-2-size                         Gen 2 Heap Size
      loh-size                           LOH Size
      alloc-rate                         Number of bytes allocated in the managed heap between update intervals
      assembly-count                     Number of Assemblies Loaded
      exception-count                    Number of Exceptions / sec
      threadpool-thread-count            Number of ThreadPool Threads
      monitor-lock-contention-count      Number of times there were contention when trying to take the monitor lock between update intervals
      threadpool-queue-length            ThreadPool Work Items Queue Length
      threadpool-completed-items-count   ThreadPool Completed Work Items Count
      active-timer-count                 Number of timers that are currently active

  Microsoft.AspNetCore.Hosting
      requests-per-second                Number of requests between update intervals
      total-requests                     Total number of requests
      current-requests                   Current number of requests
      failed-requests                    Failed number of requests
  ```

- Exiba todos os contadores conhecidos que estão disponíveis no `dotnet-counters` para aplicativos .NET 5:

  ```console
  > dotnet-counters list --runtime-version 5.0

  Showing well-known counters for .NET (Core) version 5.0 only. Specific processes may support additional counters.
  System.Runtime
      cpu-usage                          The percent of process' CPU usage relative to all of the system CPU resources [0-100]
      working-set                        Amount of working set used by the process (MB)
      gc-heap-size                       Total heap size reported by the GC (MB)
      gen-0-gc-count                     Number of Gen 0 GCs between update intervals
      gen-1-gc-count                     Number of Gen 1 GCs between update intervals
      gen-2-gc-count                     Number of Gen 2 GCs between update intervals
      time-in-gc                         % time in GC since the last GC
      gen-0-size                         Gen 0 Heap Size
      gen-1-size                         Gen 1 Heap Size
      gen-2-size                         Gen 2 Heap Size
      loh-size                           LOH Size
      poh-size                           POH (Pinned Object Heap) Size
      alloc-rate                         Number of bytes allocated in the managed heap between update intervals
      gc-fragmentation                   GC Heap Fragmentation
      assembly-count                     Number of Assemblies Loaded
      exception-count                    Number of Exceptions / sec
      threadpool-thread-count            Number of ThreadPool Threads
      monitor-lock-contention-count      Number of times there were contention when trying to take the monitor lock between update intervals
      threadpool-queue-length            ThreadPool Work Items Queue Length
      threadpool-completed-items-count   ThreadPool Completed Work Items Count
      active-timer-count                 Number of timers that are currently active
      il-bytes-jitted                    Total IL bytes jitted
      methods-jitted-count               Number of methods jitted

  Microsoft.AspNetCore.Hosting
      requests-per-second   Number of requests between update intervals
      total-requests        Total number of requests
      current-requests      Current number of requests
      failed-requests       Failed number of requests

  Microsoft-AspNetCore-Server-Kestrel
      connections-per-second      Number of connections between update intervals
      total-connections           Total Connections
      tls-handshakes-per-second   Number of TLS Handshakes made between update intervals
      total-tls-handshakes        Total number of TLS handshakes made
      current-tls-handshakes      Number of currently active TLS handshakes
      failed-tls-handshakes       Total number of failed TLS handshakes
      current-connections         Number of current connections
      connection-queue-length     Length of Kestrel Connection Queue
      request-queue-length        Length total HTTP request queue

  System.Net.Http
      requests-started        Total Requests Started
      requests-started-rate   Number of Requests Started between update intervals
      requests-aborted        Total Requests Aborted
      requests-aborted-rate   Number of Requests Aborted between update intervals
      current-requests        Current Requests
  ```

- Inicie `my-aspnet-server.exe` e monitore o número de assemblies carregados a partir de sua inicialização (somente .net 5,0 ou posterior):

  > [!IMPORTANT]
  > Isso funciona somente para aplicativos que executam o .NET 5,0 ou posterior.

  ```console
  > dotnet-counters monitor --counters System.Runtime[assembly-count] -- my-aspnet-server.exe

  Press p to pause, r to resume, q to quit.
    Status: Running

  [System.Runtime]
      Number of Assemblies Loaded                   24
  ```
  
- Inicie `my-aspnet-server.exe` com `arg1` e `arg2` como argumentos de linha de comando e monitore seu conjunto de trabalho e o tamanho do heap de GC de sua inicialização (somente .NET 5,0 ou posterior):

  > [!IMPORTANT]
  > Isso funciona somente para aplicativos que executam o .NET 5,0 ou posterior.

  ```console
  > dotnet-counters monitor --counters System.Runtime[working-set,gc-heap-size] -- my-aspnet-server.exe arg1 arg2
  ```

  ```console
  Press p to pause, r to resume, q to quit.
    Status: Running

  [System.Runtime]
      GC Heap Size (MB)                                 39
      Working Set (MB)                                  59
  ```

## <a name="dotnet-counters-ps"></a>dotnet-contadores PS

Exibe uma lista de processos dotnet que podem ser monitorados.

### <a name="synopsis"></a>Sinopse

```console
dotnet-counters ps [-h|--help]
```

### <a name="example"></a>Exemplo

```console
> dotnet-counters ps
  
  15683 WebApi     /home/user/repos/WebApi/WebApi
  16324 dotnet     /usr/local/share/dotnet/dotnet
```

## <a name="using-diagnostic-port"></a>Usando a porta de diagnóstico

  > [!IMPORTANT]
  > Isso funciona somente para aplicativos que executam o .NET 5,0 ou posterior.

A porta de diagnóstico é um novo recurso de tempo de execução que foi adicionado no .NET 5 que permite que você inicie o monitoramento ou coleta de contadores da inicialização do aplicativo. Para fazer isso usando o `dotnet-counters` , você pode usar o `dotnet-counters <collect|monitor> -- <command>` conforme descrito nos exemplos acima ou usar a `--diagnostic-port` opção.

Usar `dotnet-counters <collect|monitor> -- <command>` o para iniciar o aplicativo como um processo filho é a maneira mais simples de monitorá-lo rapidamente a partir de sua inicialização.

No entanto, quando você quiser obter um controle mais preciso sobre o tempo de vida do aplicativo que está sendo monitorado (por exemplo, monitorar o aplicativo pelos primeiros 10 minutos e continuar executando) ou se precisar interagir com o aplicativo usando a CLI, o uso da `--diagnostic-port` opção permitirá que você controle o aplicativo de destino que está sendo monitorado e `dotnet-counters` .

1. O comando a seguir faz o dotnet-Counters criar um soquete de diagnóstico chamado `myport.sock` e aguardar uma conexão.

    > ```dotnet-cli
    > dotnet-counters collect --diagnostic-port myport.sock
    > ```

    Saída:

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ```

2. Em um console separado, inicie o aplicativo de destino com a variável de ambiente `DOTNET_DiagnosticPorts` definida como o valor na `dotnet-counters` saída.

    > ```bash
    > export DOTNET_DiagnosticPorts=/home/user/myport.sock
    > ./my-dotnet-app arg1 arg2
    > ```

    Isso deve, então, habilitar `dotnet-counters` para começar a coletar contadores em `my-dotnet-app` :

    > ```bash
    > Waiting for connection on myport.sock
    > Start an application with the following environment variable: DOTNET_DiagnosticPorts=myport.sock
    > Starting a counter session. Press Q to quit.
    > ```

    > [!IMPORTANT]
    > Iniciar seu aplicativo com `dotnet run` pode ser problemático porque a CLI dotnet pode gerar muitos processos filho que não são seu aplicativo e podem se conectar `dotnet-counters` antes do seu aplicativo, deixando seu aplicativo para ser suspenso em tempo de execução. É recomendável que você use diretamente uma versão independente do aplicativo ou use `dotnet exec` para iniciar o aplicativo.
