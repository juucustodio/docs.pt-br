---
title: Regras de código desnecessárias
description: Saiba mais sobre regras de código desnecessárias da análise de código
ms.date: 09/30/2020
ms.topic: reference
author: gewarren
ms.author: gewarren
dev_langs:
- CSharp
- VB
ms.openlocfilehash: 16c4ba0e4bee2388736bf9813a3e8290d8d4da32
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2020
ms.locfileid: "96585549"
---
# <a name="unnecessary-code-rules"></a>Regras de código desnecessárias

Regras de código desnecessárias identificam diferentes partes da base de código desnecessárias e podem ser Refatorada ou removidas. A presença de código desnecessário indica um ou mais dos seguintes problemas:

- Legibilidade: código que está degradando desnecessariamente a legibilidade. Por exemplo, [IDE0001](ide0001.md) sinaliza qualificações de nome de tipo desnecessárias.
- Facilidade de manutenção: código que não é mais usado após a refatoração e que está sendo mantido desnecessariamente. Por exemplo, [IDE0051](ide0051.md) sinaliza campos particulares não utilizados, propriedades, eventos e métodos.
- Desempenho: computação desnecessária que não tem efeitos colaterais e leva à sobrecarga de desempenho desnecessária. Por exemplo, [IDE0059](ide0059.md) sinaliza as atribuições de valor não utilizado em que a expressão para computar um valor não tem efeitos colaterais.
- Funcionalidade: problema funcional no código que leva ao código necessário sendo processado redundante. Por exemplo, [IDE0060](ide0060.md) sinaliza parâmetros não utilizados em que o método ignora acidentalmente um parâmetro de entrada.

As regras nesta seção se preocupam com as seguintes regras de código desnecessárias:

- [Simplificar o nome (IDE0001)](ide0001.md)
- [Simplificar o acesso de membro (IDE0002)](ide0002.md)
- [Remover conversão desnecessária (IDE0004)](ide0004.md)
- [Remover importação desnecessária (IDE0005)](ide0005.md)
- [Remover código inacessível (IDE0035)](ide0035.md)
- [Remover membro privado não utilizado (IDE0051)](ide0051.md)
- [Remover membro privado não lido (IDE0052)](ide0052.md)
- [Remover valor de expressão não utilizado (IDE0058)](ide0058.md)
- [Remover atribuição de valor desnecessário (IDE0059)](ide0059.md)
- [Remover parâmetro não utilizado (IDE0060)](ide0060.md)
- [Remover supressão desnecessária (IDE0079)](ide0079.md)
- [Remover IDE0080 (operador de supressão desnecessária)](ide0080.md) -somente C#.
- [Remover ' ByVal ' (IDE0081)](ide0081.md) -somente Visual Basic.
- [Remover operador de igualdade desnecessária (IDE0100)](ide0100.md)
- [Remover descarte desnecessário (IDE0110)](ide0110.md) -somente C#.

Algumas dessas regras têm opções para configurar o comportamento da regra:

- [csharp_style_unused_value_expression_statement_preference (IDE0058)](ide0058.md#csharp_style_unused_value_expression_statement_preference)
- [visual_basic_style_unused_value_expression_statement_preference (IDE0058)](ide0058.md#visual_basic_style_unused_value_expression_statement_preference)
- [csharp_style_unused_value_assignment_preference (IDE0059)](ide0059.md#csharp_style_unused_value_assignment_preference)
- [visual_basic_style_unused_value_assignment_preference (IDE0059)](ide0059.md#visual_basic_style_unused_value_assignment_preference)
- [dotnet_code_quality_unused_parameters (IDE0060)](ide0060.md#dotnet_code_quality_unused_parameters)
- [dotnet_remove_unnecessary_suppression_exclusions (IDE0079)](ide0079.md#dotnet_remove_unnecessary_suppression_exclusions)

## <a name="see-also"></a>Confira também

- [Regras de linguagem de estilo de código](language-rules.md)
- [Referência de regras de estilo de código](index.md)
