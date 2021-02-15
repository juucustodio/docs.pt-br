---
title: Como localizar um elemento com um elemento filho específico-LINQ to XML
description: Localizar um elemento cujo elemento filho tenha um valor específico
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 00cf5555-374e-4369-bf93-7bd2e7f21db3
ms.openlocfilehash: 2f97f920ce09222858a0a51eb52ffe0d58dba960
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90678634"
---
# <a name="how-to-find-an-element-with-a-specific-child-element-linq-to-xml"></a>Como localizar um elemento com um elemento filho específico (LINQ to XML)

Este artigo mostra como localizar um elemento cujo elemento filho tem um valor específico.

## <a name="example-find-an-element-whose-child-element-has-a-specific-value"></a>Exemplo: localizar um elemento cujo elemento filho tem um valor específico

O exemplo localiza o `Test` elemento cujo `CommandLine` elemento filho tem um valor de "Examp2.EXE". O exemplo usa arquivo XML de exemplo de documento XML [: configuração de teste](sample-xml-file-test-configuration.md).

```csharp
XElement root = XElement.Load("TestConfig.xml");
IEnumerable<XElement> tests =
    from el in root.Elements("Test")
    where (string)el.Element("CommandLine") == "Examp2.EXE"
    select el;
foreach (XElement el in tests)
    Console.WriteLine((string)el.Attribute("TestId"));
```

```vb
Dim root As XElement = XElement.Load("TestConfig.xml")
Dim tests As IEnumerable(Of XElement) = _
    From el In root.<Test> _
    Where el.<CommandLine>.Value = "Examp2.EXE" _
    Select el
For Each el as XElement In tests
    Console.WriteLine(el.@TestId)
Next
```

Esse exemplo gera a saída a seguir:

```output
0002
0006
```

Observe que a versão Visual Basic do código usa a [Propriedade eixo filho XML](../../visual-basic/language-reference/xml-axis/xml-child-axis-property.md), a [Propriedade eixo de atributo XML](../../visual-basic/language-reference/xml-axis/xml-attribute-axis-property.md)e a [propriedade valor XML](../../visual-basic/language-reference/xml-axis/xml-value-property.md).

## <a name="example-find-when-the-xml-is-in-a-namespace"></a>Exemplo: localizar quando o XML está em um namespace

O exemplo a seguir faz o mesmo que o anterior, mas para XML que está em um namespace. O exemplo usa [arquivo XML de exemplo de documento XML: configuração de teste em um namespace](sample-xml-file-test-configuration-namespace.md).

Para obter mais informações, consulte [visão geral de namespaces](namespaces-overview.md).

```csharp
XElement root = XElement.Load("TestConfigInNamespace.xml");
XNamespace ad = "http://www.adatum.com";
IEnumerable<XElement> tests =
    from el in root.Elements(ad + "Test")
    where (string)el.Element(ad + "CommandLine") == "Examp2.EXE"
    select el;
foreach (XElement el in tests)
    Console.WriteLine((string)el.Attribute("TestId"));
```

```vb
Imports <xmlns='http://www.adatum.com'>

Module Module1
    Sub Main()
        Dim root As XElement = XElement.Load("TestConfigInNamespace.xml")
        Dim tests As IEnumerable(Of XElement) = _
            From el In root.<Test> _
            Where el.<CommandLine>.Value = "Examp2.EXE" _
            Select el
        For Each el As XElement In tests
            Console.WriteLine(el.@TestId)
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
0002
0006
```

## <a name="see-also"></a>Confira também

- <xref:System.Xml.Linq.XElement.Attribute%2A>
- <xref:System.Xml.Linq.XContainer.Elements%2A>
- [Visão geral de operadores de consulta padrão](../../csharp/programming-guide/concepts/linq/standard-query-operators-overview.md)
- [Operações de projeção](../../csharp/programming-guide/concepts/linq/projection-operations.md)
