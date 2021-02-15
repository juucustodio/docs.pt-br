---
title: 'Alteração significativa: Localização: classe ResourceManagerWithCultureStringLocalizer e membro de interface WithCulture removido'
description: 'Saiba mais sobre a alteração significativa na ASP.NET Core 5,0 localização de título: classe ResourceManagerWithCultureStringLocalizer e membro da interface WithCulture removidos'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: ac7723cd9b961b34b3f87a55119d421668c87417
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96437854"
---
# <a name="localization-resourcemanagerwithculturestringlocalizer-class-and-withculture-interface-member-removed"></a>Localização: classe ResourceManagerWithCultureStringLocalizer e membro da interface WithCulture removidos

A classe [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) e o método [WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) foram removidos no .NET 5,0 Preview 1.

Para contexto, consulte [ASPNET/comunicados # 346](https://github.com/aspnet/Announcements/issues/346) e [dotnet/aspnetcore # 3324](https://github.com/dotnet/aspnetcore/issues/3324). Para discussão sobre essa alteração, consulte [dotnet/aspnetcore # 7756](https://github.com/dotnet/aspnetcore/issues/7756).

## <a name="version-introduced"></a>Versão introduzida

5,0 visualização 1

## <a name="old-behavior"></a>Comportamento antigo

A `ResourceManagerWithCultureStringLocalizer` classe e o `ResourceManagerStringLocalizer.WithCulture` método são [obsoletos no .NET Core 3,0 Preview 3 e posterior](../../3.0.md#localization-resourcemanagerwithculturestringlocalizer-and-withculture-marked-obsolete).

## <a name="new-behavior"></a>Novo comportamento

A `ResourceManagerWithCultureStringLocalizer` classe e o `ResourceManagerStringLocalizer.WithCulture` método foram removidos no .NET 5,0 Preview 1. Para obter um inventário das alterações feitas, consulte a solicitação pull em [dotnet/Extensions # 2562](https://github.com/dotnet/extensions/pull/2562/files).

## <a name="reason-for-change"></a>Motivo da alteração

A classe [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1) e o método [ResourceManagerStringLocalizer. WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1) geralmente eram fontes de confusão para os usuários da localização. A confusão era especialmente alta ao criar uma <xref:Microsoft.Extensions.Localization.IStringLocalizer> implementação personalizada. Essa classe e o método dão aos consumidores a impressão de que uma `IStringLocalizer` instância deve ser "por idioma, por recurso". Na realidade, a instância só deve ser "por recurso". Em tempo de execução, a <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=nameWithType> propriedade determina o idioma a ser usado.

## <a name="recommended-action"></a>Ação recomendada

Pare de usar a `ResourceManagerWithCultureStringLocalizer` classe e o `ResourceManagerStringLocalizer.WithCulture` método.

## <a name="affected-apis"></a>APIs afetadas

- [ResourceManagerWithCultureStringLocalizer](/dotnet/api/microsoft.extensions.localization.resourcemanagerwithculturestringlocalizer?view=dotnet-plat-ext-3.1)
- [ResourceManagerStringLocalizer.WithCulture](/dotnet/api/microsoft.extensions.localization.resourcemanagerstringlocalizer.withculture?view=dotnet-plat-ext-3.1)

<!--

### Category

ASP.NET Core

### Affected APIs

- `T:Microsoft.Extensions.Localization.ResourceManagerWithCultureStringLocalizer`
- `Overload:Microsoft.Extensions.Localization.ResourceManagerStringLocalizer.WithCulture`

-->
