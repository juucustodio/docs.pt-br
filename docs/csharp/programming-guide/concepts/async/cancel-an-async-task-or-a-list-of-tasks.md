---
title: Cancelar uma lista de tarefas (C#)
description: Saiba como usar tokens de cancelamento para sinalizar uma solicitação de cancelamento para uma lista de tarefas.
ms.date: 02/03/2021
ms.topic: tutorial
ms.assetid: eec32dbb-70ea-4c88-bd27-fa2e34546914
ms.openlocfilehash: 532c61ab6499583620ba2ee5c710c58f7886f89d
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585735"
---
# <a name="cancel-a-list-of-tasks-c"></a>Cancelar uma lista de tarefas (C#)

Você pode cancelar um aplicativo de console assíncrono se não quiser esperar que ele seja concluído. Seguindo o exemplo neste tópico, você pode adicionar um cancelamento a um aplicativo que baixa o conteúdo de uma lista de sites. Você pode cancelar várias tarefas associando a <xref:System.Threading.CancellationTokenSource> instância a cada tarefa. Se você selecionar a tecla <kbd>Enter</kbd> , cancelará todas as tarefas que ainda não foram concluídas.

Este tutorial abrange:

> [!div class="checklist"]
>
> - Criando um aplicativo de console .NET
> - Escrevendo um aplicativo assíncrono que dá suporte ao cancelamento
> - Demonstrando o cancelamento de sinalização

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial exige o seguinte:

- [SDK do .NET 5,0 ou posterior](https://dotnet.microsoft.com/download/dotnet/5.0)
- IDE (ambiente de desenvolvimento integrado)
  - [Recomendamos o Visual Studio, Visual Studio Code ou Visual Studio para Mac](https://visualstudio.microsoft.com)

### <a name="create-example-application"></a>Criar aplicativo de exemplo

Crie um novo aplicativo de console .NET Core. Você pode criar um usando o [`dotnet new console`](../../../../core/tools/dotnet-new.md#console) comando ou do [Visual Studio](/visualstudio/install/install-visual-studio). Abra o arquivo *Program.cs* em seu editor de código favorito.

### <a name="replace-using-statements"></a>Substituir usando instruções

Substitua as instruções using existentes por estas declarações:

```csharp
using System;
using System.Collections.Generic;
using System.Diagnostics;
using System.Net.Http;
using System.Threading;
using System.Threading.Tasks;
```

## <a name="add-fields"></a>Adicionar campos

Na `Program` definição de classe, adicione estes três campos:

```csharp
static readonly CancellationTokenSource s_cts = new CancellationTokenSource();

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

O <xref:System.Threading.CancellationTokenSource> é usado para sinalizar um cancelamento solicitado para um <xref:System.Threading.CancellationToken> . O `HttpClient` expõe a capacidade de enviar solicitações HTTP e receber respostas http. O `s_urlList` mantém todas as URLs que o aplicativo planeja processar.

## <a name="update-application-entry-point"></a>Atualizar ponto de entrada do aplicativo

O ponto de entrada principal no aplicativo de console é o `Main` método. Substitua o método existente pelo seguinte:

```csharp
static async Task Main()
{
    Console.WriteLine("Application started.");
    Console.WriteLine("Press the ENTER key to cancel...\n");

    Task cancelTask = Task.Run(() =>
    {
        while (Console.ReadKey().Key != ConsoleKey.Enter)
        {
            Console.WriteLine("Press the ENTER key to cancel...");
        }

        Console.WriteLine("\nENTER key pressed: cancelling downloads.\n");
        s_cts.Cancel();
    });

    Task sumPageSizesTask = SumPageSizesAsync();

    await Task.WhenAny(new[] { cancelTask, sumPageSizesTask });

    Console.WriteLine("Application ending.");
}
```

O `Main` método atualizado agora é considerado um [Async Main](../../../whats-new/csharp-7.md#async-main), que permite um ponto de entrada assíncrono no executável. Ele grava algumas mensagens instrutivas no console e, em seguida, declara uma <xref:System.Threading.Tasks.Task> instância chamada `cancelTask` , que lerá os traços de tecla do console. Se a tecla <kbd>Enter</kbd> for pressionada, será feita uma chamada para <xref:System.Threading.CancellationTokenSource.Cancel?displayProperty=nameWithType> . Isso sinalizará o cancelamento. Em seguida, a `sumPageSizesTask` variável é atribuída a partir do `SumPageSizesAsync` método. Em seguida, as duas tarefas são passadas para <xref:System.Threading.Tasks.Task.WhenAny(System.Threading.Tasks.Task[])?displayProperty=nameWithType> o, o que continuará quando qualquer uma das duas tarefas for concluída.

## <a name="create-the-asynchronous-sum-page-sizes-method"></a>Criar o método de tamanhos de página de soma assíncrona

Abaixo do `Main` método, adicione o `SumPageSizesAsync` método:

```csharp
static async Task SumPageSizesAsync()
{
    var stopwatch = Stopwatch.StartNew();

    int total = 0;
    foreach (string url in s_urlList)
    {
        int contentLength = await ProcessUrlAsync(url, s_client, s_cts.Token);
        total += contentLength;
    }

    stopwatch.Stop();

    Console.WriteLine($"\nTotal bytes returned:  {total:#,#}");
    Console.WriteLine($"Elapsed time:          {stopwatch.Elapsed}\n");
}
```

O método começa instanciando e iniciando um <xref:System.Diagnostics.Stopwatch> . Em seguida, ele executa um loop em cada URL nas `s_urlList` chamadas e `ProcessUrlAsync` . Com cada iteração, o `s_cts.Token` é passado para o `ProcessUrlAsync` método e o código retorna um <xref:System.Threading.Tasks.Task%601> , em que `TResult` é um inteiro:

```csharp
int total = 0;
foreach (string url in s_urlList)
{
    int contentLength = await ProcessUrlAsync(url, s_client, s_cts.Token);
    total += contentLength;
}
```

## <a name="add-process-method"></a>Adicionar método de processo

Adicione o seguinte `ProcessUrlAsync` método abaixo do `SumPageSizesAsync` método:

```csharp
static async Task<int> ProcessUrlAsync(string url, HttpClient client, CancellationToken token)
{
    HttpResponseMessage response = await client.GetAsync(url, token);
    byte[] content = await response.Content.ReadAsByteArrayAsync(token);
    Console.WriteLine($"{url,-60} {content.Length,10:#,#}");

    return content.Length;
}
```

Para qualquer URL fornecida, o método usará a `client` instância fornecida para obter a resposta como um `byte[]` . A <xref:System.Threading.CancellationToken> instância é passada para os <xref:System.Net.Http.HttpClient.GetAsync(System.String,System.Threading.CancellationToken)?displayProperty=nameWithType> <xref:System.Net.Http.HttpContent.ReadAsByteArrayAsync?displayProperty=nameWithType> métodos e. O `token` é usado para se registrar para o cancelamento solicitado. O comprimento é retornado depois que a URL e o comprimento são gravados no console.

### <a name="example-application-output"></a>Exemplo de saída de aplicativo

```console
Application started.
Press the ENTER key to cancel...

https://docs.microsoft.com                                       37,357
https://docs.microsoft.com/aspnet/core                           85,589
https://docs.microsoft.com/azure                                398,939
https://docs.microsoft.com/azure/devops                          73,663
https://docs.microsoft.com/dotnet                                67,452
https://docs.microsoft.com/dynamics365                           48,582
https://docs.microsoft.com/education                             22,924

ENTER key pressed: cancelling downloads.

Application ending.
```

## <a name="complete-example"></a>Exemplo completo

O código a seguir é o texto completo do arquivo *Program.cs* para o exemplo.

:::code language="csharp" source="snippets/cancel-tasks/cancel-tasks/Program.cs":::

## <a name="see-also"></a>Consulte também

- <xref:System.Threading.CancellationToken>
- <xref:System.Threading.CancellationTokenSource>
- [Programação assíncrona com async e await (C#)](index.md)

## <a name="next-steps"></a>Próximas etapas

> [!div class="nextstepaction"]
> [Cancelar tarefas assíncronas após um período (C#)](cancel-async-tasks-after-a-period-of-time.md)
