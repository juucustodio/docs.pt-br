---
title: 'Alteração significativa: Razor: APIs RazorEngine marcadas como obsoletas'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 6,0 intitulado Razor: APIs RazorEngine marcadas como obsoletas'
author: scottaddie
ms.author: scaddie
ms.date: 02/09/2021
ms.openlocfilehash: 173ff0ee5c062f050c967c6edc7bed333d1a2031
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488277"
---
# <a name="razor-razorengine-apis-marked-obsolete"></a>Razor: APIs RazorEngine marcadas como obsoletas

Os tipos relacionados ao <xref:Microsoft.AspNetCore.Razor.Language.RazorEngine> tipo no mais baixo foram marcados como obsoletos.

## <a name="version-introduced"></a>Versão introduzida

6,0 visualização 1

## <a name="old-behavior"></a>Comportamento antigo

As `RazorEngine` APIs não são obsoletas.

## <a name="new-behavior"></a>Novo comportamento

As `RazorEngine` APIs estão obsoletas.

## <a name="reason-for-change"></a>Motivo da alteração

O `RazorEngine` tipo foi preterido em favor do <xref:Microsoft.AspNetCore.Razor.Language.RazorProjectEngine> tipo.

## <a name="recommended-action"></a>Ação recomendada

Migre o código-fonte do `RazorEngine` tipo para o `RazorProjectEngine` tipo.

## <a name="affected-apis"></a>APIs afetadas

- [Microsoft. AspNetCore. Mvc. Razor. Extensions. InjectDirective. Register](/dotnet/api/microsoft.aspnetcore.mvc.razor.extensions.injectdirective.register?view=aspnetcore-3.1&preserve-view=true)
- [Microsoft. AspNetCore. Mvc. Razor. Extensions. ModelDirective. Register](/dotnet/api/microsoft.aspnetcore.mvc.razor.extensions.namespacedirective.register?view=aspnetcore-2.2&preserve-view=true)
- [Microsoft. AspNetCore. Mvc. Razor. Extensions. PageDirective. Register](/dotnet/api/microsoft.aspnetcore.mvc.razor.extensions.namespacedirective.register?view=aspnetcore-2.2&preserve-view=true)
- [Microsoft. AspNetCore. Razor. Language. Extensions. FunctionsDirective. Register](/dotnet/api/microsoft.aspnetcore.razor.language.extensions.functionsdirective.register?view=aspnetcore-3.0&preserve-view=true)
- [Microsoft. AspNetCore. Razor. Language. Extensions. InheritsDirective. Register](/dotnet/api/microsoft.aspnetcore.razor.language.extensions.inheritsdirective.register?view=aspnetcore-3.0&preserve-view=true)
- [Microsoft. AspNetCore. Razor. Language. Extensions. SectionDirective. Register](/dotnet/api/microsoft.aspnetcore.razor.language.extensions.sectiondirective.register?view=aspnetcore-3.0&preserve-view=true)
- [Microsoft. AspNetCore. Razor. Language. IRazorEngineBuilder](/dotnet/api/microsoft.aspnetcore.razor.language.irazorenginebuilder?view=aspnetcore-3.0&preserve-view=true)

<!--

## Category

ASP.NET Core

## Affected APIs

- `Overload:Microsoft.AspNetCore.Mvc.Razor.Extensions.InjectDirective.Register`
- `Overload:Microsoft.AspNetCore.Mvc.Razor.Extensions.ModelDirective.Register`
- `Overload:Microsoft.AspNetCore.Mvc.Razor.Extensions.PageDirective.Register`
- `Overload:Microsoft.AspNetCore.Razor.Language.Extensions.FunctionsDirective.Register`
- `Overload:Microsoft.AspNetCore.Razor.Language.Extensions.InheritsDirective.Register`
- `Overload:Microsoft.AspNetCore.Razor.Language.Extensions.SectionDirective.Register`
- `T:Microsoft.AspNetCore.Razor.Language.IRazorEngineBuilder`

-->
