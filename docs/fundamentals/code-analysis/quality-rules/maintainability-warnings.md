---
title: Regras de manutenção (análise de código)
description: Saiba mais sobre as regras de manutenção da análise de código.
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
- vs.codeanalysis.maintainabilityrules
helpviewer_keywords:
- rules, maintainability
- managed code analysis rules, maintainability rules
- maintainability rules
author: gewarren
ms.author: gewarren
ms.openlocfilehash: fc2ef2b42eeba241b7af66b579a60365ad2b88c7
ms.sourcegitcommit: 2e4adc490c1d2a705a0592b295d606b10b9f51f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/25/2020
ms.locfileid: "96584726"
---
# <a name="maintainability-rules"></a>Regras de facilidade de manutenção

As regras de manutenção dão suporte à manutenção da biblioteca e do aplicativo.

## <a name="in-this-section"></a>Nesta seção

| Regra | Descrição |
|-----------|-----------------------------------|
| [CA1501: Evitar herança excessiva](ca1501.md) | Um tipo está mais de quatro níveis abaixo na hierarquia de herança. As hierarquias de tipo profundamente aninhado podem ser difíceis de seguir, compreender e manter. |
| [CA1502: Evitar complexidade excessiva](ca1502.md) | Esta regra mede o número de caminhos linearmente independentes por meio do método, o que é determinado pelo número e pela complexidade das ramificações condicionais. |
| [CA1505: Evitar código de difícil manutenção](ca1505.md) | Um tipo ou um método tem um baixo valor de índice de facilidade de manutenção. Um baixo índice de facilidade de manutenção indica que um tipo ou um método é provavelmente difícil de manter e seria um bom candidato para um novo design. |
| [CA1506: Evitar acoplamento de classes excessivo](ca1506.md) | Esta regra mede o acoplamento de classes contando o número de referências de tipo exclusivas que um tipo ou um método contém. |
| [CA1507: Usar nameof no lugar da cadeia de caracteres](ca1507.md) | Um literal de cadeia de caracteres é usado como um argumento em que uma `nameof` expressão pode ser usada. |
| [CA1508: Evitar código condicional morto](ca1508.md) | Um método tem código condicional que sempre é avaliado como `true` ou `false` em tempo de execução. Isso leva a um código inativo na `false` ramificação da condição. |
| [CA1509: Entrada inválida no arquivo de configuração de métrica de código](ca1509.md) | As regras de métricas de código, como [CA1501](ca1501.md), [CA1502](ca1502.md), [CA1505](ca1505.md) e [CA1506](ca1506.md), forneciam um arquivo de configuração chamado `CodeMetricsConfig.txt` que tem uma entrada inválida. |

## <a name="see-also"></a>Confira também

- [Meça a complexidade e a facilidade de manutenção do código gerenciado](/visualstudio/code-quality/code-metrics-values)
