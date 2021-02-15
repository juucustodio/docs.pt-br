---
title: 'Alteração significativa: CA2014: não use stackalloc em loops'
description: Saiba mais sobre a alteração significativa no .NET 5,0 causada pela habilitação da regra de análise de código CA2014.
ms.date: 09/03/2020
ms.openlocfilehash: 7ad6203c0edd930bbbe43cdb8df0413cba833d8e
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760301"
---
# <a name="warning-ca2014-do-not-use-stackalloc-in-loops"></a>Aviso CA2014: não use stackalloc em loops

A regra do analisador de código .NET [CA2014](/visualstudio/code-quality/ca2014) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para qualquer código C# em que uma expressão [stackalloc](../../../../csharp/language-reference/operators/stackalloc.md) é usada dentro de um loop.

## <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../fundamentals/code-analysis/overview.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA2014](/visualstudio/code-quality/ca2014). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

A regra CA2014 procura código C# em que uma [expressão stackalloc](../../../../csharp/language-reference/operators/stackalloc.md) é usada dentro de um loop. [stackalloc](../../../../csharp/language-reference/operators/stackalloc.md) aloca memória a partir do quadro de pilhas atual. A memória não é liberada até que a chamada de método atual seja retornada, o que pode levar a estouros de pilha. Como não é possível capturar exceções de estouro de pilha, o aplicativo será encerrado em caso de estouro de pilha.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

- Evite usar loops [stackalloc](../../../../csharp/language-reference/operators/stackalloc.md) . Aloque o bloco de memória fora do loop e reutilize-o dentro do loop. Para obter mais informações, consulte [CA2014](/visualstudio/code-quality/ca2014).

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../project-sdk/msbuild-props.md#enablenetanalyzers).

## <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

### Affected APIs

Not detectable via API analysis.

### Category

Code analysis

-->
