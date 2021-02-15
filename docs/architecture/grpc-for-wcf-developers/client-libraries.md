---
title: Criar bibliotecas de cliente do gRPC-gRPC para desenvolvedores do WCF
description: Discussão de bibliotecas/pacotes de cliente compartilhado para serviços gRPCs.
ms.date: 01/06/2021
ms.openlocfilehash: dee62bc793ab384f2556f1b3ff2fcb856c040f3a
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100427564"
---
# <a name="create-grpc-client-libraries"></a>Criar bibliotecas de cliente do gRPC

Não é necessário distribuir bibliotecas de cliente para um aplicativo gRPC. Você pode criar uma biblioteca compartilhada de `.proto` arquivos em sua organização e outras equipes podem usar esses arquivos para gerar o código do cliente em seus próprios projetos. Mas se você tiver um repositório do NuGet privado e muitas outras equipes estiverem usando o .NET, você poderá criar e publicar pacotes NuGet do cliente como parte do seu projeto de serviço. Essa abordagem pode ser uma boa maneira de compartilhar e promover seu serviço.

Uma vantagem de distribuir uma biblioteca de cliente é que você pode aprimorar as classes gRPC e Protobuf geradas com métodos e propriedades "conveniência" úteis. No código do cliente, como no servidor, todas as classes são declaradas como `partial` , para que você possa estendê-las sem editar o código gerado. Esse comportamento significa que é fácil adicionar construtores, métodos e propriedades calculadas aos tipos básicos.

> [!CAUTION]
> Você não deve usar código personalizado para fornecer funcionalidade essencial. Você não deseja restringir essa funcionalidade essencial às equipes do .NET que usam a biblioteca compartilhada e não fornecê-la a equipes que usam outras linguagens ou plataformas, como Python ou Java.

Verifique se o máximo de equipes possível pode acessar o serviço gRPC. A melhor maneira de fazer essa funcionalidade é compartilhar `.proto` arquivos para que os desenvolvedores possam gerar seus próprios clientes. Essa abordagem é particularmente verdadeira em um ambiente de várias plataformas, em que equipes diferentes frequentemente usam estruturas e linguagens de programação diferentes, ou onde sua API está acessível externamente.

## <a name="useful-extensions"></a>Extensões úteis

Há duas interfaces comumente usadas no .NET para lidar com fluxos de objetos: <xref:System.Collections.Generic.IEnumerable%601> e <xref:System.IObservable%601> . A partir do .NET Core 3,0 e do C# 8,0, há uma <xref:System.Collections.Generic.IAsyncEnumerable%601> interface para processar fluxos de forma assíncrona e uma `await foreach` sintaxe para usar a interface. Esta seção apresenta código reutilizável para aplicar essas interfaces a fluxos de gRPC.

Com as bibliotecas de cliente do .NET gRPC, há um `ReadAllAsync` método de extensão para `IAsyncStreamReader<T>` o que cria uma `IAsyncEnumerable<T>` interface. Para os desenvolvedores que usam a programação reativa, um método de extensão equivalente para criar uma `IObservable<T>` interface pode ser semelhante ao exemplo na seção a seguir.

### <a name="iobservable"></a>IObservable

A `IObservable<T>` interface é o inverso "reativo" de `IEnumerable<T>` . Em vez de extrair itens de um fluxo, a abordagem reativa permite que o fluxo Envie itens por push para um assinante. Esse comportamento é muito semelhante aos fluxos de gRPC, e é fácil encapsular uma `IObservable<T>` interface em uma `IAsyncStreamReader<T>` interface.

Esse código é maior do que o `IAsyncEnumerable<T>` código, porque o C# não tem suporte interno para trabalhar com observáveis. Você precisa criar a classe de implementação manualmente. No entanto, é uma classe genérica, portanto, uma única implementação funciona em todos os tipos.

```csharp
using System;
using System.Threading;

namespace Grpc.Core
{
    public class GrpcStreamObservable<T> : IObservable<T>
    {
        private readonly IAsyncStreamReader<T> _reader;
        private readonly CancellationToken _token;
        private int _used;

        public GrpcStreamObservable(IAsyncStreamReader<T> reader, CancellationToken token = default)
        {
            _reader = reader ?? throw new ArgumentNullException(nameof(reader));
            _token = token;
            _used = 0;
        }

        public IDisposable Subscribe(IObserver<T> observer) =>
            Interlocked.Exchange(ref _used, 1) == 0
                ? new GrpcStreamSubscription<T>(_reader, observer, _token)
                : throw new InvalidOperationException("Subscribe can only be called once.");

    }
}
```

> [!IMPORTANT]
> Essa implementação observável permite que o `Subscribe` método seja chamado apenas uma vez, porque ter vários assinantes tentando ler a partir do fluxo resultaria em caos. Há operadores, como `Replay` no [sistema. Reactive. Linq](https://www.nuget.org/packages/System.Reactive.Linq), que habilitam o armazenamento em buffer e o compartilhamento repetível de observáveis, que podem ser usados com essa implementação.

A `GrpcStreamSubscription` classe manipula a enumeração do `IAsyncStreamReader` :

```csharp
public class GrpcStreamSubscription<T> : IDisposable
{
    private readonly IAsyncStreamReader<T> _reader;
    private readonly IObserver<T> _observer;

    private readonly CancellationTokenSource _tokenSource;

    private readonly Task _task;

    private bool _completed;

    public GrpcStreamSubscription(IAsyncStreamReader<T> reader, IObserver<T> observer, CancellationToken token = default)
    {
        _reader = reader ?? throw new ArgumentNullException(nameof(reader));
        _observer = observer ?? throw new ArgumentNullException(nameof(observer));

        _tokenSource = new CancellationTokenSource();
        token.Register(_tokenSource.Cancel);

        _task = Run(_tokenSource.Token);
    }

    private async Task Run(CancellationToken token)
    {
        while (!token.IsCancellationRequested)
        {
            try
            {
                if (!await _reader.MoveNext(token)) break;
            }
            catch (RpcException e) when (e.StatusCode == Grpc.Core.StatusCode.NotFound)
            {
                break;
            }
            catch (OperationCanceledException)
            {
                break;
            }
            catch (Exception e)
            {
                _observer.OnError(e);
                _completed = true;
                return;
            }

            _observer.OnNext(_reader.Current);
        }

        _completed = true;
        _observer.OnCompleted();
    }

    public void Dispose()
    {
        if (!_completed && !_tokenSource.IsCancellationRequested)
        {
            _tokenSource.Cancel();
        }

        _tokenSource.Dispose();
        _task.Dispose();
    }

}
```

Tudo o que é necessário agora é um método de extensão simples para criar o observável do leitor de fluxo.

```csharp
using System;
using System.Threading;

namespace Grpc.Core
{
    public static class AsyncStreamReaderObservableExtensions
    {
        public static IObservable<T> AsObservable<T>(
            this IAsyncStreamReader<T> reader,
            CancellationToken cancellationToken = default) =>
            new GrpcStreamObservable<T>(reader, cancellationToken);
    }
}
```

## <a name="summary"></a>Resumo

Os <xref:System.Collections.Generic.IAsyncEnumerable%601> <xref:System.IObservable%601> modelos e são maneiras bem suportadas e bem documentadas de lidar com fluxos de dados assíncronos no .net. o gRPC streams mapeia bem para ambos os paradigmas, oferecendo integração próxima com o .NET e estilos de programação reativos e assíncronos.

>[!div class="step-by-step"]
>[Anterior](streaming-versus-repeated.md) 
> [Avançar](security.md)
