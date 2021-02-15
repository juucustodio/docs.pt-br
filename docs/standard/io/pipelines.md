---
title: Pipelines de e/s-.NET
description: Saiba como usar pipelines de e/s com eficiência no .NET e evitar problemas em seu código.
ms.date: 08/27/2020
helpviewer_keywords:
- Pipelines
- Pipelines I/O
- I/O [.NET], Pipelines
author: rick-anderson
ms.author: riande
ms.openlocfilehash: 508ae0e2b854f81ee639a63063a8f6d73ae84863
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94830630"
---
# <a name="systemiopipelines-in-net"></a>System. IO. pipelines no .NET

<xref:System.IO.Pipelines> é uma nova biblioteca criada para facilitar a execução de e/s de alto desempenho no .NET. É uma biblioteca direcionada .NET Standard que funciona em todas as implementações do .NET.

<a name="solve"></a>

## <a name="what-problem-does-systemiopipelines-solve"></a>Qual problema o System. IO. pipelines resolve

<!-- corner case doesn't MT (machine translate)   -->
Aplicativos que analisam dados de streaming são compostos por código clichê com muitos fluxos de código especializados e incomuns. O código de caso clichê e especial é complexo e difícil de manter.

`System.IO.Pipelines` foi arquitetado para:

* Ter dados de streaming de análise de alto desempenho.
* Reduza a complexidade do código.

O código a seguir é típico para um servidor TCP que recebe mensagens delimitadas por linha (delimitadas por `'\n'` ) de um cliente:

```csharp
async Task ProcessLinesAsync(NetworkStream stream)
{
    var buffer = new byte[1024];
    await stream.ReadAsync(buffer, 0, buffer.Length);

    // Process a single line from the buffer
    ProcessLine(buffer);
}
```

O código anterior tem vários problemas:

* A mensagem inteira (fim da linha) não pode ser recebida em uma única chamada para `ReadAsync` .
* Ele está ignorando o resultado de `stream.ReadAsync` . `stream.ReadAsync` Retorna o número de dados lidos.
* Ele não manipula o caso em que várias linhas são lidas em uma única `ReadAsync` chamada.
* Ele aloca uma `byte` matriz com cada leitura.

Para corrigir os problemas anteriores, as seguintes alterações são necessárias:

* Armazenar os dados de entrada em buffer até que uma nova linha seja encontrada.
* Analise todas as linhas retornadas no buffer.
* É possível que a linha seja maior que 1 KB (1024 bytes). O código precisa redimensionar o buffer de entrada até que o delimitador seja encontrado para ajustar a linha completa dentro do buffer.

  * Se o buffer for redimensionado, mais cópias de buffer serão feitas conforme as linhas mais longas aparecerem na entrada.
  * Para reduzir o espaço desperdiçado, compacte o buffer usado para ler as linhas.

* Considere o uso do pool de buffers para evitar a alocação repetida de memória.
* O código a seguir aborda alguns desses problemas:

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/ProcessLinesAsync.cs" id="snippet":::

O código anterior é complexo e não aborda todos os problemas identificados. A rede de alto desempenho geralmente significa escrever código muito complexo para maximizar o desempenho. `System.IO.Pipelines` foi projetado para tornar mais fácil a criação desse tipo de código.

[!INCLUDE [localized code comments](../../../includes/code-comments-loc.md)]

## <a name="pipe"></a>Pipe

A <xref:System.IO.Pipelines.Pipe> classe pode ser usada para criar um `PipeWriter/PipeReader` par. Todos os dados gravados no `PipeWriter` estão disponíveis no `PipeReader` :

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/Pipe.cs" id="snippet2":::

<a name="pbu"></a>

### <a name="pipe-basic-usage"></a>Uso básico do pipe

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/Pipe.cs" id="snippet":::

Há dois loops:

* `FillPipeAsync` lê do `Socket` e grava no `PipeWriter` .
* `ReadPipeAsync` lê de `PipeReader` e analisa as linhas de entrada.

Não há buffers explícitos alocados. Todo o gerenciamento de buffer é delegado às `PipeReader` `PipeWriter` implementações e. A delegação do gerenciamento de buffer facilita o consumo do código para se concentrar exclusivamente na lógica de negócios.

No primeiro loop:

* <xref:System.IO.Pipelines.PipeWriter.GetMemory(System.Int32)?displayProperty=nameWithType> é chamado para obter memória do gravador subjacente.
* <xref:System.IO.Pipelines.PipeWriter.Advance(System.Int32)?displayProperty=nameWithType> é chamado para informar a `PipeWriter` quantidade de dados gravados no buffer.
* <xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A?displayProperty=nameWithType> é chamado para disponibilizar os dados para o `PipeReader` .

No segundo loop, o `PipeReader` consome os buffers gravados pelo `PipeWriter` . Os buffers são provenientes do soquete. A chamada para `PipeReader.ReadAsync` :

* Retorna um <xref:System.IO.Pipelines.ReadResult> que contém duas partes importantes de informações:

  * Os dados que foram lidos na forma de `ReadOnlySequence<byte>` .
  * Um booliano `IsCompleted` que indica se o fim de dados (EOF) foi atingido.

Depois de encontrar o delimitador de fim de linha (EOL) e analisar a linha:

* A lógica processa o buffer para ignorar o que já foi processado.
* `PipeReader.AdvanceTo` é chamado para informar a `PipeReader` quantidade de dados consumidos e examinados.

Os loops de leitor e gravador terminam chamando `Complete` . `Complete` permite que o pipe subjacente libere a memória alocada.

### <a name="backpressure-and-flow-control"></a>Controle de fluxo e de pressão

Idealmente, a leitura e a análise funcionam em conjunto:

* O thread de gravação consome dados da rede e os coloca em buffers.
* O thread de análise é responsável por construir as estruturas de dados apropriadas.

Normalmente, a análise leva mais tempo do que apenas copiar blocos de dados da rede:

* O thread de leitura fica à frente do thread de análise.
* O thread de leitura precisa diminuir ou alocar mais memória para armazenar os dados para o thread de análise.

Para um desempenho ideal, há um equilíbrio entre pausas frequentes e alocação de mais memória.

Para resolver o problema anterior, o `Pipe` tem duas configurações para controlar o fluxo de dados:

* <xref:System.IO.Pipelines.PipeOptions.PauseWriterThreshold>: Determina a quantidade de dados que deve ser armazenada em buffer antes das chamadas para <xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A> Pausar.
* <xref:System.IO.Pipelines.PipeOptions.ResumeWriterThreshold>: Determina a quantidade de dados que o leitor deve observar antes de chamar a `PipeWriter.FlushAsync` retomada.

![Diagrama com ResumeWriterThreshold e PauseWriterThreshold](media/pipelines/resume-pause.png)

<xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A?displayProperty=nameWithType>:

* Retorna um incompleto `ValueTask<FlushResult>` quando a quantidade de dados em `Pipe` cruza `PauseWriterThreshold` .
* É concluído `ValueTask<FlushResult>` quando se torna menor que `ResumeWriterThreshold` .

Dois valores são usados para evitar o ciclo rápido, que pode ocorrer se um valor for usado.

### <a name="examples"></a>Exemplos

```csharp
// The Pipe will start returning incomplete tasks from FlushAsync until
// the reader examines at least 5 bytes.
var options = new PipeOptions(pauseWriterThreshold: 10, resumeWriterThreshold: 5);
var pipe = new Pipe(options);
```

### <a name="pipescheduler"></a>PipeScheduler

Normalmente, ao usar o `async` e `await` o, o código assíncrono continua em um <xref:System.Threading.Tasks.TaskScheduler> ou no atual <xref:System.Threading.SynchronizationContext> .

Ao fazer e/s, é importante ter um controle refinado sobre onde a e/s é executada. Esse controle permite aproveitar os caches de CPU com eficiência. O cache eficiente é essencial para aplicativos de alto desempenho, como servidores Web. <xref:System.IO.Pipelines.PipeScheduler> fornece controle sobre onde os retornos de chamada assíncronos são executados. Por padrão:

* O atual <xref:System.Threading.SynchronizationContext> é usado.
* Se não houver `SynchronizationContext` , ele usará o pool de threads para executar retornos de chamada.

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/Program.cs" id="snippet":::

[PipeScheduler. ThreadPool](xref:System.IO.Pipelines.PipeScheduler.ThreadPool) é a <xref:System.IO.Pipelines.PipeScheduler> implementação que enfileira os retornos de chamada para o pool de threads. `PipeScheduler.ThreadPool` é o padrão e geralmente é a melhor opção. [PipeScheduler. Inline](xref:System.IO.Pipelines.PipeScheduler.Inline) pode causar consequências indesejadas, como deadlocks.

### <a name="pipe-reset"></a>Redefinição de pipe

Com frequência, é eficiente reutilizar o `Pipe` objeto. Para redefinir o pipe, chame <xref:System.IO.Pipelines.PipeReader> <xref:System.IO.Pipelines.Pipe.Reset%2A> quando o `PipeReader` e o `PipeWriter` estiverem concluídos.

## <a name="pipereader"></a>PipeReader

<xref:System.IO.Pipelines.PipeReader> gerencia a memória em nome do chamador. **Sempre** chamar <xref:System.IO.Pipelines.PipeReader.AdvanceTo%2A?displayProperty=nameWithType> após a chamada <xref:System.IO.Pipelines.PipeReader.ReadAsync%2A?displayProperty=nameWithType> . Isso permite `PipeReader` saber quando o chamador é feito com a memória para que possa ser acompanhado. O `ReadOnlySequence<byte>` retornado de `PipeReader.ReadAsync` é válido somente até a chamada de `PipeReader.AdvanceTo` . É ilegal usar depois de `ReadOnlySequence<byte>` chamar `PipeReader.AdvanceTo` .

`PipeReader.AdvanceTo` usa dois <xref:System.SequencePosition> argumentos:

* O primeiro argumento determina a quantidade de memória consumida.
* O segundo argumento determina o quanto do buffer foi observado.

Marcar dados como consumidos significa que o pipe pode retornar a memória para o pool de buffers subjacente. Marcar dados como observados controla o que a próxima chamada `PipeReader.ReadAsync` faz. Marcar tudo como observado significa que a próxima chamada para `PipeReader.ReadAsync` não retornará até que haja mais dados gravados no pipe. Qualquer outro valor fará com que a próxima chamada seja `PipeReader.ReadAsync` retornada imediatamente com os dados observados *e* inobservados, mas não os dados que já foram consumidos.

### <a name="read-streaming-data-scenarios"></a>Ler cenários de dados de streaming

Há alguns padrões típicos que surgem ao tentar ler dados de streaming:

* Dado um fluxo de dados, analise uma única mensagem.
* Dado um fluxo de dados, analise todas as mensagens disponíveis.

Os exemplos a seguir usam o `TryParseMessage` método para analisar mensagens de um `ReadOnlySequence<byte>` . `TryParseMessage` analisa uma única mensagem e atualiza o buffer de entrada para cortar a mensagem analisada do buffer. `TryParseMessage` Não faz parte do .NET, é um método escrito pelo usuário usado nas seções a seguir.

```csharp
bool TryParseMessage(ref ReadOnlySequence<byte> buffer, out Message message);
```

### <a name="read-a-single-message"></a>Ler uma única mensagem

O código a seguir lê uma única mensagem de a `PipeReader` e retorna-a para o chamador.

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/ReadSingleMsg.cs" id="snippet":::

O código anterior:

* Analisa uma única mensagem.
* Atualiza o consumido `SequencePosition` e examinado `SequencePosition` para apontar para o início do buffer de entrada cortado.

Os dois `SequencePosition` argumentos são atualizados porque `TryParseMessage` o Remove a mensagem analisada do buffer de entrada. Geralmente, ao analisar uma única mensagem do buffer, a posição examinada deve ser uma das seguintes:

* O fim da mensagem.
* O final do buffer recebido se nenhuma mensagem for encontrada.

O caso de mensagem única tem o maior potencial para erros. Passar os valores incorretos para *examinados* pode resultar em uma exceção de memória insuficiente ou um loop infinito. Para obter mais informações, consulte a seção [problemas comuns do PipeReader](#gotchas) neste artigo.

### <a name="reading-multiple-messages"></a>Lendo várias mensagens

O código a seguir lê todas as mensagens de um `PipeReader` e chamadas `ProcessMessageAsync` em cada uma.

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/MyConnection1.cs" id="snippet":::

### <a name="cancellation"></a>Cancelamento

`PipeReader.ReadAsync`:

* Dá suporte à passagem de um <xref:System.Threading.CancellationToken> .
* Gera um <xref:System.OperationCanceledException> se o `CancellationToken` for cancelado enquanto houver uma leitura pendente.
* O oferece suporte a uma maneira de cancelar a operação de leitura atual por meio do <xref:System.IO.Pipelines.PipeReader.CancelPendingRead%2A?displayProperty=nameWithType> , que evita a geração de uma exceção. `PipeReader.CancelPendingRead`A chamada faz com que a chamada atual ou seguinte para `PipeReader.ReadAsync` retorne um <xref:System.IO.Pipelines.ReadResult> com `IsCanceled` definido como `true` . Isso pode ser útil para interromper o loop de leitura existente de forma não destrutiva e não excepcional.

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/MyConnection.cs" id="snippet":::

<a name="gotchas"></a>

### <a name="pipereader-common-problems"></a>Problemas comuns do PipeReader

* Passar os valores incorretos para `consumed` ou `examined` pode resultar na leitura de dados já lidos.
* Passar `buffer.End` como examinado pode resultar em:

  * Dados interrompidos
  * Possivelmente uma exceção de memória insuficiente (OOM) se os dados não forem consumidos. Por exemplo, `PipeReader.AdvanceTo(position, buffer.End)` ao processar uma única mensagem por vez do buffer.

* Passar os valores incorretos para `consumed` ou `examined` pode resultar em um loop infinito. Por exemplo, `PipeReader.AdvanceTo(buffer.Start)` se não alterado, fará com que `buffer.Start` a próxima chamada a `PipeReader.ReadAsync` seja retornada imediatamente antes que novos dados cheguem.
* Passar os valores incorretos para `consumed` ou `examined` pode resultar em buffer infinito (OOM eventual).
* Usar o `ReadOnlySequence<byte>` após chamar `PipeReader.AdvanceTo` pode resultar em corrupção de memória (use depois de gratuito).
* A falha na chamada `PipeReader.Complete/CompleteAsync` pode resultar em um vazamento de memória.
* Verificar <xref:System.IO.Pipelines.ReadResult.IsCompleted?displayProperty=nameWithType> e sair da lógica de leitura antes de processar o buffer resulta em perda de dados. A condição de saída do loop deve ser baseada em `ReadResult.Buffer.IsEmpty` e `ReadResult.IsCompleted` . Fazer isso incorretamente pode resultar em um loop infinito.

#### <a name="problematic-code"></a>Código problemático

❌ **Perda de dados**

O `ReadResult` pode retornar o segmento final de dados quando `IsCompleted` é definido como `true` . Não ler os dados antes de sair do loop de leitura resultará em perda de dados.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/DoNotUse.cs" id="snippet":::

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

❌**Loop infinito**

A lógica a seguir pode resultar em um loop infinito se o `Result.IsCompleted` for `true` , mas nunca há uma mensagem completa no buffer.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/DoNotUse.cs" id="snippet2":::

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

Aqui está outra parte do código com o mesmo problema. Ele está verificando um buffer não vazio antes de verificar `ReadResult.IsCompleted` . Como ele está em um `else if` , ele fará um loop contínuo se nunca houver uma mensagem completa no buffer.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/DoNotUse.cs" id="snippet3":::

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

❌**Falha inesperada**

Chamar incondicionalmente `PipeReader.AdvanceTo` com `buffer.End` na `examined` posição pode resultar em suspensões durante a análise de uma única mensagem. A próxima chamada para `PipeReader.AdvanceTo` não retornará até:

* Há mais dados gravados no pipe.
* E os novos dados não foram examinados anteriormente.

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/DoNotUse.cs" id="snippet4":::

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

❌**Memória insuficiente (OOM)**

Com as condições a seguir, o código a seguir mantém o buffer até <xref:System.OutOfMemoryException> ocorrer:

* Não há tamanho máximo de mensagem.
* Os dados retornados de `PipeReader` não fazem uma mensagem completa. Por exemplo, ele não faz uma mensagem completa porque o outro lado está escrevendo uma mensagem grande (por exemplo, uma mensagem de 4 GB).

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/DoNotUse.cs" id="snippet5":::

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

❌**Corrupção de memória**

Ao escrever auxiliares que lêem o buffer, qualquer carga retornada deve ser copiada antes de chamar `Advance` . O exemplo a seguir retornará a memória que o `Pipe` foi descartada e pode reutilizá-lo para a próxima operação (leitura/gravação).

[!INCLUDE [pipelines-do-not-use-1](../../../includes/pipelines-do-not-use-1.md)]

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/DoNotUse.cs" id="snippetMessage":::

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/DoNotUse.cs" id="snippet6":::

[!INCLUDE [pipelines-do-not-use-2](../../../includes/pipelines-do-not-use-2.md)]

## <a name="pipewriter"></a>PipeWriter

O <xref:System.IO.Pipelines.PipeWriter> gerencia buffers para gravação em nome do chamador. `PipeWriter` implementa [`IBufferWriter<byte>`](xref:System.Buffers.IBufferWriter%601) . `IBufferWriter<byte>` torna possível obter acesso a buffers para executar gravações sem cópias de buffer adicionais.

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/MyPipeWriter.cs" id="snippet":::

O código anterior:

* Solicita um buffer de pelo menos 5 bytes do `PipeWriter` uso do <xref:System.IO.Pipelines.PipeWriter.GetMemory%2A> .
* Grava bytes para a cadeia de caracteres ASCII no `"Hello"` retornado `Memory<byte>` .
* Chama <xref:System.IO.Pipelines.PipeWriter.Advance%2A> para indicar quantos bytes foram gravados no buffer.
* Libera o `PipeWriter` , que envia os bytes para o dispositivo subjacente.

O método anterior de gravação usa os buffers fornecidos pelo `PipeWriter` . Como alternativa, <xref:System.IO.Pipelines.PipeWriter.WriteAsync%2A?displayProperty=nameWithType> :

* Copia o buffer existente para o `PipeWriter` .
* Chamadas `GetSpan` , `Advance` conforme apropriado e chamadas <xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A> .

:::code language="csharp" source="~/samples/snippets/csharp/pipelines/MyPipeWriter.cs" id="snippet2":::

### <a name="cancellation"></a>Cancelamento

<xref:System.IO.Pipelines.PipeWriter.FlushAsync%2A> dá suporte à passagem de um <xref:System.Threading.CancellationToken> . Passar um `CancellationToken` resultado em um `OperationCanceledException` se o token for cancelado enquanto houver uma liberação pendente. `PipeWriter.FlushAsync` dá suporte a uma maneira de cancelar a operação de liberação atual por meio <xref:System.IO.Pipelines.PipeWriter.CancelPendingFlush%2A?displayProperty=nameWithType> de sem gerar uma exceção. `PipeWriter.CancelPendingFlush`A chamada faz com que a chamada atual ou próxima chame `PipeWriter.FlushAsync` ou `PipeWriter.WriteAsync` retorne um <xref:System.IO.Pipelines.FlushResult> com `IsCanceled` definido como `true` . Isso pode ser útil para interromper a liberação de rendimento de forma não destrutiva e não excepcional.

<a name="pwcp"></a>

### <a name="pipewriter-common-problems"></a>Problemas comuns do PipeWriter

* <xref:System.IO.Pipelines.PipeWriter.GetSpan%2A> e <xref:System.IO.Pipelines.PipeWriter.GetMemory%2A> retornam um buffer com pelo menos a quantidade solicitada de memória. **Não** presuma os tamanhos de buffer exatos.
* Não há nenhuma garantia de que as chamadas sucessivas retornarão o mesmo buffer ou o buffer de mesmo tamanho.
* Um novo buffer deve ser solicitado após <xref:System.IO.Pipelines.PipeWriter.Advance%2A> a chamada para continuar gravando mais dados. Não é possível gravar no buffer adquirido anteriormente.
* Chamar `GetMemory` ou `GetSpan` embora haja uma chamada incompleta para `FlushAsync` não é seguro.
* Chamar `Complete` ou `CompleteAsync` embora haja dados não liberados pode resultar em corrupção de memória.

## <a name="iduplexpipe"></a>IDuplexPipe

O <xref:System.IO.Pipelines.IDuplexPipe> é um contrato para tipos que dão suporte à leitura e gravação. Por exemplo, uma conexão de rede seria representada por um `IDuplexPipe` .

 Ao contrário de `Pipe` , que contém um `PipeReader` e um `PipeWriter` , `IDuplexPipe` representa um único lado de uma conexão Full duplex. Isso significa que o que é gravado no `PipeWriter` não será lido no `PipeReader` .

## <a name="streams"></a>Fluxos

Ao ler ou gravar dados de fluxo, você normalmente lê dados usando um desserializador e grava dados usando um serializador. A maioria dessas APIs de leitura e gravação de fluxo tem um `Stream` parâmetro. Para facilitar a integração com essas APIs existentes `PipeReader` e `PipeWriter` expor um <xref:System.IO.Pipelines.PipeReader.AsStream%2A> método. <xref:System.IO.Pipelines.PipeWriter.AsStream%2A> Retorna uma `Stream` implementação em relação ao `PipeReader` ou ao `PipeWriter` .

### <a name="stream-example"></a>Exemplo de fluxo

`PipeReader``PipeWriter`as instâncias e podem ser criadas usando os métodos estáticos de `Create` acordo com um <xref:System.IO.Stream> objeto e as opções de criação correspondentes opcionais.

O <xref:System.IO.Pipelines.StreamPipeReaderOptions> Permitir controle sobre a criação da `PipeReader` instância com os seguintes parâmetros:

- <xref:System.IO.Pipelines.StreamPipeReaderOptions.BufferSize?displayProperty=nameWithType> é o tamanho mínimo do buffer em bytes usado ao aluguel a memória do pool e usa como padrão `4096` .
- <xref:System.IO.Pipelines.StreamPipeReaderOptions.LeaveOpen?displayProperty=nameWithType> sinalizador determina se o fluxo subjacente é deixado aberto após a `PipeReader` conclusão e o padrão é `false` .
- <xref:System.IO.Pipelines.StreamPipeReaderOptions.MinimumReadSize?displayProperty=nameWithType> representa o limite de bytes restantes no buffer antes de um novo buffer ser alocado e o padrão é `1024` .
- <xref:System.IO.Pipelines.StreamPipeReaderOptions.Pool?displayProperty=nameWithType> é `MemoryPool<byte>` usado ao alocar memória e usa como padrão `null` .

O <xref:System.IO.Pipelines.StreamPipeWriterOptions> Permitir controle sobre a criação da `PipeWriter` instância com os seguintes parâmetros:

- <xref:System.IO.Pipelines.StreamPipeWriterOptions.LeaveOpen?displayProperty=nameWithType> sinalizador determina se o fluxo subjacente é deixado aberto após a `PipeWriter` conclusão e o padrão é `false` .
- <xref:System.IO.Pipelines.StreamPipeWriterOptions.MinimumBufferSize?displayProperty=nameWithType> representa o tamanho mínimo do buffer a ser usado ao aluguel a memória do <xref:System.IO.Pipelines.StreamPipeWriterOptions.Pool> e o padrão é `4096` .
- <xref:System.IO.Pipelines.StreamPipeWriterOptions.Pool?displayProperty=nameWithType> é `MemoryPool<byte>` usado ao alocar memória e usa como padrão `null` .

> [!IMPORTANT]
> Ao criar `PipeReader` e `PipeWriter` instâncias usando os `Create` métodos, você precisa considerar o `Stream` tempo de vida do objeto. Se você precisar de acesso ao fluxo depois que o leitor ou o gravador for feito com ele, você precisará definir o `LeaveOpen` sinalizador como `true` nas opções de criação. Caso contrário, o fluxo será fechado.

O código a seguir demonstra a criação `PipeReader` de `PipeWriter` instâncias e usando os `Create` métodos de um fluxo.

:::code language="csharp" source="snippets/pipelines/Program.cs":::

O aplicativo usa um <xref:System.IO.StreamReader> para ler o arquivo de *lorem-ipsum.txt* como um fluxo. O <xref:System.IO.FileStream> é passado para <xref:System.IO.Pipelines.PipeReader.Create%2A?displayProperty=nameWithType> , que instancia um `PipeReader` objeto. Em seguida, o aplicativo de console passa seu fluxo de saída padrão para o <xref:System.IO.Pipelines.PipeWriter.Create%2A?displayProperty=nameWithType> usando <xref:System.Console.OpenStandardOutput?displayProperty=nameWithType> . O exemplo dá suporte ao [cancelamento](#cancellation).
