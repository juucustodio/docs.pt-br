---
title: Cancelar tarefas assíncronas após um período de tempo (C#) "
description: Saiba como agendar o cancelamento de todas as tarefas associadas que não foram concluídas em um período de tempo.
ms.date: 02/03/2021
ms.topic: tutorial
ms.assetid: 194282c2-399f-46da-a7a6-96674e00b0b3
ms.openlocfilehash: 98c42a2df6153d668b99b6dec49ffe380293b205
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585371"
---
# <a name="cancel-async-tasks-after-a-period-of-time-c"></a>Cancelar tarefas assíncronas após um período (C#)

Você pode cancelar uma operação assíncrona após um período de tempo usando o <xref:System.Threading.CancellationTokenSource.CancelAfter%2A?displayProperty=nameWithType> método se não quiser aguardar a conclusão da operação. Esse método agenda o cancelamento de todas as tarefas associadas que não são concluídas dentro do período designado pela `CancelAfter` expressão.

Este exemplo adiciona ao código desenvolvido em [cancelar uma lista de tarefas (C#)](cancel-an-async-task-or-a-list-of-tasks.md) para baixar uma lista de sites e exibir o comprimento do conteúdo de cada um.

Este tutorial abrange:

> [!div class="checklist"]
>
> - Atualizando um aplicativo de console .NET existente
> - Agendando um cancelamento

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial exige o seguinte:

- Você deve ter criado um aplicativo no tutorial [cancelar uma lista de tarefas (C#)](cancel-an-async-task-or-a-list-of-tasks.md)
- [SDK do .NET 5,0 ou posterior](https://dotnet.microsoft.com/download/dotnet/5.0)
- IDE (ambiente de desenvolvimento integrado)
  - [Recomendamos o Visual Studio, Visual Studio Code ou Visual Studio para Mac](https://visualstudio.microsoft.com)

## <a name="update-application-entry-point"></a>Atualizar ponto de entrada do aplicativo

Substitua o `Main` método existente pelo seguinte:

```csharp
static async Task Main()
{
    Console.WriteLine("Application started.");

    try
    {
        s_cts.CancelAfter(3500);

        await SumPageSizesAsync();
    }
    catch (TaskCanceledException)
    {
        Console.WriteLine("\nTasks cancelled: timed out.\n");
    }
    finally
    {
        s_cts.Dispose();
    }

    Console.WriteLine("Application ending.");
}
```

O `Main` método atualizado grava algumas mensagens instrutivas no console do. Dentro de [try catch](../../../language-reference/keywords/try-catch.md), uma chamada para <xref:System.Threading.CancellationTokenSource.CancelAfter(System.Int32)?displayProperty=nameWithType> agendar um cancelamento. Isso sinalizará o cancelamento após um período de tempo.

Em seguida, o `SumPageSizesAsync` método é aguardado. Se o processamento de todas as URLs ocorrer mais rápido do que o cancelamento agendado, o aplicativo será encerrado. No entanto, se o cancelamento agendado for disparado antes que todas as URLs sejam processadas, um <xref:System.Threading.Tasks.TaskCanceledException> será lançado.

### <a name="example-application-output"></a>Exemplo de saída de aplicativo

```console
Application started.

https://docs.microsoft.com                                       37,357
https://docs.microsoft.com/aspnet/core                           85,589
https://docs.microsoft.com/azure                                398,939
https://docs.microsoft.com/azure/devops                          73,663

Tasks cancelled: timed out.

Application ending.
```

## <a name="complete-example"></a>Exemplo completo

O código a seguir é o texto completo do arquivo *Program.cs* para o exemplo.

:::code language="csharp" source="snippets/cancel-tasks/cancel-task-after-period-of-time/Program.cs":::

## <a name="see-also"></a>Consulte também

- <xref:System.Threading.CancellationToken>
- <xref:System.Threading.CancellationTokenSource>
- [Programação assíncrona com async e await (C#)](index.md)
- [Cancelar uma lista de tarefas (C#)](cancel-an-async-task-or-a-list-of-tasks.md)
