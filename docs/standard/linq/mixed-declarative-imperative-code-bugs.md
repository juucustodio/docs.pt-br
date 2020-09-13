---
title: Bugs de código declarativo/imperativo misto-LINQ to XML
description: Saiba como reconhecer e evitar problemas que podem ocorrer quando o código é iterado ao longo de um eixo que faz alterações.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: fada62d0-0680-4e73-945a-2b00d7a507af
ms.openlocfilehash: 280bb62d15ff28d1fd09ca2d0c52c0a0c36d7282
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551963"
---
# <a name="mixed-declarativeimperative-code-bugs-linq-to-xml"></a>Bugs de código declarativo/imperativo mistos (LINQ to XML)

O LINQ to XML contém vários métodos que permitem que você modifique uma árvore XML diretamente. Você pode adicionar elementos, excluir elementos, modifica o conteúdo de um elemento, adiciona atributos, e assim por diante. Essa interface de programação é descrita em [Modificar árvores XML](in-memory-xml-tree-modification-vs-functional-construction.md). Se você estiver Iterando por meio de um dos eixos, como <xref:System.Xml.Linq.XContainer.Elements%2A> e estiver modificando a árvore XML à medida que itera pelo eixo, poderá acabar com alguns bugs estranhos.

Esse problema é às vezes conhecido como “o problema do Dia De Bruxas”.

Quando você escreve um código usando LINQ que itera em uma coleção, você está escrevendo código em um estilo declarativo. É mais semelhante a descrever *o que* você deseja, em vez de *como* você deseja fazer isso. Se você escreve o código que 1) obtém o primeiro elemento, 2) testá-la para alguma condição, 3) altera-a, e 4) coloque-a de novo na lista, então este código seria obrigatório. Você está informando ao computador *como* fazer o que você deseja concluir.

Misturar esses estilos de código na mesma operação é o que resulta em problemas. Considere o seguinte:

Suponha que você tenha uma lista vinculada com três itens nele (a, b, e c#):

> a-> b-> c

Agora, suponha que você deseja mover através da lista vinculada, adicionando novos itens três (a, b, e c#). Você deseja a lista vinculada resultante para ter esta aparência:

 > a-> um '-> b-> b '-> c-> c '

Assim você escreve o código que itera através da lista, e para cada item, adicione um novo item mesmo após ele. O que acontece são que seu código verá o primeiro elemento de `a` , e inserção `a'` após ele. Agora, seu código será movido para o próximo nó da lista, que agora é `a'` , portanto, adiciona um novo item entre um ' e o b à lista!

Como você resolveria isso? Bem, você pode fazer uma cópia do original associado para listar, e criar uma lista completamente nova. Ou, se você estiver escrevendo código puramente imperativo, poderá encontrar o primeiro item, adicionar o novo item e, em seguida, avançar duas vezes na lista vinculada, avançando sobre o elemento que você acabou de adicionar.

## <a name="example-adding-while-iterating"></a>Exemplo: adicionando ao iterar

Por exemplo, suponha que você queira escrever código para criar uma duplicata de cada elemento em uma árvore:

```csharp
XElement root = new XElement("Root",
    new XElement("A", "1"),
    new XElement("B", "2"),
    new XElement("C", "3")
);
foreach (XElement e in root.Elements())
    root.Add(new XElement(e.Name, (string)e));
```

```vb
Dim root As XElement = _
    <Root>
        <A>1</A>
        <B>2</B>
        <C>3</C>
    </Root>
For Each e As XElement In root.Elements()
    root.Add(New XElement(e.Name, e.Value))
Next
```

Esse código entra em um loop infinito. A declaração de `foreach` itera através do eixo de `Elements()` , adicionando novos elementos para o elemento de `doc` . Acaba também iterar através dos elementos que acabou de adicionar. E como atribuir novos objetos com cada iteração do loop, consumirá se houver qualquer memória disponível.

Você pode corrigir este problema recebendo a coleção na memória usando o operador padrão de consulta de <xref:System.Linq.Enumerable.ToList%2A> , como segue:

```csharp
XElement root = new XElement("Root",
    new XElement("A", "1"),
    new XElement("B", "2"),
    new XElement("C", "3")
);
foreach (XElement e in root.Elements().ToList())
    root.Add(new XElement(e.Name, (string)e));
Console.WriteLine(root);
```

```vb
Dim root As XElement = _
    <Root>
        <A>1</A>
        <B>2</B>
        <C>3</C>
    </Root>
For Each e As XElement In root.Elements().ToList()
    root.Add(New XElement(e.Name, e.Value))
Next
Console.WriteLine(root)
```

Agora o código. A árvore XML resultante é a seguinte:

```xml
<Root>
  <A>1</A>
  <B>2</B>
  <C>3</C>
  <A>1</A>
  <B>2</B>
  <C>3</C>
</Root>
```

## <a name="example-deleting-while-iterating"></a>Exemplo: excluindo durante a iteração

Se você deseja excluir todos os nós em um determinado nível, você pode ter tentado escrever código como o seguinte:

```csharp
XElement root = new XElement("Root",
    new XElement("A", "1"),
    new XElement("B", "2"),
    new XElement("C", "3")
);
foreach (XElement e in root.Elements())
    e.Remove();
Console.WriteLine(root);
```

```vb
Dim root As XElement = _
    <Root>
        <A>1</A>
        <B>2</B>
        <C>3</C>
    </Root>
For Each e As XElement In root.Elements()
    e.Remove()
Next
Console.WriteLine(root)
```

No entanto, isso não faz o que você deseja. Nessa situação, depois de remover o primeiro elemento, A, ele é removido da árvore XML contida na raiz e o código no método Elements que faz a iteração não pode localizar o próximo elemento.

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <B>2</B>
  <C>3</C>
</Root>
```

A solução é novamente chamar <xref:System.Linq.Enumerable.ToList%2A> para materializar a coleção, como segue:

```csharp
XElement root = new XElement("Root",
    new XElement("A", "1"),
    new XElement("B", "2"),
    new XElement("C", "3")
);
foreach (XElement e in root.Elements().ToList())
    e.Remove();
Console.WriteLine(root);
```

```vb
Dim root As XElement = _
    <Root>
        <A>1</A>
        <B>2</B>
        <C>3</C>
    </Root>
For Each e As XElement In root.Elements().ToList()
    e.Remove()
Next
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root />
```

Como alternativa, você pode eliminar a iteração completamente chamando <xref:System.Xml.Linq.XElement.RemoveAll%2A> no elemento pai:

```csharp
XElement root = new XElement("Root",
    new XElement("A", "1"),
    new XElement("B", "2"),
    new XElement("C", "3")
);
root.RemoveAll();
Console.WriteLine(root);
```

```vb
Dim root As XElement = _
    <Root>
        <A>1</A>
        <B>2</B>
        <C>3</C>
    </Root>
root.RemoveAll()
Console.WriteLine(root)
```

## <a name="example-why-linq-cant-automatically-handle-these-issues"></a>Exemplo: por que o LINQ não pode lidar com esses problemas automaticamente

Uma abordagem seria sempre trazer tudo na memória em vez de fazer a avaliação lazy. No entanto, seria muito cara em termos de uso de desempenho e de memória. Na verdade, se o LINQ e o LINQ to XML, tomaram essa abordagem, ele falharia em situações do mundo real.

Outra abordagem possível seria colocar algum tipo de sintaxe de transação no LINQ, e fazer com que o compilador tentasse analisar o código para determinar se alguma coleção específica precisava ser materializada. No entanto, tentar determinar qualquer código que tiver efeitos colaterais é incredibly complexa. Considere o seguinte código:

```csharp
var z =
    from e in root.Elements()
    where TestSomeCondition(e)
    select DoMyProjection(e);
```

```vb
Dim z = _
    From e In root.Elements() _
    Where (TestSomeCondition(e)) _
    Select DoMyProjection(e)
```

Esse código de análise precisaria analisar métodos TestSomeCondition e DoMyProjection, e todos os métodos que esses métodos chamados a partir, para determinar se qualquer código tinha efeitos colaterais. Mas o código de análise não pode apenas procurar qualquer código que tem efeitos colaterais. Precisaria para selecionar apenas o código que tinha efeitos colaterais em elementos filho de `root` nesta situação.

LINQ to XML não tenta fazer nenhuma análise. Cabe a você evitar esses problemas.

## <a name="example-use-declarative-code-to-generate-a-new-xml-tree-rather-than-modify-the-existing-tree"></a>Exemplo: Use o código declarativo para gerar uma nova árvore XML em vez de modificar a árvore existente

Para evitar esses problemas, não misture códigos declarativos e imperativos, mesmo se você souber exatamente a semântica de suas coleções e a semântica dos métodos que modificam a árvore XML. Se você escrever um código que evite problemas, seu código precisará ser mantido por outros desenvolvedores no futuro, e eles podem não estar tão claros quanto aos problemas. Se você mistura estilos declarativo e obrigatórias de codificação, seu código será mais frágil.  Se você escreve o código que materializa uma coleção para que esses problemas são impedidos, observar-la com comentários apropriadas em seu código, para que os desenvolvedores de aplicativos compreendam o problema.

Se o desempenho e outras considerações permitirem, use apenas o código declarativo. Não altere sua árvore XML existente. Em vez disso, gere um novo, conforme mostrado no exemplo a seguir:

```csharp
XElement root = new XElement("Root",
    new XElement("A", "1"),
    new XElement("B", "2"),
    new XElement("C", "3")
);
XElement newRoot = new XElement("Root",
    root.Elements(),
    root.Elements()
);
Console.WriteLine(newRoot);
```

```vb
Dim root As XElement = _
    <Root>
        <A>1</A>
        <B>2</B>
        <C>3</C>
    </Root>
Dim newRoot As XElement = New XElement("Root", _
    root.Elements(), root.Elements())
Console.WriteLine(newRoot)
```
