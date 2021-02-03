---
title: Diretrizes de injeção de dependência
description: Conheça várias diretrizes de injeção de dependência e práticas recomendadas para o desenvolvimento de aplicativos .NET.
author: IEvangelist
ms.author: dapine
ms.date: 10/29/2020
ms.topic: guide
ms.openlocfilehash: 105536df873829dc79dcca1b86d080360e71303f
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505400"
---
# <a name="dependency-injection-guidelines"></a>Diretrizes de injeção de dependência

Este artigo fornece diretrizes gerais e práticas recomendadas para implementar a injeção de dependência em aplicativos .NET.

## <a name="design-services-for-dependency-injection"></a>Projetar serviços para injeção de dependência

Ao projetar serviços para injeção de dependência:

- Evite classes e membros com estado e estáticos. Evite criar o estado global criando aplicativos para usar os serviços singleton.
- Evite a instanciação direta das classes dependentes em serviços. A instanciação direta acopla o código a uma implementação específica.
- Torne os serviços pequenos, bem fatorados e facilmente testados.

Se uma classe tiver muitas dependências injetadas, poderá ser um sinal de que a classe tem muitas responsabilidades e violará o [princípio de responsabilidade única (SRP)](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#single-responsibility). Tente refatorar a classe movendo algumas de suas responsabilidades para novas classes.

### <a name="disposal-of-services"></a>Descarte de serviços

O contêiner é responsável pela limpeza dos tipos que cria e chama <xref:System.IDisposable.Dispose%2A> em <xref:System.IDisposable> instâncias. Os serviços resolvidos do contêiner nunca devem ser descartados pelo desenvolvedor. Se um tipo ou fábrica for registrado como um singleton, o contêiner descartará o singleton automaticamente.

No exemplo a seguir, os serviços são criados pelo contêiner de serviço e descartados automaticamente:

:::code language="csharp" source="snippets/configuration/console-di-disposable/TransientDisposable.cs":::

O descartável anterior deve ter um tempo de vida transitório.

:::code language="csharp" source="snippets/configuration/console-di-disposable/ScopedDisposable.cs":::

O descartável anterior tem como objetivo ter um tempo de vida de escopo.

:::code language="csharp" source="snippets/configuration/console-di-disposable/SingletonDisposable.cs":::

O descartável anterior deve ter um tempo de vida singleton.

:::code language="csharp" source="snippets/configuration/console-di-disposable/Program.cs" range="1-21,41-60" highlight="":::

O console de depuração mostra a seguinte saída de exemplo após a execução:

```console
Scope 1...
ScopedDisposable.Dispose()
TransientDisposable.Dispose()

Scope 2...
ScopedDisposable.Dispose()
TransientDisposable.Dispose()

info: Microsoft.Hosting.Lifetime[0]
      Application started.Press Ctrl+C to shut down.
info: Microsoft.Hosting.Lifetime[0]
     Hosting environment: Production
info: Microsoft.Hosting.Lifetime[0]
     Content root path: .\configuration\console-di-disposable\bin\Debug\net5.0
info: Microsoft.Hosting.Lifetime[0]
     Application is shutting down...
SingletonDisposable.Dispose()
```

### <a name="services-not-created-by-the-service-container"></a>Serviços não criados pelo contêiner de serviço

Considere o seguinte código:

```csharp
public void ConfigureServices(IServiceCollection services)
{
    services.AddSingleton(new ExampleService());

    // ...
}
```

No código anterior:

- A `ExampleService` instância **não** é criada pelo contêiner de serviço.
- A estrutura não **descarta os** serviços automaticamente.
- O desenvolvedor é responsável por descartar os serviços.

### <a name="idisposable-guidance-for-transient-and-shared-instances"></a>Diretrizes de IDisposable para instâncias transitórias e compartilhadas

#### <a name="transient-limited-lifetime"></a>Tempo de vida transitório, limitado

**Cenário**

O aplicativo requer uma <xref:System.IDisposable> instância com um tempo de vida transitório para qualquer um dos seguintes cenários:

- A instância é resolvida no escopo raiz (contêiner raiz).
- A instância deve ser descartada antes do término do escopo.

**Solução**

Use o padrão de fábrica para criar uma instância fora do escopo pai. Nessa situação, o aplicativo geralmente teria um `Create` método que chamasse o construtor do tipo final diretamente. Se o tipo final tiver outras dependências, a fábrica poderá:

- Receber um <xref:System.IServiceProvider> em seu construtor.
- Use <xref:Microsoft.Extensions.DependencyInjection.ActivatorUtilities.CreateInstance%2A?displayProperty=nameWithType> para instanciar a instância fora do contêiner, ao usar o contêiner para suas dependências.

#### <a name="shared-instance-limited-lifetime"></a>Instância compartilhada, tempo de vida limitado

**Cenário**

O aplicativo requer uma <xref:System.IDisposable> instância compartilhada em vários serviços, mas a <xref:System.IDisposable> instância deve ter um tempo de vida limitado.

**Solução**

Registre a instância com um tempo de vida de escopo. Use <xref:Microsoft.Extensions.DependencyInjection.IServiceScopeFactory.CreateScope%2A?displayProperty=nameWithType> para criar um novo <xref:Microsoft.Extensions.DependencyInjection.IServiceScope> . Use o escopo <xref:System.IServiceProvider> para obter os serviços necessários. Descarte o escopo quando ele não for mais necessário.

#### <a name="general-idisposable-guidelines"></a>`IDisposable`Diretrizes gerais

- Não registre <xref:System.IDisposable> instâncias com um tempo de vida transitório. Em vez disso, use o padrão de fábrica.
- Não resolva <xref:System.IDisposable> instâncias com um tempo de vida transitório ou com escopo definido no escopo raiz. A única exceção a isso é se o aplicativo cria/recria e descarta <xref:System.IServiceProvider> , mas esse não é um padrão ideal.
- O recebimento de uma <xref:System.IDisposable> dependência por meio de di não exige que o receptor se implemente <xref:System.IDisposable> . O receptor da <xref:System.IDisposable> dependência não deve chamar <xref:System.IDisposable.Dispose%2A> essa dependência.
- Use escopos para controlar os tempos de vida dos serviços. Os escopos não são hierárquicos e não há nenhuma conexão especial entre escopos.

Para obter mais informações sobre a limpeza de recursos, consulte [implementar um `Dispose` método](../../standard/garbage-collection/implementing-dispose.md)ou [implementar um `DisposeAsync` método](../../standard/garbage-collection/implementing-disposeasync.md). Além disso, considere os [Serviços transitórios descartáveis capturados pelo](#disposable-transient-services-captured-by-container) cenário de contêiner, pois ele se relaciona com a limpeza de recursos.

## <a name="default-service-container-replacement"></a>Substituição do contêiner de serviço padrão

O contêiner de serviço interno foi projetado para atender às necessidades da estrutura e da maioria dos aplicativos de consumidor. É recomendável usar o contêiner interno, a menos que você precise de um recurso específico ao qual ele não ofereça suporte, como:

- Injeção de propriedade
- Injeção com base no nome
- Contêineres filho
- Gerenciamento de tempo de vida personalizado
- Suporte de `Func<T>` para inicialização lenta
- Registro baseado em Convenção

Os seguintes contêineres de terceiros podem ser usados com aplicativos ASP.NET Core:

- [Autofac](https://autofac.readthedocs.io/en/latest/integration/aspnetcore.html)
- [DryIoc](https://www.nuget.org/packages/DryIoc.Microsoft.DependencyInjection)
- [Grace](https://www.nuget.org/packages/Grace.DependencyInjection.Extensions)
- [LightInject](https://github.com/seesharper/LightInject.Microsoft.DependencyInjection)
- [Lamar](https://jasperfx.github.io/lamar/)
- [Stashbox](https://github.com/z4kn4fein/stashbox-extensions-dependencyinjection)
- [Unity](https://www.nuget.org/packages/Unity.Microsoft.DependencyInjection)

## <a name="thread-safety"></a>Acesso thread-safe

Crie serviços singleton thread-safe. Se um serviço singleton tiver uma dependência em um serviço transitório, o serviço transitório também poderá exigir a segurança do thread dependendo de como ele é usado pelo singleton.

O método de fábrica de um serviço singleton, como o segundo argumento para [addsingleton \<TService> (IServiceCollection, Func \<IServiceProvider,TService> )](xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionServiceExtensions.AddSingleton%2A), não precisa ser thread-safe. Como um construtor de tipo ( `static` ), é garantido que ele seja chamado apenas uma vez por um único thread.

## <a name="recommendations"></a>Recomendações

- `async/await` e a `Task` resolução de serviço baseada não tem suporte. Como o C# não dá suporte a construtores assíncronos, use métodos assíncronos após a resolução síncrona do serviço.
- Evite armazenar dados e a configuração diretamente no contêiner do serviço. Por exemplo, o carrinho de compras de um usuário normalmente não deve ser adicionado ao contêiner do serviço. A configuração deve usar o padrão de opções. Da mesma forma, evite objetos de "portador de dados" que existem somente para permitir o acesso a outro objeto. É melhor solicitar o item real por meio da DI.
- Evite o acesso estático aos serviços. Por exemplo, evite capturar [IApplicationBuilder. ApplicationServices](xref:Microsoft.AspNetCore.Builder.IApplicationBuilder.ApplicationServices) como um campo ou propriedade estática para uso em outro lugar.
- Mantenha as [fábricas de injeção](#async-di-factories-can-cause-deadlocks) rápida e síncrona.
- Evite usar o [*padrão de localizador de serviço*](#scoped-service-as-singleton). Por exemplo, não invoque <xref:System.IServiceProvider.GetService%2A> para obter uma instância de serviço quando for possível usar a DI.
- Outra variação de localizador de serviço a ser evitada é injetar um alocador que resolve as dependências em runtime. Essas duas práticas misturam estratégias de [inversão de controle](/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion).
- Evite chamadas para <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionContainerBuilderExtensions.BuildServiceProvider%2A> no `ConfigureServices` . Chamar `BuildServiceProvider` normalmente acontece quando o desenvolvedor deseja resolver um serviço no `ConfigureServices` .
- [Serviços Inposados transitórios são capturados](#disposable-transient-services-captured-by-container) pelo contêiner para descarte. Isso pode transformar em um vazamento de memória se resolvido do contêiner de nível superior.
- Habilite a validação de escopo para certificar-se de que o aplicativo não tem singletons que capturam serviços com escopo. Para obter mais informações, confira [Validação de escopo](dependency-injection.md#scope-validation).

Como todos os conjuntos de recomendações, talvez você encontre situações em que é necessário ignorar uma recomendação. As exceções são raras, principalmente os casos especiais dentro da própria estrutura.

A DI é uma *alternativa* aos padrões de acesso a objeto estático/global. Talvez você não obtenha os benefícios da DI se combiná-lo com o acesso a objeto estático.

## <a name="example-anti-patterns"></a>Antipadrões de exemplo

Além das diretrizes neste artigo, há vários antipadrões *que você **deve** evitar*. Alguns desses antipadrões são aprender a desenvolver os tempos de execução em si.

> [!WARNING]
> Esses são antipadrões de exemplo, *não copiam* o código, *não usam esses* padrões e evitam esses padrões com todos os custos.

### <a name="disposable-transient-services-captured-by-container"></a>Serviços transitórios descartáveis capturados pelo contêiner

Quando você registra serviços *transitórios* que implementam <xref:System.IDisposable> , por padrão, o contêiner di manterá essas referências e não delas <xref:System.IDisposable.Dispose> até que o contêiner seja Descartado quando o aplicativo for interrompido se ele for resolvido no contêiner ou até que o escopo seja Descartado se eles forem resolvidos a partir de um escopo. Isso pode transformar em um vazamento de memória se resolvido do nível de contêiner.

:::code language="csharp" source="snippets/configuration/di-anti-patterns/Program.cs" range="18-30":::

No antipadrão anterior, 1.000 `ExampleDisposable` objetos são instanciados e com raiz. Eles não serão descartados até que a `serviceProvider` instância seja descartada.

Para obter mais informações sobre como depurar vazamentos de memória, consulte [depurar um vazamento de memória no .net](../diagnostics/debug-memory-leak.md).

### <a name="async-di-factories-can-cause-deadlocks"></a>Fábricas de DI assíncronas podem causar deadlocks

O termo "fábricas de DI" refere-se aos métodos de sobrecarga que existem ao chamar `Add{LIFETIME}` . Há sobrecargas aceitando um `Func<IServiceProvider, T>` onde `T` o serviço está sendo registrado e o parâmetro é nomeado `implementationFactory` . O `implementationFactory` pode ser fornecido como uma expressão lambda, uma função local ou um método. Se a fábrica for assíncrona, e você usar <xref:System.Threading.Tasks.Task%601.Result?displayProperty=nameWithType> , isso gerará um deadlock.

:::code language="csharp" source="snippets/configuration/di-anti-patterns/Program.cs" range="32-45" highlight="4-8":::

No código anterior, o recebe `implementationFactory` uma expressão lambda em que o corpo chama <xref:System.Threading.Tasks.Task%601.Result?displayProperty=nameWithType> um método de `Task<Bar>` retorno. Isso ***causa um deadlock***. O `GetBarAsync` método simplesmente emula uma operação de trabalho assíncrona com <xref:System.Threading.Tasks.Task.Delay%2A?displayProperty=nameWithType> e, em seguida, chama <xref:Microsoft.Extensions.DependencyInjection.ServiceProviderServiceExtensions.GetRequiredService%60%601(System.IServiceProvider)> .

:::code language="csharp" source="snippets/configuration/di-anti-patterns/Program.cs" range="47-53":::

Para obter mais informações sobre diretrizes assíncronas, consulte [programação assíncrona: informações importantes e conselhos](../../csharp/async.md#important-info-and-advice). Para obter mais informações sobre depuração de deadlocks, consulte [depurar um deadlock no .net](../diagnostics/debug-deadlock.md).

Quando você estiver executando esse antipadrão e o deadlock ocorrer, poderá exibir os dois threads aguardando a janela de pilhas paralelas do Visual Studio. Para obter mais informações, consulte [exibir threads e tarefas na janela pilhas paralelas](/visualstudio/debugger/using-the-parallel-stacks-window).

### <a name="captive-dependency"></a>Dependência cativo

O termo ["dependência cativo"](https://blog.ploeh.dk/2014/06/02/captive-dependency) foi cunhado por [Mark Seeman](https://blog.ploeh.dk/about)e refere-se à configuração incorreta de tempos de vida do serviço, em que um serviço de vida maior tem um serviço de vida mais curto cativo.

:::code language="csharp" source="snippets/configuration/di-anti-patterns/Program.cs" range="55-65":::

No código anterior, `Foo` é registrado como um singleton e `Bar` tem o escopo, que na superfície parece válido. No entanto, considere a implementação de `Foo` .

:::code language="csharp" source="snippets/configuration/di-anti-patterns/Foo.cs" highlight="5":::

O `Foo` objeto requer um `Bar` objeto e, como `Foo` é um singleton e `Bar` tem o escopo definido, essa é uma configuração incorreta. Como está, `Foo` ela só seria instanciada uma vez e seria mantida `Bar` por seu tempo de vida, o que é mais longo do que o tempo de vida do escopo pretendido de `Bar` . Você deve considerar a validação de escopos, passando `validateScopes: true` para o <xref:Microsoft.Extensions.DependencyInjection.ServiceCollectionContainerBuilderExtensions.BuildServiceProvider(Microsoft.Extensions.DependencyInjection.IServiceCollection,System.Boolean)> . Ao validar os escopos, você receberá um <xref:System.InvalidOperationException> com uma mensagem semelhante a "não é possível consumir o serviço no escopo ' bar ' do singleton ' foo '.".

Para obter mais informações, confira [Validação de escopo](dependency-injection.md#scope-validation).

### <a name="scoped-service-as-singleton"></a>Serviço com escopo como singleton

Ao usar serviços com escopo, se você não estiver criando um escopo ou dentro de um escopo existente, o serviço se tornará um singleton.

:::code language="csharp" source="snippets/configuration/di-anti-patterns/Program.cs" range="68-82" highlight="13-14":::

No código anterior, `Bar` é recuperado em um <xref:Microsoft.Extensions.DependencyInjection.IServiceScope> , que está correto. O antipadrão é a recuperação de `Bar` fora do escopo, e a variável é nomeada `avoid` para mostrar qual exemplo de recuperação está incorreto.

## <a name="see-also"></a>Consulte também

- [Injeção de dependência no .NET](dependency-injection.md)
- [Tutorial: usar injeção de dependência no .NET](dependency-injection-usage.md)
