---
description: 'Saiba mais sobre: Localizando linhas'
title: Localizar linhas
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 5da300e2-74c0-4d13-9202-fc20ed8212d8
ms.openlocfilehash: bf4752255945d5bbc0dd5551cd6e84c98fd78c3f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652465"
---
# <a name="finding-rows"></a>Localizar linhas

Você pode pesquisar linhas de acordo com seus valores de chave de classificação usando <xref:System.Data.DataView.Find%2A> os <xref:System.Data.DataView.FindRows%2A> métodos e do <xref:System.Data.DataView> . A diferenciação de maiúsculas e minúsculas dos valores de pesquisa nos métodos **Find** e **FindRows** é determinada pela propriedade **CaseSensitive** do subjacente <xref:System.Data.DataTable> . Os valores de pesquisa devem corresponder valores de chave de classificação existentes em sua totalidade para retornar um resultado.  
  
 O método **Find** retorna um inteiro com o índice do <xref:System.Data.DataRowView> que corresponde aos critérios de pesquisa. Se mais de uma linha corresponder aos critérios de pesquisa, somente o índice do primeiro **DataRowView** correspondente será retornado. Se nenhuma correspondência for encontrada, **Find** retornará-1.  
  
 Para retornar os resultados da pesquisa que correspondem a várias linhas, use o método **FindRows** . **FindRows** funciona exatamente como o método **Find** , exceto pelo fato de que ele retorna uma matriz **DataRowView** que faz referência a todas as linhas correspondentes no **DataView**. Se nenhuma correspondência for encontrada, a matriz **DataRowView** estará vazia.  
  
 Para usar os métodos **Find** ou **FindRows** , você deve especificar uma ordem de classificação definindo **ApplyDefaultSort** como **true** ou usando a propriedade **Sort** . Se nenhuma ordem de classificação for especificada, uma exceção será lançada.  
  
 Os métodos **Find** e **FindRows** pegam uma matriz de valores como entrada cujo comprimento corresponde ao número de colunas na ordem de classificação. No caso de uma classificação em uma única coluna, você pode passar um único valor. Para ordens de classificação que contêm várias colunas, você passa uma matriz de objetos. Observe que, para uma classificação em várias colunas, os valores na matriz de objetos devem corresponder à ordem das colunas especificadas na propriedade **Sort** do **DataView**.  
  
 O exemplo de código a seguir mostra o método **Find** sendo chamado em relação a um **DataView** com uma ordem de classificação de coluna única.  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName", DataViewRowState.CurrentRows)  
  
Dim rowIndex As Integer = custView.Find("The Cracker Box")  
  
If rowIndex = -1 Then  
  Console.WriteLine("No match found.")  
Else  
  Console.WriteLine("{0}, {1}", _  
    custView(rowIndex)("CustomerID").ToString(), _  
    custView(rowIndex)("CompanyName").ToString())  
End If  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",
  "CompanyName", DataViewRowState.CurrentRows);  
  
int rowIndex = custView.Find("The Cracker Box");  
  
if (rowIndex == -1)  
  Console.WriteLine("No match found.");  
else  
  Console.WriteLine("{0}, {1}",  
    custView[rowIndex]["CustomerID"].ToString(),  
    custView[rowIndex]["CompanyName"].ToString());  
```  
  
 Se sua propriedade de **classificação** especificar várias colunas, você deverá passar uma matriz de objetos com os valores de pesquisa para cada coluna na ordem especificada pela propriedade **Sort** , como no exemplo de código a seguir.  
  
```vb  
Dim custView As DataView = _  
  New DataView(custDS.Tables("Customers"), "", _  
  "CompanyName, ContactName", _  
  DataViewRowState.CurrentRows)  
  
Dim foundRows() As DataRowView = _  
  custView.FindRows(New object() {"The Cracker Box", "Liu Wong"})  
  
If foundRows.Length = 0 Then  
  Console.WriteLine("No match found.")  
Else  
  Dim myDRV As DataRowView  
  For Each myDRV In foundRows  
    Console.WriteLine("{0}, {1}", _  
      myDRV("CompanyName").ToString(), myDRV("ContactName").ToString())  
  Next  
End If  
```  
  
```csharp  
DataView custView = new DataView(custDS.Tables["Customers"], "",  
  "CompanyName, ContactName",  
  DataViewRowState.CurrentRows);  
  
DataRowView[] foundRows =
  custView.FindRows(new object[] {"The Cracker Box", "Liu Wong"});  
  
if (foundRows.Length == 0)  
  Console.WriteLine("No match found.");  
else  
  foreach (DataRowView myDRV in foundRows)  
    Console.WriteLine("{0}, {1}", myDRV["CompanyName"].ToString(),
      myDRV["ContactName"].ToString());  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataTable>
- <xref:System.Data.DataView>
- [DataViews](dataviews.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
