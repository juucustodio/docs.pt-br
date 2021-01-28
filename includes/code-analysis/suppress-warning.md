---
ms.openlocfilehash: b26e346f7076a57aef8ae7587ab1222b4100a323
ms.sourcegitcommit: 7e42488c2f8f63f6d499b5f8fb1dec5bac9ad254
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/28/2021
ms.locfileid: "98957930"
---
## <a name="suppress-a-warning"></a>Suprimir um aviso

Para suprimir uma violação de regra, defina a opção severidade para a ID de regra específica como `none` em um arquivo EditorConfig. Por exemplo:

```ini
[*.{cs,vb}]
dotnet_diagnostic.CA1822.severity = none
```

O Visual Studio fornece maneiras adicionais de suprimir avisos das regras de análise de código. Para obter mais informações, consulte [suprimir violações](/visualstudio/code-quality/use-roslyn-analyzers#suppress-violations).

Para obter mais informações sobre severidades de regra, consulte [Configurar a severidade da regra](~/docs/fundamentals/code-analysis/configuration-options.md#severity-level).
