---
title: Como transformar a forma de uma árvore XML-LINQ to XML
description: Você pode usar a construção funcional para alterar a forma de um documento XML; ou seja, para manter os dados, mas alterar itens como nomes de elementos, nomes de atributo e hierarquia.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 93c5d426-dea2-4709-a991-60204de42e8f
ms.openlocfilehash: 7f78cb2542357be674d771f93825b7f4a56abea0
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90554502"
---
# <a name="how-to-transform-the-shape-of-an-xml-tree-linq-to-xml"></a>Como transformar a forma de uma árvore XML (LINQ to XML)

A *forma* de um documento XML refere-se aos seus nomes de elemento, nomes de atributo e às características de sua hierarquia.

Às vezes você precisará alterar a forma de um documento XML. Por exemplo, você pode ter que enviar um documento XML existente para outro sistema que requer nomes diferentes de elementos e atributos. Você pode examinar o documento, excluir e renomeando elementos conforme necessário, mas usando funcionais resultados de compilação em um código mais legível e mais sustentável. Para obter mais informações sobre a construção funcional, consulte [construção funcional](functional-construction.md).

O primeiro exemplo neste artigo altera a organização de um documento XML. Mover elementos complexos de um local na árvore para outro.

O segundo exemplo cria um documento XML cuja forma difere do documento de origem. Ele omite alguns elementos, renomeia outros e altera a capitalização dos nomes dos elementos.

## <a name="example-use-embedded-query-expressions-to-change-the-shape-of-an-xml-tree"></a>Exemplo: usar expressões de consulta inseridas para alterar a forma de uma árvore XML

O exemplo a seguir altera a forma de um arquivo XML usando expressões de consulta inseridas.

O documento XML de origem deste exemplo, [arquivo XML de exemplo: Customers e Orders](sample-xml-file-customers-orders.md), contém um `Customers` elemento sob o `Root` elemento que contém todos os clientes. Também contém um elemento de `Orders` no elemento de `Root` que contém todos os pedidos. O exemplo cria uma nova árvore XML na qual os pedidos de cada cliente estão contidos em um `Orders` elemento dentro do `Customer` elemento. O documento original também contém um `CustomerID` elemento no `Order` elemento; esse elemento é omitido da nova árvore.

```csharp
XElement co = XElement.Load("CustomersOrders.xml");
XElement newCustOrd =
    new XElement("Root",
        from cust in co.Element("Customers").Elements("Customer")
        select new XElement("Customer",
            cust.Attributes(),
            cust.Elements(),
            new XElement("Orders",
                from ord in co.Element("Orders").Elements("Order")
                where (string)ord.Element("CustomerID") == (string)cust.Attribute("CustomerID")
                select new XElement("Order",
                    ord.Attributes(),
                    ord.Element("EmployeeID"),
                    ord.Element("OrderDate"),
                    ord.Element("RequiredDate"),
                    ord.Element("ShipInfo")
                )
            )
        )
    );
Console.WriteLine(newCustOrd);
```

 ```vb
Dim co As XElement = XElement.Load("CustomersOrders.xml")
Dim newCustOrd = _
    <Root>
        <%= From cust In co.<Customers>.<Customer> _
            Select _
            <Customer>
                <%= cust.Attributes() %>
                <%= cust.Elements() %>
                <Orders>
                    <%= From ord In co.<Orders>.<Order> _
                        Where ord.<CustomerID>.Value = cust.@CustomerID _
                        Select _
                        <Order>
                            <%= ord.Attributes() %>
                            <%= ord.<EmployeeID> %>
                            <%= ord.<OrderDate> %>
                            <%= ord.<RequiredDate> %>
                            <%= ord.<ShipInfo> %>
                        </Order> _
                    %>
                </Orders>
            </Customer> _
        %>
    </Root>
Console.WriteLine(newCustOrd)
```

Esse exemplo gera a saída a seguir:

```xml
<Root>
  <Customer CustomerID="GREAL">
    <CompanyName>Great Lakes Food Market</CompanyName>
    <ContactName>Howard Snyder</ContactName>
    <ContactTitle>Marketing Manager</ContactTitle>
    <Phone>(503) 555-7555</Phone>
    <FullAddress>
      <Address>2732 Baker Blvd.</Address>
      <City>Eugene</City>
      <Region>OR</Region>
      <PostalCode>97403</PostalCode>
      <Country>USA</Country>
    </FullAddress>
    <Orders />
  </Customer>
  <Customer CustomerID="HUNGC">
    <CompanyName>Hungry Coyote Import Store</CompanyName>
    <ContactName>Yoshi Latimer</ContactName>
    <ContactTitle>Sales Representative</ContactTitle>
    <Phone>(503) 555-6874</Phone>
    <Fax>(503) 555-2376</Fax>
    <FullAddress>
      <Address>City Center Plaza 516 Main St.</Address>
      <City>Elgin</City>
      <Region>OR</Region>
      <PostalCode>97827</PostalCode>
      <Country>USA</Country>
    </FullAddress>
    <Orders />
  </Customer>
  ...
</Root>
```

## <a name="example-create-a-document-whose-shape-differs-from-that-of-the-source-document"></a>Exemplo: criar um documento cuja forma difere da do documento de origem

Este exemplo renomeia alguns elementos e converte alguns atributos para elementos. Ele chama `ConvertAddress` , que retorna uma lista de <xref:System.Xml.Linq.XElement> objetos. O argumento para o método é uma consulta que determina o elemento complexo de `Address` onde o atributo de `Type` tem um valor de `"Shipping"`. O exemplo usa arquivo XML de exemplo de documento XML [: ordem de compra típica](sample-xml-file-typical-purchase-order.md).

```csharp
static IEnumerable<XElement> ConvertAddress(XElement add)
{
    List<XElement> fragment = new List<XElement>() {
        new XElement("NAME", (string)add.Element("Name")),
        new XElement("STREET", (string)add.Element("Street")),
        new XElement("CITY", (string)add.Element("City")),
        new XElement("ST", (string)add.Element("State")),
        new XElement("POSTALCODE", (string)add.Element("Zip")),
        new XElement("COUNTRY", (string)add.Element("Country"))
    };
    return fragment;
}

static void Main(string[] args)
{
    XElement po = XElement.Load("PurchaseOrder.xml");
    XElement newPo = new XElement("PO",
        new XElement("ID", (string)po.Attribute("PurchaseOrderNumber")),
        new XElement("DATE", (DateTime)po.Attribute("OrderDate")),
        ConvertAddress(
            (from el in po.Elements("Address")
            where (string)el.Attribute("Type") == "Shipping"
            select el)
            .First()
        )
    );
    Console.WriteLine(newPo);
}
```

```vb
Function ConvertAddress(ByVal add As XElement) As IEnumerable(Of XElement)
    Dim fragment = New List(Of XElement)
    fragment.Add(<NAME><%= add.<Name>.Value %></NAME>)
    fragment.Add(<STREET><%= add.<Street>.Value %></STREET>)
    fragment.Add(<CITY><%= add.<City>.Value %></CITY>)
    fragment.Add(<ST><%= add.<State>.Value %></ST>)
    fragment.Add(<POSTALCODE><%= add.<Zip>.Value %></POSTALCODE>)
    fragment.Add(<COUNTRY><%= add.<Country>.Value %></COUNTRY>)
    Return fragment
End Function

Sub Main()
    Dim po As XElement = XElement.Load("PurchaseOrder.xml")
    Dim newPo As XElement = _
        <PO>
            <ID><%= po.@PurchaseOrderNumber %></ID>
            <DATE><%= CDate(po.@OrderDate) %></DATE>
            <%= _
                ConvertAddress( _
                (From el In po.<Address> _
                Where el.@Type = "Shipping" _
                Select el) _
                .First() _
                ) _
            %>
        </PO>
    Console.WriteLine(newPo)
End Sub
```

Esse exemplo gera a saída a seguir:

```xml
<PO>
  <ID>99503</ID>
  <DATE>1999-10-20T00:00:00</DATE>
  <NAME>Ellen Adams</NAME>
  <STREET>123 Maple Street</STREET>
  <CITY>Mill Valley</CITY>
  <ST>CA</ST>
  <POSTALCODE>10999</POSTALCODE>
  <COUNTRY>USA</COUNTRY>
</PO>
```

## <a name="see-also"></a>Confira também

- [Projeções e transformações (LINQ to XML) (Visual Basic)](./work-dictionaries-linq-xml.md)
