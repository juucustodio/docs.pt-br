---
title: Rastreamento distribuído-.NET
description: Uma introdução ao rastreamento distribuído do .NET.
ms.date: 02/02/2021
ms.openlocfilehash: d29c803dfec00474562abdc61ce65ea3f3faa133
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100431432"
---
# <a name="net-distributed-tracing"></a>Rastreamento distribuído do .NET

O rastreamento distribuído é a maneira de publicar e observar dados de rastreamento em um sistema distribuído.
O .NET Framework e o .NET Core têm suporte para rastreamento por meio de <xref:System.Diagnostics> APIs.

- <xref:System.Diagnostics.Activity?displayProperty=nameWithType> classe que permite armazenar e acessar o contexto de diagnóstico e consumi-lo com o sistema de registro em log.
- <xref:System.Diagnostics.DiagnosticSource?displayProperty=nameWithType> Isso permite que o código seja instrumentado para o log do tempo de produção de cargas de dados avançadas para consumo no processo que foi instrumentado.

Aqui está um exemplo que mostra como publicar dados de rastreamento das solicitações de entrada HTTP:

```csharp
   public void OnIncomingRequest(DiagnosticListener httpListener, HttpContext context)
   {
       if (httpListener.IsEnabled("Http_In"))
       {
           var activity = new Activity("Http_In");

           //add tags, baggage, etc.
           activity.SetParentId(context.Request.headers["Request-id"])
           foreach (var pair in context.Request.Headers["Correlation-Context"])
           {
               var baggageItem = NameValueHeaderValue.Parse(pair);
               activity.AddBaggage(baggageItem.Key, baggageItem.Value);
           }
           httpListener.StartActivity(activity, new { context });
           try
           {
               //process request ...
           }
           finally
           {
               //stop activity
               httpListener.StopActivity(activity, new {context} );
           }
       }
   }
```

Aqui está um exemplo de como escutar os eventos de atividade:

```csharp
    DiagnosticListener.AllListeners.Subscribe(delegate (DiagnosticListener listener)
    {
        if (listener.Name == "MyActivitySource")
        {
            listener.Subscribe(delegate (KeyValuePair<string, object> value)
            {
                if (value.Key.EndsWith("Start", StringComparison.Ordinal))
                    LogActivityStart();
                else if (value.Key.EndsWith("Stop", StringComparison.Ordinal))
                    LogActivityStop();
            });
        }
    }
```

O .NET 5,0 ampliou a capacidade do rastreamento distribuído para permitir os cenários de rastreamento de [OpenTelemetry](https://opentelemetry.io/) , adicionou funcionalidades de amostragem, simplificou o padrão de codificação de rastreamento e tornou mais fácil e flexível a escuta dos eventos de atividade.

> [!NOTE]
> Para acessar todos os recursos do .NET 5,0 adicionados, verifique se o seu projeto faz referência à versão 5,0 ou posterior do pacote NuGet [System. Diagnostics. Diagnostics](https://www.nuget.org/packages/System.Diagnostics.DiagnosticSource/) . Esse pacote pode ser usado em bibliotecas e aplicativos destinados a qualquer versão com suporte do .NET Framework, .NET Core e .NET Standard. Se estiver direcionando o .NET 5,0 ou posterior, não será necessário fazer referência ao pacote manualmente, pois ele está incluído na biblioteca compartilhada instalada com o tempo de execução do .NET.

## <a name="getting-started-with-tracing"></a>Introdução com rastreamento

Aplicativos e bibliotecas podem facilmente publicar dados de rastreamento simplesmente usando as <xref:System.Diagnostics.ActivitySource?displayProperty=nameWithType> classes e <xref:System.Diagnostics.Activity?displayProperty=nameWithType> .

### <a name="activitysource"></a>Atividade

A primeira etapa para publicar dados de rastreamento é criar uma instância da classe Activityry. A ActivityName é a classe que fornece APIs para criar e iniciar objetos de atividade e para registrar objetos ActivityListener para escutar os eventos de atividade.

```csharp
    private static ActivitySource source = new ActivitySource("MyCompany.MyComponent.SourceName", "v1");
```

#### <a name="best-practices"></a>Práticas Recomendadas

- Crie a ActivityName uma vez e armazene-a em uma variável estática e use essa instância desde que seja necessário.

- O nome de origem passado para o construtor deve ser exclusivo para evitar conflitos com outras fontes. É recomendável usar um nome hierárquico que contenha o nome da empresa, o nome do componente e o nome da origem. Por exemplo, `Microsoft.System.HttpClient.HttpInOutRequests`.

- O parâmetro version é opcional. É recomendável fornecer a versão caso você planeje lançar várias versões da biblioteca ou do aplicativo e desejar distinguir entre as fontes de versões diferentes.

### <a name="activity-creation"></a>Criação de atividade

Agora, o objeto Activityprovider criado pode ser usado para criar e iniciar objetos de atividade que são usados para registrar quaisquer dados de rastreamento em qualquer lugar desejado no código.

```csharp
        using (Activity activity = source.StartActivity("OperationName"))
        {
            // Do something

            activity?.AddTag("key", "value"); // log the tracing
        }
```

Este código de exemplo tenta criar o objeto de atividade e, em seguida, registra em log alguma marca `key` de rastreamento e `value` .

#### <a name="notes"></a>Anotações

- `ActivitySource.StartActivity` tenta criar e iniciar a atividade ao mesmo tempo. O padrão de código listado está usando o `using` bloco que descarta automaticamente o objeto de atividade criado após a execução do bloco. Descartar o objeto de atividade interromperá essa atividade iniciada e o código não precisará parar explicitamente a atividade. Isso simplifica o padrão de codificação.

- `ActivitySource.StartActivity` descobre internamente se há algum ouvinte para esses eventos. Se não houver ouvintes registrados ou se houver ouvintes que não estejam interessados nesse evento, `ActivitySource.StartActivity` simplesmente retornará `null` e evitará a criação do objeto de atividade. É por isso que o código usou o operador Nullable `?`  na instrução `activity?.AddTag` . Em geral, dentro do `using` bloco, sempre use o operador Nullable `?` após o nome do objeto de atividade.

## <a name="listening-to-the-activity-events"></a>Ouvindo os eventos de atividade

O .NET fornece a classe <xref:System.Diagnostics.ActivityListener?displayProperty=nameWithType> que pode ser usada para escutar os eventos de atividade disparados a partir de um ou mais ActivitySources.
O ouvinte pode ser usado para coletar dados de rastreamento, exemplo ou forçar a criação do objeto de atividade.

A `ActivityListener` classe fornece um retorno de chamada diferente para lidar com eventos diferentes.

```csharp

ActivityListener listener = new ActivityListener()

ShouldListenTo = (activitySource) => object.ReferenceEquals(source, activitySource),
ActivityStarted = activity => /* Handle the Activity start event here */ DoSomething(),
ActivityStopped = activity => /* Handle the Activity stop event here */ DoSomething(),
SampleUsingParentId = (ref ActivityCreationOptions<string> activityOptions) => ActivitySamplingResult.AllData,
Sample = (ref ActivityCreationOptions<ActivityContext> activityOptions) => ActivitySamplingResult.AllData

// Enable the listener
ActivitySource.AddActivityListener(listener);
```

- `ShouldListenTo` habilita a escuta de `ActivitySource` objetos específicos. No exemplo, ele permite ouvir o objeto que criamos `ActivitySource` anteriormente. Há mais flexibilidade para escutar quaisquer outros `ActivitySource` objetos, verificando o `Name` e `Version` da entrada `ActivitySource` .

- `ActivityStarted` e `ActivityStopped` habilitar a obtenção dos `Activity` eventos Start e Stop para todos os `Activity` objetos criados pelos `ActivitySource` objetos que foram habilitados pelo `ShouldListenTo` retorno de chamada.

- `Sample` e `SampleUsingParentId` são os principais retornos de chamada que se destinam à amostragem. Esses dois retornos de chamada retornam o `ActivitySamplingResult` valor de enumeração que pode indicar a amostra ou saída da `Activity` solicitação de criação atual. Se o retorno de chamada retornar `ActivitySamplingResult.None` e nenhum outro ouvinte habilitado retornar um valor diferente, a atividade não será criada e `ActivitySource.StartActivity` retornará `null` . Caso contrário, o `Activity` objeto será criado.

## <a name="net-50-new-features"></a>Novos recursos do .NET 5,0

Por algum tempo, a `Activity` classe tem suporte a cenários de rastreamento. Ele permitia a adição de marcas que são pares chave-valor dos dados de rastreamento. Ele tem sido compatível com bagagem, que são pares chave-valor destinados a serem propagados pela conexão.

O .NET 5,0 dá suporte a mais recursos principalmente para habilitar cenários OpenTelemetry.

### <a name="activitycontext"></a>ActivityContext

<xref:System.Diagnostics.ActivityContext?displayProperty=nameWithType> é o struct que possui o contexto das operações de rastreamento (por exemplo, a ID de rastreamento, a ID de extensão, os sinalizadores de rastreamento e o estado de rastreamento). Agora é possível criar um novo `Activity` fornecendo o contexto de rastreamento pai. Além disso, é fácil extrair o contexto de rastreamento de qualquer `Activity` objeto chamando a `Activity.Context` propriedade.

### <a name="activitylink"></a>ActivityLink

<xref:System.Diagnostics.ActivityLink?displayProperty=nameWithType> é o struct que contém a instância de contexto de rastreamento que pode ser vinculada a objetos eventualmente relacionados `Activity` . Os links podem ser adicionados ao `Activity` objeto passando a lista de links para o `ActivitySource.StartActivity` método ao criar o `Activity` . Os `Activity` links anexados ao objeto podem ser recuperados usando a propriedade `Activity.Links` .

### <a name="activityevent"></a>ActivityEvent

<xref:System.Diagnostics.ActivityEvent?displayProperty=nameWithType> representa um evento que contém um nome e um carimbo de data/hora, bem como uma lista opcional de marcas. Os eventos podem ser adicionados ao `Activity` objeto chamando o `Activity.AddEvent` método. A lista completa dos `Activity` eventos de objeto pode ser recuperada usando a propriedade `Activity.Events` .

### <a name="activitykind"></a>ActivityKind

<xref:System.Diagnostics.ActivityKind?displayProperty=nameWithType> Descreve a relação entre a atividade, seus pais e seus filhos em um rastreamento. O tipo pode ser definido para o `Activity` objeto passando o valor do tipo para o `ActivitySource.StartActivity` método ao criar o `Activity` . O `Activity` tipo de objeto pode ser recuperado usando a propriedade `Activity.Kind` .

### <a name="isalldatarequested"></a>IsAllDataRequested

<xref:System.Diagnostics.Activity.IsAllDataRequested?displayProperty=nameWithType> indica se essa atividade deve ser preenchida com todas as informações de propagação, bem como todas as outras propriedades, como links, marcas e eventos. O valor de `IsAllDataRequested` é determinado do resultado retornado de todos os ouvintes `Sample` e `SampleUsingParentId` retornos de chamada. O valor pode ser recuperado usando a `Activity.IsAllDataRequested` propriedade.

### <a name="activitysource"></a>Atividade. origem

<xref:System.Diagnostics.Activity.Source?displayProperty=nameWithType> Obtém a origem da atividade associada a esta atividade.

### <a name="activitydisplayname"></a>Activity. DisplayName

<xref:System.Diagnostics.Activity.DisplayName?displayProperty=nameWithType> permite obter ou definir um nome de exibição para a atividade.

### <a name="activitytagobjects"></a>Activity. TagObjects

`Activity` a classe tem a propriedade `Activity.Tags` que retorna uma lista de pares chave-valor das marcas do tipo cadeia de caracteres para a chave e o valor. Essas marcas podem ser adicionadas ao `Activity` usando o método `AddTag(string, string)` . `Activity` ampliou o suporte de marcas fornecendo o método sobrecarregado, `AddTag(string, object)` permitindo valores de qualquer tipo.  A lista completa dessas marcas pode ser recuperada usando <xref:System.Diagnostics.Activity.TagObjects?displayProperty=nameWithType> .

## <a name="sampling"></a>amostragem

A amostragem é um mecanismo para controlar o ruído e a sobrecarga, reduzindo o número de amostras de rastreamentos coletados e enviados ao back-end. A amostragem é um cenário de OpenTelemetry importante. No .NET 5,0, é fácil permitir a amostragem. Uma prática recomendada é criar os novos `Activity` objetos usando `ActivitySource.StartActivity` e tentar fornecer todos os dados disponíveis possíveis (por exemplo, marcas, tipos, links,... etc.) ao chamar esse método. Fornecer os dados permitirá que os exemplos implementados usando o `ActivityListener` para tenham uma decisão de amostragem adequada. Se o desempenho for crítico para evitar a criação dos dados antes da criação do `Activity` objeto, a propriedade será `ActivitySource.HasListeners` útil para verificar se há ouvintes antes de criar os dados necessários.

## <a name="opentelemetry"></a>OpenTelemetry

O SDK do OpenTelemetry vem com muitos recursos que dão suporte a cenários de rastreamento distribuído de ponta a ponta. Ele fornece vários exemplos e exportadores dos quais você pode escolher. Ele também permite criar uma amostra e exportadores personalizados.

O OpenTelemetry dá suporte à exportação dos dados de rastreamento coletados para back-ends diferentes (por exemplo, Jaeger, Zipkin, New Relic,... etc.). Consulte [OpenTelemetry-dotnet](https://github.com/open-telemetry/opentelemetry-dotnet/) para obter mais detalhes e Pesquisar NuGet.org para pacotes começando com `OpenTelemetry.Exporter.` para obter a lista de pacotes exportadores.

Aqui está o código de exemplo portado de [introdução OpenTelemetry-dotnet](https://github.com/open-telemetry/opentelemetry-dotnet/tree/main/docs/trace/getting-started) que mostra como é fácil criar amostras e exportar dados de rastreamento para o console.

```csharp
// <copyright file="Program.cs" company="OpenTelemetry Authors">
// Copyright The OpenTelemetry Authors
//
// Licensed under the Apache License, Version 2.0 (the "License");
// you may not use this file except in compliance with the License.
// You may obtain a copy of the License at
//
//     http://www.apache.org/licenses/LICENSE-2.0
//
// Unless required by applicable law or agreed to in writing, software
// distributed under the License is distributed on an "AS IS" BASIS,
// WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
// See the License for the specific language governing permissions and
// limitations under the License.
// </copyright>

using System.Diagnostics;
using OpenTelemetry;
using OpenTelemetry.Trace;

public class Program
{
    private static readonly ActivitySource MyActivitySource = new ActivitySource(
        "MyCompany.MyProduct.MyLibrary");

    public static void Main()
    {
        using var tracerProvider = Sdk.CreateTracerProviderBuilder()
            .SetSampler(new AlwaysOnSampler())
            .AddSource("MyCompany.MyProduct.MyLibrary")
            .AddConsoleExporter()
            .Build();

        using (var activity = MyActivitySource.StartActivity("SayHello"))
        {
            activity?.SetTag("foo", 1);
            activity?.SetTag("bar", "Hello, World!");
            activity?.SetTag("baz", new int[] { 1, 2, 3 });
        }
    }
}
```

O exemplo precisa fazer referência ao pacote [OpenTelemetry. exportador. console](https://www.nuget.org/packages/OpenTelemetry.Exporter.Console/1.0.0-rc2).
