---
title: Comparar a autenticação e a autorização entre o ASP.NET MVC e o ASP.NET Core
description: Um resumo das diferenças de autenticação e autorização entre o ASP.NET MVC e o ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: fd8c11290a296612af822dd6c1a7816f915f09f7
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488415"
---
# <a name="compare-authentication-and-authorization-between-aspnet-mvc-and-aspnet-core"></a>Comparar a autenticação e a autorização entre o ASP.NET MVC e o ASP.NET Core

No ASP.NET MVC 5, a autenticação é configurada em *Startup.auth.cs* na pasta *App_Start* . No ASP.NET Core MVC, essa configuração ocorre no `Startup.cs` . A autenticação e a autorização são executadas usando o middleware adicionado ao pipeline de solicitação no `ConfigureServices` :

```csharp
// inside Startup.ConfigureServices

app.UseRouting();

app.UseAuthentication();
app.UseAuthorization();

app.UseEndpoints(endpoints =>
{
    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}");
    endpoints.MapRazorPages();
});
```

É importante adicionar o middleware de autenticação na ordem apropriada no pipeline de middleware. Somente as solicitações que o fazem para o middleware serão afetadas por ele. Por exemplo, se uma chamada para `UseStaticFiles()` foi colocada acima do código mostrado aqui, ela não seria protegida pela autenticação e autorização.

No ASP.NET MVC e na API Web, os aplicativos geralmente se referem ao usuário atual usando a `ClaimsPrincipal.Current` propriedade. Essa propriedade não é definida em ASP.NET Core, e qualquer comportamento em seu aplicativo que depende dele precisará ser [migrado de ClaimsPrincipal. Current](https://docs.microsoft.com/aspnet/core/migration/claimsprincipal-current) usando a `User` propriedade `ControllerBase` ou obtendo acesso ao atual `HttpContext` e referenciando sua `User` propriedade. Se nenhuma dessas soluções for uma opção, os serviços poderão solicitar o usuário como um argumento; nesse caso, ele deve ser fornecido de outro lugar no aplicativo ou `IHttpContextAccessor` pode ser solicitado e usado para obter o `HttpContext` .

## <a name="authorization"></a>Autorização

A autorização define o que um determinado usuário pode fazer dentro do aplicativo. Ele é separado da autenticação, que se preocupa apenas com a identificação de quem é o usuário. O ASP.NET Core fornece uma função declarativa simples e um modelo avançado baseado em políticas para autorização. Especificar que um recurso requer autorização é geralmente tão simples quanto adicionar o `[Authorize]` atributo à ação ou ao controlador. Se você estiver migrando para Razor Pages de exibições do MVC, deverá [especificar convenções de autorização ao configurar Razor Pages na inicialização](https://docs.microsoft.com/aspnet/core/security/authorization/razor-pages-authorization).

A autorização no ASP.NET Core pode ser tão simples quanto proibir usuários anônimos e, ao mesmo tempo, permitir usuários autenticados. Ou pode escalar verticalmente para oferecer suporte a abordagens baseadas em função, baseadas em declarações ou de autorização baseada em políticas. Para obter mais informações sobre essas abordagens, consulte a documentação sobre [autorização no ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/authorization/introduction). Você provavelmente descobrirá que um deles está fortemente alinhado com sua abordagem de autorização atual.

## <a name="references"></a>Referências

- [Segurança, autenticação e autorização com o ASP.NET MVC](https://docs.microsoft.com/aspnet/mvc/overview/security/)
- [Migrar autenticação e identidade para ASP.NET Core](https://docs.microsoft.com/aspnet/mvc/overview/security/)
- [Migrar de ClaimsPrincipal. Current](https://docs.microsoft.com/aspnet/core/migration/claimsprincipal-current)
- [Introdução à autorização no ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/authorization/introduction)

>[!div class="step-by-step"]
>[Anterior](webapi-differences.md) 
> [Avançar](identity-differences.md)
