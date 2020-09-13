---
ms.openlocfilehash: a51160a8ab5a4b437e51db31def577f8d8f50182
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465554"
---
### <a name="ca2014-do-not-use-stackalloc-in-loops"></a>CA2014: Não usar stackalloc em loops

A regra do analisador de código .NET [CA2014](/visualstudio/code-quality/ca2014) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para qualquer código C# em que uma expressão [stackalloc](../../../../docs/csharp/language-reference/operators/stackalloc.md) é usada dentro de um loop.

#### <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../docs/fundamentals/productivity/code-analysis.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA2014](/visualstudio/code-quality/ca2014). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

A regra CA2014 procura código C# em que uma [expressão stackalloc](../../../../docs/csharp/language-reference/operators/stackalloc.md) é usada dentro de um loop. [stackalloc](../../../../docs/csharp/language-reference/operators/stackalloc.md) aloca memória a partir do quadro de pilhas atual. A memória não é liberada até que a chamada de método atual seja retornada, o que pode levar a estouros de pilha. Como não é possível capturar exceções de estouro de pilha, o aplicativo será encerrado em caso de estouro de pilha.

#### <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

#### <a name="recommended-action"></a>Ação recomendada

- Evite usar loops [stackalloc](../../../../docs/csharp/language-reference/operators/stackalloc.md) . Aloque o bloco de memória fora do loop e reutilize-o dentro do loop. Para obter mais informações, consulte [CA2014](/visualstudio/code-quality/ca2014).

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).

#### <a name="category"></a>Categoria

Análise de código

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
