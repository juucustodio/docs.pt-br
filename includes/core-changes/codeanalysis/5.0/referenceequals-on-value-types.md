---
ms.openlocfilehash: b01424c63d6e7956127bf889c53422b60ba2f219
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598047"
---
### <a name="ca2013-do-not-use-referenceequals-with-value-types"></a>CA2013: Não usar ReferenceEquals com tipos de valor

A regra do analisador de código .NET [CA2013](/visualstudio/code-quality/ca2013) está habilitada, por padrão, a partir do .NET 5,0. Ele produz um aviso de compilação para qualquer código em que <xref:System.Object.ReferenceEquals(System.Object,System.Object)> é usado para comparar um ou mais tipos de valor para igualdade.

#### <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, o SDK do .NET inclui [analisadores de código-fonte .net](../../../../docs/fundamentals/productivity/code-analysis.md). Várias dessas regras estão habilitadas, por padrão, incluindo [CA2013](/visualstudio/code-quality/ca2013). Se o seu projeto contiver código que viole essa regra e estiver configurado para tratar avisos como erros, essa alteração poderá interromper sua compilação.

A regra CA2013 localiza instâncias em que <xref:System.Object.ReferenceEquals(System.Object,System.Object)> é usada para comparar um ou mais tipos de valor para igualdade. Comparar tipos de valor para igualdade dessa maneira pode levar a resultados incorretos, porque os valores estão em caixa antes que eles sejam comparados. <xref:System.Object.ReferenceEquals(System.Object,System.Object)> retornará `false` mesmo se os valores comparados representarem a mesma instância de um tipo de valor.

#### <a name="version-introduced"></a>Versão introduzida

5,0 Preview 8

#### <a name="recommended-action"></a>Ação recomendada

- Altere o código para usar um operador de igualdade apropriado, como `==` . Você não deve suprimir este aviso.

- Para desabilitar completamente a análise de código, defina `EnableNETAnalyzers` como `false` em seu arquivo de projeto. Para obter mais informações, consulte [EnableNETAnalyzers](../../../../docs/core/project-sdk/msbuild-props.md#enablenetanalyzers).

#### <a name="category"></a>Categoria

Análise de código

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Object.ReferenceEquals(System.Object,System.Object)?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.Object.ReferenceEquals(System.Object,System.Object)`

-->
