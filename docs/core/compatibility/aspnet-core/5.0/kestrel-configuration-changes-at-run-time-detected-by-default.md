---
title: 'Alteração significativa: Kestrel: alterações de configuração em tempo de execução detectadas por padrão'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado Kestrel: alterações de configuração em tempo de execução detectadas por padrão'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 2e879f020dd108baa14fa8ff67dee7b948209faf
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760311"
---
# <a name="kestrel-configuration-changes-at-run-time-detected-by-default"></a>Kestrel: alterações de configuração em tempo de execução detectadas por padrão

Kestrel agora reage às alterações feitas na `Kestrel` seção da instância do projeto `IConfiguration` (por exemplo, *appsettings.json*) em tempo de execução. Para saber mais sobre como configurar o Kestrel usando o *appsettings.jsno*, consulte o *appsettings.jsno* exemplo na [configuração do ponto de extremidade](/aspnet/core/fundamentals/servers/kestrel#endpoint-configuration).

Kestrel irá ligar, desassociar e reassociar pontos de extremidade conforme necessário para reagir a essas alterações de configuração.

Para obter uma discussão, veja Issue [dotnet/aspnetcore # 22807](https://github.com/dotnet/aspnetcore/issues/22807).

## <a name="version-introduced"></a>Versão introduzida

5,0 Preview 7

## <a name="old-behavior"></a>Comportamento antigo

Antes da ASP.NET Core 5,0 Preview 6, o Kestrel não tinha suporte para alterar a configuração em tempo de execução.

No ASP.NET Core 5,0 Preview 6, você poderia optar pelo comportamento agora padrão de reagir às alterações de configuração em tempo de execução. Optando pela configuração do Kestrel de vinculação necessária manualmente:

```csharp
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Hosting;

public class Program
{
    public static void Main(string[] args) =>
        CreateHostBuilder(args).Build().Run();

    public static IHostBuilder CreateHostBuilder(string[] args) =>
        Host.CreateDefaultBuilder(args)
            .ConfigureWebHostDefaults(webBuilder =>
            {
                webBuilder.UseKestrel((builderContext, kestrelOptions) =>
                {
                    kestrelOptions.Configure(
                        builderContext.Configuration.GetSection("Kestrel"), reloadOnChange: true);
                });

                webBuilder.UseStartup<Startup>();
            });
}
```

## <a name="new-behavior"></a>Novo comportamento

O Kestrel reage às alterações de configuração em tempo de execução por padrão. Para dar suporte a essa alteração, o <xref:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults%2A> chama `KestrelServerOptions.Configure(IConfiguration, bool)` com `reloadOnChange: true` por padrão.

## <a name="reason-for-change"></a>Motivo da alteração

A alteração foi feita para dar suporte à reconfiguração de ponto de extremidade em tempo de execução sem reiniciar completamente o servidor. Ao contrário de uma reinicialização completa do servidor, os pontos de extremidade inalterados não são desassociados mesmo temporariamente.

## <a name="recommended-action"></a>Ação recomendada

* Para a maioria dos cenários em que a seção de configuração padrão do Kestrel não é alterada em tempo de execução, essa alteração não tem nenhum impacto e nenhuma ação é necessária.
* Para cenários nos quais a seção de configuração padrão do Kestrel é alterada em tempo de execução e Kestrel deve reagir a ela, esse agora é o comportamento padrão.
* Para cenários nos quais a seção de configuração padrão do Kestrel é alterada em tempo de execução e Kestrel não deve reagir a ela, você pode recusar da seguinte maneira:

    ```csharp
    using Microsoft.AspNetCore.Hosting;
    using Microsoft.Extensions.Hosting;

    public class Program
    {
        public static void Main(string[] args) =>
            CreateHostBuilder(args).Build().Run();

        public static IHostBuilder CreateHostBuilder(string[] args) =>
            Host.CreateDefaultBuilder(args)
                .ConfigureWebHostDefaults(webBuilder =>
                {
                    webBuilder.UseKestrel((builderContext, kestrelOptions) =>
                    {
                        kestrelOptions.Configure(
                            builderContext.Configuration.GetSection("Kestrel"), reloadOnChange: false);
                    });

                    webBuilder.UseStartup<Startup>();
                });
    }
    ```

**Observações:**

Essa alteração não modifica o comportamento da `KestrelServerOptions.Configure(IConfiguration)` sobrecarga, que ainda usa como padrão o `reloadOnChange: false` comportamento.

Também é importante verificar se a fonte de configuração dá suporte ao recarregamento. Para fontes JSON, o recarregamento é configurado chamando `AddJsonFile(path, reloadOnChange: true)` . O recarregamento já está configurado por padrão para *appsettings.jsem* e *appSettings. { Ambiente}. JSON*.

## <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults%2A?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

`Overload:Microsoft.Extensions.Hosting.GenericHostBuilderExtensions.ConfigureWebHostDefaults`

-->
