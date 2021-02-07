---
description: 'Saiba mais sobre: adicionando restrições existentes a um conjunto de informações'
title: Adicionar restrições existentes a um DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 307d2809-208b-4cf8-b6a9-5d16f15fc16c
ms.openlocfilehash: cad0dd1bd16747a5e76e10784d00c14cd9aa8c2a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99729566"
---
# <a name="adding-existing-constraints-to-a-dataset"></a>Adicionar restrições existentes a um DataSet

O método **Fill** do **DataAdapter** preenche um <xref:System.Data.DataSet> somente com colunas de tabela e linhas de uma fonte de dados; embora as restrições sejam normalmente definidas pela fonte de dados, o método **Fill** não adiciona essas informações de esquema ao **DataSet** por padrão. Para popular um **conjunto** de dados com informações de restrição de chave primária existentes de uma fonte, você pode chamar o método **FillSchema** do **DataAdapter** ou definir a propriedade **MissingSchemaAction** do **DataAdapter** como **AddWithKey** antes de chamar **Fill**. Isso fará com que as restrições de chave primária do **DataSet** reflitam as restrições da fonte de dados. As informações de restrição de chave estrangeira não estão incluídas e devem ser criadas explicitamente, conforme mostrado em [restrições de DataTable](./dataset-datatable-dataview/datatable-constraints.md).  
  
A adição de informações de esquema a um **DataSet** antes de preenchê-lo com os dados desejados faz com que as restrições de chave primária sejam incluídas com os objetos <xref:System.Data.DataTable> no **DataSet**. Como resultado, quando as chamadas adicionais para preencher o **DataSet** são feitas, as informações da coluna de chave primária são usadas para fazer a correspondência de novas linhas da fonte de dados com as linhas atuais de cada **DataTable**, e os dados atuais das tabelas são substituídos pelos dados da fonte de dados. Sem as informações do esquema, as novas linhas da fonte de dados são acrescentadas ao **DataSet**, resultando em linhas duplicadas.  
  
> [!NOTE]
> Se uma coluna em uma fonte de dados for identificada como incrementação automática, o método **FillSchema** ou o método **Fill** com um **MissingSchemaAction** de **AddWithKey**, criará uma **DataColumn** com uma propriedade **AutoIncrement** definida como `true` . No entanto, você precisará definir os valores de **AutoIncrementStep** e **AutoIncrementSeed** por conta própria. Para obter mais informações sobre colunas de incrementação automática, consulte [criando colunas de incremento](./dataset-datatable-dataview/creating-autoincrement-columns.md)automático.  
  
O uso do **FillSchema** ou a definição do **MissingSchemaAction** como **AddWithKey** requer processamento extra na fonte de dados para determinar as informações da coluna de chave primária. Esse processamento adicional pode prejudicar o desempenho. Se você souber as informações de chave primária em tempo de design, recomendamos especificar explicitamente a coluna (ou colunas) de chave primária, a fim de alcançar um desempenho ideal. Para obter informações sobre como definir explicitamente informações de chave primária para uma tabela, consulte [definindo chaves primárias](./dataset-datatable-dataview/defining-primary-keys.md).
  
O exemplo de código a seguir mostra como adicionar informações de esquema a um **conjunto** de dados usando **FillSchema**:
  
```vb  
Dim custDataSet As New DataSet()  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers")  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
var custDataSet = new DataSet();  
  
custAdapter.FillSchema(custDataSet, SchemaType.Source, "Customers");  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
O exemplo de código a seguir mostra como adicionar informações de esquema a um **conjunto** de dados usando a propriedade **MissingSchemaAction. AddWithKey** do método **Fill** :
  
```vb  
Dim custDataSet As New DataSet()  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey  
custAdapter.Fill(custDataSet, "Customers")  
```  
  
```csharp  
var custDataSet = new DataSet();  
  
custAdapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
custAdapter.Fill(custDataSet, "Customers");  
```  
  
## <a name="handling-multiple-result-sets"></a>Manipulando vários conjuntos de resultados  

Se o **DataAdapter** encontrar vários conjuntos de resultados retornados do **SelectCommand**, ele criará várias tabelas no **conjunto** de linhas. As tabelas receberão um nome padrão incremental partindo do zero correspondente a **Tabela** *N*, começando apenas com **Tabela** em vez de "Table0". Se um nome de tabela for passado como um argumento para o método **FillSchema** , as tabelas receberão um nome incremental com base em zero de **TableName** *N*, começando com **TableName** em vez de "TableName0".  
  
> [!NOTE]
> Se o método **FillSchema** do objeto **OleDbDataAdapter** for chamado para um comando que retorna vários conjuntos de resultados, somente as informações de esquema do primeiro conjunto de resultados serão retornadas. Ao retornar informações de esquema para vários conjuntos de resultados usando o **OleDbDataAdapter**, é recomendável que você especifique um **MissingSchemaAction** de **AddWithKey** e obtenha as informações de esquema ao chamar o método **Fill** .  
  
## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-and-datareaders.md)
- [DataSets, DataTables e DataViews](./dataset-datatable-dataview/index.md)
- [Recuperando e modificando dados no ADO.NET](retrieving-and-modifying-data.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
