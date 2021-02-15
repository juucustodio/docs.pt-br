---
title: Injeção de dependência no .NET
description: Saiba como o .NET implementa a injeção de dependência e como usá-la.
author: IEvangelist
ms.author: dapine
ms.date: 10/28/2020
ms.topic: overview
ms.openlocfilehash: cc030e32846690b6544b99030800b50055a3113e
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94818824"
---
# <a name="dependency-injection-in-net"></a>Injeção de dependência no .NET

O .NET dá suporte ao padrão de design de software de injeção de dependência (DI), que é uma técnica para obter [inversão de controle (IOC)](../../architecture/modern-web-apps-azure/architectural-principles.md#dependency-inversion) entre classes e suas dependências. A injeção de dependência no .NET é um [cidadão de primeira classe](https://en.wikipedia.org/wiki/First-class_citizen), juntamente com configuração, registro em log e o padrão de opções.

Uma *dependência* é um objeto do qual outro objeto depende. Examine a seguinte `MessageWriter` classe com um `Write` método de que outras classes dependem:

```csharp
public class MessageWriter
{
    public void Write(string message)
    {
        Console.WriteLine($"MessageWriter.Write(message: \"{message}\")");
    }
}
```

Uma classe pode criar uma instância da `MessageWriter` classe para fazer uso de seu `Write` método. No exemplo a seguir, a `MessageWriter` classe é uma dependência da `Worker` classe:

```csharp
public class Worker : BackgroundService
{
    private readonly MessageWriter _messageWriter = new MessageWriter();

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            _messageWriter.Write($"Worker running at: {DateTimeOffset.Now}");
            await Task.Delay(1000, stoppingToken);
        }
    }
}
```

A classe cria e depende diretamente da `MessageWriter` classe. As dependências embutidas em código, como no exemplo anterior, são problemáticas e devem ser evitadas pelos seguintes motivos:

- Para substituir `MessageWriter` por uma implementação diferente, a `Worker` classe deve ser modificada.
- Se `MessageWriter` tiver dependências, elas também deverão ser configuradas pela `Worker` classe. Em um projeto grande com várias classes dependendo da `MessageWriter`, o código de configuração fica pulverizado por todo o aplicativo.
- É difícil testar a unidade dessa implementação. O aplicativo deve usar uma simulação ou stub da classe `MessageWriter`, o que não é possível com essa abordagem.

Injeção de dependência trata desses problemas da seguinte maneira:

- O uso de uma interface ou classe base para abstrair a implementação da dependência.
- Registrando a dependência em um contêiner de serviço. O .NET fornece um contêiner de serviço interno, <xref:System.IServiceProvider> . Normalmente, os serviços são registrados na inicialização do aplicativo e anexados a um <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection> . Depois que todos os serviços forem adicionados, você usará <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionContainerBuilderExtensions.BuildServiceProvider%2A> para criar o contêiner de serviço.
- *Injeção* do serviço no construtor da classe na qual ele é usado. A estrutura assume a responsabilidade de criar uma instância da dependência e de descartá-la quando não for mais necessária.

Por exemplo, a `IMessageWriter` interface define o `Write` método:

:::code language="csharp" source="snippets/configuration/dependency-injection/IMessageWriter.cs":::

Essa interface é implementada por um tipo concreto, `MessageWriter`:

:::code language="csharp" source="snippets/configuration/dependency-injection/MessageWriter.cs":::

O código de exemplo registra o `IMessageWriter` serviço com o tipo concreto `MessageWriter` . O <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionServiceExtensions.AddScoped%2A> método registra o serviço com um tempo de vida de escopo, o tempo de vida de uma única solicitação. Os [tempos de vida do serviço](#service-lifetimes) são descritos posteriormente neste artigo.

:::code language="csharp" source="snippets/configuration/dependency-injection/Program.cs" highlight="16":::

No aplicativo de exemplo, o `IMessageWriter` serviço é solicitado e usado para chamar o `Write` método:

:::code language="csharp" source="snippets/configuration/dependency-injection/Worker.cs":::

Usando o padrão DI, o serviço de trabalho:

- Não usa o tipo concreto `MessageWriter` , apenas a `IMessageWriter` interface que o implementa. Isso facilita a alteração da implementação que o controlador usa sem modificar o controlador.
- Não cria uma instância do `MessageWriter` , ela é criada pelo contêiner de di.

A implementação da `IMessageWriter` interface pode ser aprimorada usando a API de registro em log interna:

:::code language="csharp" source="snippets/configuration/dependency-injection/LoggingMessageWriter.cs":::

O `ConfigureServices` método atualizado registra a nova `IMessageWriter` implementação:

```csharp
static IHostBuilder CreateHostBuilder(string[] args) =>
    Host.CreateDefaultBuilder(args)
        .ConfigureServices((_, services) =>
            services.AddHostedService<Worker>()
                    .AddScoped<IMessageWriter, LoggingMessageWriter>());
```

`LoggingMessageWriter` depende de <xref:Microsoft.Extensions.Logging.ILogger%601> , que ele solicita no construtor. `ILogger<TCategoryName>` é um [serviço fornecido pelo Framework](#framework-provided-services).

Não é incomum usar a injeção de dependência de uma maneira encadeada. Por sua vez, cada dependência solicitada solicita suas próprias dependências. O contêiner resolve as dependências no grafo e retorna o serviço totalmente resolvido. O conjunto de dependências que precisa ser resolvido normalmente é chamado de *árvore de dependência*, *grafo de dependência* ou *grafo de objeto*.

O contêiner resolve aproveitando `ILogger<TCategoryName>` os [tipos abertos (genéricos)](/dotnet/csharp/language-reference/language-specification/types#open-and-closed-types), eliminando a necessidade de registrar cada [tipo construído (genérico)](/dotnet/csharp/language-reference/language-specification/types#constructed-types).

Na terminologia de injeção de dependência, um serviço:

- Normalmente é um objeto que fornece um serviço para outros objetos, como o `IMessageWriter` serviço.
- O não está relacionado a um serviço Web, embora o serviço possa usar um serviço Web.

A estrutura fornece um sistema de registro em log robusto. As `IMessageWriter` implementações mostradas nos exemplos anteriores foram escritas para demonstrar a di básica, não para implementar o registro em log. A maioria dos aplicativos não deve precisar gravar agentes. O código a seguir demonstra como usar o log padrão, que requer que apenas o seja `Worker` registrado no `ConfigureServices` como um serviço hospedado <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionHostedServiceExtensions.AddHostedService%2A> :

```csharp
public class Worker : BackgroundService
{
    private readonly ILogger<Worker> _logger;

    public Worker(ILogger<Worker> logger) =>
        _logger = logger;

    protected override async Task ExecuteAsync(CancellationToken stoppingToken)
    {
        while (!stoppingToken.IsCancellationRequested)
        {
            _logger.LogInformation("Worker running at: {time}", DateTimeOffset.Now);
            await Task.Delay(1000, stoppingToken);
        }
    }
}
```

Usando o código anterior, não há necessidade de atualizar `ConfigureServices` , porque o registro em log é fornecido pela estrutura.

## <a name="register-groups-of-services-with-extension-methods"></a>Registrar grupos de serviços com métodos de extensão

O Microsoft Extensions usa uma Convenção para registrar um grupo de serviços relacionados. A Convenção é usar um método de `Add{GROUP_NAME}` extensão único para registrar todos os serviços exigidos por um recurso de estrutura. Por exemplo, o <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions%2A> método de extensão registra todos os serviços necessários para usar as opções.

## <a name="framework-provided-services"></a>Serviços fornecidos pela estrutura

O `ConfigureServices` método registra os serviços que o aplicativo usa, incluindo recursos de plataforma. Inicialmente, o `IServiceCollection` fornecido para o `ConfigureServices` tem serviços definidos pela estrutura, dependendo de [como o host foi configurado](generic-host.md#host-configuration). Para aplicativos baseados nos modelos .NET, a estrutura registra centenas de serviços.

A tabela a seguir lista uma pequena amostra desses serviços registrados no Framework:

| Tipo de Serviço                                                                       | Tempo de vida  |
|------------------------------------------------------------------------------------|-----------|
| <xref:Microsoft.Extensions.Hosting.IHostApplicationLifetime>                       | Singleton |
| <xref:Microsoft.Extensions.Logging.ILogger%601?displayProperty=fullName>           | Singleton |
| <xref:Microsoft.Extensions.Logging.ILoggerFactory?displayProperty=fullName>        | Singleton |
| <xref:Microsoft.Extensions.ObjectPool.ObjectPoolProvider?displayProperty=fullName> | Singleton |
| <xref:Microsoft.Extensions.Options.IConfigureOptions%601?displayProperty=fullName> | Transitório |
| <xref:Microsoft.Extensions.Options.IOptions%601?displayProperty=fullName>          | Singleton |
| <xref:System.Diagnostics.DiagnosticListener?displayProperty=fullName>              | Singleton |
| <xref:System.Diagnostics.DiagnosticSource?displayProperty=fullName>                | Singleton |

## <a name="service-lifetimes"></a>Tempos de vida do serviço

Os serviços podem ser registrados com um dos seguintes tempos de vida:

- Transitório
- Com escopo
- Singleton

As seções a seguir descrevem cada um dos tempos de vida anteriores. Escolha um tempo de vida apropriado para cada serviço registrado.

### <a name="transient"></a>Transitório

Serviços temporários de tempo de vida são criados cada vez que são solicitados pelo contêiner de serviço. Esse tempo de vida funciona melhor para serviços leves e sem estado. Registre serviços transitórios com <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionServiceExtensions.AddTransient%2A> .

Em aplicativos que processam solicitações, os serviços transitórios são descartados no final da solicitação.

### <a name="scoped"></a>Com escopo

Para aplicativos Web, um tempo de vida com escopo indica que os serviços são criados uma vez por solicitação do cliente (conexão). Registre os serviços com escopo com <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionServiceExtensions.AddScoped%2A> .

Em aplicativos que processam solicitações, os serviços com escopo são descartados no final da solicitação.

Ao usar Entity Framework Core, o <xref:Microsoft.Extensions.DependencyInjection.EntityFrameworkServiceCollectionExtensions.AddDbContext%2A> método de extensão registra os `DbContext` tipos com um tempo de vida com escopo definido por padrão.

> [!NOTE]
> **Não resolva** um serviço com escopo de um singleton e tenha cuidado para não fazê-lo indiretamente, por exemplo, por meio de um serviço transitório. Pode fazer com que o serviço tenha um estado incorreto durante o processamento das solicitações seguintes. Não há problema em:
>
> - Resolva um serviço singleton de um serviço com escopo ou transitório.
> - Resolva um serviço com escopo de outro serviço com escopo ou transitório.

Por padrão, no ambiente de desenvolvimento, a resolução de um serviço de outro serviço com um tempo de vida maior gera uma exceção. Para obter mais informações, confira [Validação de escopo](#scope-validation).

### <a name="singleton"></a>Singleton

Os serviços de vida útil singleton são criados:

- Na primeira vez que forem solicitadas.
- Pelo desenvolvedor, ao fornecer uma instância de implementação diretamente para o contêiner. Essa abordagem raramente é necessária.

Cada solicitação subsequente da implementação do serviço do contêiner de injeção de dependência usa a mesma instância. Se o aplicativo exigir um comportamento singleton, permita que o contêiner de serviço gerencie o tempo de vida do serviço. Não implemente o padrão de design singleton e forneça código para descartar o singleton. Os serviços nunca devem ser descartados pelo código que resolveu o serviço do contêiner. Se um tipo ou fábrica for registrado como um singleton, o contêiner descartará o singleton automaticamente.

Registre os serviços singleton com <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionServiceExtensions.AddSingleton%2A> . Os serviços singleton devem ser thread-safe e geralmente são usados em serviços sem estado.

Em aplicativos que processam solicitações, os serviços singleton são descartados quando o <xref:Microsoft.Extensions.DependencyInjection.ServiceProvider> é Descartado no desligamento do aplicativo. Como a memória não é liberada até que o aplicativo seja desligado, considere o uso de memória com um serviço singleton.

> [!WARNING]
> _*_Não_*_ resolva um serviço com escopo de um singleton. Pode fazer com que o serviço tenha um estado incorreto durante o processamento das solicitações seguintes. É bom resolver um serviço singleton de um serviço com escopo ou transitório.

## <a name="service-registration-methods"></a>Métodos de registro do serviço

A estrutura fornece métodos de extensão de registro de serviço que são úteis em cenários específicos:

| Método | Automática<br>objeto<br>descarte | Vários<br>implementações | Passar argumentos |
|--|:-:|:-:|:-:|
| `Add{LIFETIME}<{SERVICE}, {IMPLEMENTATION}>()`<br><br>Exemplo:<br><br>`services.AddSingleton<IMyDep, MyDep>();` | Sim | Sim | Não |
| `Add{LIFETIME}<{SERVICE}>(sp => new {IMPLEMENTATION})`<br><br>Exemplos:<br><br>`services.AddSingleton<IMyDep>(sp => new MyDep());`<br>`services.AddSingleton<IMyDep>(sp => new MyDep(99));` | Sim | Sim | Sim |
| `Add{LIFETIME}<{IMPLEMENTATION}>()`<br><br>Exemplo:<br><br>`services.AddSingleton<MyDep>();` | Sim | Não | Não |
| `AddSingleton<{SERVICE}>(new {IMPLEMENTATION})`<br><br>Exemplos:<br><br>`services.AddSingleton<IMyDep>(new MyDep());`<br>`services.AddSingleton<IMyDep>(new MyDep(99));` | Não | Sim | Sim |
| `AddSingleton(new {IMPLEMENTATION})`<br><br>Exemplos:<br><br>`services.AddSingleton(new MyDep());`<br>`services.AddSingleton(new MyDep(99));` | Não | Não | Sim |

Para obter mais informações sobre o descarte de tipos, consulte a seção [Descarte de serviços](dependency-injection-guidelines.md#disposal-of-services).

O registro de um serviço com apenas um tipo de implementação é equivalente ao registro desse serviço com a mesma implementação e tipo de serviço. É por isso que várias implementações de um serviço não podem ser registradas usando os métodos que não usam um tipo de serviço explícito. Esses métodos podem registrar vários _instances * de um serviço, mas todos terão o mesmo tipo de *implementação* .

Qualquer um dos métodos de registro de serviço acima pode ser usado para registrar várias instâncias de serviço do mesmo tipo de serviço. No exemplo a seguir, `AddSingleton` é chamado duas vezes com `IMessageWriter` como o tipo de serviço. A segunda chamada para `AddSingleton` substitui a anterior quando resolvida como `IMessageWriter` e a adiciona à anterior quando vários serviços são resolvidos por meio de `IEnumerable<IMessageWriter>` . Os serviços aparecem na ordem em que foram registrados quando resolvidos por meio de `IEnumerable<{SERVICE}>` .

:::code language="csharp" source="snippets/configuration/console-di-ienumerable/Program.cs" highlight="19-24":::

O código-fonte de exemplo anterior registra duas implementações do `IMessageWriter` .

:::code language="csharp" source="snippets/configuration/console-di-ienumerable/ExampleService.cs" highlight="9-18":::

O `ExampleService` define dois parâmetros de Construtor; um único `IMessageWriter` e um `IEnumerable<IMessageWriter>` . O único `IMessageWriter` é a última implementação a ser registrada, enquanto que `IEnumerable<IMessageWriter>` representa todas as implementações registradas.

A estrutura também fornece `TryAdd{LIFETIME}` métodos de extensão, que registram o serviço somente se ainda não houver uma implementação registrada.

No exemplo a seguir, a chamada para `AddSingleton` registra `ConsoleMessageWriter` como uma implementação para `IMessageWriter` . A chamada para `TryAddSingleton` não tem efeito porque `IMessageWriter` já tem uma implementação registrada:

```csharp
services.AddSingleton<IMessageWriter, ConsoleMessageWriter>();
services.TryAddSingleton<IMessageWriter, LoggingMessageWriter>();
```

O `TryAddSingleton` não tem efeito, pois já foi adicionado e o "try" falhará. O `ExampleService` declararia o seguinte:

```csharp
public class ExampleService
{
    public ExampleService(
        IMessageWriter messageWriter,
        IEnumerable<IMessageWriter> messageWriters)
    {
        Trace.Assert(messageWriter is ConsoleMessageWriter);
        Trace.Assert(messageWriters.Single() is ConsoleMessageWriter);
    }
}
```

Para obter mais informações, consulte:

- <xref:Microsoft.Extensions.DependencyInjection.Extensions.ServiceCollectionDescriptorExtensions.TryAdd%2A>
- <xref:Microsoft.Extensions.DependencyInjection.Extensions.ServiceCollectionDescriptorExtensions.TryAddTransient%2A>
- <xref:Microsoft.Extensions.DependencyInjection.Extensions.ServiceCollectionDescriptorExtensions.TryAddScoped%2A>
- <xref:Microsoft.Extensions.DependencyInjection.Extensions.ServiceCollectionDescriptorExtensions.TryAddSingleton%2A>

Os métodos [TryAddEnumerable (Service Descriptor)](xref:Microsoft.Extensions.DependencyInjection.Extensions.ServiceCollectionDescriptorExtensions.TryAddEnumerable%2A) registram o serviço somente se ainda não houver uma implementação *do mesmo tipo*. Vários serviços são resolvidos via `IEnumerable<{SERVICE}>`. Ao registrar serviços, adicione uma instância se um dos mesmos tipos ainda não tiver sido adicionado. Os autores de biblioteca usam `TryAddEnumerable` para evitar o registro de várias cópias de uma implementação no contêiner.

No exemplo a seguir, a primeira chamada para `TryAddEnumerable` registra `MessageWriter` como uma implementação para `IMessageWriter1` . A segunda chamada é registrada `MessageWriter` para `IMessageWriter2` . A terceira chamada não tem nenhum efeito porque `IMessageWriter1` já tem uma implementação registrada de `MessageWriter` :

```csharp
public interface IMessageWriter1 { }
public interface IMessageWriter2 { }

public class MessageWriter : IMessageWriter1, IMessageWriter2
{
}

services.TryAddEnumerable(ServiceDescriptor.Singleton<IMessageWriter1, MessageWriter>());
services.TryAddEnumerable(ServiceDescriptor.Singleton<IMessageWriter2, MessageWriter>());
services.TryAddEnumerable(ServiceDescriptor.Singleton<IMessageWriter1, MessageWriter>());
```

O registro de serviço geralmente é independente de ordem, exceto ao registrar várias implementações do mesmo tipo.

`IServiceCollection` é uma coleção de <xref:Microsoft.Extensions.DependencyInjection.ServiceDescriptor> objetos. O exemplo a seguir mostra como registrar um serviço criando e adicionando um `ServiceDescriptor` :

```csharp
string secretKey = Configuration["SecretKey"];
var descriptor = new ServiceDescriptor(
    typeof(IMessageWriter),
    _ => new DefaultMessageWriter(secretKey),
    ServiceLifetime.Transient);

services.Add(descriptor);
```

Os `Add{LIFETIME}` métodos internos usam a mesma abordagem. Por exemplo, consulte o [código-fonte de Addscoped](https://github.com/dotnet/extensions/blob/v3.1.8/src/DependencyInjection/DI.Abstractions/src/ServiceCollectionServiceExtensions.cs#L216-L237).

### <a name="constructor-injection-behavior"></a>Comportamento da injeção de construtor

Os serviços podem ser resolvidos usando:

- <xref:System.IServiceProvider>
- <xref:Microsoft.Extensions.DependencyInjection.ActivatorUtilities>:
  - Cria objetos que não estão registrados no contêiner.
  - Usado com alguns recursos de estrutura.

Os construtores podem aceitar argumentos que não são fornecidos pela injeção de dependência, mas que precisam atribuir valores padrão.

Quando os serviços são resolvidos por `IServiceProvider` ou `ActivatorUtilities`, a injeção do construtor exige um construtor *público*.

Quando os serviços são resolvidos por `ActivatorUtilities`, a injeção de construtor exige a existência de apenas de um construtor aplicável. Há suporte para sobrecargas de construtor, mas somente uma sobrecarga pode existir, cujos argumentos podem ser todos atendidos pela injeção de dependência.

## <a name="scope-validation"></a>Validação de escopo

Quando o aplicativo é executado no `Development` ambiente e chama [CreateDefaultBuilder](generic-host.md#default-builder-settings) para criar o host, o provedor de serviço padrão executa verificações para verificar se:

- Os serviços com escopo não são resolvidos do provedor de serviços raiz.
- Os serviços com escopo não são injetados em singletons.

O provedor de serviços raiz é criado quando <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionContainerBuilderExtensions.BuildServiceProvider%2A> é chamado. O tempo de vida do provedor de serviço raiz corresponde ao tempo de vida do aplicativo quando o provedor começa com o aplicativo e é Descartado quando o aplicativo é desligado.

Os serviços com escopo são descartados pelo contêiner que os criou. Se um serviço com escopo for criado no contêiner raiz, o tempo de vida do serviço será efetivamente promovido para singleton porque é descartado apenas pelo contêiner raiz quando o aplicativo é desligado. A validação dos escopos de serviço detecta essas situações quando `BuildServiceProvider` é chamado.

## <a name="see-also"></a>Confira também

- [Usar injeção de dependência no .NET](dependency-injection-usage.md)
- [Diretrizes de injeção de dependência](dependency-injection-guidelines.md)
- [Injeção de dependência no ASP.NET Core](/aspnet/core/fundamentals/dependency-injection)
- [Padrões de conferência NDC para desenvolvimento de aplicativo de DI](https://www.youtube.com/watch?v=x-C-CNBVTaY)
- [Princípio de dependências explícitas](../../architecture/modern-web-apps-azure/architectural-principles.md#explicit-dependencies)
- [Inversão de contêineres de controle e padrão de injeção de dependência (Martin Fowler)](https://www.martinfowler.com/articles/injection.html)
- Os bugs de injeção de erros devem ser criados no repositório [github.com/dotnet/Extensions](https://github.com/dotnet/extensions/issues)
