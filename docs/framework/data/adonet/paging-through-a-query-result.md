---
description: 'Saiba mais sobre: paginação por meio de um resultado de consulta'
title: Paginação por um resultado de consulta
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
ms.openlocfilehash: ead2c74e19cfb81c83c7bf1e73b0c0d7a0a7cc67
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99672355"
---
# <a name="paging-through-a-query-result"></a>Paginação por um resultado de consulta

A paginação por meio de um resultado de consulta é o processo de retornar os resultados de uma consulta em subconjuntos menores de dados ou páginas. Essa é uma prática comum a fim de exibir os resultados para um usuário em partes pequenas e fáceis de gerenciar.  
  
 O **DataAdapter** fornece um recurso para retornar apenas uma página de dados, por meio de sobrecargas do método **Fill** . No entanto, essa pode não ser a melhor opção para paginar grandes resultados de consulta porque, embora o **DataAdapter** preencha o <xref:System.Data.DataTable> de destino ou o <xref:System.Data.DataSet> apenas com os registros solicitados, ainda serão usados os recursos para retornar a consulta inteira. Para retornar uma página de dados de uma fonte de dados sem usar os recursos para retornar a consulta inteira, especifique critérios adicionais na consulta que reduzam as linhas retornadas para apenas aquelas necessárias.  
  
 Para usar o método **Fill** para retornar uma página de dados, especifique um parâmetro **startRecord** , para o primeiro registro na página de dados e um parâmetro **MaxRecords** , para o número de registros na página de dados.  
  
 O exemplo de código a seguir mostra como usar o método **Fill** para retornar a primeira página de um resultado de consulta em que o tamanho da página é cinco registros.  
  
```vb  
Dim currentIndex As Integer = 0  
Dim pageSize As Integer = 5  
  
Dim orderSQL As String = "SELECT * FROM dbo.Orders ORDER BY OrderID"  
' Assumes that connection is a valid SqlConnection object.  
Dim adapter As SqlDataAdapter = _  
  New SqlDataAdapter(orderSQL, connection)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders")  
```  
  
```csharp  
int currentIndex = 0;  
int pageSize = 5;  
  
string orderSQL = "SELECT * FROM Orders ORDER BY OrderID";  
// Assumes that connection is a valid SqlConnection object.  
SqlDataAdapter adapter = new SqlDataAdapter(orderSQL, connection);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders");  
```  
  
 No exemplo anterior, o **DataSet** é preenchido apenas com cinco registros, mas a tabela **Orders** inteira é retornada. Para preencher o **conjunto** de um com os mesmos cinco registros, mas retornar apenas cinco registros, use as cláusulas Top e WHERE na sua instrução SQL, como no exemplo de código a seguir.  
  
```vb  
Dim pageSize As Integer = 5  
  
Dim orderSQL As String = "SELECT TOP " & pageSize & _  
  " * FROM Orders ORDER BY OrderID"  
Dim adapter As SqlDataAdapter = _  
  New SqlDataAdapter(orderSQL, connection)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, "Orders")
```  
  
```csharp  
int pageSize = 5;  
  
string orderSQL = "SELECT TOP " + pageSize +
  " * FROM Orders ORDER BY OrderID";  
SqlDataAdapter adapter = new SqlDataAdapter(orderSQL, connection);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "Orders");  
```  
  
 Observe que, ao paginar os resultados da consulta dessa forma, você deve preservar o identificador exclusivo que ordena as linhas, a fim de passar a ID exclusiva para o comando para retornar a próxima página de registros, conforme mostrado no exemplo de código a seguir.  
  
```vb  
Dim lastRecord As String = _  
  dataSet.Tables("Orders").Rows(pageSize - 1)("OrderID").ToString()  
```  
  
```csharp  
string lastRecord =
  dataSet.Tables["Orders"].Rows[pageSize - 1]["OrderID"].ToString();  
```  
  
 Para retornar a próxima página de registros usando a sobrecarga do método **Fill** que usa os parâmetros **startRecord** e **MaxRecords** , aumente o índice do registro atual pelo tamanho da página e preencha a tabela. Lembre-se de que o servidor de banco de dados retorna todos os resultados da consulta, muito embora apenas uma página de registros seja adicionada ao **DataSet**. No exemplo de código a seguir, as linhas da tabela são limpas antes de serem preenchidas com a próxima página de dados. Talvez você queira preservar um determinado número de linhas retornadas em um cache local a fim de reduzir os acessos ao servidor de banco de dados.  
  
```vb  
currentIndex = currentIndex + pageSize  
  
dataSet.Tables("Orders").Rows.Clear()  
  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders")  
```  
  
```csharp  
currentIndex += pageSize;  
  
dataSet.Tables["Orders"].Rows.Clear();  
  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders");  
```  
  
 Para retornar a próxima página de registros sem que o servidor de banco de dados precise retornar a consulta inteira, especifique critérios restritivos na instrução SELECT. Como o exemplo anterior preservava o último registro retornado, você pode usá-lo na cláusula WHERE a fim de especificar um ponto de partida para a consulta, conforme mostrado no exemplo de código a seguir.  
  
```vb  
orderSQL = "SELECT TOP " & pageSize & _  
  " * FROM Orders WHERE OrderID > " & lastRecord & " ORDER BY OrderID"  
adapter.SelectCommand.CommandText = orderSQL  
  
dataSet.Tables("Orders").Rows.Clear()  
  
adapter.Fill(dataSet, "Orders")  
```  
  
```csharp  
orderSQL = "SELECT TOP " + pageSize +
  " * FROM Orders WHERE OrderID > " + lastRecord + " ORDER BY OrderID";  
adapter.SelectCommand.CommandText = orderSQL;  
  
dataSet.Tables["Orders"].Rows.Clear();  
  
adapter.Fill(dataSet, "Orders");  
```  
  
## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-and-datareaders.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
