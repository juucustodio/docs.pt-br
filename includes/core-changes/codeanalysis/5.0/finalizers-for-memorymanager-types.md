---
ms.openlocfilehash: 4fc31f75e8f8cdd50abebd399d9749688e6faa5a
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465556"
---
### <a name="ca2015-do-not-define-finalizers-for-types-derived-from-memorymanagert"></a>CA2015: Não definir finalizadores para tipos derivados do MemoryManager\<T>

A regra do analisador de código .NET [CA2015](/visualstudio/code-quality/ca2015) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para todos os tipos que derivam de <xref:System.Buffers.MemoryManager%601> que definem um finalizador.

#### <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../docs/fundamentals/productivity/code-analysis.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA2015](/visualstudio/code-quality/ca2015). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

Os tipos de sinalizadores CA2015 de regra que derivam de <xref:System.Buffers.MemoryManager%601> que definem um finalizador. A adição de um finalizador a um tipo derivado de <xref:System.Buffers.MemoryManager%601> é provavelmente uma indicação de um bug. Ele sugere que um recurso nativo que poderia ter sido obtido em um <xref:System.Span%601> está sendo limpo, possivelmente enquanto ainda está em uso pelo <xref:System.Span%601> .

#### <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

#### <a name="recommended-action"></a>Ação recomendada

- Remova a definição do finalizador. Para obter mais informações, consulte [CA2015](/visualstudio/code-quality/ca2015).

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).

#### <a name="category"></a>Categoria

Análise de código

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
