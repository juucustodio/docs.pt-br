---
title: 'Alteração significativa: mais incrivelmente: alterações na lógica de roteamento em aplicativos mais Incrivelmenteos'
description: 'Saiba mais sobre as alterações significativas no ASP.NET Core 5,0 intitulados mais recentes: alterações na lógica de roteamento em aplicativos mais Incrivelmenteos'
author: scottaddie
ms.author: scaddie
ms.date: 12/14/2020
ms.openlocfilehash: 4ab8289565c88b17eb204a11724bb12a09b033c2
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97513516"
---
# <a name="blazor-route-precedence-logic-changed-in-blazor-apps"></a>Mais incrivelmente: lógica de precedência de rota alterada em aplicativos mais Incrivelmenteos

Um bug na implementação de roteamento mais incrivelmente afetou a forma como a precedência das rotas foi determinada. Esse bug afeta todas as rotas ou rotas com parâmetros opcionais em seu aplicativo mais rápido.

## <a name="version-introduced"></a>Versão introduzida

5.0.1

## <a name="old-behavior"></a>Comportamento antigo

Com o comportamento errado, as rotas com precedência mais baixa são consideradas e correspondidas em rotas com precedência mais alta. Por exemplo, a `{*slug}` rota é correspondida antes de `/customer/{id}` .

## <a name="new-behavior"></a>Novo comportamento

O comportamento atual corresponde mais próximo ao comportamento de roteamento definido em aplicativos ASP.NET Core. A estrutura determina primeiro a precedência de rota para cada segmento. O comprimento da rota é usado apenas como um segundo critério para quebrar as ligações.

## <a name="reason-for-change"></a>Motivo da alteração

O comportamento original é considerado um bug na implementação. Como meta, o sistema de roteamento em aplicativos mais podestas deve se comportar da mesma forma que o sistema de roteamento no restante de ASP.NET Core.

## <a name="recommended-action"></a>Ação recomendada

Se estiver atualizando de versões anteriores do mais do que o 5. x, use o `PreferExactMatches` atributo no `Router` componente. Esse atributo pode ser usado para aceitar o comportamento correto. Por exemplo:

```razor
<Router AppAssembly="@typeof(Program).Assembly" PreferExactMatches="true">
```

Quando `PreferExactMatches` é definido como `true` , a correspondência de rota prefere correspondências exatas sobre curingas.

## <a name="affected-apis"></a>APIs afetadas

Nenhum

<!--

## Category

ASP.NET Core

## Affected APIs

Not detectable via API analysis

-->
