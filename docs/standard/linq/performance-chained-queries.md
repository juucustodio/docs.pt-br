---
title: Desempenho de consultas encadeadas-LINQ to XML
description: Saiba mais sobre as consultas encadeadas que podem ser executadas, bem como uma única consulta maior e mais complicada.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b2f1d715-8946-4dc0-8d56-fb3d1bba54a6
ms.openlocfilehash: c1dae1eaf008a1f17c6884ef6b8e67d042719ad9
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551909"
---
# <a name="performance-of-chained-queries-linq-to-xml"></a>Desempenho de consultas encadeadas (LINQ to XML)

Um dos benefícios mais importantes do LINQ (e LINQ to XML) é que as consultas encadeadas podem ser executadas, bem como uma única consulta que é maior e mais complicada do que as consultas encadeadas.

Uma consulta encadeada é uma consulta que usa outra consulta como sua fonte. Por exemplo, o seguinte código simples, `query2` tem `query1` como sua fonte:

```csharp
XElement root = new XElement("Root",
    new XElement("Child", 1),
    new XElement("Child", 2),
    new XElement("Child", 3),
    new XElement("Child", 4)
);

var query1 = from x in root.Elements("Child")
             where (int)x >= 3
             select x;

var query2 = from e in query1
             where (int)e % 2 == 0
             select e;

foreach (var i in query2)
    Console.WriteLine("{0}", (int)i);
```

```vb
Dim root As New XElement("Root", New XElement("Child", 1), New XElement("Child", 2), New XElement("Child", 3), New XElement("Child", 4))

Dim query1 = From x In root.Elements("Child") Where CInt(x) >= 3x

Dim query2 = From e In query1 Where CInt(e) Mod 2 = 0e

For Each i As var In query2
    Console.WriteLine("{0}", CInt(i))
Next
```

Esse exemplo gera a saída a seguir:

```output
4
```

Esta consulta encadeada fornece o mesmo perfil de desempenho que iterando através de uma lista vinculada.

- O eixo de <xref:System.Xml.Linq.XContainer.Elements%2A> tem essencialmente o mesmo desempenho que iterando através de uma lista vinculada. <xref:System.Xml.Linq.XContainer.Elements%2A> é implementado como um iterador com execução adiada. Isso significa que faz qualquer trabalho adicional a iterar através da lista vinculada, como alocar do objeto de iterador e manter controle de estado de execução. Este trabalho pode ser dividida em duas categorias: o trabalho que é feito no momento no iterador é configurado, e o trabalho que é feito em cada iteração. O trabalho de configuração é uma pequena quantidade, fixa de trabalho e o trabalho feito em cada iteração é proporcionalmente para o número de itens na coleção de origem.
- No `query1` , a `where` cláusula ( `Where` em Visual Basic) faz com que a consulta chame o <xref:System.Linq.Enumerable.Where%2A> método. Esse método também é implementado como um iterador. O trabalho de configuração consiste em criar uma instância do representante que fará referência a expressão lambda, mais a configuração normal para um iterador. A cada iteração, o representante é chamado para executar o predicado. O trabalho de configuração e o trabalho realizado durante cada iteração são semelhantes ao trabalho feito durante a iteração por meio do eixo.
- Em `query1`, a cláusula SELECT faz com que a consulta chama o método de <xref:System.Linq.Enumerable.Select%2A> . Este método tem o mesmo perfil de desempenho que o método de <xref:System.Linq.Enumerable.Where%2A> .
- No `query2` , a `where` cláusula ( `Where` em Visual Basic) e a `select` cláusula têm o mesmo perfil de desempenho do `query1` .

A interação com `query2` é portanto diretamente proporcionalmente para o número de itens na fonte da primeira consulta, ou ser uma das vezes.

Para obter mais informações sobre iteradores, consulte [yield](../../csharp/language-reference/keywords/yield.md).

Para obter um tutorial mais detalhado sobre como encadear consultas, consulte [tutorial: encadear consultas juntas (C#)](chain-queries-example.md).
