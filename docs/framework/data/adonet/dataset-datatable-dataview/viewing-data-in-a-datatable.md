---
description: 'Saiba mais sobre: Exibindo dados em uma DataTable'
title: Exibindo dados em uma DataTable
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1d26e0fb-f6e0-4afa-9a9c-b8d55b8f20dc
ms.openlocfilehash: ffaa8283da17c98fc58486af8dad741a61bbafc8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651373"
---
# <a name="viewing-data-in-a-datatable"></a>Exibindo dados em uma DataTable

Você pode acessar o conteúdo de um <xref:System.Data.DataTable> usando as coleções **Rows** e **Columns** da **DataTable**. Você também pode usar o <xref:System.Data.DataTable.Select%2A> método para retornar subconjuntos de dados em uma **DataTable** de acordo com os critérios, incluindo critérios de pesquisa, ordem de classificação e estado de linha. Além disso, você pode usar o <xref:System.Data.DataRowCollection.Find%2A> método de **DataRowCollection** ao pesquisar uma linha específica usando um valor de chave primária.

O método **Select** do objeto **DataTable** retorna um conjunto de <xref:System.Data.DataRow> objetos que correspondem aos critérios especificados. **Select** usa argumentos opcionais de uma expressão de filtro, expressão de classificação e **DataViewRowState**. A expressão de filtro identifica quais linhas retornar com base nos valores de **DataColumn** , como `LastName = 'Smith'` . A expressão de classificação segue as convenções padrão de SQL para ordenar colunas, por exemplo `LastName ASC, FirstName ASC`. Para regras sobre como escrever expressões, consulte a <xref:System.Data.DataColumn.Expression%2A> propriedade da classe **DataColumn** .

> [!TIP]
> Se você estiver executando várias chamadas para o método **Select** de uma **DataTable**, poderá aumentar o desempenho criando primeiro um <xref:System.Data.DataView> para a **DataTable**. A criação do **DataView** indexa as linhas da tabela. Em seguida, o método **Select** usa esse índice, reduzindo significativamente o tempo para gerar o resultado da consulta. Para obter informações sobre como criar um **DataView** para uma **DataTable**, consulte [DataViews](dataviews.md).

O método **Select** determina qual versão das linhas exibir ou manipular com base em um <xref:System.Data.DataViewRowState> . A tabela a seguir descreve os valores de enumeração **DataViewRowState** possíveis.

|Valor de DataViewRowState|Descrição|
|----------------------------|-----------------|
|**CurrentRows**|Linhas atuais, incluindo inalteradas, adicionadas e modificadas.|
|**Excluída**|Uma linha excluída.|
|**ModifiedCurrent**|A versão atual, que é uma versão modificada dos dados originais. (Consulte **ModifiedOriginal**.)|
|**ModifiedOriginal**|A versão original de todas as linhas alteradas. A versão atual está disponível usando **ModifiedCurrent**.|
|**Adicionado**|Uma nova linha.|
|**Nenhum**|Nenhum.|
|**OriginalRows**|Linhas originais, incluindo linhas inalteradas e excluídas.|
|**Inalterado**|Uma linha inalterada.|

No exemplo a seguir, o objeto **DataSet** é filtrado para que você só trabalhe com linhas cujo **DataViewRowState** está definido como **CurrentRows**.

```vb
Dim column As DataColumn
Dim row As DataRow

Dim currentRows() As DataRow = _
    workTable.Select(Nothing, Nothing, DataViewRowState.CurrentRows)

If (currentRows.Length < 1 ) Then
  Console.WriteLine("No Current Rows Found")
Else
  For Each column in workTable.Columns
    Console.Write(vbTab & column.ColumnName)
  Next

  Console.WriteLine(vbTab & "RowState")

  For Each row In currentRows
    For Each column In workTable.Columns
      Console.Write(vbTab & row(column).ToString())
    Next

    Dim rowState As String = _
        System.Enum.GetName(row.RowState.GetType(), row.RowState)
    Console.WriteLine(vbTab & rowState)
  Next
End If
```

```csharp
DataRow[] currentRows = workTable.Select(
    null, null, DataViewRowState.CurrentRows);

if (currentRows.Length < 1 )
  Console.WriteLine("No Current Rows Found");
else
{
  foreach (DataColumn column in workTable.Columns)
    Console.Write("\t{0}", column.ColumnName);

  Console.WriteLine("\tRowState");

  foreach (DataRow row in currentRows)
  {
    foreach (DataColumn column in workTable.Columns)
      Console.Write("\t{0}", row[column]);

    Console.WriteLine("\t" + row.RowState);
  }
}
```

O método **Select** pode ser usado para retornar linhas com valores de campo ou valores de **RowState** diferentes. O exemplo a seguir retorna uma matriz **DataRow** que faz referência a todas as linhas que foram excluídas e retorna outra matriz **DataRow** que faz referência a todas as linhas, ordenadas por **CustLName**, em que a coluna **CustID** é maior que 5. Para obter informações sobre como exibir as informações na linha **excluída** , consulte [Estados de linha e versões de linha](row-states-and-row-versions.md).

```vb
' Retrieve all deleted rows.
Dim deletedRows() As DataRow = workTable.Select(Nothing, Nothing, DataViewRowState.Deleted)

' Retrieve rows where CustID > 5, and order by CustLName.
Dim custRows() As DataRow = workTable.Select( _
    "CustID > 5", "CustLName ASC")
```

```csharp
// Retrieve all deleted rows.
DataRow[] deletedRows = workTable.Select(
    null, null, DataViewRowState.Deleted);

// Retrieve rows where CustID > 5, and order by CustLName.
DataRow[] custRows = workTable.Select("CustID > 5", "CustLName ASC");
```

## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataRow>
- <xref:System.Data.DataSet>
- <xref:System.Data.DataTable>
- <xref:System.Data.DataViewRowState>
- [Manipulando dados em uma DataTable](manipulating-data-in-a-datatable.md)
- [Estados de linha e versões de linha](row-states-and-row-versions.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
