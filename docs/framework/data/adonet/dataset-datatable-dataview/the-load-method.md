---
description: 'Saiba mais sobre: o método Load'
title: O método Load
ms.date: 03/30/2017
dev_langs:
- vb
ms.assetid: e22e5812-89c6-41f0-9302-bb899a46dbff
ms.openlocfilehash: a14008597d88ad4af93c3646998244d94b5561d7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651516"
---
# <a name="the-load-method"></a>O método Load

Você pode usar o <xref:System.Data.DataTable.Load%2A> método para carregar um <xref:System.Data.DataTable> com linhas de uma fonte de dados. Esse é um método sobrecarregado que, em sua forma mais simples, aceita um único parâmetro, um **DataReader**. Neste formulário, ele simplesmente carrega a **DataTable** com linhas. Opcionalmente, você pode especificar o parâmetro **LoadOption** para controlar como os dados são adicionados à **DataTable**.  
  
 O parâmetro **LoadOption** é particularmente útil nos casos em que **DataTable** já contém linhas de dados, pois descreve como os dados de entrada da fonte de dados serão combinados com os dados que já estão na tabela. Por exemplo, **PreserveCurrentValues** (o padrão) especifica que, nos casos em que uma linha é marcada como **adicionada** à **DataTable**, o valor **original** ou cada coluna é definido como o conteúdo da linha correspondente da fonte de dados. O valor **atual** manterá os valores atribuídos quando a linha foi adicionada e o **RowState** da linha será definido como **alterado**.  
  
 A tabela a seguir fornece uma breve descrição dos <xref:System.Data.LoadOption> valores de enumeração.  
  
|Valor de LoadOption|Descrição|  
|----------------------|-----------------|  
|**OverwriteRow**|Se as linhas de entrada tiverem o mesmo valor de **PrimaryKey** que uma linha já na **DataTable**, os valores **original** e **atual** de cada coluna serão substituídos pelos valores na linha de entrada e a propriedade **RowState** será definida como **inalterada**.<br /><br /> As linhas da fonte de dados que ainda não existem na **DataTable** são adicionadas com um valor de **RowState** de **inalterado**.<br /><br /> Essa opção em vigor atualiza o conteúdo da **DataTable** para que ela corresponda ao conteúdo da fonte de dados.|  
|**PreserveCurrentValues (padrão)**|Se as linhas de entrada tiverem o mesmo valor de **PrimaryKey** que uma linha já na **DataTable**, o valor **original** será definido como o conteúdo da linha de entrada e o valor **atual** não será alterado.<br /><br /> Se o **RowState** for **adicionado** ou **modificado**, ele será definido como **modificado**.<br /><br /> Se o **RowState** tiver sido **excluído**, ele permanecerá **excluído**.<br /><br /> As linhas da fonte de dados que ainda não existem na **DataTable** são adicionadas e o **RowState** é definido como **inalterado**.|  
|**UpdateCurrentValues**|Se as linhas de entrada tiverem o mesmo valor de **PrimaryKey** que a linha já na **DataTable**, o valor **atual** será copiado para o valor **original** e o valor **atual** será definido como o conteúdo da linha de entrada.<br /><br /> Se o **RowState** na **DataTable** tiver sido **adicionado**, o **RowState** permanecerá **adicionado**. Para linhas marcadas como **modificadas** ou **excluídas**, o **RowState** é **modificado**.<br /><br /> As linhas da fonte de dados que ainda não existem na **DataTable** são adicionadas e o **RowState** é definido como **adicionado**.|  
  
 O exemplo a seguir usa o método **Load** para exibir uma lista de aniversários para os funcionários no banco de dados **Northwind** .  
  
```vb  
Private Sub LoadBirthdays(ByVal connectionString As String)  
    ' Assumes that connectionString is a valid connection string  
    ' to the Northwind database on SQL Server.  
    Dim queryString As String = _  
    "SELECT LastName, FirstName, BirthDate " & _  
      " FROM dbo.Employees " & _  
      "ORDER BY BirthDate, LastName, FirstName"  
  
    ' Open and fill a DataSet.
    Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
        queryString, connectionString)  
    Dim employees As New DataSet  
    adapter.Fill(employees, "Employees")  
  
    ' Create a SqlDataReader for use with the Load Method.  
    Dim reader As DataTableReader = employees.GetDataReader()  
  
    ' Create an instance of DataTable and assign the first  
    ' DataTable in the DataSet.Tables collection to it.  
    Dim dataTableEmp As DataTable = employees.Tables(0)  
  
    ' Fill the DataTable with data by calling Load and  
    ' passing the SqlDataReader.  
    dataTableEmp.Load(reader, LoadOption.OverwriteRow)  
  
    ' Loop through the rows collection and display the values  
    ' in the console window.  
    Dim employeeRow As DataRow  
    For Each employeeRow In dataTableEmp.Rows  
        Console.WriteLine("{0:MM\\dd\\yyyy}" & ControlChars.Tab & _  
          "{1}, {2}", _  
          employeeRow("BirthDate"), _  
          employeeRow("LastName"), _  
          employeeRow("FirstName"))  
    Next employeeRow  
  
    ' Keep the window opened to view the contents.  
    Console.ReadLine()  
End Sub  
```  
  
## <a name="see-also"></a>Consulte também

- [Manipulando dados em uma DataTable](manipulating-data-in-a-datatable.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
