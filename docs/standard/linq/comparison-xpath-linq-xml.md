---
title: Comparação entre XPath e LINQ to XML-LINQ to XML
description: As consultas XPath e LINQ to XML podem consultar árvores XML. Este artigo compara as duas opções e localiza LINQ to XML consultas para serem, em todo, a opção mais potente, versátil, mais rápida, segura e mais conveniente.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 87d361b1-daa9-4fd4-a53a-cbfa40111ad3
ms.openlocfilehash: b98651ffd7e0df0057164f40bedbc43d654d8c81
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551994"
---
# <a name="comparison-of-xpath-and-linq-to-xml"></a>Comparação XPath e de LINQ to XML

XPath e LINQ to XML são semelhantes de algumas maneiras. Ambos podem ser usados para ver uma árvore XML, retornando resultados como uma coleção de elementos, uma coleção de atributos, uma coleção de nós, ou o valor de um elemento ou de um atributo. No entanto, há diferenças significativas entre as duas opções.

## <a name="differences-between-xpath-and-linq-to-xml"></a>Diferenças entre XPath e LINQ to XML

O XPath não permite a projeção de novos tipos. Somente é possível retornar coleções de nós de árvore, enquanto o LINQ to XML pode executar uma consulta e projetar um grafo de objeto ou uma árvore XML em uma nova forma. LINQ to XML consultas podem fazer muito mais do que expressões XPath.

As expressões XPath existem no isolamento dentro de uma cadeia de caracteres. O compilador C# não pode ajudar a analisar a expressão XPath no tempo de compilação. Por outro lado, as consultas do LINQ to XML são analisadas e compiladas pelo compilador do C#. O compilador pode capturar muitos erros de consulta.

Os resultados XPath não são fortemente tipados. Em várias circunstâncias, o resultado da avaliação de uma expressão XPath é um objeto, e cabe ao desenvolvedor determinar o tipo adequado e converter o resultado conforme necessário. Por outro lado, as projeções de uma consulta do LINQ to XML são fortemente tipadas.

## <a name="result-ordering"></a>Ordenação de resultados

A recomendação do XPath 1,0 afirma que uma coleção que é o resultado da avaliação de uma expressão XPath não é ordenada.

Entretanto, ao fazer iterações por uma coleção retornada por um método do eixo XPath do LINQ to XML, os nós na coleção são retornados na ordem do documento. Este é o caso mesmo quando acessando os eixos XPath onde os predicados são expressos em termos de ordem inversa de documento, como `preceding` e `preceding-sibling`.

Por outro lado, a maioria dos eixos de LINQ to XML retorna coleções na ordem do documento. No entanto, dois deles, <xref:System.Xml.Linq.XNode.Ancestors%2A> e <xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A> , retornam coleções na ordem inversa do documento. A tabela a seguir enumera os eixos e indica a ordem da coleção para cada um:

|O eixo LINQ to XML|Ordenando|
|----------------------|--------------|
|XContainer.DescendantNodes|Ordem de documento|
|XContainer.Descendants|Ordem de documento|
|XContainer.Elements|Ordem de documento|
|XContainer.Nodes|Ordem de documento|
|XContainer.NodesAfterSelf|Ordem de documento|
|XContainer.NodesBeforeSelf|Ordem de documento|
|XElement.AncestorsAndSelf|Ordem inversa de documento|
|XElement.Attributes|Ordem de documento|
|XElement.DescendantNodesAndSelf|Ordem de documento|
|XElement.DescendantsAndSelf|Ordem de documento|
|XNode.Ancestors|Ordem inversa de documento|
|XNode.ElementsAfterSelf|Ordem de documento|
|XNode.ElementsBeforeSelf|Ordem de documento|
|XNode.NodesAfterSelf|Ordem de documento|
|XNode.NodesBeforeSelf|Ordem de documento|

## <a name="positional-predicates"></a>Predicados posicionais

Dentro de uma expressão XPath, os predicados de posição são expressos em termos de ordem de documentos para muitos eixos, mas são expressos em ordem inversa de documentos para eixos inversos. Os eixos inversos são: `preceding` , `preceding-sibling` , `ancestor` e `ancestor-or-self` . Por exemplo, a expressão XPath `preceding-sibling::*[1]` retorna imediatamente antes o irmão. Este é o caso mesmo que o conjunto de resultados final é apresentado na ordem de documento.

Por outro lado, todos os predicados posicionais em LINQ to XML sempre são expressos em termos de pedido do eixo. Por exemplo, `anElement.ElementsBeforeSelf().ElementAt(0)` retorna o primeiro elemento filho do pai do elemento consultado, não irmão anterior imediato. Outro exemplo: `anElement.Ancestors().ElementAt(0)` retorna o elemento pai.

Se você desejar localizar imediatamente o elemento precedente no LINQ to XML, escreva a expressão a seguir:

```csharp
ElementsBeforeSelf().Last()
```

```vb
ElementsBeforeSelf().Last()
```

## <a name="performance-differences"></a>Diferenças de desempenho

As consultas XPath que usam a funcionalidade XPath no LINQ to XML serão mais lentas do que LINQ to XML consultas.

## <a name="comparison-of-composition"></a>Comparação de composição

A composição de uma consulta de LINQ to XML é semelhante à composição de uma expressão XPath, mas a sintaxe é muito diferente.

Por exemplo, se você tiver um elemento em uma variável chamada `customers` e quiser encontrar um elemento neto chamado `CompanyName` em todos os elementos filho chamados `Customer` , escreveria essa expressão XPath:

```csharp
customers.XPathSelectElements("./Customer/CompanyName")
```

```vb
customers.XPathSelectElements("./Customer/CompanyName")
```

A consulta do LINQ to XML equivalente é:

```csharp
customers.Elements("Customer").Elements("CompanyName")
```

```vb
customers.Elements("Customer").Elements("CompanyName")
```

Há paralelas semelhantes para cada um dos eixos XPath.

|O eixo XPath|O eixo LINQ to XML|
|----------------|----------------------|
|o eixo filho (padrão)|<xref:System.Xml.Linq.XContainer.Elements%2A?displayProperty=nameWithType>|
|Pai (.).|<xref:System.Xml.Linq.XObject.Parent%2A?displayProperty=nameWithType>|
|o eixo de atributo (@)|<xref:System.Xml.Linq.XElement.Attribute%2A?displayProperty=nameWithType><br /><br /> ou<br /><br /> <xref:System.Xml.Linq.XElement.Attributes%2A?displayProperty=nameWithType>|
|o eixo de ancestral|<xref:System.Xml.Linq.XNode.Ancestors%2A?displayProperty=nameWithType>|
|o eixo de antepassado-ou- auto|<xref:System.Xml.Linq.XElement.AncestorsAndSelf%2A?displayProperty=nameWithType>|
|o eixo descendente (/)|<xref:System.Xml.Linq.XContainer.Descendants%2A?displayProperty=nameWithType><br /><br /> ou<br /><br /> <xref:System.Xml.Linq.XContainer.DescendantNodes%2A?displayProperty=nameWithType>|
|descendente-ou-auto|<xref:System.Xml.Linq.XElement.DescendantsAndSelf%2A?displayProperty=nameWithType><br /><br /> ou<br /><br /> <xref:System.Xml.Linq.XElement.DescendantNodesAndSelf%2A?displayProperty=nameWithType>|
|seguir-irmão|<xref:System.Xml.Linq.XNode.ElementsAfterSelf%2A?displayProperty=nameWithType><br /><br /> ou<br /><br /> <xref:System.Xml.Linq.XNode.NodesAfterSelf%2A?displayProperty=nameWithType>|
|acima-irmão|<xref:System.Xml.Linq.XNode.ElementsBeforeSelf%2A?displayProperty=nameWithType><br /><br /> ou<br /><br /> <xref:System.Xml.Linq.XNode.NodesBeforeSelf%2A?displayProperty=nameWithType>|
|após|Nenhum equivalente direto.|
|precedência|Nenhum equivalente direto.|
