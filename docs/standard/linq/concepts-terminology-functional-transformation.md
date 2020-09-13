---
title: Conceitos e terminologia (transformação funcional)-LINQ to XML
description: Aprenda os conceitos e a terminologia de transformações funcionais puras.
ms.date: 07/20/2015
ms.assetid: 03defb3a-7e17-4ab1-8efa-4dd66621e860
ms.openlocfilehash: a1c9c582235ac63fe50dd585ef5f046e9be8170e
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89552029"
---
# <a name="concepts-and-terminology-functional-transformation-linq-to-xml"></a>Conceitos e terminologia (transformação funcional) (LINQ to XML)

Este artigo apresenta os conceitos e a terminologia de transformações funcionais puras. A abordagem de transformação funcional para transformar dados gera códigos que geralmente são mais rápidos de programar, mais expressivos e fáceis de depurar e manter do que a programação mais tradicional e imperativa.

Observe que os artigos nesta seção não se destinam a explicar totalmente a programação funcional. Em vez disso, esses artigos identificam alguns dos recursos de programação funcional que facilitam a transformação de XML de uma forma para outra.

## <a name="what-is-pure-functional-transformation"></a>O que é transformação funcional pura

Na *transformação funcional pura*, um conjunto de funções, chamadas *funções puras*, define como transformar um conjunto de dados estruturados de sua forma original em outra forma. A palavra "puro" indica que as funções são *combináveis*, o que exige que elas sejam:

- *Autocontidas*, de modo que elas possam ser ordenadas e reorganizadas livremente sem complicação ou interdependências com o restante do programa. As transformações puras não têm nenhum conhecimento de efetuam-no ou em cima do seu ambiente. Isto é, as funções usadas na transformação não têm *efeito colateral*.
- *Sem monitoração de estado*, de modo que a execução da mesma função ou conjunto específico de funções, na mesma entrada, sempre resultará na mesma saída. As transformações puras não têm memória do seu uso prévio.

> [!IMPORTANT]
> No restante deste tutorial, o termo “function” pura é usado em um sentido geral indicar uma abordagem de programação, e não em um recurso de linguagem específica.
>
> Observe que as funções puras devem ser implementadas como métodos em C# e como funções no Visual Basic.
>
> Você não deve confundir funções puras com métodos virtuais puros em C++. O último indica que a classe recipiente é abstrato e que nenhum corpo do método é fornecido.

### <a name="functional-programming"></a>Programação funcional

A *programação funcional* é uma abordagem de programação que dá suporte diretamente à transformação funcional pura.

Historicamente, as linguagens de programação funcionais de uso geral, como o ML, Scheme, Haskell e F#, têm sido, principalmente, de interesse da comunidade acadêmica. Embora é sempre possível escrever transformações e puras em C# e Visual Basic, a dificuldade de fazer isso que não irá fazer uma opção atrativas a maioria de programadores. Em versões recentes desses idiomas, no entanto, novas construções de linguagem, como expressões lambda e inferência de tipos, tornam a programação funcional muito mais fácil e mais produtiva.

Para obter mais informações sobre a programação funcional, consulte programação [funcional vs. programa imperativo](functional-vs-imperative-programming.md).

#### <a name="domain-specific-functional-programming-languages"></a>Linguagens de programação funcional específicas de domínio

Embora as linguagens de programação funcional gerais não tenham sido amplamente adotadas, algumas linguagens de programação funcional específicas de domínio tiveram melhor sucesso. Por exemplo, folhas de estilos em cascata (CSS) são usadas para determinar a aparência de muitas páginas da Web e folhas de estilo XSLT (extensível de transformações de linguagem de folha de estilos) são usadas extensivamente na manipulação de dados XML. Para obter mais informações sobre XSLT, consulte [Transformações XSLT](../data/xml/xslt-transformations.md).

## <a name="terminology"></a>Terminologia

A lista a seguir define alguns termos relacionados a transformações funcionais.

função de ordem superior (primeira classe) \
Uma função que pode ser tratado como um objeto através de programação. Por exemplo, uma função de pedido superior pode ser passada para ou retornado de outras funções. Em C# e Visual Basic, representantes e expressões lambda são recursos de linguagem que suportam funções de pedido superior. Para gravar uma função de pedido superior, você declara um ou mais argumentos para tomar representantes, e você frequentemente usa expressões lambda para chamá-lo. Muitos dos operadores de consulta padrão são funções de pedido superior.

Para obter mais informações, consulte Visão geral [dos operadores de consulta padrão (C#)](../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md) e [visão geral dos operadores de consulta padrão (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md).

expressão lambda \
Essencialmente, uma função anônimo embutido que pode ser usada em que um tipo delegate é esperada. Esta é uma definição simplificada de expressões lambda, mas é adequada para os fins deste tutorial.

Para obter mais informações, consulte [expressões lambda (guia de programação C#)](../../csharp/programming-guide/statements-expressions-operators/lambda-expressions.md) e [expressões lambda (Visual Basic))](../../visual-basic/programming-guide/language-features/procedures/lambda-expressions.md).

coleção \
Um conjunto estruturada de dados, geralmente um tipo de uniforme. Para ser compatível com LINQ, uma coleção deve implementar a interface de <xref:System.Collections.IEnumerable> ou a interface de <xref:System.Linq.IQueryable> (ou uma de suas contrapartes genéricos, de <xref:System.Collections.Generic.IEnumerator%601> ou de <xref:System.Linq.IQueryable%601>).

tupla (tipos anônimos) \
Um conceito matemático, um tuple é uma sequência finito rotuladas de objetos, cada um de um tipo específico. Um tuple também é conhecido como uma lista ordenada. Tipos anônimos são uma implementação de linguagem desse conceito, que permitem que um tipo sem nome da classe ser declarados e um objeto do tipo a ser instanciada ao mesmo tempo.

Para obter mais informações, consulte [tipos anônimos (guia de programação C#)](../../csharp/programming-guide/classes-and-structs/anonymous-types.md) e [tipos anônimos (Visual Basic)](../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).

inferência de tipos (digitação implícita) \
A capacidade de um compilador de determinar o tipo de uma variável na ausência de uma declaração de tipo explícita.

Para obter mais informações, consulte [variáveis de local digitadas implicitamente (guia de programação C#)](../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md) e [inferência de tipo local (Visual Basic)](../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).

execução adiada e avaliação lenta \
O atraso de avaliação de uma expressão até que o valor resolvido é realmente necessário. A execução adiada é suportado em coleções.

Para obter mais informações sobre C#, consulte [introdução às consultas LINQ (c#)](../../csharp/programming-guide/concepts/linq/introduction-to-linq-queries.md) e [execução retardada e avaliação lenta em LINQ to XML (c#)](../../csharp/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).

Para obter mais Visual Basic informações, consulte [operações de consulta básica (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md) e a [execução retardada e a avaliação lenta no LINQ to XML (Visual Basic)](../../visual-basic/programming-guide/concepts/linq/deferred-execution-and-lazy-evaluation-in-linq-to-xml.md).

Esses recursos de idioma serão usados em exemplos de código em todo esta seção.

## <a name="see-also"></a>Confira também

- [Introdução às transformações funcionais puras](introduction-pure-functional-transformations.md)
- [Programação funcional versus programação imperativa](functional-vs-imperative-programming.md)
