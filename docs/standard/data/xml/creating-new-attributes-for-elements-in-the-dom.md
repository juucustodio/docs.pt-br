---
description: 'Saiba mais sobre: criando novos atributos para elementos no DOM'
title: Criando novos atributos para elementos no DOM
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: dd6dc920-b011-418a-b3db-f1580a7d9251
ms.openlocfilehash: b5d9075fd2a8621252bdbfb595525a4dd8c17991
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99783398"
---
# <a name="creating-new-attributes-for-elements-in-the-dom"></a>Criando novos atributos para elementos no DOM

Criar novos atributos é diferente de criar outros tipos de nó, pois os atributos não são nós, mas propriedades de um nó de elemento e estão contidos em um **XmlAttributeCollection** associado ao elemento. Há várias maneiras de criar um atributo e anexá-lo a um elemento:

- Obter o nó de elemento e usar **SetAttribute** para adicionar um atributo à coleção de atributos do elemento.

- Criar um nó **XmlAttribute** usando o método **CreateAttribute**, obter o nó do elemento e usar **SetAttributeNode** para adicionar o nó à coleção de atributos desse elemento.

O exemplo a seguir mostra como adicionar um atributo a um elemento usando o método **SetAttribute** :

```vb
Imports System.IO
Imports System.Xml

Public Class Sample

    Public Shared Sub Main()

        Dim doc As New XmlDocument()
        doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" & _
                    "<title>Pride And Prejudice</title>" & _
                    "</book>")
        Dim root As XmlElement = doc.DocumentElement

        ' Add a new attribute.
        root.SetAttribute("genre", "urn:samples", "novel")

        Console.WriteLine("Display the modified XML...")
        Console.WriteLine(doc.InnerXml)
    End Sub
End Class
```  
  
```csharp
using System;
using System.IO;
using System.Xml;

public class Sample
{
    public static void Main()
    {
        var doc = new XmlDocument();
        doc.LoadXml("<book xmlns:bk='urn:samples' bk:ISBN='1-861001-57-5'>" +
                    "<title>Pride And Prejudice</title>" +
                    "</book>");
        XmlElement root = doc.DocumentElement;

        // Add a new attribute.
        root.SetAttribute("genre", "urn:samples", "novel");

        Console.WriteLine("Display the modified XML...");
        Console.WriteLine(doc.InnerXml);
    }
}
```

O exemplo a seguir mostra um novo atributo criado usando o método **CreateAttribute**. Em seguida, ele mostra o atributo adicionado à coleção de atributos do elemento **book** usando o método **SetAttributeNode**.

Com o seguinte XML:
  
```xml
<book genre='novel' ISBN='1-861001-57-5'>
<title>Pride And Prejudice</title>
</book>
```

crie um novo atributo e atribua um valor a ele:

```vb
Dim attr As XmlAttribute = doc.CreateAttribute("publisher")
attr.Value = "WorldWide Publishing"
```

```csharp
XmlAttribute attr = doc.CreateAttribute("publisher");
attr.Value = "WorldWide Publishing";
```

e anexe-o ao elemento:

```vb
doc.DocumentElement.SetAttributeNode(attr)
```

```csharp
doc.DocumentElement.SetAttributeNode(attr);
```

**Saída**

```xml
<book genre="novel" ISBN="1-861001-57-5" publisher="WorldWide Publishing">
<title>Pride And Prejudice</title>
</book>
```

O exemplo de código completo pode ser encontrado em <xref:System.Xml.XmlDocument.CreateAttribute%2A>.

Você também pode criar um nó **XmlAttribute** e usar o método **InsertBefore** ou **InsertAfter** para colocá-lo na posição apropriada na coleção. Se um atributo com o mesmo nome já estiver presente na coleção de atributos, o nó **XmlAttribute** existente será removido da coleção, e o novo nó **XmlAttribute** será inserido. Isso é executado da mesma forma que o método **SetAttribute**. Esses métodos usam, como parâmetro, um nó existente como um ponto de referência para fazer **InsertBefore** e **InsertAfter**. Se você não fornecer um nó de referência indicando onde inserir o novo nó, o padrão para o método **InsertAfter** será inserir o novo nó no início da coleção. A posição padrão de **InsertBefore**, se nenhum nó de referência for fornecido, será no final da coleção.

Se você criou um **XmlNamedNodeMap** de atributos, você pode adicionar um atributo por nome usando o <xref:System.Xml.XmlNamedNodeMap.SetNamedItem%2A> método. Para saber mais, confira [Coleções de nó em NamedNodeMaps e em NodeLists](node-collections-in-namednodemaps-and-nodelists.md).

## <a name="default-attributes"></a>Atributos padrão

Se você criar um elemento que está declarado para ter um atributo padrão, um novo atributo padrão com seu valor padrão será criado pelo DOM (Document Object Model) XML e anexado ao elemento. Os nós filhos do atributo padrão também são criados neste momento.

## <a name="attribute-child-nodes"></a>Nós filho do atributo

O valor de um nó de atributo se torna os seus nós filhos. Há apenas dois tipos de nós filho válidos: nós **XmlText** e nós **XmlEntityReference** . Esses são nós filhos no sentido de que métodos como **FirstChild** e **LastChild** os processam como nós filhos. Essa distinção de um atributo que possui nós filhos é importante ao tentar remover atributos ou nós filhos do atributo. Para saber mais, confira [Removendo atributos de um nó de elemento no DOM](removing-attributes-from-an-element-node-in-the-dom.md).

## <a name="see-also"></a>Consulte também

- [XML Document Object Model (DOM)](xml-document-object-model-dom.md)
