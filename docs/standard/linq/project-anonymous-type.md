---
title: Como projetar um tipo anônimo-LINQ to XML
description: Você pode projetar para um tipo anônimo em vez de criar um tipo apenas para uso na projeção. Este artigo fornece um exemplo de C# e Visual Basic.
ms.date: 07/20/2015
dev_langs:
- csharp
- vb
ms.assetid: 5cb9be13-5ac4-4373-a034-b3520a5b2dec
ms.openlocfilehash: 5851492f075068337c60316664138dd09c97443b
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89551962"
---
# <a name="how-to-project-an-anonymous-type-linq-to-xml"></a>Como projetar um tipo anônimo (LINQ to XML)

Em alguns casos, talvez você queira projetar uma consulta para um novo tipo, mas a consulta seria seu único uso para o novo tipo. Em vez de criar o tipo, você pode projetar para um tipo anônimo. Os tipos anônimos fornecem uma maneira conveniente de encapsular um conjunto de propriedades somente leitura em um objeto sem precisar definir explicitamente um tipo primeiro. Se você escrever uma consulta que cria um objeto de um tipo anônimo na `select` cláusula, a consulta retornará um <xref:System.Collections.IEnumerable> do tipo.

O exemplo a seguir mostra a criação de um objeto de um tipo anônimo que é inicializado com duas propriedades `Amount` e `Message` .

```csharp
var v = new { Amount = 108, Message = "Hello" };
```

```vb
Dim v = New With { .Amount = 108, .Message = "Hello" };
```

O tipo de cada propriedade é inferido pelo compilador. O nome do tipo é gerado pelo compilador e não está disponível no nível do código-fonte.

Para obter mais informações sobre tipos anônimos, consulte:

- [Tipos anônimos (Guia de Programação em C#)](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)
- [Tipos anônimos (Visual Basic)](../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)

## <a name="example-project-an-anonymous-type-by-creating-objects-in-the-select-clause"></a>Exemplo: projetar um tipo anônimo criando objetos na `select` cláusula

Nesse exemplo, a cláusula de `select` projetos de um tipo anônimo. O exemplo usa em `var` para criar o objeto de `IEnumerable` . Dentro do loop de `foreach` , a variável de iteração torna-se em uma instância do tipo anônimo criado na expressão de consulta.

Este exemplo usa [arquivo XML de exemplo de documento XML: clientes e pedidos](sample-xml-file-customers-orders.md).

```csharp
XElement custOrd = XElement.Load("CustomersOrders.xml");
var custList =
    from el in custOrd.Element("Customers").Elements("Customer")
    select new {
        CustomerID = (string)el.Attribute("CustomerID"),
        CompanyName = (string)el.Element("CompanyName"),
        ContactName = (string)el.Element("ContactName")
    };
foreach (var cust in custList)
    Console.WriteLine("{0}:{1}:{2}", cust.CustomerID, cust.CompanyName, cust.ContactName);
```

```vb
Dim custOrd As XElement = XElement.Load("CustomersOrders.xml")
Dim custList = _
    From el In custOrd.<Customers>.<Customer> _
    Select New With { _
        .CustomerID = el.@<CustomerID>, _
        .CompanyName = el.<CompanyName>.Value, _
        .ContactName = el.<ContactName>.Value _
    }
For Each cust In custList
    Console.WriteLine("{0}:{1}:{2}", cust.CustomerID, cust.CompanyName, cust.ContactName)
Next
```

Esse exemplo gera a saída a seguir:

```output
GREAL:Great Lakes Food Market:Howard Snyder
HUNGC:Hungry Coyote Import Store:Yoshi Latimer
LAZYK:Lazy K Kountry Store:John Steel
LETSS:Let's Stop N Shop:Jaime Yorres
```

## <a name="see-also"></a>Confira também

- [Tipos anônimos (Guia de Programação em C#)](../../csharp/programming-guide/classes-and-structs/anonymous-types.md)
- [Tipos anônimos (Visual Basic)](../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)
