---
title: 'Alteração significativa: mais incrivelmente: RenderTreeFrame campos públicos ReadOnly se tornaram Propriedades'
description: 'Saiba mais sobre as alterações significativas no ASP.NET Core 5,0 intitulados mais recentes: os campos públicos RenderTreeFrame ReadOnly se tornaram Propriedades'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: e9da9c538cc0a8ed4f138ef64ece0c7d144f28d3
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760315"
---
# <a name="blazor-rendertreeframe-readonly-public-fields-have-become-properties"></a>Mais do que: RenderTreeFrame campos públicos ReadOnly se tornaram Propriedades

No ASP.NET Core 3,0 e 3,1, a <xref:Microsoft.AspNetCore.Components.RenderTree.RenderTreeFrame> estrutura expôs vários `readonly public` campos, incluindo <xref:Microsoft.AspNetCore.Components.RenderTree.RenderTreeFrame.FrameType> , <xref:Microsoft.AspNetCore.Components.RenderTree.RenderTreeFrame.Sequence> e outros. No ASP.NET Core 5,0 RC1 e versões posteriores, todos os `readonly public` campos foram alterados para `readonly public` Propriedades.

Essa alteração não afetará muitos desenvolvedores porque:

* Qualquer aplicativo ou biblioteca que simplesmente usa `.razor` arquivos (ou até mesmo <xref:Microsoft.AspNetCore.Components.Rendering.RenderTreeBuilder> chamadas manuais) para definir seus componentes não referenciaria esse tipo diretamente.
* O `RenderTreeFrame` próprio tipo é considerado um detalhe de implementação, não destinado ao uso fora da estrutura. ASP.NET Core 3,0 e posterior inclui um analisador que emite avisos do compilador se o tipo estiver sendo usado diretamente.
* Mesmo se você fizer referência `RenderTreeFrame` diretamente, essa alteração será de quebra de binário, mas não de quebra de fonte. Ou seja, o código-fonte existente será compilado e se comportará corretamente. Você encontrará um problema apenas se estiver compilando em uma estrutura do .NET Core 3. x e, em seguida, executando esses binários no .NET 5,0 RC1 e no Framework posterior.

Para obter uma discussão, consulte o problema do GitHub [dotnet/aspnetcore # 25727](https://github.com/dotnet/aspnetcore/issues/25727).

## <a name="version-introduced"></a>Versão introduzida

RC1 5,0

## <a name="old-behavior"></a>Comportamento antigo

Os membros públicos em `RenderTreeFrame` são definidos como campos. Por exemplo, `renderTreeFrame.Sequence` e `renderTreeFrame.ElementName`.

## <a name="new-behavior"></a>Novo comportamento

Os membros públicos em `RenderTreeFrame` são definidos como propriedades com os mesmos nomes de antes. Por exemplo, `renderTreeFrame.Sequence` e `renderTreeFrame.ElementName`.

Se o código pré-compilado mais antigo não tiver sido recompilado desde essa alteração, ele poderá lançar uma exceção semelhante a *MissingFieldException: campo não encontrado: ' Microsoft. AspNetCore. Components. RenderTree. RenderTreeFrame. FrameType '*.

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração foi necessária para implementar melhorias de desempenho de alto impacto na renderização de componente mais incrivelmente no ASP.NET Core 5,0. Os mesmos níveis de segurança e encapsulamento são mantidos.

## <a name="recommended-action"></a>Ação recomendada

A maioria dos desenvolvedores não é afetada por essa mudança. É mais provável que a alteração afete os autores de biblioteca e pacote, mas apenas em casos raros. Especificamente, se você estiver desenvolvendo:

* Um aplicativo e usar ASP.NET Core 3. x ou atualizar para o 5,0 RC1 ou posterior, você não precisa alterar seu próprio código. No entanto, se você depender de uma biblioteca atualizada para considerar essa alteração, precisará atualizar para uma versão mais recente dessa biblioteca.
* Uma biblioteca e deseja dar suporte apenas ao ASP.NET Core 5,0 RC1 ou posterior, nenhuma ação é necessária. Apenas verifique se o arquivo de projeto declara um `<TargetFramework>` valor de `net5.0` ou uma versão posterior.
* Uma biblioteca e deseja dar suporte às ASP.NET Core 3. x *e* 5,0, determinar se o código lê os `RenderTreeFrame` Membros. Por exemplo, avaliar `someRenderTreeFrame.FrameType` .
  * A maioria das bibliotecas não lê `RenderTreeFrame` Membros, incluindo bibliotecas que contêm `.razor` componentes. Nesse caso, nenhuma ação é necessária.
  * No entanto, se sua biblioteca faz isso, você precisará de vários destinos para dar suporte a `netstandard2.1` e ao `net5.0` . Aplique as seguintes alterações no arquivo de projeto:
    * Substitua o `<TargetFramework>` elemento existente por `<TargetFrameworks>netstandard2.0;net5.0</TargetFrameworks>` .
    * Use uma `Microsoft.AspNetCore.Components` referência de pacote condicional para considerar as duas versões às quais você deseja dar suporte. Por exemplo:

        ```xml
        <PackageReference Include="Microsoft.AspNetCore.Components" Version="3.0.0" Condition="'$(TargetFramework)' == 'netstandard2.0'" />
        <PackageReference Include="Microsoft.AspNetCore.Components" Version="5.0.0-rc.1.*" Condition="'$(TargetFramework)' != 'netstandard2.0'" />
        ```

Para obter mais esclarecimentos, consulte esta [diferença mostrando como @jsakamoto o já atualizou a `Toolbelt.Blazor.HeadElement` biblioteca](https://github.com/jsakamoto/Toolbelt.Blazor.HeadElement/commit/090df430ba725f9420d412753db8104e8c32bf51).

## <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Components.RenderTree.RenderTreeFrame?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

`T:Microsoft.AspNetCore.Components.RenderTree.RenderTreeFrame`

-->
