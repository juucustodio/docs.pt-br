---
title: Use o IHttpClientFactory para implementar solicitações HTTP resilientes
description: Saiba como usar o IHttpClientFactory, disponível desde o .NET Core 2,1, para criar `HttpClient` instâncias, facilitando seu uso em seus aplicativos.
ms.date: 01/13/2021
ms.openlocfilehash: 056a8982fe4331e7e680b33cf1f43785b48da7d6
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188992"
---
# <a name="use-ihttpclientfactory-to-implement-resilient-http-requests"></a>Use o IHttpClientFactory para implementar solicitações HTTP resilientes

<xref:System.Net.Http.IHttpClientFactory> é um contrato implementado pelo `DefaultHttpClientFactory` , uma fábrica conceituada, disponível desde o .NET Core 2,1, para <xref:System.Net.Http.HttpClient> a criação de instâncias a serem usadas em seus aplicativos.

## <a name="issues-with-the-original-httpclient-class-available-in-net"></a>Problemas com a classe HttpClient original disponível no .NET

A classe original e conhecida <xref:System.Net.Http.HttpClient> pode ser facilmente usada, mas, em alguns casos, ela não está sendo usada corretamente por muitos desenvolvedores.

Embora essa classe implemente `IDisposable` , a declaração e a criação de uma instância dele dentro de uma `using` instrução não é preferida porque, quando o `HttpClient` objeto é Descartado, o soquete subjacente não é lançado imediatamente, o que pode levar a um problema de _esgotamento de soquete_ . Para obter mais informações sobre esse problema, consulte a postagem de blog [que você está usando HttpClient errado e está desestabilizando o software](https://aspnetmonsters.com/2016/08/2016-08-27-httpclientwrong/).

Portanto, `HttpClient` deve ser instanciado uma única vez e reutilizado durante a vida útil de um aplicativo. A criação de uma instância de uma classe `HttpClient` para cada solicitação esgotará o número de soquetes disponíveis em condições de carga pesada. Esse problema resultará em erros de `SocketException`. Abordagens possíveis para resolver o problema baseiam-se na criação do objeto `HttpClient` como singleton ou estático, conforme é explicado neste [artigo da Microsoft sobre o uso do HttpClient](../../../csharp/tutorials/console-webapiclient.md). Isso pode ser uma boa solução para aplicativos de console de curta duração ou semelhante, que são executados algumas vezes por dia.

Outro problema que os desenvolvedores executam é ao usar uma instância compartilhada do `HttpClient` em processos de execução longa. Em uma situação em que o HttpClient é instanciado como um singleton ou um objeto estático, ele não lida com as alterações de DNS, conforme descrito neste [problema](https://github.com/dotnet/runtime/issues/18348) do repositório do GitHub de dotnet/tempo de execução.

No entanto, o problema não é realmente com `HttpClient` o por si, mas com o [construtor padrão para HttpClient](/dotnet/api/system.net.http.httpclient.-ctor?view=netcore-3.1#System_Net_Http_HttpClient__ctor), porque ele cria uma nova instância concreta do <xref:System.Net.Http.HttpMessageHandler> , que é aquela que tem os problemas de *esgotamento de soquetes* e alterações de DNS mencionados acima.

Para resolver os problemas mencionados acima e tornar as `HttpClient` instâncias gerenciáveis, o .NET Core 2,1 introduziu a <xref:System.Net.Http.IHttpClientFactory> interface que pode ser usada para configurar e criar `HttpClient` instâncias em um aplicativo por meio de injeção de dependência (di). Ele também fornece extensões para que o middleware baseado em Polly Aproveite a delegação de manipuladores no HttpClient.

O [Polly](http://www.thepollyproject.org/) é uma biblioteca de tratamento de falhas transitórias que ajuda os desenvolvedores a adicionar resiliência aos seus aplicativos, usando algumas políticas predefinidas de forma fluente e thread-safe.

## <a name="benefits-of-using-ihttpclientfactory"></a>Benefícios do uso do IHttpClientFactory

A implementação atual do <xref:System.Net.Http.IHttpClientFactory> , que também implementa <xref:System.Net.Http.IHttpMessageHandlerFactory> , oferece os seguintes benefícios:

- Fornece um local central para nomear e configurar `HttpClient` objetos lógicos. Por exemplo, você pode configurar um cliente (agente de serviço) pré-configurado para acessar um microsserviço específico.
- Codificar o conceito de middleware de saída por meio da delegação de manipuladores no `HttpClient` e implementação do middleware baseado em Polly para tirar proveito das políticas de Polly para resiliência.
- O `HttpClient` já tem o conceito de delegar manipuladores que podem ser vinculados uns aos outros para solicitações HTTP de saída. Você pode registrar clientes HTTP na fábrica e usar um manipulador Polly para usar políticas de Polly para repetir, CircuitBreakers e assim por diante.
- Gerencie o tempo de vida de <xref:System.Net.Http.HttpMessageHandler> para evitar problemas/problemas mencionados que podem ocorrer ao gerenciar os `HttpClient` tempos de vida por conta própria.

> [!TIP]
> As `HttpClient` instâncias injetadas por di podem ser descartadas de forma segura, porque o associado `HttpMessageHandler` é gerenciado pela fábrica. Na verdade, as instâncias injetadas `HttpClient` têm o *escopo* de uma perspectiva de di.

> [!NOTE]
> A implementação de `IHttpClientFactory` ( `DefaultHttpClientFactory` ) está rigidamente ligada à implementação de di no `Microsoft.Extensions.DependencyInjection` pacote NuGet. Para obter mais informações sobre como usar outros contêineres de DI, consulte esta [discussão do GitHub](https://github.com/dotnet/extensions/issues/1345).

## <a name="multiple-ways-to-use-ihttpclientfactory"></a>Várias maneiras de usar o IHttpClientFactory

Há várias maneiras de usar o `IHttpClientFactory` no aplicativo:

- Uso básico
- Usar clientes nomeados
- Usar clientes tipados
- Usar clientes gerados

Para fins de brevidade, essas diretrizes mostram a maneira mais estruturada de usar `IHttpClientFactory` , que é usar clientes digitados (padrão de agente de serviço). No entanto, todas as opções estão documentadas e estão listadas neste [artigo abordando o `IHttpClientFactory` uso](/aspnet/core/fundamentals/http-requests#consumption-patterns).

## <a name="how-to-use-typed-clients-with-ihttpclientfactory"></a>Como usar clientes digitados com IHttpClientFactory

Portanto, o que é um "cliente tipado"? É apenas um `HttpClient` que é pré-configurado para um uso específico. Essa configuração pode incluir valores específicos, como o servidor base, cabeçalhos HTTP ou tempos limite.

O diagrama a seguir mostra como os clientes tipados são usados com o `IHttpClientFactory`:

![Diagrama mostrando como os clientes digitados são usados com IHttpClientFactory.](./media/use-httpclientfactory-to-implement-resilient-http-requests/client-application-code.png)

**Figura 8-4**. Usando `IHttpClientFactory` com classes de cliente tipadas.

Na imagem acima, a `ClientService` (usada por um controlador ou código de cliente) usa um `HttpClient` criado pelo registrado `IHttpClientFactory` . Essa fábrica atribui um `HttpMessageHandler` de um pool ao `HttpClient` . O `HttpClient` pode ser configurado com as políticas do Polly ao registrar o `IHttpClientFactory` no contêiner di com o método de extensão <xref:Microsoft.Extensions.DependencyInjection.HttpClientFactoryServiceCollectionExtensions.AddHttpClient%2A> .

Para configurar a estrutura acima, adicione <xref:System.Net.Http.IHttpClientFactory> em seu aplicativo instalando o `Microsoft.Extensions.Http` pacote NuGet que inclui o <xref:Microsoft.Extensions.DependencyInjection.HttpClientFactoryServiceCollectionExtensions.AddHttpClient%2A> método de extensão para <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection> . Esse método de extensão registra a `DefaultHttpClientFactory` classe interna a ser usada como um singleton para a interface `IHttpClientFactory` . Ele define uma configuração transitória para o <xref:Microsoft.Extensions.Http.HttpMessageHandlerBuilder>. Esse manipulador de mensagens (objeto <xref:System.Net.Http.HttpMessageHandler>), obtido de um pool, é usado pelo `HttpClient` retornado do alocador.

No próximo código, veja como `AddHttpClient()` pode ser usado para registrar clientes tipados (agentes de serviço) que precisam usar `HttpClient`.

```csharp
// Startup.cs
//Add http client services at ConfigureServices(IServiceCollection services)
services.AddHttpClient<ICatalogService, CatalogService>();
services.AddHttpClient<IBasketService, BasketService>();
services.AddHttpClient<IOrderingService, OrderingService>();
```

O registro dos serviços do cliente, conforme mostrado no código anterior, faz com que o `DefaultClientFactory` crie um padrão `HttpClient` para cada serviço.

Você também pode adicionar a configuração específica da instância no registro para, por exemplo, configurar o endereço base e adicionar algumas políticas de resiliência, conforme mostrado no código a seguir:

```csharp
services.AddHttpClient<ICatalogService, CatalogService>(client =>
{
    client.BaseAddress = new Uri(Configuration["BaseUrl"]);
})
    .AddPolicyHandler(GetRetryPolicy())
    .AddPolicyHandler(GetCircuitBreakerPolicy());
```

Apenas para o exemplo, você pode ver uma das políticas acima no próximo código:

```csharp
static IAsyncPolicy<HttpResponseMessage> GetRetryPolicy()
{
    return HttpPolicyExtensions
        .HandleTransientHttpError()
        .OrResult(msg => msg.StatusCode == System.Net.HttpStatusCode.NotFound)
        .WaitAndRetryAsync(6, retryAttempt => TimeSpan.FromSeconds(Math.Pow(2, retryAttempt)));
}
```

Você pode encontrar mais detalhes sobre como usar o Polly no [próximo artigo](implement-http-call-retries-exponential-backoff-polly.md).

### <a name="httpclient-lifetimes"></a>Tempos de vida de HttpClient

Sempre que você receber um objeto `HttpClient` do `IHttpClientFactory`, uma nova instância será retornada. Mas cada `HttpClient` usa um `HttpMessageHandler` que foi colocado em pool e reutilizado pelo `IHttpClientFactory` para reduzir o consumo de recursos, desde que o tempo de vida do `HttpMessageHandler` não tenha expirado.

O pooling de manipuladores é interessante porque cada manipulador normalmente gerencia suas próprias conexões de HTTP subjacentes. Criar mais manipuladores do que o necessário pode resultar em atrasos de conexão. Alguns manipuladores também mantêm as conexões abertas indefinidamente, o que pode impedir que o manipulador reaja a alterações de DNS.

Os objetos `HttpMessageHandler` no pool têm um tempo de vida que é o período de tempo em que uma instância `HttpMessageHandler` no pool pode ser reutilizada. O valor padrão é dois minutos, mas pode ser substituído por cliente tipado. Para substituí-lo, chame `SetHandlerLifetime()` no <xref:Microsoft.Extensions.DependencyInjection.IHttpClientBuilder> que é retornado ao criar o cliente, como mostra o código a seguir:

```csharp
//Set 5 min as the lifetime for the HttpMessageHandler objects in the pool used for the Catalog Typed Client
services.AddHttpClient<ICatalogService, CatalogService>()
    .SetHandlerLifetime(TimeSpan.FromMinutes(5));
```

Cada cliente tipado pode ter seu próprio valor de tempo de vida do manipulador configurado. Defina o tempo de vida como `InfiniteTimeSpan` para desabilitar a expiração do manipulador.

### <a name="implement-your-typed-client-classes-that-use-the-injected-and-configured-httpclient"></a>Implementar suas classes de cliente tipado que usam o HttpClient injetado e configurado

Como uma etapa anterior, você precisa ter suas classes de cliente digitadas definidas, como as classes no código de exemplo, como ' BasketService ', ' CatalogService ', ' OrderingService ', etc. – um cliente tipado é uma classe que aceita um `HttpClient` objeto (injetado através de seu construtor) e o usa para chamar algum serviço http remoto. Por exemplo:

```csharp
public class CatalogService : ICatalogService
{
    private readonly HttpClient _httpClient;
    private readonly string _remoteServiceBaseUrl;

    public CatalogService(HttpClient httpClient)
    {
        _httpClient = httpClient;
    }

    public async Task<Catalog> GetCatalogItems(int page, int take,
                                               int? brand, int? type)
    {
        var uri = API.Catalog.GetAllCatalogItems(_remoteServiceBaseUrl,
                                                 page, take, brand, type);

        var responseString = await _httpClient.GetStringAsync(uri);

        var catalog = JsonConvert.DeserializeObject<Catalog>(responseString);
        return catalog;
    }
}
```

O cliente digitado ( `CatalogService` no exemplo) é ativado por di (injeção de dependência), isso significa que ele pode aceitar qualquer serviço registrado em seu construtor, além de `HttpClient` .

Um cliente tipado é efetivamente um objeto transitório, isso significa que uma nova instância é criada cada vez que uma é necessária. Ele recebe uma nova `HttpClient` instância toda vez que ela é construída. No entanto, os `HttpMessageHandler` objetos no pool são os objetos que são reutilizados por várias `HttpClient` instâncias.

### <a name="use-your-typed-client-classes"></a>Usar suas classes de cliente tipado

Por fim, depois de implementar as classes tipadas, você poderá tê-las registradas e configuradas com `AddHttpClient()` . Depois disso, você pode usá-los sempre que tiverem serviços injetados por DI. Por exemplo, em um código de página do Razor ou no controlador de um aplicativo Web MVC, como no código a seguir de eShopOnContainers:

```csharp
namespace Microsoft.eShopOnContainers.WebMVC.Controllers
{
    public class CatalogController : Controller
    {
        private ICatalogService _catalogSvc;

        public CatalogController(ICatalogService catalogSvc) =>
                                                           _catalogSvc = catalogSvc;

        public async Task<IActionResult> Index(int? BrandFilterApplied,
                                               int? TypesFilterApplied,
                                               int? page,
                                               [FromQuery]string errorMsg)
        {
            var itemsPage = 10;
            var catalog = await _catalogSvc.GetCatalogItems(page ?? 0,
                                                            itemsPage,
                                                            BrandFilterApplied,
                                                            TypesFilterApplied);
            //… Additional code
        }

        }
}
```

Até este ponto, o trecho de código acima só mostrou o exemplo de execução de solicitações HTTP regulares. Mas a "mágica" vem nas seções a seguir, em que ele mostra como todas as solicitações HTTP feitas pelo `HttpClient` podem ter políticas resilientes, como repetições com retirada exponencial, separadores de circuito, recursos de segurança usando tokens de autenticação ou até mesmo qualquer outro recurso personalizado. E tudo isso pode ser feito apenas adicionando políticas e delegando manipuladores a seus clientes tipados registrados.

## <a name="additional-resources"></a>Recursos adicionais

- **Usando o HttpClientFactory no .NET**  
  [https://docs.microsoft.com/aspnet/core/fundamentals/http-requests](/aspnet/core/fundamentals/http-requests)

- **HttpClientFactory o código-fonte no `dotnet/extensions` repositório github**  
  <https://github.com/dotnet/extensions/tree/v3.1.8/src/HttpClientFactory>

- **Polly (biblioteca de tratamento de falhas transitórias e resiliência do .NET)**  
  <http://www.thepollyproject.org/>
  
- **Usando IHttpClientFactory sem injeção de dependência (problema do GitHub)**  
  <https://github.com/dotnet/extensions/issues/1345>

>[!div class="step-by-step"]
>[Anterior](implement-resilient-entity-framework-core-sql-connections.md) 
> [Avançar](implement-http-call-retries-exponential-backoff-polly.md)
