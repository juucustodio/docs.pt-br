---
title: Modificação da árvore XML na memória versus construção funcional-LINQ to XML
description: Veja exemplos de duas abordagens diferentes para modificar árvores XML.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: b5afc31d-a325-4ec6-bf17-0ff90a20ffca
ms.openlocfilehash: 71f76d12024bb07cf90df2299df14646ae271b47
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551869"
---
# <a name="in-memory-xml-tree-modification-vs-functional-construction-linq-to-xml"></a>Modificação da árvore XML na memória versus construção funcional (LINQ to XML)

Modificar uma árvore XML no local é uma abordagem tradicional para alterar a forma de um documento XML. Um aplicativo típico carrega um documento em um armazenamento de dados, como DOM ou LINQ to XML; usa uma interface de programação para inserir ou excluir nós ou alterar o conteúdo; e, em seguida, salva o XML em um arquivo ou o transmite por uma rede.

LINQ to XML habilita outra abordagem útil em muitos cenários: *construção funcional*. Deleites funcionais de compilação que modificam dados como um problema de transformação, em vez de como tratamento detalhada de um armazenamento de dados. Se você pode ter uma representação dos dados e a transformação com eficiência de um formulário para outro, o resultado é o mesmo como se você recebe um armazenamento de dados e o manipulou de alguma maneira para executar outra forma. Uma chave para a abordagem de construção funcional é passar os resultados de consultas para os construtores <xref:System.Xml.Linq.XDocument> e <xref:System.Xml.Linq.XElement>.

Em muitos casos, você pode escrever o código de transformação em uma fração do tempo que levaria para manipular o armazenamento de dados, e o código resultante é mais robusto e mais fácil de manter. Nesses casos, embora a abordagem de transformação possa levar mais poder de processamento, é uma maneira mais eficaz de modificar os dados. Se um desenvolvedor estiver familiarizado com a abordagem funcional, o código resultante em muitos casos será mais fácil de entender, e será fácil encontrar o código que modifica cada parte da árvore.

A abordagem em que você modifica uma árvore XML em vigor é mais familiar para muitos programadores DOM, enquanto o código escrito usando a abordagem funcional pode parecer desconhecido para um desenvolvedor que ainda não entendeu essa abordagem. Se você precisa apenas fazer uma alteração pequena a uma grande árvore XML, a abordagem onde você altera uma árvore no lugar em muitos casos terá menos processador central - tempo.

Este artigo fornece exemplos de ambas as abordagens. Suponha que você queira modificar o seguinte documento XML simples para que os atributos se tornem elementos:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Root Data1="123" Data2="456">
  <Child1>Content</Child1>
</Root>
```

O primeiro dos exemplos a seguir usa a abordagem de modificação in-loco tradicional, e a segunda usa a abordagem de construção funcional.

## <a name="example-transform-attributes-into-elements-with-the-traditional-in-place-approach"></a>Exemplo: transformar atributos em elementos com a abordagem in-loco tradicional

Você pode escrever qualquer código procedural para criar elementos de atributos, e exclui os atributos, como segue:

```csharp
XElement root = XElement.Load("Data.xml");
foreach (XAttribute att in root.Attributes()) {
    root.Add(new XElement(att.Name, (string)att));
}
root.Attributes().Remove();
Console.WriteLine(root);
```

```vb
Dim root As XElement = XElement.Load("Data.xml")
For Each att As XAttribute In root.Attributes()
    root.Add(New XElement(att.Name, att.Value))
Next
root.Attributes().Remove()
Console.WriteLine(root)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Child1>Content</Child1>
  <Data1>123</Data1>
  <Data2>456</Data2>
</Root>
```

## <a name="example-transform-attributes-into-elements-with-the-functional-construction-approach"></a>Exemplo: transformar atributos em elementos com a abordagem de construção funcional

Por outro lado, uma abordagem funcional consiste em código para formar uma nova árvore, selecionando e escolhendo elementos e atributos da árvore de origem e transformando-os conforme apropriado à medida que são adicionados à nova árvore.

```csharp
XElement root = XElement.Load("Data.xml");
XElement newTree = new XElement("Root",
    root.Element("Child1"),
    from att in root.Attributes()
    select new XElement(att.Name, (string)att)
);
Console.WriteLine(newTree);
```

```vb
Dim root As XElement = XElement.Load("Data.xml")
Dim newTree As XElement = _
    <Root>
        <%= root.<Child1> %>
        <%= From att In root.Attributes() _
            Select New XElement(att.Name, att.Value) %>
    </Root>
Console.WriteLine(newTree)
```

Saída deste exemplo mesmo XML que o primeiro exemplo. No entanto, observe que você pode realmente consulte a estrutura XML resultante de novo na abordagem funcional. Você pode ver a criação do elemento de `Root` , o código que recebe o elemento de `Child1` de árvore de origem, e o código que transforma os atributos de árvore de origem aos elementos na árvore novo.

O exemplo funcional, nesse caso, não é mais curto nem mais simples do que o primeiro exemplo. No entanto, se você tiver muitas alterações a serem feitas em uma árvore XML, a abordagem do procedimento se tornará bastante complexa e, de certa forma, obtuso. Por outro lado, ao usar a abordagem funcional, você ainda forma apenas XML desejado, inserindo consultas e expressões apropriadas, para receber dentro do conteúdo desejado. Os passa funcionais de abordagem código que é mais fácil de manter.

Observe que neste caso a abordagem funcional provavelmente não deseja executar muito bem como a abordagem de manipulação de árvore. O principal problema é que a abordagem funcional cria mais objetos de curta duração. No entanto, as troca são eficiente usar a abordagem funcional permite maior produtividade do programador.

Este é um exemplo muito simples, mas serve para mostrar a diferença na filosofia entre as duas abordagens. A abordagem mais funcional fornece ganhos de produtividade para transformar documentos XML maiores.
