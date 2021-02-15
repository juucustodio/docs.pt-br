---
title: Rastreando aplicativos .NET com PerfCollect.
description: Um tutorial que orienta você pela coleta de um rastreamento com perfcollect no .NET.
ms.topic: tutorial
ms.date: 10/23/2020
ms.openlocfilehash: 53e4584953d2af4e766daadfa757cca752ae7329
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97593214"
---
# <a name="trace-net-applications-with-perfcollect"></a>Rastrear aplicativos .NET com PerfCollect

**Este artigo aplica-se a: ✔️** SDK do .net Core 2,1 e versões posteriores

Quando são encontrados problemas de desempenho no Linux, a coleta de um rastreamento com `perfcollect` o pode ser usada para reunir informações detalhadas sobre o que estava acontecendo no computador no momento do problema de desempenho.

`perfcollect` é um script bash que aproveita a [geração de Tookit-Next de rastreamento do Linux (LTTng)](https://lttng.org) para coletar eventos gravados do tempo de execução ou de qualquer [EventSource](xref:System.Diagnostics.Tracing.EventListener), bem como [perf](https://perf.wiki.kernel.org/) , para coletar amostras de CPU do processo de destino.

## <a name="prepare-your-machine"></a>Preparar seu computador

Siga estas etapas para preparar seu computador para coletar um rastreamento de desempenho com o `perfcollect` .

> [!NOTE]
> Se você estiver em um ambiente de contêiner, seu contêiner precisará ter `SYS_ADMIN` capacidade. Para obter mais informações sobre como rastrear aplicativos dentro de contêineres usando o PerfCollect, consulte [coletar diagnósticos em contêineres](./diagnostics-in-containers.md).

1. Baixar `perfcollect` .

    > ```bash
    > curl -OL https://aka.ms/perfcollect
    > ```

2. Torne o script executável.

    > ```bash
    > chmod +x perfcollect
    > ```

3. Instalar os pré-requisitos de rastreamento-essas são as bibliotecas de rastreamento reais.

    > ```bash
    > sudo ./perfcollect install
    > ```

    Isso instalará os seguintes pré-requisitos em seu computador:

    1. `perf`: o subsistema de eventos de desempenho do Linux e o aplicativo de coleta/Visualizador do modo de usuário complementar. `perf` faz parte da origem do kernel do Linux, mas geralmente não é instalado por padrão.

    2. `LTTng`: Usado para capturar dados de eventos emitidos em tempo de execução pelo CoreCLR. Esses dados são usados para analisar o comportamento de vários componentes de tempo de execução, como GC, JIT e pool de threads.

As versões recentes do .NET Core e da ferramenta de desempenho do Linux dão suporte à resolução automática de nomes de método para código de estrutura. Se você estiver trabalhando com o .NET Core versão 3,1 ou menos, será necessária uma etapa extra. Consulte [resolvendo símbolos de estrutura](#resolve-framework-symbols) para obter detalhes.

Para resolver nomes de método de DLLs de tempo de execução nativas (como libcoreclr.so), o `perfcollect` resolve os símbolos para eles ao converter os dados, mas somente se os símbolos desses binários estiverem presentes. Consulte [obtendo símbolos para a seção de tempo de execução nativo](#get-symbols-for-the-native-runtime) para obter detalhes.

## <a name="collect-a-trace"></a>Coletar um rastreamento

1. Ter dois shells disponíveis-um para controlar o rastreamento, conhecido como **[Trace]** e outro para executar o aplicativo, chamado de **[App]**.

2. **[Rastreamento]** Iniciar coleção.

    > ```bash
    > sudo ./perfcollect collect sampleTrace
    > ```

    Saída esperada:

    > ```bash
    > Collection started.  Press CTRL+C to stop.
    > ```

3. **[Aplicativo]** Configure o Shell de aplicativo com as seguintes variáveis de ambiente – isso habilita a configuração de rastreamento do CoreCLR.

    > ```bash
    > export COMPlus_PerfMapEnabled=1
    > export COMPlus_EnableEventLog=1
    > ```

4. **[Aplicativo]** Execute o aplicativo-deixe que ele seja executado desde que você precise para capturar o problema de desempenho. O comprimento exato pode ser tão curto quanto necessário, desde que ele Capture suficientemente a janela de tempo onde o problema de desempenho que você deseja investigar ocorre.

    > ```bash
    > dotnet run
    > ```

5. **[Rastreamento]** Parar coleção-pressione CTRL + C.

    > ```bash
    > ^C
    > ...STOPPED.
    >
    > Starting post-processing. This may take some time.
    >
    > Generating native image symbol files
    > ...SKIPPED
    > Saving native symbols
    > ...FINISHED
    > Exporting perf.data file
    > ...FINISHED
    > Compressing trace files
    > ...FINISHED
    > Cleaning up artifacts
    > ...FINISHED
    >
    > Trace saved to sampleTrace.trace.zip
    > ```

    O arquivo de rastreamento compactado agora é armazenado no diretório de trabalho atual.

## <a name="view-a-trace"></a>Exibir um rastreamento

Há várias opções para exibir o rastreamento que foi coletado. Os rastreamentos são mais bem exibidos usando o [Perfview](https://aka.ms/perfview) no Windows, mas eles podem ser exibidos diretamente no Linux usando- `PerfCollect` se ou `TraceCompass` .

### <a name="use-perfcollect-to-view-the-trace-file"></a>Use PerfCollect para exibir o arquivo de rastreamento

Você pode usar o perfcollect em si para exibir o rastreamento que você coletou. Para isso, use o seguinte comando:

```bash
./perfcollect view sampleTrace.trace.zip
```

Por padrão, isso mostrará o rastreamento de CPU do aplicativo usando `perf` .

Para examinar os eventos que foram coletados por meio `LTTng` do, você pode passar o sinalizador `-viewer lttng` para ver os eventos individuais:

```bash
./perfcollect view sampleTrace.trace.zip -viewer lttng
```

Isso usará `babeltrace` o visualizador para imprimir a carga de eventos:

```bash
# [01:02:18.189217659] (+0.020132603) ubuntu-xenial DotNETRuntime:ExceptionThrown_V1: { cpu_id = 0 }, { ExceptionType = "System.Exception", ExceptionMessage = "An exception happened", ExceptionEIP = 139875671834775, ExceptionHRESULT = 2148734208, ExceptionFlags = 16, ClrInstanceID = 0 }
# [01:02:18.189250227] (+0.020165171) ubuntu-xenial DotNETRuntime:ExceptionCatchStart: { cpu_id = 0 }, { EntryEIP = 139873639728404, MethodID = 139873626968120, MethodName = "void [helloworld] helloworld.Program::Main(string[])", ClrInstanceID = 0 }
```

### <a name="use-perfview-to-open-the-trace-file"></a>Use PerfView para abrir o arquivo de rastreamento

Para ver uma exibição agregada do exemplo de CPU e dos eventos, você pode usar `PerfView` em um computador Windows.

1. Copie o arquivo de trace.zip do Linux para um computador Windows.

2. Baixe o PerfView de <https://aka.ms/perfview> .

3. Executar PerfView.exe

    > ```cmd
    > PerfView.exe <path to trace.zip file>
    > ```

PerfView exibirá a lista de exibições com suporte com base nos dados contidos no arquivo de rastreamento.

- Para investigações de CPU, escolha **pilhas de CPU**.

- Para obter informações detalhadas do GC, escolha **GCStats**.

- Para obter informações de JIT por processo/módulo/método, escolha **JITStats**.

- Se não houver uma exibição para as informações necessárias, você poderá tentar procurar os eventos na exibição de eventos brutos.  Escolha **eventos**.

Para obter mais informações sobre como interpretar exibições no PerfView, consulte links de ajuda na própria exibição ou na janela principal do PerfView, escolha **ajuda – >guia de usuários**.

### <a name="use-tracecompass-to-open-the-trace-file"></a>Use TraceCompass para abrir o arquivo de rastreamento

O [Eclipse TraceCompass](https://www.eclipse.org/tracecompass/) é outra opção que você pode usar para exibir os rastreamentos. `TraceCompass` também funciona em computadores Linux, portanto, você não precisa mover seu rastreamento para um computador Windows. Para usar `TraceCompass` o para abrir o arquivo de rastreamento, será necessário descompactar o arquivo.

```bash
unzip myTrace.trace.zip
```

`perfcollect` o salvará o rastreamento LTTng coletado em um formato de arquivo CTF em um subdiretório no `lttngTrace` . Especificamente, o arquivo CTF estará localizado em um diretório parecido com `lttngTrace/auto-20201025-101230\ust\uid\1000\64-bit\` .

Você pode abrir o arquivo de rastreamento CTF no selecionando `TraceCompass` `File -> Open Trace` e selecionando o `metadata` arquivo.

Para obter mais detalhes, consulte a [ `TraceCompass` documentação](https://www.eclipse.org/tracecompass/).

## <a name="resolve-framework-symbols"></a>Resolver símbolos de estrutura

Os símbolos de estrutura precisam ser gerados manualmente no momento em que o rastreamento é coletado. Eles são diferentes dos símbolos de nível de aplicativo porque a estrutura é pré-compilado enquanto o código do aplicativo é compilado just-in-time. Para o código de estrutura que foi pré-compilado ao código nativo, você precisa chamar `crossgen` isso que sabe como gerar o mapeamento do código nativo para o nome dos métodos.

`perfcollect` pode lidar com a maioria dos detalhes para você, mas ele precisa ter `crossgen` disponível. Por padrão, ele não é instalado com a distribuição do .NET. Se `crossgen` não estiver, o `perfcollect` avisará e se referirá a essas instruções. Para corrigir as coisas necessárias para buscar exatamente a versão correta do CrossGen para o tempo de execução que você está usando. Se você posicionar a ferramenta CrossGen no mesmo diretório que as DLLs de tempo de execução do .NET (por exemplo, libcoreclr.so), `perfcollect` poderá encontrá-la e adicionar os símbolos de estrutura ao arquivo de rastreamento para você.

Normalmente, quando você cria um aplicativo .NET, ele apenas gera a DLL para o código que você escreveu, usando uma cópia compartilhada do tempo de execução para o restante.   No entanto, você também pode gerar o que é chamado de uma versão ' autocontida ' de um aplicativo e isso contém todas as DLLs de tempo de execução. `crossgen` faz parte do pacote NuGet usado para criar aplicativos independentes, portanto, uma maneira de obter a versão correta do `crossgen` é criar um pacote independente de seu aplicativo.

Por exemplo:

   >```bash
   > mkdir helloWorld
   > cd helloWorld
   > dotnet new console
   > dotnet publish --self-contained -r linux-x64
   >```

Isso cria um novo aplicativo Olá, Mundo e o compila como um aplicativo independente.

Como um efeito colateral da criação do aplicativo independente, a ferramenta dotnet baixará um pacote NuGet chamado Runtime. Linux-x64. Microsoft. NetCore. app e o coloca no diretório ~/.nuget/packages/runtime.linux-x64.microsoft.netcore.app/VERSION, em que VERSION é o número de versão do seu tempo de execução do .NET Core (por exemplo, 2.1.0). Isso é um diretório de ferramentas e, dentro daí, há a ferramenta CrossGen de que você precisa. A partir do .NET Core 3,0, o local do pacote é ~/.nuget/packages/microsoft.netcore.app.runtime.linux-x64/VERSION.

A `crossgen` ferramenta precisa ser colocada ao lado do tempo de execução que é realmente usado pelo seu aplicativo. Normalmente, seu aplicativo usa a versão compartilhada do .NET Core que está instalada em/usr/share/dotnet/shared/Microsoft.NETCore.App/VERSION, em que VERSION é o número de versão do tempo de execução do .NET. Esse é um local compartilhado, portanto, você precisa ser um superusuário para modificá-lo. Se a versão for 2.1.0, os comandos a serem atualizados `crossgen` seriam:

   >```bash
   > sudo bash
   > cp ~/.nuget/packages/runtime.linux-x64.microsoft.netcore.app/2.1.0/tools/crossgen /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0
   >```

Depois de fazer isso, o `perfcollect` usará CrossGen para incluir símbolos de estrutura. O aviso que `perfcollect` costumava ser emitido deve desaparecer. Isso só precisa ser uma vez por computador (até que você atualize seu tempo de execução).

### <a name="alternative-turn-off-use-of-precompiled-code"></a>Alternativa: desativar o uso de código pré-compilado

Se você não tiver a capacidade de atualizar o tempo de execução do .NET (para adicionar `crossgen` ) ou se o procedimento acima não funcionou por algum motivo, há outra abordagem para obter os símbolos de estrutura. Você pode dizer ao tempo de execução para simplesmente não usar o código de estrutura pré-compilado. O código será compilado just-in-time e `crossgen` não será necessário.

> [!NOTE]
> A escolha dessa abordagem pode aumentar o tempo de inicialização para seu aplicativo.

Para fazer isso, você pode adicionar a seguinte variável de ambiente:

```bash
export COMPlus_ZapDisable=1
```

Com essa alteração, você deve obter os símbolos para todo o código .NET.

## <a name="get-symbols-for-the-native-runtime"></a>Obter símbolos para o tempo de execução nativo

Na maioria das vezes, você está interessado em seu próprio código, que é `perfcollect` resolvido por padrão. Às vezes, é útil ver o que está acontecendo dentro das DLLs do .NET (que é a última seção sobre), mas às vezes, o que está acontecendo nas DLLs do tempo de execução nativo (normalmente libcoreclr.so) é interessante.  `perfcollect` o resolverá os símbolos para eles quando ele converter seus dados, mas somente se os símbolos para essas DLLs nativas estiverem presentes (e estiverem ao lado da biblioteca de onde estão).

Há um comando global chamado [dotnet-símbolo](https://github.com/dotnet/symstore/blob/master/src/dotnet-symbol/README.md#symbol-downloader-dotnet-cli-extension) que faz isso. Para usar dotnet-Symbol para obter símbolos de tempo de execução nativos:

1. Instale `dotnet-symbol`:

    ```bash
    dotnet tool install -g dotnet-symbol
    ```

2. Baixe os símbolos. Se a versão instalada do tempo de execução do .NET Core for 2.1.0, o comando para fazer isso é:

    ```bash
    mkdir mySymbols
    dotnet symbol --symbols --output mySymbols  /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0/lib*.so
    ```

3. Copie os símbolos para o local correto.

    ```bash
    sudo cp mySymbols/* /usr/share/dotnet/shared/Microsoft.NETCore.App/2.1.0
    ```

    Se isso não puder ser feito porque você não tem acesso de gravação ao diretório apropriado, você pode usar `perf buildid-cache` para adicionar os símbolos.

Depois disso, você deve obter nomes simbólicos para as DLLs nativas ao executar o `perfcollect` .

## <a name="collect-in-a-docker-container"></a>Coletar em um contêiner do Docker

Para obter mais informações sobre como usar `perfcollect` em ambientes de contêiner, consulte [coletar diagnósticos em contêineres](./diagnostics-in-containers.md).

## <a name="learn-more-about-collection-options"></a>Saiba mais sobre as opções de coleta

Você pode especificar os seguintes sinalizadores opcionais com o `perfcollect` para atender melhor às suas necessidades de diagnóstico.

### <a name="collect-for-a-specific-duration"></a>Coletar por uma duração específica

Quando desejar coletar um rastreamento para uma duração específica, você poderá usar `-collectsec` a opção seguida de um número especificando o total de segundos para coletar um rastreamento.

### <a name="collect-threadtime-traces"></a>Coletar rastreamentos de threadtime

Especificar `-threadtime` with `perfcollect` permite que você colete dados de uso de CPU por thread. Isso permite que você analise onde cada thread estava gastando seu tempo de CPU.

### <a name="collect-traces-for-managed-memory-and-garbage-collector-performance"></a>Coletar rastreamentos para memória gerenciada e desempenho do coletor de lixo

As opções a seguir permitem que você colete especificamente os eventos de GC do tempo de execução.

* `perfcollect collect -gccollectonly`

Colete apenas um conjunto mínimo de eventos de coleta de GC. Esse é o perfil de coleção de eventos do GC menos detalhado com o menor impacto no desempenho do aplicativo de destino. Esse comando é análogo ao `PerfView.exe /GCCollectOnly collect` comando no Perfview.

* `perfcollect collect -gconly`

Colete eventos de coleta de GC mais detalhados com eventos JIT, Loader e Exception. Isso solicita eventos mais detalhados (como as informações de alocação e informações de ingresso no GC) e terá mais impacto na opção desempenho do aplicativo de destino do que `-gccollectonly` . Esse comando é análogo ao `PerfView.exe /GCOnly collect` comando no Perfview.

* `perfcollect collect -gcwithheap`

Colete os eventos de coleta de GC mais detalhados que controlam a sobrevivência e os movimentos de heap também. Isso fornece uma análise detalhada do comportamento do GC, mas incorrerá em custo de alto desempenho, já que cada GC pode levar mais de duas vezes mais. É recomendável que você entenda a implicação de desempenho do uso dessa opção de rastreamento ao rastrear em ambientes de produção.
