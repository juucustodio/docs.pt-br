---
title: Padrão de opções no .NET
author: IEvangelist
description: Saiba como usar o padrão de opções para representar grupos de configurações relacionadas em aplicativos .NET.
ms.author: dapine
ms.date: 01/21/2021
ms.openlocfilehash: 413f731337a6012bb1e29f1f38c2df6da7525867
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99216025"
---
# <a name="options-pattern-in-net"></a>Padrão de opções no .NET

O padrão de opções usa classes para fornecer acesso fortemente tipado a grupos de configurações relacionadas. Quando as [definições de configuração](configuration.md) são isoladas por cenário em classes separadas, o aplicativo segue dois princípios importantes de engenharia de software:

- O [princípio de diferenciação de interface (ISP) ou encapsulamento](../../architecture/modern-web-apps-azure/architectural-principles.md#encapsulation): cenários (classes) que dependem de definições de configuração dependem apenas dos parâmetros de configuração que eles usam.
- [Separação de Interesses](../../architecture/modern-web-apps-azure/architectural-principles.md#separation-of-concerns): as configurações para diferentes partes do aplicativo não são dependentes nem acopladas entre si.

As opções também fornecem um mecanismo para validar os dados da configuração. Para obter mais configurações, consulte a seção [Validação de opções](#options-validation).

## <a name="bind-hierarchical-configuration"></a>Associar configuração hierárquica

A maneira preferida de ler valores de configuração relacionados é usar o padrão de opções. O padrão de opções é possível por meio da <xref:Microsoft.Extensions.Options.IOptions%601> interface, onde o parâmetro de tipo genérico `TOptions` é restrito `class` . Posteriormente, o `IOptions<TOptions>` pode ser fornecido por meio de injeção de dependência. Para obter mais informações, consulte [injeção de dependência no .net](dependency-injection.md).

Por exemplo, para ler os seguintes valores de configuração:

:::code language="json" source="snippets/configuration/console-json/appsettings.json" range="3-6":::

Crie a seguinte `TransientFaultHandlingOptions` classe:

:::code language="csharp" source="snippets/configuration/console-json/TransientFaultHandlingOptions.cs" range="5-9":::

<span id="options-class"></span> Ao usar o padrão de opções, uma classe de opções:

- Deve ser não-abstrato com um construtor público sem parâmetros
- Conter Propriedades de leitura/gravação públicas para associar (os campos são ***não** associados)

O seguinte código:

_ Chama [ConfigurationBinder. bind](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Bind%2A) para associar a `TransientFaultHandlingOptions` classe à `"TransientFaultHandlingOptions"` seção.
* Exibe os dados de configuração.

:::code language="csharp" source="snippets/configuration/console-json/Program.cs" range="31-38":::

No código anterior, as alterações no arquivo de configuração JSON depois que o aplicativo é iniciado são lidas.

[`ConfigurationBinder.Get<T>`](xref:Microsoft.Extensions.Configuration.ConfigurationBinder.Get%2A) associa e retorna o tipo especificado. `ConfigurationBinder.Get<T>` pode ser mais conveniente do que usar o `ConfigurationBinder.Bind` . O código a seguir mostra como usar `ConfigurationBinder.Get<T>` com a `TransientFaultHandlingOptions` classe:

```csharp
IConfigurationRoot configurationRoot = configuration.Build();

var options =
    configurationRoot.GetSection(nameof(TransientFaultHandlingOptions))
                     .Get<TransientFaultHandlingOptions>();

Console.WriteLine($"TransientFaultHandlingOptions.Enabled={options.Enabled}");
Console.WriteLine($"TransientFaultHandlingOptions.AutoRetryDelay={options.AutoRetryDelay}");
```

No código anterior, as alterações no arquivo de configuração JSON depois que o aplicativo é iniciado são lidas.

> [!IMPORTANT]
> A <xref:Microsoft.Extensions.Configuration.ConfigurationBinder> classe expõe várias APIs, como `.Bind(object instance)` e `.Get<T>()` que são ***não** _ restritas `class` . Ao usar qualquer uma das [interfaces de opções](#options-interfaces), você deve seguir as [restrições de classe de opções](#options-class)mencionadas anteriormente.

Uma abordagem alternativa ao usar o padrão de opções é associar a `"TransientFaultHandlingOptions"` seção e adicioná-la ao [contêiner de serviço de injeção de dependência](dependency-injection.md). No código a seguir, `TransientFaultHandlingOptions` é adicionado ao contêiner de serviço com <xref:Microsoft.Extensions.DependencyInjection.OptionsConfigurationServiceCollectionExtensions.Configure%2A> e associado à configuração:

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        key: nameof(TransientFaultHandlingOptions)));
```

> [!TIP]
> O `key` parâmetro é o nome da seção de configuração a ser pesquisada. Ele _not * precisa corresponder ao nome do tipo que o representa. Por exemplo, você poderia ter uma seção chamada `"FaultHandling"` e ela poderia ser representada pela `TransientFaultHandlingOptions` classe. Nessa instância, você passaria `"FaultHandling"` para a <xref:Microsoft.Extensions.Configuration.IConfiguration.GetSection%2A> função em vez disso. O `nameof` operador é usado como uma conveniência quando a seção nomeada corresponde ao tipo ao qual ela corresponde.

Usando o código anterior, o código a seguir lê as opções de posição:

:::code language="csharp" source="snippets/configuration/console-json/ExampleService.cs":::

No código anterior, as alterações no arquivo de configuração JSON após o aplicativo ter sido iniciado são ***não** lidas. Para ler as alterações depois que o aplicativo for iniciado, use [IOptionsSnapshot](#use-ioptionssnapshot-to-read-updated-data).

## <a name="options-interfaces"></a>Interfaces de opções

<xref:Microsoft.Extensions.Options.IOptions%601>:

- Não _*_oferece suporte a_*_ :
  - Leitura de dados de configuração após o aplicativo ser iniciado.
  - [Opções nomeadas](#named-options-support-using-iconfigurenamedoptions)
- É registrado como um [singleton](dependency-injection.md#singleton) e pode ser injetado em qualquer [tempo de vida do serviço](dependency-injection.md#service-lifetimes).

<xref:Microsoft.Extensions.Options.IOptionsSnapshot%601>:

- É útil em cenários em que as opções devem ser recomputadas em cada resolução de injeção, em [tempos de vida transitórios ou de escopo](dependency-injection.md#service-lifetimes). Para obter mais informações, consulte [usar IOptionsSnapshot para ler dados atualizados](#use-ioptionssnapshot-to-read-updated-data).
- Está registrado como [escopo](dependency-injection.md#scoped) e, portanto, não pode ser injetado em um serviço singleton.
- Dá suporte a [Opções nomeadas](#named-options-support-using-iconfigurenamedoptions)

<xref:Microsoft.Extensions.Options.IOptionsMonitor%601>:

- É usado para recuperar opções e gerenciar notificações de opções para `TOptions` instâncias.
- É registrado como um [singleton](dependency-injection.md#singleton) e pode ser injetado em qualquer [tempo de vida do serviço](dependency-injection.md#service-lifetimes).
- Oferece suporte a:
  - Notificações de alteração
  - [Opções nomeadas](#named-options-support-using-iconfigurenamedoptions)
  - [Configuração recarregável](#use-ioptionssnapshot-to-read-updated-data)
  - Invalidação seletiva de opções (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601>)
  
O <xref:Microsoft.Extensions.Options.IOptionsFactory%601> é responsável por criar novas instâncias de opções. Ele tem um único método <xref:Microsoft.Extensions.Options.IOptionsFactory%601.Create%2A>. A implementação padrão usa todos os <xref:Microsoft.Extensions.Options.IConfigureOptions%601> e <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601> registrados e executa todas as configurações primeiro, seguidas da pós-configuração. Ela faz distinção entre <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> e <xref:Microsoft.Extensions.Options.IConfigureOptions%601> e chama apenas a interface apropriada.

O <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> é usado pelo <xref:Microsoft.Extensions.Options.IOptionsMonitor%601> para armazenar em cache as instâncias do `TOptions`. O <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601> invalida as instâncias de opções no monitor, de modo que o valor seja recalculado (<xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryRemove%2A>). Os valores podem ser manualmente inseridos com <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.TryAdd%2A>. O método <xref:Microsoft.Extensions.Options.IOptionsMonitorCache%601.Clear%2A> é usado quando todas as instâncias nomeadas devem ser recriadas sob demanda.

## <a name="use-ioptionssnapshot-to-read-updated-data"></a>Usar IOptionsSnapshot para ler dados atualizados

Quando você usa <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601> , as opções são computadas uma vez por solicitação quando acessadas e armazenadas em cache durante o tempo de vida da solicitação. As alterações na configuração são lidas depois que o aplicativo é iniciado ao usar provedores de configuração que dão suporte à leitura de valores de configuração atualizados.

A diferença entre `IOptionsMonitor` e `IOptionsSnapshot` é que:

- `IOptionsMonitor` é um [serviço singleton](dependency-injection.md#singleton) que recupera os valores de opção atuais a qualquer momento, o que é especialmente útil em dependências singleton.
- `IOptionsSnapshot` é um [serviço com escopo](dependency-injection.md#scoped) e fornece um instantâneo das opções no momento em que o `IOptionsSnapshot<T>` objeto é construído. Os instantâneos de opções são projetados para uso com dependências transitórias e com escopo definido.

O código a seguir usa <xref:Microsoft.Extensions.Options.IOptionsSnapshot%601> .

:::code language="csharp" source="snippets/configuration/console-json/ScopedService.cs":::

O código a seguir registra uma instância de configuração que se `TransientFaultHandlingOptions` associa a:

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        nameof(TransientFaultHandlingOptions)));
```

No código anterior, as alterações no arquivo de configuração JSON depois que o aplicativo é iniciado são lidas.

## <a name="ioptionsmonitor"></a>IOptionsMonitor

O código a seguir registra uma instância de configuração que é `TransientFaultHandlingOptions` associada a.

```csharp
services.Configure<TransientFaultHandlingOptions>(
    configurationRoot.GetSection(
        nameof(TransientFaultHandlingOptions)));
```

O exemplo a seguir usa <xref:Microsoft.Extensions.Options.IOptionsMonitor%601>:

:::code language="csharp" source="snippets/configuration/console-json/MonitorService.cs":::

No código anterior, as alterações no arquivo de configuração JSON depois que o aplicativo é iniciado são lidas.

## <a name="named-options-support-using-iconfigurenamedoptions"></a>Suporte a opções nomeadas usando IConfigureNamedOptions

Opções nomeadas:

- São úteis quando várias seções de configuração se associam às mesmas propriedades.
- Diferenciam maiúsculas de minúsculas.

Considere o seguinte _appsettings.jsno arquivo *:

```json
{
  "Features": {
    "Personalize": {
      "Enabled": true,
      "ApiKey": "aGEgaGEgeW91IHRob3VnaHQgdGhhdCB3YXMgcmVhbGx5IHNvbWV0aGluZw=="
    },
    "WeatherStation": {
      "Enabled": true,
      "ApiKey": "QXJlIHlvdSBhdHRlbXB0aW5nIHRvIGhhY2sgdXM/"
    }
  }
}
```

Em vez de criar duas classes para associar `Features:Personalize` e `Features:WeatherStation` , a seguinte classe é usada para cada seção:

```csharp
public class Features
{
    public const string Personalize = nameof(Personalize);
    public const string WeatherStation = nameof(WeatherStation);

    public bool Enabled { get; set; }
    public string ApiKey { get; set; }
}
```

O código a seguir configura as opções nomeadas:

```csharp
ConfigureServices(services =>
{
    services.Configure<Features>(
        Features.Personalize,
        Configuration.GetSection("Features:Personalize"));

    services.Configure<Features>(
        Features.WeatherStation,
        Configuration.GetSection("Features:WeatherStation"));
});
```

O código a seguir exibe as opções nomeadas:

```csharp
public class Service
{
    private readonly Features _personalizeFeature;
    private readonly Features _weatherStationFeature;

    public Service(IOptionsSnapshot<Features> namedOptionsAccessor)
    {
        _personalizeFeature = namedOptionsAccessor.Get(Features.Personalize);
        _weatherStationFeature = namedOptionsAccessor.Get(Features.WeatherStation);
    }
}
```

Todas as opções são instâncias nomeadas. <xref:Microsoft.Extensions.Options.IConfigureOptions%601> as instâncias são tratadas como destino da `Options.DefaultName` instância, que é `string.Empty` . <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> também implementa <xref:Microsoft.Extensions.Options.IConfigureOptions%601>. A implementação padrão de <xref:Microsoft.Extensions.Options.IOptionsFactory%601> tem lógica para usar cada um de forma adequada. A `null` opção nomeada é usada para direcionar todas as instâncias nomeadas em vez de uma instância nomeada específica. <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.ConfigureAll%2A> e <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> Use essa convenção.

## <a name="optionsbuilder-api"></a>API OptionsBuilder

<xref:Microsoft.Extensions.Options.OptionsBuilder%601> é usada para configurar instâncias `TOptions`. `OptionsBuilder` simplifica a criação de opções nomeadas, pois é apenas um único parâmetro para a chamada `AddOptions<TOptions>(string optionsName)` inicial, em vez de aparecer em todas as chamadas subsequentes. A validação de opções e as sobrecargas `ConfigureOptions` que aceitam dependências de serviço só estão disponíveis por meio de `OptionsBuilder`.

`OptionsBuilder` é usado na seção [validação de opções](#options-validation) .

## <a name="use-di-services-to-configure-options"></a>Usar os serviços de injeção de dependência para configurar as opções

Os serviços podem ser acessados da injeção de dependência ao configurar opções de duas maneiras:

- Passe um delegado de configuração para [Configurar](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) no [OptionsBuilder \<TOptions> ](xref:Microsoft.Extensions.Options.OptionsBuilder%601). `OptionsBuilder<TOptions>` fornece sobrecargas de [configuração](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) que permitem o uso de até cinco serviços para configurar opções:

  ```csharp
  services.AddOptions<MyOptions>("optionalName")
      .Configure<ExampleService, ScopedService, MonitorService>(
          (options, es, ss, ms) =>
              options.Property = DoSomethingWith(es, ss, ms));
  ```

- Crie um tipo que implemente <xref:Microsoft.Extensions.Options.IConfigureOptions%601> ou <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601> Registre o tipo como um serviço.

É recomendável transmitir um delegado de configuração para [Configurar](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A), já que a criação de um serviço é algo mais complexo. Criar um tipo é equivalente ao que a estrutura faz ao chamar [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A). Chamar [Configure](xref:Microsoft.Extensions.Options.OptionsBuilder%601.Configure%2A) registra um genérico transitório <xref:Microsoft.Extensions.Options.IConfigureNamedOptions%601>, que tem um construtor que aceita os tipos de serviço genérico especificados.

## <a name="options-validation"></a>Validação de opções

A validação de opções permite que os valores de opção sejam validados.

Considere o seguinte *appsettings.jsno* arquivo:

```json
{
  "Settings": {
    "SiteTitle": "Amazing docs from Awesome people!",
    "Scale": 10,
    "VerbosityLevel": 32
  }
}
```

A seguinte classe é associada à `"Settings"` seção de configuração e aplica algumas `DataAnnotations` regras:

:::code language="csharp" source="snippets/configuration/console-json/SettingsOptions.cs":::

O seguinte código:

- Chama <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.AddOptions%2A> para obter um [OptionsBuilder \<TOptions> ](xref:Microsoft.Extensions.Options.OptionsBuilder%601) que se associa à `SettingsOptions` classe.
- Chamadas <xref:Microsoft.Extensions.DependencyInjection.OptionsBuilderDataAnnotationsExtensions.ValidateDataAnnotations%2A> para habilitar a validação usando `DataAnnotations` .

```csharp
services.AddOptions<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.Settings))
    .ValidateDataAnnotations();
```

O `ValidateDataAnnotations` método de extensão é definido no pacote NuGet [Microsoft. Extensions. Options. Annotations](https://www.nuget.org/packages/Microsoft.Extensions.Options.DataAnnotations) .

O código a seguir exibe os valores de configuração ou os erros de validação:

:::code language="csharp" source="snippets/configuration/console-json/ValidationService.cs":::

O código a seguir aplica uma regra de validação mais complexa usando um delegado:

```csharp
services.AddOptions<SettingsOptions>()
    .Bind(Configuration.GetSection(SettingsOptions.Settings))
    .ValidateDataAnnotations()
    .Validate(config =>
    {
        if (config.Scale != 0)
        {
            return config.VerbosityLevel > config.Scale;
        }

        return true;
    }, "VerbosityLevel must be > than Scale.");
```

### <a name="ivalidateoptions-for-complex-validation"></a>IValidateOptions para validação complexa

A seguinte classe implementa <xref:Microsoft.Extensions.Options.IValidateOptions%601> :

:::code language="csharp" source="snippets/configuration/console-json/ValidateSettingsOptions.cs":::

`IValidateOptions` permite mover o código de validação para uma classe.

Usando o código anterior, a validação é habilitada no `ConfigureServices` com o seguinte código:

```csharp
services.Configure<SettingsOptions>(
    Configuration.GetSection(
        SettingsOptions.Settings));
services.TryAddEnumerable(
    ServiceDescriptor.Singleton
        <IValidateOptions<SettingsOptions>, ValidateSettingsOptions>());
```

## <a name="options-post-configuration"></a>Pós-configuração de opções

Defina a pós-configuração com <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601>. Pós-configuração é executado depois <xref:Microsoft.Extensions.Options.IConfigureOptions%601> que toda a configuração ocorre e pode ser útil em cenários quando você precisa substituir a configuração:

```csharp
services.PostConfigure<CustomOptions>(customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

O <xref:Microsoft.Extensions.Options.IPostConfigureOptions%601.PostConfigure%2A> está disponível para pós-configurar opções nomeadas:

```csharp
services.PostConfigure<CustomOptions>("named_options_1", customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

Use <xref:Microsoft.Extensions.DependencyInjection.OptionsServiceCollectionExtensions.PostConfigureAll%2A> para pós-configurar todas as instâncias de configuração:

```csharp
services.PostConfigureAll<CustomOptions>(customOptions =>
{
    customOptions.Option1 = "post_configured_option1_value";
});
```

## <a name="see-also"></a>Confira também

- [Configuração no .NET](configuration.md)
- [Diretrizes de padrão de opções para autores de biblioteca do .NET](options-library-authors.md)
