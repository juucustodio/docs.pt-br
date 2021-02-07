---
description: 'Saiba mais sobre: criando colunas de incremento automático'
title: Criar colunas AutoIncrement
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: cf09732a-ab54-4d98-89e2-4d0a1f28fbce
ms.openlocfilehash: 7568b1013b7af5aef7a6fc1f28dc163a082743a7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739632"
---
# <a name="creating-autoincrement-columns"></a>Criar colunas AutoIncrement

Para garantir valores de coluna exclusivos, você pode definir os valores de coluna para incrementar automaticamente quando novas linhas forem adicionadas à tabela. Para criar um incremento automático <xref:System.Data.DataColumn> , defina a <xref:System.Data.DataColumn.AutoIncrement%2A> propriedade da coluna como **true**. <xref:System.Data.DataColumn>Em seguida, começa com o valor definido na <xref:System.Data.DataColumn.AutoIncrementSeed%2A> propriedade e, com cada linha adicionada, o valor da coluna **AutoIncrement** aumenta pelo valor definido na <xref:System.Data.DataColumn.AutoIncrementStep%2A> propriedade da coluna.  
  
 Para colunas de **incremento automático** , recomendamos que a <xref:System.Data.DataColumn.ReadOnly%2A> propriedade de **DataColumn** seja definida como **true**.  
  
 O exemplo a seguir demonstra como criar uma coluna que começa com um valor de 200 e adiciona incrementalmente em etapas de 3.  
  
```vb  
Dim workColumn As DataColumn = workTable.Columns.Add( _  
    "CustomerID", typeof(Int32))  
workColumn.AutoIncrement = true  
workColumn.AutoIncrementSeed = 200  
workColumn.AutoIncrementStep = 3  
```  
  
```csharp  
DataColumn workColumn = workTable.Columns.Add(  
    "CustomerID", typeof(Int32));  
workColumn.AutoIncrement = true;  
workColumn.AutoIncrementSeed = 200;  
workColumn.AutoIncrementStep = 3;  
```  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Data.DataColumn>
- [Definição do esquema de DataTable](datatable-schema-definition.md)
- [DataTables](datatables.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
