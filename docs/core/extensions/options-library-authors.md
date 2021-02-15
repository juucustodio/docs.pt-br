---
title: Diretrizes de padrão de opções para autores de biblioteca do .NET
author: IEvangelist
description: Saiba como expor o padrão de opções como um autor de biblioteca no .NET.
ms.author: dapine
ms.date: 01/28/2021
ms.openlocfilehash: d0da94a8f25c9e5aba6093fab07ccca6a0a7c345
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99217208"
---
# <a name="options-pattern-guidance-for-net-library-authors"></a>Diretrizes de padrão de opções para autores de biblioteca do .NET

Com a ajuda de injeção de dependência, o registro de seus serviços e suas configurações correspondentes podem fazer uso do *padrão de opções*. O padrão de opções permite que os consumidores da sua biblioteca (e seus serviços) exijam instâncias de [interfaces de opções](options.md#options-interfaces) em que `TOptions` é sua classe de opções. O consumo de opções de configuração por meio de objetos fortemente tipados ajuda a garantir uma representação de valor consistente e remove a carga de valores de cadeia de caracteres de análise manual. Há muitos [provedores de configuração](configuration-providers.md) para os consumidores de sua biblioteca usarem. Com esses provedores, os consumidores podem configurar sua biblioteca de várias maneiras.

Como autor da biblioteca do .NET, você aprenderá as diretrizes gerais sobre como expor corretamente o padrão de opções aos consumidores da sua biblioteca. Há várias maneiras de obter a mesma coisa e várias considerações a serem feitas.

## <a name="naming-conventions"></a>Convenções de nomenclatura

Por convenção, os métodos de extensão responsáveis pelo registro de serviços são nomeados `Add{Service}` , em que `{Service}` é um nome significativo e descritivo. Dependendo do pacote, o registro de serviços pode ser acompanhado por métodos de `Use{Service}` extensão. Os `Use{Service}` métodos de extensão são comuns em [ASP.NET Core](/aspnet).

✔️ CONSIDERAR nomes que desambiguam seu serviço de outras ofertas.

❌ Não use nomes que já fazem parte do ecossistema .NET dos pacotes oficiais da Microsoft.

✔️ Considere nomear classes estáticas que exponham métodos de extensão como `{Type}Extensions` , em que `{Type}` é o tipo que você está estendendo.

### <a name="namespace-guidance"></a>Diretrizes de namespace

Os pacotes da Microsoft fazem uso do `Microsoft.Extensions.DependencyInjection` namespace para unificar o registro de várias ofertas de serviço.

✔️ CONSIDERAR um namespace que identifica claramente sua oferta de pacote.

❌ Não use o `Microsoft.Extensions.DependencyInjection` namespace para pacotes Microsoft não oficiais.

## <a name="parameterless"></a>Construtor

Se o serviço puder trabalhar com uma configuração mínima ou nenhuma explícita, considere um método de extensão sem parâmetros.

:::code language="csharp" source="snippets/configuration/options-noparams/ServiceCollectionExtensions.cs" highlight="10-14":::

No código anterior, o `AddMyLibraryService` :

- Estende uma instância de <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>
- Chamadas <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions%60%601(Microsoft.Extensions.DependencyInjection.IServiceCollection)?displayProperty=nameWithType> com o parâmetro de tipo de `LibraryOptions`
- Encadeia uma chamada para <xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A> , que especifica os valores de opção padrão

## <a name="iconfiguration-parameter"></a>Parâmetro `IConfiguration`

Ao criar uma biblioteca que expõe muitas opções aos consumidores, talvez você queira considerar a necessidade de um `IConfiguration` método de extensão de parâmetro. A instância esperada `IConfiguration` deve ter como escopo uma seção nomeada da configuração usando a <xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection%2A?displayProperty=nameWithType> função.

:::code language="csharp" source="snippets/configuration/options-configparam/ServiceCollectionExtensions.cs" highlight="10,12-16":::

No código anterior, o `AddMyLibraryService` :

- Estende uma instância de <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>
- Define um <xref:Microsoft.Extensions.Configuration.IConfiguration> parâmetro `namedConfigurationSection`
- Chama a <xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind(Microsoft.Extensions.Configuration.IConfiguration,System.Object)> passagem de uma instância de opções à qual a configuração se associa

Os consumidores neste padrão fornecem a instância com escopo `IConfiguration` da seção nomeada:

:::code language="csharp" source="snippets/configuration/options-configparam/Program.cs" highlight="22-23":::

A chamada para `.AddMyLibraryService` é feita no <xref:Microsoft.Extensions.Hosting.IHostBuilder.ConfigureServices%2A> método. O mesmo é verdadeiro ao usar uma `Startup` classe, a adição de serviços registrados ocorre no `ConfigureServices` .

Como o autor da biblioteca, a especificação de valores padrão é até você.

> [!NOTE]
> É possível associar a configuração a uma instância de opções. No entanto, há um risco de colisões de nome – o que causará erros. Além disso, ao ligar manualmente dessa forma, você limita o consumo de seu padrão de opções para uma única leitura. As alterações nas configurações não serão revinculadas, pois esses consumidores não poderão usar a interface [IOptionsMonitor](options.md#ioptionsmonitor) .
>
> ```csharp
> services.AddOptions<LibraryOptions>()
>     .Configure<IConfiguration>(
>         (options, configuration) =>
>             configuration.GetSection("LibraryOptions").Bind(options));
> ```

## <a name="actiontoptions-parameter"></a>Parâmetro `Action<TOptions>`

Os consumidores de sua biblioteca podem estar interessados em fornecer uma expressão lambda que produza uma instância da sua classe Options. Nesse cenário, você define um `Action<LibraryOptions>` parâmetro em seu método de extensão.

:::code language="csharp" source="snippets/configuration/options-action/ServiceCollectionExtensions.cs" highlight="10,12":::

No código anterior, o `AddMyLibraryService` :

- Estende uma instância de <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>
- Define um <xref:System.Action%601> `T` parâmetro Where is `LibraryOptions``configureOptions`
- Chamadas <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.Configure%2A> dadas a `configureOptions` ação

Os consumidores neste padrão fornecem uma expressão lambda (ou um delegado que satisfaça o `Action<LibraryOptions>` parâmetro):

:::code language="csharp" source="snippets/configuration/options-action/Program.cs" highlight="22-26":::

## <a name="options-instance-parameter"></a>Parâmetro de instância de opções

Os consumidores de sua biblioteca podem preferir fornecer uma instância de opções embutidas. Nesse cenário, você expõe um método de extensão que usa uma instância do seu objeto Options, `LibraryOptions` .

:::code language="csharp" source="snippets/configuration/options-object/ServiceCollectionExtensions.cs" highlight="9,11-17":::

No código anterior, o `AddMyLibraryService` :

- Estende uma instância de <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>
- Chamadas <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions%60%601(Microsoft.Extensions.DependencyInjection.IServiceCollection)?displayProperty=nameWithType> com o parâmetro de tipo de `LibraryOptions`
- Encadeia uma chamada para <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.Configure%2A> , que especifica os valores de opção padrão que podem ser substituídos da `userOptions` instância especificada

Os consumidores neste padrão fornecem uma instância da `LibraryOptions` classe, definindo os valores de propriedade desejados embutidos:

:::code language="csharp" source="snippets/configuration/options-object/Program.cs" highlight="22-26":::

## <a name="post-configuration"></a>Pós-configuração

Depois que todos os valores de opção de configuração forem associados ou especificados, a funcionalidade de configuração de postagem estará disponível. Expondo o mesmo [ `Action<TOptions>` parâmetro](#actiontoptions-parameter) detalhado anteriormente, você pode optar por chamar <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigure%2A> . Pós-configuração é executado após todas as `.Configure` chamadas.

:::code language="csharp" source="snippets/configuration/options-postconfig/ServiceCollectionExtensions.cs" highlight="10,12":::

No código anterior, o `AddMyLibraryService` :

- Estende uma instância de <xref:Microsoft.Extensions.DependencyInjection.IServiceCollection>
- Define um <xref:System.Action%601> `T` parâmetro Where is `LibraryOptions``configureOptions`
- Chamadas <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigure%2A> dadas a `configureOptions` ação

Os consumidores neste padrão fornecem uma expressão lambda (ou um delegado que satisfaça o `Action<LibraryOptions>` parâmetro), assim como faria com o [ `Action<TOptions>` Parameter] em um cenário de configuração não post:

:::code language="csharp" source="snippets/configuration/options-postconfig/Program.cs" highlight="22-26":::

## <a name="see-also"></a>Confira também

- [Padrão de opções no .NET](options.md)
- [Injeção de dependência no .NET](dependency-injection.md)
- [Diretrizes de injeção de dependência](dependency-injection-guidelines.md)
