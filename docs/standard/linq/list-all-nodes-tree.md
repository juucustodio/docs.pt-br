---
title: Como listar todos os nós em uma árvore-LINQ to XML
description: Você pode usar o XPath para listar todos os nós em uma árvore XML. Este artigo fornece um exemplo de C# e Visual Basic que lista os nós de uma árvore. Cada nó é representado por uma expressão XPath que especifica o local do nó na árvore.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 3e934371-f4c6-458b-9f6b-f9061b596f5b
ms.openlocfilehash: b2a02beea34434da52cd8770d7f9802acf227760
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551972"
---
# <a name="how-to-list-all-nodes-in-a-tree-linq-to-xml"></a>Como listar todos os nós em uma árvore (LINQ to XML)

Às vezes, é útil listar todos os nós em uma árvore – por exemplo, para saber exatamente como um método ou uma propriedade afeta a árvore. O exemplo a seguir para C# e Visual Basic lista os nós de uma árvore. Cada nó é representado por uma expressão XPath que especifica o local do nó na árvore.

> [!NOTE]
> Não é particularmente útil executar expressões XPath usando LINQ to XML. As consultas de LINQ to XML têm melhor desempenho do que as expressões XPath e são muito mais poderosas. No entanto, como uma maneira de identificar nós na árvore XML, o XPath funciona bem.

## <a name="example-use-xpath-to-list-all-nodes-in-a-tree"></a>Exemplo: usar XPath para listar todos os nós em uma árvore

Este exemplo tem uma função chamada `GetXPath` que gera uma expressão XPath específica para qualquer nó na árvore XML. Ele faz isso mesmo quando os nós estão em um namespace. Os elementos nas expressões XPath geradas têm prefixos de namespace conforme necessário.

O exemplo primeiro cria uma pequena árvore XML que contém vários tipos de nós. Em seguida, ele faz a iteração pelos nós e imprime a expressão XPath para cada nó.

A declaração XML não é um nó na árvore.

Aqui está a árvore XML que serve como entrada:

```xml
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<?target data?>
<Root AttName="An Attribute" xmlns:aw="http://www.adventure-works.com">
  <!--This is a comment-->
  <Child>Text</Child>
  <Child>Other Text</Child>
  <ChildWithMixedContent>text<b>BoldText</b>otherText</ChildWithMixedContent>
  <aw:ElementInNamespace>
    <aw:ChildInNamespace />
  </aw:ElementInNamespace>
</Root>
```

Aqui está a lista de nós na árvore XML, conforme definido pelas expressões XPath:

```text
/processing-instruction()
/Root
/Root/@AttName
/Root/@xmlns:aw
/Root/comment()
/Root/Child[1]
/Root/Child[1]/text()
/Root/Child[2]
/Root/Child[2]/text()
/Root/ChildWithMixedContent
/Root/ChildWithMixedContent/text()[1]
/Root/ChildWithMixedContent/b
/Root/ChildWithMixedContent/b/text()
/Root/ChildWithMixedContent/text()[2]
/Root/aw:ElementInNamespace
/Root/aw:ElementInNamespace/aw:ChildInNamespace
```

Este é o código para o exemplo:

```csharp
public static class MyExtensions
{
    private static string GetQName(XElement xe)
    {
        string prefix = xe.GetPrefixOfNamespace(xe.Name.Namespace);
        if (xe.Name.Namespace == XNamespace.None || prefix == null)
            return xe.Name.LocalName.ToString();
        else
            return prefix + ":" + xe.Name.LocalName.ToString();
    }

    private static string GetQName(XAttribute xa)
    {
        string prefix =
            xa.Parent.GetPrefixOfNamespace(xa.Name.Namespace);
        if (xa.Name.Namespace == XNamespace.None || prefix == null)
            return xa.Name.ToString();
        else
            return prefix + ":" + xa.Name.LocalName;
    }

    private static string NameWithPredicate(XElement el)
    {
        if (el.Parent != null && el.Parent.Elements(el.Name).Count() != 1)
            return GetQName(el) + "[" +
                (el.ElementsBeforeSelf(el.Name).Count() + 1) + "]";
        else
            return GetQName(el);
    }

    public static string StrCat<T>(this IEnumerable<T> source,
        string separator)
    {
        return source.Aggregate(new StringBuilder(),
                   (sb, i) => sb
                       .Append(i.ToString())
                       .Append(separator),
                   s => s.ToString());
    }

    public static string GetXPath(this XObject xobj)
    {
        if (xobj.Parent == null)
        {
            XDocument doc = xobj as XDocument;
            if (doc != null)
                return ".";
            XElement el = xobj as XElement;
            if (el != null)
                return "/" + NameWithPredicate(el);
            // The XPath data model doesn't include white space text nodes
            // that are children of a document, so this method returns null.
            XText xt = xobj as XText;
            if (xt != null)
                return null;
            XComment com = xobj as XComment;
            if (com != null)
                return
                    "/" +
                    (
                        com
                        .Document
                        .Nodes()
                        .OfType<XComment>()
                        .Count() != 1 ?
                        "comment()[" +
                        (com
                        .NodesBeforeSelf()
                        .OfType<XComment>()
                        .Count() + 1) +
                        "]" :
                        "comment()"
                    );
            XProcessingInstruction pi = xobj as XProcessingInstruction;
            if (pi != null)
                return
                    "/" +
                    (
                        pi.Document.Nodes()
                        .OfType<XProcessingInstruction>()
                        .Count() != 1 ?
                        "processing-instruction()[" +
                        (pi
                        .NodesBeforeSelf()
                        .OfType<XProcessingInstruction>()
                        .Count() + 1) +
                        "]" :
                        "processing-instruction()"
                    );
            return null;
        }
        else
        {
            XElement el = xobj as XElement;
            if (el != null)
            {
                return
                    "/" +
                    el
                    .Ancestors()
                    .InDocumentOrder()
                    .Select(e => NameWithPredicate(e))
                    .StrCat("/") +
                    NameWithPredicate(el);
            }
            XAttribute at = xobj as XAttribute;
            if (at != null)
                return
                    "/" +
                    at
                    .Parent
                    .AncestorsAndSelf()
                    .InDocumentOrder()
                    .Select(e => NameWithPredicate(e))
                    .StrCat("/") +
                    "@" + GetQName(at);
            XComment com = xobj as XComment;
            if (com != null)
                return
                    "/" +
                    com
                    .Parent
                    .AncestorsAndSelf()
                    .InDocumentOrder()
                    .Select(e => NameWithPredicate(e))
                    .StrCat("/") +
                    (
                        com
                        .Parent
                        .Nodes()
                        .OfType<XComment>()
                        .Count() != 1 ?
                        "comment()[" +
                        (com
                        .NodesBeforeSelf()
                        .OfType<XComment>()
                        .Count() + 1) + "]" :
                        "comment()"
                    );
            XCData cd = xobj as XCData;
            if (cd != null)
                return
                    "/" +
                    cd
                    .Parent
                    .AncestorsAndSelf()
                    .InDocumentOrder()
                    .Select(e => NameWithPredicate(e))
                    .StrCat("/") +
                    (
                        cd
                        .Parent
                        .Nodes()
                        .OfType<XText>()
                        .Count() != 1 ?
                        "text()[" +
                        (cd
                        .NodesBeforeSelf()
                        .OfType<XText>()
                        .Count() + 1) + "]" :
                        "text()"
                    );
            XText tx = xobj as XText;
            if (tx != null)
                return
                    "/" +
                    tx
                    .Parent
                    .AncestorsAndSelf()
                    .InDocumentOrder()
                    .Select(e => NameWithPredicate(e))
                    .StrCat("/") +
                    (
                        tx
                        .Parent
                        .Nodes()
                        .OfType<XText>()
                        .Count() != 1 ?
                        "text()[" +
                        (tx
                        .NodesBeforeSelf()
                        .OfType<XText>()
                        .Count() + 1) + "]" :
                        "text()"
                    );
            XProcessingInstruction pi = xobj as XProcessingInstruction;
            if (pi != null)
                return
                    "/" +
                    pi
                    .Parent
                    .AncestorsAndSelf()
                    .InDocumentOrder()
                    .Select(e => NameWithPredicate(e))
                    .StrCat("/") +
                    (
                        pi
                        .Parent
                        .Nodes()
                        .OfType<XProcessingInstruction>()
                        .Count() != 1 ?
                        "processing-instruction()[" +
                        (pi
                        .NodesBeforeSelf()
                        .OfType<XProcessingInstruction>()
                        .Count() + 1) + "]" :
                        "processing-instruction()"
                    );
            return null;
        }
    }
}

class Program
{
    static void Main(string[] args)
    {
        XNamespace aw = "http://www.adventure-works.com";
        XDocument doc = new XDocument(
            new XDeclaration("1.0", "utf-8", "yes"),
            new XProcessingInstruction("target", "data"),
            new XElement("Root",
                new XAttribute("AttName", "An Attribute"),
                new XAttribute(XNamespace.Xmlns + "aw", aw.ToString()),
                new XComment("This is a comment"),
                new XElement("Child",
                    new XText("Text")
                ),
                new XElement("Child",
                    new XText("Other Text")
                ),
                new XElement("ChildWithMixedContent",
                    new XText("text"),
                    new XElement("b", "BoldText"),
                    new XText("otherText")
                ),
                new XElement(aw + "ElementInNamespace",
                    new XElement(aw + "ChildInNamespace")
                )
            )
        );
        doc.Save("Test.xml");
        Console.WriteLine(File.ReadAllText("Test.xml"));
        Console.WriteLine("------");
        foreach (XObject obj in doc.DescendantNodes())
        {
            Console.WriteLine(obj.GetXPath());
            XElement el = obj as XElement;
            if (el != null)
                foreach (XAttribute at in el.Attributes())
                    Console.WriteLine(at.GetXPath());
        }
    }
}
```

```vb
Module Module1
<System.Runtime.CompilerServices.Extension()> _
    Private Function StrCat(Of T)(ByVal source As IEnumerable(Of T), _
                                  ByVal separator As String) As String
        Return _
        source.Aggregate(New StringBuilder(), _
            Function(sb, i) sb _
                .Append(i.ToString()) _
                .Append(separator), _
                Function(s) s.ToString())
    End Function

    <System.Runtime.CompilerServices.Extension()> _
    Public Function GetXPath(ByVal xobj As XObject) As String
        Dim retStr As String
        If xobj.Parent Is Nothing Then
            Dim doc As XDocument = TryCast(xobj, XDocument)
            If doc IsNot Nothing Then
                Return "."
            End If
            Dim el As XElement = TryCast(xobj, XElement)
            If el IsNot Nothing Then
                Return ("/" & NameWithPredicate(el))
            End If

            ' The XPath data model doesn't include white space text nodes
            ' that are children of a document, so this method returns null.
            Dim xt As XText = TryCast(xobj, XText)
            If xt IsNot Nothing Then
                Return Nothing
            End If
            Dim com As XComment = TryCast(xobj, XComment)
            If com IsNot Nothing Then
                If com.Document().Nodes().OfType(Of XComment)().Count() <> 1 Then
                    Return "/comment()[" & (com.NodesBeforeSelf().OfType _
                        (Of XComment)().Count() + 1) & "]"
                Else
                    Return "/comment()"
                End If
            End If

            Dim pi As XProcessingInstruction = TryCast(xobj, XProcessingInstruction)
            If pi IsNot Nothing Then
                If pi.Document.Nodes().OfType(Of XProcessingInstruction)(). _
                        Count() <> 1 Then
                    Return "/processing-instruction()[" & _
                        (pi.NodesBeforeSelf().OfType(Of XProcessingInstruction)() _
                        .Count() + 1) & "]"
                Else
                    Return "/processing-instruction()"
                End If
            End If
        Else
            Dim el As XElement = TryCast(xobj, XElement)
            If el IsNot Nothing Then
                Return "/" & el.Ancestors().InDocumentOrder(). _
                    Select(Function(e) NameWithPredicate(e)) _
                    .StrCat("/") & NameWithPredicate(el)
            End If

            Dim at As XAttribute = TryCast(xobj, XAttribute)
            If at IsNot Nothing Then
                Return "/" & at.Parent().AncestorsAndSelf().InDocumentOrder(). _
                    Select(Function(e) NameWithPredicate(e)).StrCat("/") & _
                    "@" & GetQName(at)
            End If

            Dim com As XComment = TryCast(xobj, XComment)
            If com IsNot Nothing Then
                retStr = "/" & com.Parent.AncestorsAndSelf().InDocumentOrder(). _
                Select(Function(e) NameWithPredicate(e)).StrCat("/") & "comment()"
                If com.Parent().Nodes().OfType(Of XComment)().Count() <> 1 Then
                    retStr &= "[" & (com.NodesBeforeSelf().OfType(Of XComment)().Count() + 1) & "]"
                End If
                Return retStr
            End If

            Dim cd As XCData = TryCast(xobj, XCData)
            If cd IsNot Nothing Then
                retStr = "/" & cd.Parent.AncestorsAndSelf().InDocumentOrder(). _
                    Select(Function(e) NameWithPredicate(e)).StrCat("/") & "text()"
                If cd.Parent.Nodes().OfType(Of XText)().Count() <> 1 Then
                    retStr &= "[" & (cd.NodesBeforeSelf().OfType(Of XText)(). _
                        Count() + 1) & "]"
                End If
                Return retStr
            End If

            Dim tx As XText = TryCast(xobj, XText)
            If tx IsNot Nothing Then
                retStr = "/" & tx.Parent.AncestorsAndSelf().InDocumentOrder(). _
                    Select(Function(e) NameWithPredicate(e)).StrCat("/") & "text()"
                If tx.Parent.Nodes().OfType(Of XText)().Count() <> 1 Then
                    retStr &= "[" & (tx.NodesBeforeSelf().OfType(Of XText)(). _
                        Count() + 1) & "]"
                End If
                Return retStr
            End If

            Dim pi As XProcessingInstruction = TryCast(xobj, XProcessingInstruction)
            If pi IsNot Nothing Then
                retStr = "/" & pi.Parent.AncestorsAndSelf().InDocumentOrder(). _
                    Select(Function(e) NameWithPredicate(e)). _
                    StrCat("/") & "processing-instruction()"
                If pi.Parent.Nodes().OfType(Of XProcessingInstruction)().Count() <> 1 Then
                    retStr &= "[" & (pi.NodesBeforeSelf().OfType(Of XProcessingInstruction)(). _
                        Count() + 1) & "]"
                End If
            End If
        End If
        Return Nothing
    End Function

    Private Function GetQName(ByVal xe As XElement) As String
        Dim prefix As String = xe.GetPrefixOfNamespace(xe.Name.Namespace)
        If xe.Name.Namespace = XNamespace.None Or prefix Is Nothing Then
            Return xe.Name.LocalName.ToString()
        Else
            Return prefix + ":" & xe.Name.LocalName.ToString()
        End If
    End Function

    Private Function GetQName(ByVal xa As XAttribute) As String
        Dim prefix As String = _
            xa.Parent.GetPrefixOfNamespace(xa.Name.Namespace)
        If xa.Name.Namespace = XNamespace.None Or prefix Is Nothing Then
            Return xa.Name.ToString()
        Else
            Return prefix + ":" & xa.Name.LocalName
        End If
    End Function

    Public Function NameWithPredicate(ByVal el As XElement) As String
        If el.Parent IsNot Nothing AndAlso el.Parent.Elements(el.Name).Count() <> 1 Then
            Return GetQName(el) + "[" & _
                (el.ElementsBeforeSelf(el.Name).Count() + 1) & "]"
        Else
            Return GetQName(el)
        End If
    End Function

    Sub Main()
        Dim aw As XNamespace = "http://www.adventure-works.com"
        Dim doc As XDocument = _
            <?xml version='1.0' encoding="utf-8" standalone='yes'?>
            <?target data?>
            <Root AttName='An Attribute' xmlns:aw='http://www.adventure-works.com'>
                <!--This is a comment-->
                <Child>Text</Child>
                <Child>Other Text</Child>
                <ChildWithMixedContent>text<b>BoldText</b>otherText</ChildWithMixedContent>
                <aw:ElementInNamespace>
                    <aw:ChildInNamespace/>
                </aw:ElementInNamespace>
            </Root>
        doc.Save("Test.xml")
        Console.WriteLine(File.ReadAllText("Test.xml"))
        Console.WriteLine("------")
        For Each obj As XObject In doc.DescendantNodes()
            Console.WriteLine(obj.GetXPath())
            Dim el As XElement = TryCast(obj, XElement)
            If el IsNot Nothing Then
                For Each at As XAttribute In el.Attributes()
                    Console.WriteLine(at.GetXPath())
                Next
            End If
        Next
    End Sub
End Module
```

Esse exemplo gera a saída a seguir:

```output
<?xml version="1.0" encoding="utf-8" standalone="yes"?>
<?target data?>
<Root AttName="An Attribute" xmlns:aw="http://www.adventure-works.com">
  <!--This is a comment-->
  <Child>Text</Child>
  <Child>Other Text</Child>
  <ChildWithMixedContent>text<b>BoldText</b>otherText</ChildWithMixedContent>
  <aw:ElementInNamespace>
    <aw:ChildInNamespace />
  </aw:ElementInNamespace>
</Root>
------
/processing-instruction()
/Root
/Root/@AttName
/Root/@xmlns:aw
/Root/comment()
/Root/Child[1]
/Root/Child[1]/text()
/Root/Child[2]
/Root/Child[2]/text()
/Root/ChildWithMixedContent
/Root/ChildWithMixedContent/text()[1]
/Root/ChildWithMixedContent/b
/Root/ChildWithMixedContent/b/text()
/Root/ChildWithMixedContent/text()[2]
/Root/aw:ElementInNamespace
/Root/aw:ElementInNamespace/aw:ChildInNamespace
```
