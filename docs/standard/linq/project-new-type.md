---
title: Como projetar um novo tipo-LINQ to XML
description: Sua consulta pode retornar um IEnumerable de um tipo diferente daqueles comuns. Este artigo mostra como em um exemplo.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 48145cf9-1e0b-4e73-bbfd-28fc04800dc4
ms.openlocfilehash: a0ce8d9e5199b290dc759c191c4db7a37ddc9a55
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90547532"
---
# <a name="how-to-project-a-new-type-linq-to-xml"></a>Como projetar um novo tipo (LINQ to XML)

Outros exemplos nesta seção mostraram consultas que os resultados de retorno como <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XElement>, <xref:System.Collections.Generic.IEnumerable%601> de `string`, e <xref:System.Collections.Generic.IEnumerable%601> de `int`. Esses são tipos de resultados comuns, mas não são apropriados para todos os cenários. Em muitos casos, você desejará que suas consultas retornem um <xref:System.Collections.Generic.IEnumerable%601> de algum outro tipo.

## <a name="example-define-a-new-type-and-have-the-select-statement-create-an-instance-of-the-type"></a>Exemplo: definir um novo tipo e fazer com que a `select` instrução crie uma instância do tipo

Este exemplo mostra como instanciar objetos na cláusula `select` . O código primeiro invoca um construtor para definir uma nova classe e, em seguida, modifica a `select` instrução para que a expressão seja uma nova instância da nova classe. O exemplo usa arquivo XML de exemplo de documento XML [: ordem de compra típica](sample-xml-file-typical-purchase-order.md).

```csharp
class NameQty
{
    public string name;
    public int qty;
    public NameQty(string n, int q)
    {
        name = n;
        qty = q;
    }
};

class Program {
    public static void Main()
    {
        XElement po = XElement.Load("PurchaseOrder.xml");

        IEnumerable<NameQty> nqList =
            from n in po.Descendants("Item")
            select new NameQty(
                    (string)n.Element("ProductName"),
                    (int)n.Element("Quantity")
                );

        foreach (NameQty n in nqList)
            Console.WriteLine(n.name + ":" + n.qty);
    }
}
```

```vb
Public Class NameQty
    Public name As String
    Public qty As Integer
    Public Sub New(ByVal n As String, ByVal q As Integer)
        name = n
        qty = q
    End Sub
End Class

Public Class Program
    Shared Sub Main()
        Dim po As XElement = XElement.Load("PurchaseOrder.xml")

        Dim nqList As IEnumerable(Of NameQty) = _
            From n In po...<Item> _
            Select New NameQty( _
                n.<ProductName>.Value, CInt(n.<Quantity>.Value))

        For Each n As NameQty In nqList
            Console.WriteLine(n.name & ":" & n.qty)
        Next
    End Sub
End Class
```

Este exemplo usa o <xref:System.Xml.Linq.XContainer.Element%2A> método que foi introduzido no artigo [como recuperar um único elemento filho](retrieve-single-child-element.md) . Também usa conversões para recuperar os valores dos elementos que são retornados pelo método de <xref:System.Xml.Linq.XContainer.Element%2A> .

Esse exemplo gera a saída a seguir:

```output
Lawnmower:1
Baby Monitor:2
```

## <a name="see-also"></a>Confira também

- [Projeções e transformações (LINQ to XML) (Visual Basic)](./work-dictionaries-linq-xml.md)
