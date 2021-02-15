---
title: 'Alteração significativa: middleware: página de erro do banco de dados marcada como obsoleta'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 5,0 intitulado middleware: página de erro do banco de dados marcada como obsoleta'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: f828b5e20c2a9a709d675e435caa99727aebd5b6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760487"
---
# <a name="middleware-database-error-page-marked-as-obsolete"></a>Middleware: página de erro do banco de dados marcada como obsoleta

O [DatabaseErrorPageMiddleware](/dotnet/api/microsoft.aspnetcore.diagnostics.entityframeworkcore.databaseerrorpagemiddleware?view=aspnetcore-3.0) e seus métodos de extensão associados foram marcados como obsoletos no ASP.NET Core 5,0. Os métodos de middleware e de extensão serão removidos no ASP.NET Core 6,0. Em vez disso, a funcionalidade será fornecida por `DatabaseDeveloperPageExceptionFilter` e seus métodos de extensão.

Para obter uma discussão, consulte o problema do GitHub em [dotnet/aspnetcore # 24987](https://github.com/dotnet/aspnetcore/issues/24987).

## <a name="version-introduced"></a>Versão introduzida

5,0 RC 1

## <a name="old-behavior"></a>Comportamento antigo

`DatabaseErrorPageMiddleware` e seus métodos de extensão associados não estavam obsoletos.

## <a name="new-behavior"></a>Novo comportamento

`DatabaseErrorPageMiddleware` e seus métodos de extensão associados são obsoletos.

## <a name="reason-for-change"></a>Motivo da alteração

`DatabaseErrorPageMiddleware` foi migrado para uma API extensível para a [página de exceção do desenvolvedor](/aspnet/core/fundamentals/error-handling#developer-exception-page). Para obter mais informações sobre a API extensível, consulte o problema do GitHub [dotnet/aspnetcore # 8536](https://github.com/dotnet/aspnetcore/issues/8536).

## <a name="recommended-action"></a>Ação recomendada

Conclua as seguintes etapas:

1. Pare `DatabaseErrorPageMiddleware` de usar no seu projeto. Por exemplo, remova a `UseDatabaseErrorPage` chamada de método de `Startup.Configure` :

    ```csharp
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDatabaseErrorPage();
        }
    }
    ```

1. Adicione a página de exceção do desenvolvedor ao seu projeto. Por exemplo, chame o <xref:Microsoft.AspNetCore.Builder.DeveloperExceptionPageExtensions.UseDeveloperExceptionPage%2A> método em `Startup.Configure` :

    ```csharp
    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        if (env.IsDevelopment())
        {
            app.UseDeveloperExceptionPage();
        }
    }
    ```

1. Adicione o pacote NuGet [Microsoft. AspNetCore. Diagnostics. EntityFrameworkCore](https://www.nuget.org/packages/Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore) ao arquivo de projeto.

1. Adicione o filtro de exceção da página do desenvolvedor de banco de dados à coleção de serviços. Por exemplo, chame o `AddDatabaseDeveloperPageExceptionFilter` método em `Startup.ConfigureServices` :

    ```csharp
    public void ConfigureServices(IServiceCollection services)
    {
        services.AddDatabaseDeveloperPageExceptionFilter();
    }
    ```

## <a name="affected-apis"></a>APIs afetadas

- [Microsoft. AspNetCore. Builder. DatabaseErrorPageExtensions. UseDatabaseErrorPage](/dotnet/api/microsoft.aspnetcore.builder.databaseerrorpageextensions.usedatabaseerrorpage?view=aspnetcore-3.0)
- [Microsoft. AspNetCore. Diagnostics. EntityFrameworkCore. DatabaseErrorPageMiddleware](/dotnet/api/microsoft.aspnetcore.diagnostics.entityframeworkcore.databaseerrorpagemiddleware?view=aspnetcore-3.0)

<!--

### Category

ASP.NET Core

### Affected APIs

- `Overload:Microsoft.AspNetCore.Builder.DatabaseErrorPageExtensions.UseDatabaseErrorPage`
- `T:Microsoft.AspNetCore.Diagnostics.EntityFrameworkCore.DatabaseErrorPageMiddleware`

-->
