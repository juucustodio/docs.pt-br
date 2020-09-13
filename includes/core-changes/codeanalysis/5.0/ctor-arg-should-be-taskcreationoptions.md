---
ms.openlocfilehash: 6bb3b11ef4e4cb6f6a039c97911b0acca862fe6f
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465555"
---
### <a name="ca2247-argument-to-taskcompletionsource-constructor-should-be-taskcreationoptions-value"></a>CA2247: o argumento para o Construtor TaskCompletionSource deve ser um valor TaskCreationOptions

A regra do analisador de código .NET [CA2247](/visualstudio/code-quality/ca2247) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para chamadas para o <xref:System.Threading.Tasks.TaskCompletionSource%601> Construtor que passa um argumento do tipo <xref:System.Threading.Tasks.TaskContinuationOptions> .

#### <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../docs/fundamentals/productivity/code-analysis.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA2247](/visualstudio/code-quality/ca2247). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

A regra CA2247 localiza chamadas para o <xref:System.Threading.Tasks.TaskCompletionSource%601> Construtor que passa um argumento do tipo <xref:System.Threading.Tasks.TaskContinuationOptions> . O <xref:System.Threading.Tasks.TaskCompletionSource%601> tipo tem um construtor que aceita um <xref:System.Threading.Tasks.TaskCreationOptions> valor e outro construtor que aceita um <xref:System.Object> . Se você passar acidentalmente um <xref:System.Threading.Tasks.TaskContinuationOptions> valor em vez de um <xref:System.Threading.Tasks.TaskCreationOptions> valor, o construtor com o <xref:System.Object> parâmetro será chamado em tempo de execução. Seu código será compilado e executado, mas não terá o comportamento pretendido.

#### <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

#### <a name="recommended-action"></a>Ação recomendada

- Substitua o <xref:System.Threading.Tasks.TaskContinuationOptions> argumento pelo valor correspondente <xref:System.Threading.Tasks.TaskCreationOptions> . Não suprimir este aviso, pois quase sempre realça um bug em seu código. Para obter mais informações, consulte [CA2247](/visualstudio/code-quality/ca2247).

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).

#### <a name="category"></a>Categoria

Análise de código

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Threading.Tasks.TaskCompletionSource%601.%23ctor(System.Object)>

<!--

#### Affected APIs

- ``M:System.Threading.Tasks.TaskCompletionSource`1.#ctor(System.Object)``

-->
