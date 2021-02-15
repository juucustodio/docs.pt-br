---
title: Objetos XName e XNamespace atomos-LINQ to XML
description: Saiba como objetos XName e XNamespace com o mesmo nome compartilham uma instância.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: a5b21433-b49d-415c-b00e-bcbfb0d267d7
ms.openlocfilehash: 05df7b5348fecebb7504ebb4e2623f688b6549e1
ms.sourcegitcommit: 48466b8fb7332ececff5dc388f19f6b3ff503dd4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/05/2020
ms.locfileid: "93400833"
---
# <a name="atomized-xname-and-xnamespace-objects-linq-to-xml"></a>Objetos XName e XNamespace atomed (LINQ to XML)

Os objetos <xref:System.Xml.Linq.XName> e <xref:System.Xml.Linq.XNamespace> são *atomizados* , isto é, se eles contêm o mesmo nome qualificado, referem-se ao mesmo objeto. Isso produz benefícios de desempenho para consultas: quando você compara dois nomes atomos para igualdade, a linguagem intermediária subjacente só precisa determinar se as duas referências apontam para o mesmo objeto. O código subjacente não precisa fazer comparações de cadeias de caracteres, o que levaria mais tempo.

## <a name="atomization-semantics"></a>Semântica de atomização

A atomização significa que, se dois <xref:System.Xml.Linq.XName> objetos tiverem o mesmo nome local e estiverem no mesmo namespace, eles compartilharão a mesma instância. Da mesma forma, se dois objetos de <xref:System.Xml.Linq.XNamespace> têm o mesmo URI de namespace, compartilham a mesma instância.

Para que uma classe permite objetos atomizados, o construtor para a classe deve ser particular, não público. Isso ocorre porque se foi o construtor público, você pode criar um objeto não atomizado. As classes de <xref:System.Xml.Linq.XName> e de <xref:System.Xml.Linq.XNamespace> implementam um operador de conversão implícita para converter uma cadeia de caracteres em <xref:System.Xml.Linq.XName> ou em <xref:System.Xml.Linq.XNamespace>. Isso é como você obtém uma instância desses objetos. Você não pode obter uma instância usando um construtor, pois o Construtor está inacessível.

<xref:System.Xml.Linq.XName> Além <xref:System.Xml.Linq.XNamespace> disso, implemente os operadores de igualdade e desigualdade, que determinam se os dois objetos que estão sendo comparados são referências à mesma instância.

## <a name="example-create-objects-and-show-that-identical-names-share-an-instance"></a>Exemplo: criar objetos e mostrar que nomes idênticos compartilham uma instância

O código a seguir cria alguns objetos de <xref:System.Xml.Linq.XElement> e demonstrar-los que os nomes idênticos compartilham a mesma instância.

```csharp
var r1 = new XElement("Root", "data1");
XElement r2 = XElement.Parse("<Root>data2</Root>");

if ((object)r1.Name == (object)r2.Name)
    Console.WriteLine("r1 and r2 have names that refer to the same instance.");
else
    Console.WriteLine("Different");

XName n = "Root";

if ((object)n == (object)r1.Name)
    Console.WriteLine("The name of r1 and the name in 'n' refer to the same instance.");
else
    Console.WriteLine("Different");
```

```vb
Dim r1 As New XElement("Root", "data1")
Dim r2 As XElement = XElement.Parse("<Root>data2</Root>")

If DirectCast(r1.Name, Object) = DirectCast(r2.Name, Object) Then
    Console.WriteLine("r1 and r2 have names that refer to the same instance.")
Else
    Console.WriteLine("Different")
End If

Dim n As XName = "Root"

If DirectCast(n, Object) = DirectCast(r1.Name, Object) Then
    Console.WriteLine("The name of r1 and the name in 'n' refer to the same instance.")
Else
    Console.WriteLine("Different")
End If
```

Esse exemplo gera a saída a seguir:

```output
r1 and r2 have names that refer to the same instance.
The name of r1 and the name in 'n' refer to the same instance.
```

Como mencionado anteriormente, a vantagem de objetos atomizados é que quando você usa um dos métodos do eixo que recebem <xref:System.Xml.Linq.XName> como um parâmetro, o método do eixo só precisa determinar que dois nomes referenciam a mesma instância para selecionar os elementos desejados.

O exemplo a seguir <xref:System.Xml.Linq.XName> passa a chamada de método <xref:System.Xml.Linq.XContainer.Descendants%2A> , que tem em melhor desempenho devido ao padrão de atomização.

```csharp
var root = new XElement("Root",
    new XElement("C1", 1),
    new XElement("Z1",
        new XElement("C1", 2),
        new XElement("C1", 1)
    )
);

var query = from e in root.Descendants("C1")
            where (int)e == 1
            select e;

foreach (var z in query)
    Console.WriteLine(z);
```

```vb
Dim root As New XElement("Root", New XElement("C1", 1), New XElement("Z1", New XElement("C1", 2), New XElement("C1", 1)))

Dim query = From e In root.Descendants("C1") Where CInt(e) = 1

For Each z In query
    Console.WriteLine(z)
Next
```

Esse exemplo gera a saída a seguir:

```xml
<C1>1</C1>
<C1>1</C1>
```
