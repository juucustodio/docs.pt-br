---
title: Coletar informações detalhadas de carregamento de assembly-.NET Core
description: Descrição de como coletar informações de carregamento de assembly no .NET Core
author: elinor-fung
ms.author: elfung
ms.date: 11/17/2020
ms.openlocfilehash: b121982995b440ade6d72190f44f9b9d237c8af6
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506546"
---
# <a name="collect-detailed-assembly-loading-information"></a>Coletar informações detalhadas de carregamento do assembly

A partir do .NET 5,0, o tempo de execução pode emitir eventos `EventPipe` com informações detalhadas sobre o [carregamento de assembly gerenciado](loading-managed.md) para auxiliar no diagnóstico de problemas de carregamento de assembly. Esses [eventos](../../fundamentals/diagnostics/runtime-loader-binder-events.md) são emitidos pelo `Microsoft-Windows-DotNETRuntime` provedor sob a `AssemblyLoader` palavra-chave ( `0x4` ).

## <a name="prerequisites"></a>Pré-requisitos

- [SDK do .net 5,0](https://dotnet.microsoft.com/download) ou versões posteriores
- [dotnet – ferramenta de rastreamento](../diagnostics/dotnet-trace.md) .

## <a name="collect-a-trace-with-assembly-loading-events"></a>Coletar um rastreamento com eventos de carregamento de assembly

Para habilitar os eventos de carregamento de assembly no tempo de execução e coletar um rastreamento deles, use `dotnet-trace` com o seguinte comando:

```console
dotnet-trace collect --providers Microsoft-Windows-DotNETRuntime:4 --process-id <pid>
```

Isso coletará um rastreamento do especificado `<pid>` , habilitando os `AssemblyLoader` eventos no `Microsoft-Windows-DotNETRuntime` provedor. O resultado é um `.nettrace` arquivo.

## <a name="view-a-trace"></a>Exibir um rastreamento

O arquivo de rastreamento coletado pode ser exibido no Windows usando a exibição de eventos no [Perfview](https://github.com/microsoft/perfview). Todos os eventos de carregamento de assembly serão prefixados com `Microsoft-Windows-DotNETRuntime/AssemblyLoader` .

## <a name="example-on-windows"></a>Exemplo (no Windows)

Este exemplo usa a [amostra de pontos de extensão de carregamento de assembly](https://github.com/dotnet/samples/tree/master/core/extensions/AssemblyLoading). O aplicativo tenta carregar um assembly `MyLibrary` -um assembly que não é referenciado pelo aplicativo e, portanto, requer tratamento em um ponto de extensão de carregamento de assembly a ser carregado com êxito.

### <a name="collect-the-trace"></a>Coletar o rastreamento

01. Navegue até o diretório com o exemplo baixado. Compile o aplicativo com:

    ```console
    dotnet build
    ```

01. Inicie o aplicativo com argumentos indicando que ele deve pausar, aguardando um pressionamento de tecla. Ao continuar, ele tentará carregar o assembly no padrão `AssemblyLoadContext` -sem a manipulação necessária para uma carga bem-sucedida. Navegue até o diretório de saída e execute:

    ```console
    AssemblyLoading.exe /d default
    ```

01. Localize a ID do processo do aplicativo.

    ```console
    dotnet-trace ps
    ```

    A saída listará os processos disponíveis. Por exemplo:

    ```console
    35832 AssemblyLoading C:\src\AssemblyLoading\bin\Debug\net5.0\AssemblyLoading.exe
    ```

01. Anexe `dotnet-trace` ao aplicativo em execução.

    ```console
    dotnet-trace collect --providers Microsoft-Windows-DotNETRuntime:4 --process-id 35832
    ```

01. Na janela que executa o aplicativo, pressione qualquer tecla para permitir que o programa continue. O rastreamento será interrompido automaticamente quando o aplicativo for encerrado.

### <a name="view-the-trace"></a>Exibir o rastreamento

Abra o rastreamento coletado em [Perfview](https://github.com/microsoft/perfview) e abra a exibição eventos. Filtre a lista de eventos para `Microsoft-Windows-DotNETRuntime/AssemblyLoader` eventos.

:::image type="content" source="media/collect-details/assembly-loader-filter.png" alt-text="Imagem de filtro do carregador de assembly PerfView":::

Todas as cargas de assembly que ocorreram no aplicativo após o rastreamento iniciado serão mostradas. Para inspecionar a operação de carregamento do assembly de interesse para este exemplo – `MyLibrary` , podemos fazer mais filtragem.

### <a name="assembly-loads"></a>Cargas de assembly

Filtre a exibição para os [`Start`](../../fundamentals/diagnostics/runtime-loader-binder-events.md#assemblyloadstart-event) [`Stop`](../../fundamentals/diagnostics/runtime-loader-binder-events.md#assemblyloadstop-event) eventos e em `Microsoft-Windows-DotNETRuntime/AssemblyLoader` usando a lista de eventos à esquerda. Adicione as colunas `AssemblyName` , `ActivityID` e `Success` à exibição. Filtrar para eventos que contêm `MyLibrary` .

:::image type="content" source="media/collect-details/start-stop.png" alt-text="PerfView iniciar e parar a imagem de eventos":::

| Nome do evento             | AssemblyName                                      | ActivityID | Êxito |
| ---------------------- | ------------------------------------------------- | ---------- | ------- |
| `AssemblyLoader/Start` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | 1/2/     |         |
| `AssemblyLoader/Stop`  | `MyLibrary, Culture=neutral, PublicKeyToken=null` | 1/2/     | Falso   |

Você deve ver um `Start` / `Stop` par com `Success=False` no `Stop` evento, indicando que a operação de carregamento falhou. Observe que os dois eventos têm a mesma ID de atividade. A ID da atividade pode ser usada para filtrar todos os outros eventos do carregador de assembly apenas aqueles correspondentes a essa operação de carregamento.

### <a name="breakdown-of-attempt-to-load"></a>Divisão da tentativa de carregamento

Para obter uma análise mais detalhada da operação de carregamento, filtre a exibição para os [ `ResolutionAttempted` eventos](../../fundamentals/diagnostics/runtime-loader-binder-events.md#resolutionattempted-event) em `Microsoft-Windows-DotNETRuntime/AssemblyLoader` usando a lista de eventos à esquerda. Adicione as colunas `AssemblyName` , `Stage` e `Result` à exibição. Filtrar eventos com a ID da atividade do `Start` / `Stop` par.

:::image type="content" source="media/collect-details/resolution-attempted.png" alt-text="Imagem de eventos do PerfView ResolutionAttempted":::

| Nome do evento                           | AssemblyName                                      | Estágio                               | Result             |
| ------------------------------------ | ------------------------------------------------- | ----------------------------------- | ------------------ |
| `AssemblyLoader/ResolutionAttempted` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `FindInLoadContext`                 | `AssemblyNotFound` |
| `AssemblyLoader/ResolutionAttempted` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `ApplicationAssemblies`             | `AssemblyNotFound` |
| `AssemblyLoader/ResolutionAttempted` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `AssemblyLoadContextResolvingEvent` | `AssemblyNotFound` |
| `AssemblyLoader/ResolutionAttempted` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `AppDomainAssemblyResolveEvent`     | `AssemblyNotFound` |

Os eventos acima indicam que o carregador de assembly tentou resolver o assembly examinando o contexto de carga atual, executando a lógica de investigação padrão para assemblies de aplicativos gerenciados, invocando manipuladores para o <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving?displayProperty=nameWithType> evento e invocando manipuladores para o <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> . Para todas essas etapas, o assembly não foi encontrado.

### <a name="extension-points"></a>Pontos de extensão

Para ver quais pontos de extensão foram invocados, filtre a exibição para o [`AssemblyLoadContextResolvingHandlerInvoked`](../../fundamentals/diagnostics/runtime-loader-binder-events.md#assemblyloadcontextresolvinghandlerinvoked-event) e [`AppDomainAssemblyResolveHandlerInvoked`](../../fundamentals/diagnostics/runtime-loader-binder-events.md#appdomainassemblyresolvehandlerinvoked-event) em `Microsoft-Windows-DotNETRuntime/AssemblyLoader` usando a lista de eventos à esquerda. Adicione as colunas `AssemblyName` e `HandlerName` à exibição. Filtrar eventos com a ID da atividade do `Start` / `Stop` par.

:::image type="content" source="media/collect-details/extension-point.png" alt-text="Imagem de eventos do ponto de extensão PerfView":::

| Nome do evento                                                  | AssemblyName                                      | HandlerName                      |
| ----------------------------------------------------------- | ------------------------------------------------- | -------------------------------- |
| `AssemblyLoader/AssemblyLoadContextResolvingHandlerInvoked` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `OnAssemblyLoadContextResolving` |
| `AssemblyLoader/AppDomainAssemblyResolveHandlerInvoked`     | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `OnAppDomainAssemblyResolve`     |

Os eventos acima indicam que um manipulador chamado `OnAssemblyLoadContextResolving` foi invocado para o <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving?displayProperty=nameWithType> evento e um manipulador chamado `OnAppDomainAssemblyResolve` foi invocado para o <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> evento.

### <a name="collect-another-trace"></a>Coletar outro rastreamento

Execute o aplicativo com argumentos de modo que seu manipulador para o <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving?displayProperty=nameWithType> evento carregue o `MyLibrary` assembly.

```console
AssemblyLoading /d default alc-resolving
```

Colete e abra outro `.nettrace` arquivo usando as [etapas acima](#collect-the-trace).

Filtre os `Start` eventos e `Stop` `MyLibrary` novamente. Você deve ver um `Start` / `Stop` par com outro `Start` / `Stop` entre eles. A operação de carregamento interna representa a carga disparada pelo manipulador para <xref:System.Runtime.Loader.AssemblyLoadContext.Resolving?displayProperty=nameWithType> quando ele é chamado <xref:System.Runtime.Loader.AssemblyLoadContext.LoadFromAssemblyPath%2A?displayProperty=nameWithType> . Desta vez, você deve ver `Success=True` no `Stop` evento, indicando que a operação de carregamento foi bem-sucedida. O `ResultAssemblyPath` campo mostra o caminho do assembly resultante.

:::image type="content" source="media/collect-details/start-stop-success.png" alt-text="Imagem de eventos de iniciar e parar com êxito do PerfView":::

| Nome do evento             | AssemblyName                                                       | ActivityID | Êxito | ResultAssemblyPath                                      |
| ---------------------- | ------------------------------------------------------------------ |------------|---------| ------------------------------------------------------- |
| `AssemblyLoader/Start` |                  `MyLibrary, Culture=neutral, PublicKeyToken=null` | 1/2/     |         |                                                         |
| `AssemblyLoader/Start` | `MyLibrary, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null` | 1/2/1/   |         |                                                         |
| `AssemblyLoader/Stop`  | `MyLibrary, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null` | 1/2/1/   | Verdadeiro    | *C:\src\AssemblyLoading\bin\Debug\net5.0\MyLibrary.dll* |
| `AssemblyLoader/Stop`  |                  `MyLibrary, Culture=neutral, PublicKeyToken=null` | 1/2/     | Verdadeiro    | *C:\src\AssemblyLoading\bin\Debug\net5.0\MyLibrary.dll* |

Em seguida, podemos examinar os `ResolutionAttempted` eventos com a ID da atividade da carga externa para determinar a etapa na qual o assembly foi resolvido com êxito. Desta vez, os eventos mostrarão que o `AssemblyLoadContextResolvingEvent` estágio foi bem-sucedido. O `ResultAssemblyPath` campo mostra o caminho do assembly resultante.

:::image type="content" source="media/collect-details/resolution-attempted-success.png" alt-text="Imagem de eventos de ResolutionAttempted PerfView com êxito":::

| Nome do evento                           | AssemblyName                                      | Estágio                               | Result             | ResultAssemblyPath |
| ------------------------------------ | ------------------------------------------------- | ----------------------------------- | ------------------ | ------------------ |
| `AssemblyLoader/ResolutionAttempted` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `FindInLoadContext`                 | `AssemblyNotFound` |                    |
| `AssemblyLoader/ResolutionAttempted` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `ApplicationAssemblies`             | `AssemblyNotFound` |                    |
| `AssemblyLoader/ResolutionAttempted` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `AssemblyLoadContextResolvingEvent` | `Success`          | *C:\src\AssemblyLoading\bin\Debug\net5.0\MyLibrary.dll* |

Examinar `AssemblyLoadContextResolvingHandlerInvoked` eventos mostrará que o manipulador chamado `OnAssemblyLoadContextResolving` foi invocado. O `ResultAssemblyPath` campo mostra o caminho do assembly retornado pelo manipulador.

:::image type="content" source="media/collect-details/extension-point-success.png" alt-text="Imagem de eventos do ponto de extensão com êxito do PerfView":::

| Nome do evento                                                  | AssemblyName                                      | HandlerName                      | ResultAssemblyPath |
| ----------------------------------------------------------- | ------------------------------------------------- | -------------------------------- | ------------------ |
| `AssemblyLoader/AssemblyLoadContextResolvingHandlerInvoked` | `MyLibrary, Culture=neutral, PublicKeyToken=null` | `OnAssemblyLoadContextResolving` | *C:\src\AssemblyLoading\bin\Debug\net5.0\MyLibrary.dll* |

Observe que não há mais um `ResolutionAttempted` evento com o `AppDomainAssemblyResolveEvent` estágio ou qualquer evento `AppDomainAssemblyResolveHandlerInvoked` , pois o assembly foi carregado com êxito antes de atingir a etapa do algoritmo de carregamento que gera o <xref:System.AppDomain.AssemblyResolve?displayProperty=nameWithType> evento.

## <a name="see-also"></a>Consulte também

- [Eventos do carregador de assembly](../../fundamentals/diagnostics/runtime-loader-binder-events.md)
- [dotnet-trace](../diagnostics/dotnet-trace.md)
- [PerfView](https://github.com/microsoft/perfview)
