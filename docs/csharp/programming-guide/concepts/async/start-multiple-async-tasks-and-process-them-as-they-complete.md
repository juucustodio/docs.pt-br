---
title: Processar tarefas assíncronas conforme elas são concluídas
description: Este exemplo mostra como usar Task. WhenAny em C# para iniciar várias tarefas e processar seus resultados à medida que eles são concluídos, em vez de processá-los no pedido iniciado.
ms.date: 08/19/2020
ms.assetid: 25331850-35a7-43b3-ab76-3908e4346b9d
ms.openlocfilehash: 4cdd35af900863895911ea5c2c9772af362951ec
ms.sourcegitcommit: 632818f4b527e5bf3c48fc04e0c7f3b4bdb8a248
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/20/2021
ms.locfileid: "98615965"
---
# <a name="process-asynchronous-tasks-as-they-complete-c"></a>Processar tarefas assíncronas conforme elas são concluídas (C#)

Usando <xref:System.Threading.Tasks.Task.WhenAny%2A?displayProperty=nameWithType> o, você pode iniciar várias tarefas ao mesmo tempo e processá-las uma a uma conforme elas são concluídas, em vez de processá-las na ordem em que elas são iniciadas.

O exemplo a seguir usa uma consulta para criar uma coleção de tarefas. Cada tarefa baixa o conteúdo de um site especificado. Em cada iteração de um loop "while", uma chamada esperada para <xref:System.Threading.Tasks.Task.WhenAny%2A> retorna a tarefa na coleção de tarefas que concluir o download primeiro. Essa tarefa é removida da coleção e processada. O loop é repetido até que a coleção não contenha mais tarefas.

## <a name="create-example-application"></a>Criar aplicativo de exemplo

Crie um novo aplicativo de console .NET Core. Você pode criar um usando o comando [dotnet New console](../../../../core/tools/dotnet-new.md#console) ou do [Visual Studio](/visualstudio/install/install-visual-studio). Abra o arquivo *Program.cs* em seu editor de código favorito.

### <a name="replace-using-statements"></a>Substituir usando instruções

Substitua as instruções using existentes por estas declarações:

```csharp
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Linq;
using System.Net.Http;
using System.Threading.Tasks;
```

## <a name="add-fields"></a>Adicionar campos

Na `Program` definição de classe, adicione os dois campos a seguir:

```csharp
static readonly HttpClient s_client = new HttpClient
{
    MaxResponseContentBufferSize = 1_000_000
};

static readonly IEnumerable<string> s_urlList = new string[]
{
    "https://docs.microsoft.com",
    "https://docs.microsoft.com/aspnet/core",
    "https://docs.microsoft.com/azure",
    "https://docs.microsoft.com/azure/devops",
    "https://docs.microsoft.com/dotnet",
    "https://docs.microsoft.com/dynamics365",
    "https://docs.microsoft.com/education",
    "https://docs.microsoft.com/enterprise-mobility-security",
    "https://docs.microsoft.com/gaming",
    "https://docs.microsoft.com/graph",
    "https://docs.microsoft.com/microsoft-365",
    "https://docs.microsoft.com/office",
    "https://docs.microsoft.com/powershell",
    "https://docs.microsoft.com/sql",
    "https://docs.microsoft.com/surface",
    "https://docs.microsoft.com/system-center",
    "https://docs.microsoft.com/visualstudio",
    "https://docs.microsoft.com/windows",
    "https://docs.microsoft.com/xamarin"
};
```

O `HttpClient` expõe a capacidade de enviar solicitações HTTP e receber respostas http. O `s_urlList` mantém todas as URLs que o aplicativo planeja processar.

## <a name="update-application-entry-point"></a>Atualizar ponto de entrada do aplicativo

O ponto de entrada principal no aplicativo de console é o `Main` método. Substitua o método existente pelo seguinte:

```csharp
static Task Main() => SumPageSizesAsync();
```

O `Main` método atualizado agora é considerado um [Async Main](../../../whats-new/csharp-7.md#async-main), que permite um ponto de entrada assíncrono no executável. É expressa uma chamada para `SumPageSizesAsync` .

## <a name="create-the-asynchronous-sum-page-sizes-method"></a>Criar o método de tamanhos de página de soma assíncrona

Abaixo do `Main` método, adicione o `SumPageSizesAsync` método:

```csharp
static async Task SumPageSizesAsync()
{
    var stopwatch = Stopwatch.StartNew();

    IEnumerable<Task<int>> downloadTasksQuery =
        from url in s_urlList
        select ProcessUrlAsync(url, s_client);

    List<Task<int>> downloadTasks = downloadTasksQuery.ToList();

    int total = 0;
    while (downloadTasks.Any())
    {
        Task<int> finishedTask = await Task.WhenAny(downloadTasks);
        downloadTasks.Remove(finishedTask);
        total += await finishedTask;
    }

    stopwatch.Stop();

    Console.WriteLine($"\nTotal bytes returned:  {total:#,#}");
    Console.WriteLine($"Elapsed time:          {stopwatch.Elapsed}\n");
}
```

O método começa instanciando e iniciando um <xref:System.Diagnostics.Stopwatch> . Em seguida, ele inclui uma consulta que, quando executada, cria uma coleção de tarefas. Cada chamada para `ProcessUrlAsync` no código a seguir retorna um <xref:System.Threading.Tasks.Task%601>, em que `TResult` é um inteiro:

```csharp
IEnumerable<Task<int>> downloadTasksQuery =
    from url in s_urlList
    select ProcessUrlAsync(url, s_client);
```

Devido à [execução retardada](../../../../standard/linq/deferred-execution-example.md) com o LINQ, você chama <xref:System.Linq.Enumerable.ToList%2A?displayProperty=nameWithType> para iniciar cada tarefa.

```csharp
List<Task<int>> downloadTasks = downloadTasksQuery.ToList();
```

O `while` loop executa as seguintes etapas para cada tarefa na coleção:

1. Aguarda uma chamada para `WhenAny` para identificar a primeira tarefa na coleção que concluiu seu download.

    ```csharp
    Task<int> finishedTask = await Task.WhenAny(downloadTasks);
    ```

1. Remove a tarefa da coleção.

    ```csharp
    downloadTasks.Remove(finishedTask);
    ```

1. Espera `finishedTask`, que é retornado por uma chamada para `ProcessUrlAsync`. A variável `finishedTask` é uma <xref:System.Threading.Tasks.Task%601> em que `TResult` é um inteiro. A tarefa já foi concluída, mas você espera para recuperar o tamanho do site baixado, como mostra o exemplo a seguir. Se a tarefa tiver falhado, `await` o lançará a primeira exceção filha armazenada no `AggregateException` , ao contrário da leitura da <xref:System.Threading.Tasks.Task%601.Result?displayProperty=nameWithType> propriedade, que geraria o `AggregateException` .

    ```csharp
    total += await finishedTask;
    ```

## <a name="add-process-method"></a>Adicionar método de processo

Adicione o seguinte `ProcessUrlAsync` método abaixo do `SumPageSizesAsync` método:

```csharp
static async Task<int> ProcessUrlAsync(string url, HttpClient client)
{
    byte[] content = await client.GetByteArrayAsync(url);
    Console.WriteLine($"{url,-60} {content.Length,10:#,#}");

    return content.Length;
}
```

Para qualquer URL fornecida, o método usará a `client` instância fornecida para obter a resposta como um `byte[]` . O comprimento é retornado depois que a URL e o comprimento são gravados no console.

Execute o programa várias vezes para verificar se os tamanhos baixados não aparecem sempre na mesma ordem.

> [!CAUTION]
> Você pode usar `WhenAny` em um loop, conforme descrito no exemplo, para resolver problemas que envolvem um número pequeno de tarefas. No entanto, outras abordagens são mais eficientes se você tiver um número grande de tarefas para processar. Para obter mais informações e exemplos, consulte [Processando tarefas quando elas são concluídas](https://devblogs.microsoft.com/pfxteam/processing-tasks-as-they-complete).

## <a name="complete-example"></a>Exemplo completo

O código a seguir é o texto completo do arquivo *Program.cs* para o exemplo.

:::code language="csharp" source="snippets/multiple-tasks/Program.cs":::

## <a name="see-also"></a>Veja também

- <xref:System.Threading.Tasks.Task.WhenAny%2A>
- [Programação assíncrona com async e await (C#)](index.md)
