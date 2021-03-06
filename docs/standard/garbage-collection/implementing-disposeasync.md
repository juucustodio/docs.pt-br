---
title: Implementar um método DisposeAsync
description: Saiba como implementar os métodos DisposeAsync e DisposeAsyncCore para executar a limpeza assíncrona de recursos.
author: IEvangelist
ms.author: dapine
ms.date: 09/10/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
helpviewer_keywords:
- DisposeAsync method
- garbage collection, DisposeAsync method
ms.openlocfilehash: 88adf9e484baa0e65e2ff093b4649cf35b8c86dc
ms.sourcegitcommit: 6d4ee46871deb9ea1e45bb5f3784474e240bbc26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90022903"
---
# <a name="implement-a-disposeasync-method"></a>Implementar um método DisposeAsync

A <xref:System.IAsyncDisposable?displayProperty=nameWithType> interface foi introduzida como parte do C# 8,0. Você implementa o <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> método quando precisa executar a limpeza de recursos, assim como faria ao [implementar um método Dispose](implementing-dispose.md). No entanto, uma das principais diferenças é que essa implementação permite operações de limpeza assíncronas. O <xref:System.IAsyncDisposable.DisposeAsync> retorna um <xref:System.Threading.Tasks.ValueTask> que representa a operação de descarte assíncrona.

É comum ao implementar a <xref:System.IAsyncDisposable> interface que as classes também implementarão a <xref:System.IDisposable> interface. Um bom padrão de implementação da <xref:System.IAsyncDisposable> interface é estar preparado para o descarte síncrono ou assíncrono. Todas as diretrizes para implementar o padrão Dispose também se aplicam à implementação assíncrona. Este artigo pressupõe que você já esteja familiarizado com a forma de [implementar um método Dispose](implementing-dispose.md).

## <a name="disposeasync-and-disposeasynccore"></a>DisposeAsync () e DisposeAsyncCore ()

A <xref:System.IAsyncDisposable> interface declara um único método sem parâmetros, <xref:System.IAsyncDisposable.DisposeAsync> . Qualquer classe não selada deve ter um `DisposeAsyncCore()` método adicional que também retorna um <xref:System.Threading.Tasks.ValueTask> .

- Uma `public` <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> implementação que não tem parâmetros.
- Um `protected virtual ValueTask DisposeAsyncCore()` método cuja assinatura é:

  ```csharp
  protected virtual ValueTask DisposeAsyncCore()
  {
  }
  ```

### <a name="the-disposeasync-method"></a>O método DisposeAsync ()

O `public` método sem parâmetros `DisposeAsync()` é chamado implicitamente em uma `await using` instrução, e sua finalidade é liberar recursos não gerenciados, executar a limpeza geral e indicar que o finalizador, se houver, não precisa ser executado. Liberar a memória associada a um objeto gerenciado é sempre o domínio do coletor de [lixo](index.md). Por isso, ele tem uma implementação padrão:

```csharp
public async ValueTask DisposeAsync()
{
    // Perform async cleanup.
    await DisposeAsyncCore();

    // Dispose of unmanaged resources.
    Dispose(false);
    // Suppress finalization.
    GC.SuppressFinalize(this);
}
```

> [!NOTE]
> Uma diferença principal no padrão de descarte assíncrono comparado ao padrão Dispose é que a chamada de <xref:System.IAsyncDisposable.DisposeAsync> para o `Dispose(bool)` método Overload é fornecida `false` como um argumento. <xref:System.IDisposable.Dispose?displayProperty=nameWithType>No entanto, ao implementar o método, `true` será passado. Isso ajuda a garantir a equivalência funcional com o padrão de descarte síncrono e garante ainda mais que os caminhos de código do finalizador ainda sejam invocados. Em outras palavras, o `DisposeAsyncCore()` método descartará os recursos gerenciados de forma assíncrona, de modo que você não deseje descartar também de maneira síncrona. Portanto, chame `Dispose(false)` em vez de `Dispose(true)` .

### <a name="the-disposeasynccore-method"></a>O método DisposeAsyncCore ()

O `DisposeAsyncCore()` método destina-se a executar a limpeza assíncrona de recursos gerenciados ou para chamadas em cascata para o `DisposeAsync()` . Ele encapsula as operações comuns de limpeza assíncrona quando uma subclasse herda uma classe base que é uma implementação de <xref:System.IAsyncDisposable> . O `DisposeAsyncCore()` método é `virtual` para que as classes derivadas possam definir limpeza adicional em suas substituições.

> [!TIP]
> Se uma implementação do <xref:System.IAsyncDisposable> for `sealed` , o `DisposeAsyncCore()` método não será necessário e a limpeza assíncrona poderá ser executada diretamente no <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> método.

## <a name="implement-the-async-dispose-pattern"></a>Implementar o padrão de descarte assíncrono

Todas as classes não seladas devem ser consideradas uma classe base em potencial, pois elas podem ser herdadas. Se você implementar o padrão de descarte assíncrono para qualquer classe base em potencial, você deve fornecer o `protected virtual ValueTask DisposeAsyncCore()` método. Aqui está um exemplo de implementação do padrão de descarte assíncrono que usa um <xref:System.Text.Json.Utf8JsonWriter?displayProperty=nameWithType> .

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/disposeasync.cs":::

O exemplo anterior usa o <xref:System.Text.Json.Utf8JsonWriter> . Para obter mais informações sobre `System.Text.Json` o, consulte [como migrar do Newtonsoft.Jspara o System.Text.Jsno](../serialization/system-text-json-migrate-from-newtonsoft-how-to.md).

## <a name="implement-both-dispose-and-async-dispose-patterns"></a>Implementar os padrões Dispose e assíncrona de descarte

Talvez seja necessário implementar as <xref:System.IDisposable> <xref:System.IAsyncDisposable> interfaces e, especialmente quando seu escopo de classe contiver instâncias dessas implementações. Isso garante que você possa propagar corretamente as chamadas de limpeza. Aqui está uma classe de exemplo que implementa ambas as interfaces e demonstra as diretrizes apropriadas para a limpeza.

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/dispose-and-disposeasync.cs":::

As <xref:System.IDisposable.Dispose?displayProperty=nameWithType> <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType> implementações e são código clichê simples. Os `Dispose(bool)` `DisposeAsyncCore()` métodos e começam verificando se `_disposed` é `true` e serão executados somente quando for `false` .

No `Dispose(bool)` método Overload, a <xref:System.IDisposable> instância é descartada condicionalmente de se não for `null` . A <xref:System.IAsyncDisposable> instância é convertida como <xref:System.IDisposable> e, se também não estiver `null` descartada. As duas instâncias são então atribuídas a `null` .

Com o `DisposeAsyncCore()` método, a mesma abordagem lógica é seguida. Se a <xref:System.IAsyncDisposable> instância não for `null` , sua chamada para `DisposeAsync().ConfigureAwait(false)` será esperada. Se a <xref:System.IDisposable> instância também for uma implementação do <xref:System.IAsyncDisposable> , ela também será descartada de forma assíncrona. As duas instâncias são então atribuídas a `null` .

## <a name="using-async-disposable"></a>Usando o descartável assíncrono

Para consumir corretamente um objeto que implementa a <xref:System.IAsyncDisposable> interface, use o [Await](../../csharp/language-reference/operators/await.md)e o [uso](../../csharp/language-reference/keywords/using-statement.md) de palavras-chave juntas. Considere o exemplo a seguir, em que a `ExampleAsyncDisposable` classe é instanciada e, em seguida, encapsulada em uma `await using` instrução.

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/proper-await-using.cs":::

> [!IMPORTANT]
> Use o <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)> método de extensão da <xref:System.IAsyncDisposable> interface para configurar como a continuação da tarefa é marshalled em seu contexto ou Agendador original. Para obter mais informações sobre o `ConfigureAwait` , consulte [perguntas frequentes](https://devblogs.microsoft.com/dotnet/configureawait-faq/)sobre o ConfigureAwait.

Para situações em que o uso de `ConfigureAwait` não é necessário, a `await using` instrução poderia ser simplificada da seguinte maneira:

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/await-using-non-configureawait.cs":::

Além disso, ele poderia ser escrito para usar o escopo implícito de uma [declaração using](../../csharp/whats-new/csharp-8.md#using-declarations).

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/await-using-declaration.cs":::

## <a name="stacked-usings"></a>Uso empilhado

Em situações em que você cria e usa vários objetos que implementam <xref:System.IAsyncDisposable> , é possível que as `using` instruções de empilhamento em condições errônea pudessem impedir chamadas para <xref:System.IAsyncDisposable.DisposeAsync> . Para ajudar a evitar possíveis preocupações, você deve evitar o empilhamento e, em vez disso, seguir este padrão de exemplo:

:::code language="csharp" source="../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.asyncdisposable/stacked-await-usings.cs":::

## <a name="see-also"></a>Confira também

- <xref:System.IAsyncDisposable>
- <xref:System.IAsyncDisposable.DisposeAsync?displayProperty=nameWithType>
- <xref:System.Threading.Tasks.TaskAsyncEnumerableExtensions.ConfigureAwait(System.IAsyncDisposable,System.Boolean)>
