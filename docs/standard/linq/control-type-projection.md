---
title: Como controlar o tipo de uma LINQ to XML de projeção
description: Você pode controlar o tipo de coleção que sua consulta retorna; Ele não precisa ser um IEnumerable de XElements.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: e4db6b7e-4cc9-4c8f-af85-94acf32aa348
ms.openlocfilehash: c92258fa9501aeeee46fe664cc4436f9349ff232
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90558121"
---
# <a name="how-to-control-the-type-of-a-projection-linq-to-xml"></a>Como controlar o tipo de uma projeção (LINQ to XML)

*Projeção* é o processo de filtrar um conjunto de dados, alterar sua forma e, talvez, seu tipo. A maioria das expressões de consulta faz projeções. A maioria das expressões de consulta nesta seção é avaliada como <xref:System.Collections.Generic.IEnumerable%601> de <xref:System.Xml.Linq.XElement> , mas você pode criar coleções de outros tipos. Este artigo mostra como fazer isso.

## <a name="example-define-a-new-type-and-create-a-query-that-creates-an-ienumerable-of-that-type"></a>Exemplo: definir um novo tipo e criar uma consulta que cria um IEnumerable desse tipo

O exemplo a seguir define um novo tipo, `Customer` , e a expressão de consulta cria novos `Customer` objetos na `Select` cláusula. Isso faz com que o tipo da expressão de consulta para ser <xref:System.Collections.Generic.IEnumerable%601> de `Customer`. O exemplo usa [arquivo XML de exemplo de documento XML: clientes e pedidos](sample-xml-file-customers-orders.md).

```csharp
public class Customer
{
    private string customerID;
    public string CustomerID{ get{return customerID;} set{customerID = value;}}

    private string companyName;
    public string CompanyName{ get{return companyName;} set{companyName = value;}}

    private string contactName;
    public string ContactName { get{return contactName;} set{contactName = value;}}

    public Customer(string customerID, string companyName, string contactName)
    {
        CustomerID = customerID;
        CompanyName = companyName;
        ContactName = contactName;
    }

    public override string ToString()
    {
        return $"{this.customerID}:{this.companyName}:{this.contactName}";
    }
}

class Program
{
    static void Main(string[] args)
    {
        XElement custOrd = XElement.Load("CustomersOrders.xml");
        IEnumerable<Customer> custList =
            from el in custOrd.Element("Customers").Elements("Customer")
            select new Customer(
                (string)el.Attribute("CustomerID"),
                (string)el.Element("CompanyName"),
                (string)el.Element("ContactName")
            );
        foreach (Customer cust in custList)
            Console.WriteLine(cust);
    }


}
```

```vb
Public Class Customer
    Private customerIDValue As String
    Public Property CustomerID() As String
        Get
            Return customerIDValue
        End Get
        Set(ByVal value As String)
            customerIDValue = value
        End Set
    End Property

    Private companyNameValue As String
    Public Property CompanyName() As String
        Get
            Return companyNameValue
        End Get
        Set(ByVal value As String)
            companyNameValue = value
        End Set
    End Property

    Private contactNameValue As String
    Public Property ContactName() As String
        Get
            Return contactNameValue
        End Get
        Set(ByVal value As String)
            contactNameValue = value
        End Set
    End Property

    Public Sub New(ByVal customerID As String, _
                   ByVal companyName As String, _
                   ByVal contactName As String)
        CustomerIDValue = customerID
        CompanyNameValue = companyName
        ContactNameValue = contactName
    End Sub

    Public Overrides Function ToString() As String
        Return String.Format("{0}:{1}:{2}", Me.CustomerID, Me.CompanyName, Me.ContactName)
    End Function
End Class

Sub Main()
    Dim custOrd As XElement = XElement.Load("CustomersOrders.xml")
    Dim custList As IEnumerable(Of Customer) = _
        From el In custOrd.<Customers>.<Customer> _
        Select New Customer( _
            el.@<CustomerID>, _
            el.<CompanyName>.Value, _
            el.<ContactName>.Value _
        )
    For Each cust In custList
        Console.WriteLine(cust)
    Next
End Sub
```

Esse exemplo gera a saída a seguir:

```output
GREAL:Great Lakes Food Market:Howard Snyder
HUNGC:Hungry Coyote Import Store:Yoshi Latimer
LAZYK:Lazy K Kountry Store:John Steel
LETSS:Let's Stop N Shop:Jaime Yorres
```

## <a name="see-also"></a>Confira também

- <xref:System.Linq.Enumerable.Select%2A>
- [Projeções e transformações (LINQ to XML) (Visual Basic)](./work-dictionaries-linq-xml.md)
