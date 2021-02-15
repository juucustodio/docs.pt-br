---
title: 'Alteração significativa: mais incrivelmente: o nome do parâmetro foi alterado no método RequestImageFileAsync'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core 6,0 intitulado mais recente: nome do parâmetro alterado no método RequestImageFileAsync'
author: scottaddie
ms.author: scaddie
ms.date: 02/09/2021
ms.openlocfilehash: bfaaa6bfe94c32fbc1a5b5b70db863d105d389b5
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488283"
---
# <a name="blazor-parameter-name-changed-in-requestimagefileasync-method"></a>Mais incrivelmente: nome de parâmetro alterado no método RequestImageFileAsync

O `RequestImageFileAsync` parâmetro do método `maxWith` foi renomeado de `maxWith` para `maxWidth` .

## <a name="version-introduced"></a>Versão introduzida

6,0 visualização 1

## <a name="old-behavior"></a>Comportamento antigo

O nome do parâmetro é grafado `maxWith` .

## <a name="new-behavior"></a>Novo comportamento

O nome do parâmetro é grafado `maxWidth` .

## <a name="reason-for-change"></a>Motivo da alteração

O nome do parâmetro original era um erro tipográfico.

## <a name="recommended-action"></a>Ação recomendada

Se você estiver usando parâmetros nomeados na `RequestImageFile` API, atualize o `maxWith` nome do parâmetro para `maxWidth` . Caso contrário, nenhuma alteração será necessária.

## <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.Components.Forms.BrowserFileExtensions.RequestImageFileAsync%2A?displayProperty=nameWithType>

<!--

## Category

ASP.NET Core

## Affected APIs

`Overload:Microsoft.AspNetCore.Components.Forms.BrowserFileExtensions.RequestImageFileAsync`

-->
