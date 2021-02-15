---
title: Diferenças de configuração entre ASP.NET MVC e ASP.NET Core
description: Como os valores de configuração são armazenados e lidos drasticamente entre ASP.NET e ASP.NET Core. Esta seção examina os detalhes e como migrar a configuração do ASP.NET para o ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 0ecd169535d136b5462032431bb22e3b4ddb5b13
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488404"
---
# <a name="configuration-differences-between-aspnet-mvc-and-aspnet-core"></a>Diferenças de configuração entre ASP.NET MVC e ASP.NET Core

Como os valores de configuração são armazenados e lidos drasticamente entre ASP.NET e ASP.NET Core.

## <a name="aspnet-mvc-configuration"></a>Configuração do ASP.NET MVC

Em aplicativos ASP.NET, a configuração usa os arquivos de configuração .NET internos, *web.config* na pasta de aplicativos e *machine.config* no servidor. A maioria dos aplicativos de API Web e MVC do ASP.NET armazenam suas configurações nos elementos do arquivo de configuração `appSettings` `connectionStrings` . Alguns também usam seções de configuração personalizadas que podem ser mapeadas para uma classe de configurações.

A configuração em um aplicativo .NET Framework é acessada usando a `System.Configuration.ConfigurationManager` classe. Infelizmente, essa classe fornece acesso estático aos elementos de configuração. Como resultado, muito poucos aplicativos ASP.NET MVC tendem a abstrair o acesso às suas definições de configuração ou injeta-los quando necessário. Em vez disso, a maioria dos aplicativos .NET Framework tendem a acessar diretamente o sistema de configuração em qualquer lugar em que o aplicativo precisa usar uma configuração.

Acesso típico à configuração MVC do ASP.NET:

```csharp
string connectionString =
    ConfigurationManager.ConnectionStrings["DefaultConnection"]
        .ConnectionString;
```

## <a name="aspnet-core-configuration"></a>Configuração do ASP.NET Core

Em ASP.NET Core aplicativos, a configuração é, em si, configurável. No entanto, a maioria dos aplicativos usa um conjunto de padrões fornecidos como parte dos modelos de projeto padrão e o `ConfigureWebHostDefaults` método usado neles. As configurações padrão usam arquivos JSON formatados, com a capacidade de substituir as configurações na base *appsettings.jsno* arquivo por arquivos específicos do ambiente, como *appsettings.Development.jsem*. Além disso, o sistema de configuração padrão substitui ainda mais todas as configurações baseadas em arquivo por qualquer variável de ambiente que exista para a mesma configuração nomeada. Isso é útil em muitos cenários e é especialmente útil ao implantar em um ambiente de hospedagem, já que elimina a necessidade de se preocupar se a implantação de arquivos de configuração substituirá acidentalmente as definições de configuração de produção importantes. Os valores de configuração também podem ser fornecidos como argumentos de linha de comando.

O acesso a valores de configuração pode ser feito de várias maneiras no .NET Core. Como a injeção de dependência é criada no .NET Core, os valores de configuração geralmente são acessados por meio de uma interface que é injetada em classes que precisam delas. Isso pode envolver a passagem de uma interface como <xref:Microsoft.Extensions.Configuration.IConfiguration> , mas geralmente é melhor passar apenas as configurações exigidas pela classe usando o [padrão de opções](https://docs.microsoft.com/aspnet/core/fundamentals/configuration/options).

A Figura 2-2 mostra como passar `IConfiguration` para uma página Razor e acessar as definições de configuração a partir dela:

```csharp
using Microsoft.Extensions.Configuration;

public class TestModel : PageModel
{
    private readonly IConfiguration _configuration;

    public TestModel(IConfiguration configuration)
    {
        _configuration= configuration;
    }

    public ContentResult OnGet()
    {
        var myKeyValue = _configuration["MyKey"];
        
        // ...
    }
}
```

**Figura 2-2.** Acessando valores de configuração com `IConfiguration` .

Usando o padrão de opções, o acesso às configurações é semelhante, mas é fortemente tipado e mais específico para as configurações necessárias para a classe de consumo, como demonstra a Figura 2-3.

```csharp
public class PositionOptions
{
    public const string Position = nameof(Position);

    public string Title { get; set; }
    public string Name { get; set; }
}

public class Test2Model : PageModel
{
    private readonly PositionOptions _options;

    public Test2Model(IOptions<PositionOptions> options)
    {
        _options = options.Value;
    }

    public ContentResult OnGet()
    {
        return Content($"Title: {_options.Title}\nName: {_options.Name}");
    }
}
```

**Figura 2-3.** Usando o padrão de opções no ASP.NET Core.

Para que o padrão de opções funcione, o tipo de opções deve ser configurado em `ConfigureServices` quando o aplicativo for iniciado:

```csharp
// required in ConfigureServices
services.Configure<PositionOptions>(Configuration.GetSection(PositionOptions.Position));
```

## <a name="migrate-configuration"></a>Migrar configuração

Ao considerar como portar as definições de configuração de um aplicativo de .NET Framework para o .NET Core, a primeira etapa é identificar todas as definições de configuração que estão sendo usadas. A maioria deles estará no arquivo de *web.config* na pasta raiz do aplicativo, mas alguns aplicativos esperam que as configurações sejam encontradas no arquivo de *machine.config* compartilhado também.

Depois que todas as configurações nos arquivos de configuração tiverem sido catalogadas, a próxima etapa deverá ser identificar onde e como as configurações são usadas no próprio aplicativo. Se algumas configurações não estiverem sendo usadas, elas provavelmente podem ser omitidas da migração. Para cada configuração, observe todos os locais que estão sendo usados para que você possa ter certeza de que não perderá nada ao migrar o código.

Se você ainda estiver mantendo o aplicativo ASP.NET, poderá ser útil evitar referências estáticas `ConfigurationManager` e substituí-las pelo acesso por meio de interfaces. Isso facilitará a transição para o sistema de configuração de ASP.NET Core. Em geral, o acesso estático a recursos externos torna o código mais difícil de testar e manter, portanto, esteja na consulta de qualquer lugar em que o aplicativo possa estar seguindo esse padrão.

## <a name="references"></a>Referências

- [Configuração no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/configuration/)
- [Padrão de opções no ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/configuration/options)
- [Migrar configuração para ASP.NET Core](https://docs.microsoft.com/aspnet/core/migration/configuration)
- [Refatorar o acesso de configuração estática](https://ardalis.com/refactoring-static-config-access/)

>[!div class="step-by-step"]
>[Anterior](middleware-modules-handlers.md) 
> [Avançar](routing-differences.md)
