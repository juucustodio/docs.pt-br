---
title: Execução retardada e avaliação lenta-LINQ to XML
description: Conheça as vantagens e os requisitos da execução adiada e como implementá-la usando operações de consulta e de eixo.
ms.date: 07/20/2015
ms.assetid: 8683d1b4-b7ec-407b-be12-906ebe958a09
ms.openlocfilehash: 21b1c7b7d54e7f787919f1e1601fc36bc8c1caff
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551852"
---
# <a name="deferred-execution-and-lazy-evaluation-linq-to-xml"></a>Execução retardada e avaliação lenta (LINQ to XML)

As operações de consulta e eixo são geralmente implementadas para usar a execução adiada. Este artigo explica os requisitos e as vantagens da execução adiada e algumas considerações de implementação.

## <a name="deferred-execution"></a>Execução adiada

A execução adiada significa que a avaliação de uma expressão será atrasada até que seu valor *realizado* seja realmente necessário. A execução adiada pode aumentar muito o desempenho quando você precisa manipular grandes coleções de dados, especialmente em programas que contêm uma série de consultas ou manipulações encadeadas. Na melhor das hipóteses, a execução adiada permite apenas uma única iteração pela coleção de origem.

As tecnologias LINQ usam de modo intenso a execução adiada em ambos os membros das classes <xref:System.Linq?displayProperty=nameWithType> centrais e nos métodos de extensão nos diversos namespaces LINQ, como <xref:System.Xml.Linq.Extensions?displayProperty=nameWithType>.

A execução adiada tem suporte diretamente na linguagem C# pela palavra-chave [yield (referência C#)](../../csharp/language-reference/keywords/yield.md) (na forma da `yield-return` instrução) quando usada em um bloco de iterador. Tal iterador deve retornar uma coleção do tipo <xref:System.Collections.IEnumerator> ou <xref:System.Collections.Generic.IEnumerator%601> (ou um tipo derivado).

## <a name="eager-vs-lazy-evaluation"></a>Avaliação adiantada versus lenta

Quando você escreve um método que implementa a execução adiada, também precisa decidir se deve implementar o método usando a avaliação lenta ou a avaliação ansiosa.

- Na *avaliação lenta*, um único elemento da coleção de origem é processado durante cada chamada ao iterador. Essa é a forma comum de implementação de iteradores.
- Na *avaliação adiantada*, a primeira chamada ao iterador resultará no processamento da coleção inteira. Uma cópia temporária da coleção de origem também pode ser necessária. Por exemplo, o método <xref:System.Linq.Enumerable.OrderBy%2A> precisa classificar toda a coleção antes de retornar o primeiro elemento.

A avaliação lenta normalmente gera um melhor desempenho porque distribui a sobrecarga de processamento uniformemente por toda a avaliação da coleção e minimiza o uso de dados temporários. Naturalmente, para algumas operações, não há nenhuma outra opção que não seja materializar resultados intermediários.

Consulte [exemplo de execução adiada](deferred-execution-example.md) para obter um exemplo de programação adiada de execução em C# e Visual Basic.

## <a name="see-also"></a>Confira também

- [Tutorial: encadear consultas juntas em C #](chain-queries-example.md)
- [Conceitos e terminologia (transformação funcional)](concepts-terminology-functional-transformation.md)
- [Operações de agregação (C#)](../../csharp/programming-guide/concepts/linq/aggregation-operations.md)
- [Operações de agregação (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/aggregation-operations.md)
- [yield (Referência de C#)](../../csharp/language-reference/keywords/yield.md)
