---
description: 'Saiba mais sobre: definindo chaves primárias'
title: Definir chaves primárias
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 2ea85959-e763-4669-8bd9-46a9dab894bd
ms.openlocfilehash: 2becfbd124af723f55edb39666352fc501044045
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99652543"
---
# <a name="defining-primary-keys"></a>Definir chaves primárias

Uma tabela de banco de dados normalmente tem uma coluna ou grupo de colunas que identifica exclusivamente cada linha na tabela. Essa coluna de identificação ou grupo de colunas é chamada de chave primária.  
  
 Quando você identifica um único <xref:System.Data.DataColumn> como o <xref:System.Data.DataTable.PrimaryKey%2A> para um <xref:System.Data.DataTable> , a tabela define automaticamente a <xref:System.Data.DataColumn.AllowDBNull%2A> propriedade da coluna como **false** e a <xref:System.Data.DataColumn.Unique%2A> propriedade como **true**. Para chaves primárias de várias colunas, somente a propriedade **AllowDBNull** é definida automaticamente como **false**.  
  
 A propriedade **PrimaryKey** de um <xref:System.Data.DataTable> recebe como seu valor uma matriz de um ou mais objetos **DataColumn** , conforme mostrado nos exemplos a seguir. O primeiro exemplo define uma única coluna como a chave primária.  
  
```vb  
workTable.PrimaryKey = New DataColumn() {workTable.Columns("CustID")}  
  
' Or  
  
Dim columns(1) As DataColumn  
columns(0) = workTable.Columns("CustID")  
workTable.PrimaryKey = columns  
```  
  
```csharp  
workTable.PrimaryKey = new DataColumn[] {workTable.Columns["CustID"]};  
  
// Or  
  
DataColumn[] columns = new DataColumn[1];  
columns[0] = workTable.Columns["CustID"];  
workTable.PrimaryKey = columns;  
```  
  
 O exemplo a seguir define duas colunas como uma chave primária.  
  
```vb  
workTable.PrimaryKey = New DataColumn() {workTable.Columns("CustLName"), _  
                                         workTable.Columns("CustFName")}  
  
' Or  
  
Dim keyColumn(2) As DataColumn  
keyColumn(0) = workTable.Columns("CustLName")  
keyColumn(1) = workTable.Columns("CustFName")  
workTable.PrimaryKey = keyColumn  
```  
  
```csharp  
workTable.PrimaryKey = new DataColumn[] {workTable.Columns["CustLName"],
                                         workTable.Columns["CustFName"]};  
  
// Or  
  
DataColumn[] keyColumn = new DataColumn[2];  
keyColumn[0] = workTable.Columns["CustLName"];  
keyColumn[1] = workTable.Columns["CustFName"];  
workTable.PrimaryKey = keyColumn;  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataTable>
- [Definição do esquema de DataTable](datatable-schema-definition.md)
- [DataTables](datatables.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
