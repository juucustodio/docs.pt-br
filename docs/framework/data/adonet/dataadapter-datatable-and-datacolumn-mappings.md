---
description: 'Saiba mais sobre: DataAdapter DataTable e os mapeamentos de DataColumn'
title: Mapeamentos de DataTable e de DataColumn do DataAdapter
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: d023260a-a66a-4c39-b8f4-090cd130e730
ms.openlocfilehash: 25007925afa57dd0cb6e75f808444f1bfaeea9b1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739723"
---
# <a name="dataadapter-datatable-and-datacolumn-mappings"></a>Mapeamentos de DataTable e de DataColumn do DataAdapter

Um **DataAdapter** contém uma coleção de zero ou mais <xref:System.Data.Common.DataTableMapping> objetos em sua propriedade **TableMappings** . Um **DataTableMapping** fornece um mapeamento mestre entre os dados retornados de uma consulta em relação a uma fonte de dados e um <xref:System.Data.DataTable> . O nome de **DataTableMapping** pode ser passado no lugar do nome **DataTable** para o método **Fill** do **DataAdapter**. O exemplo a seguir cria um **DataTableMapping** denominado **AuthorsMapping** para a tabela **Authors**.  
  
```vb  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors")  
```  
  
```csharp  
workAdapter.TableMappings.Add("AuthorsMapping", "Authors");  
```  
  
 Um **DataTableMapping** permite que você use nomes de colunas em um **DataTable** que sejam diferentes daqueles do banco de dados. O **DataAdapter** usa o mapeamento para corresponder as colunas quando a tabela é atualizada.  
  
 Se você não especificar um **TableName** ou um nome de **DataTableMapping** ao chamar o método **Fill** ou **Update** do **DataAdapter**, o **DataAdapter** vai procurar o **DataTableMapping** denominado "Table". Se esse **DataTableMapping** não existir, o **TableName** da **DataTable** será "Table". Você pode especificar um **DataTableMapping** padrão criando um **DataTableMapping** com o nome de "Table".  
  
 O exemplo de código a seguir cria um **DataTableMapping** (do namespace <xref:System.Data.Common>) e o transforma no mapeamento padrão para o **DataAdapter** especificado, nomeando-o como "Table". Em seguida, o exemplo mapeia as colunas da primeira tabela no resultado da consulta (a tabela **Customers** do banco de dados **Northwind**) para um conjunto de nomes mais amigáveis na tabela **Northwind Customers** no <xref:System.Data.DataSet>. Para colunas que não são mapeadas, o nome da coluna na fonte de dados é usado.  
  
```vb  
Dim mapping As DataTableMapping = _  
  adapter.TableMappings.Add("Table", "NorthwindCustomers")  
mapping.ColumnMappings.Add("CompanyName", "Company")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode")  
  
adapter.Fill(custDS)  
```  
  
```csharp  
DataTableMapping mapping =
  adapter.TableMappings.Add("Table", "NorthwindCustomers");  
mapping.ColumnMappings.Add("CompanyName", "Company");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIPCode");  
  
adapter.Fill(custDS);  
```  
  
 Em situações mais avançadas, você pode decidir que deseja que o mesmo **DataAdapter** dê suporte ao carregamento de diferentes tabelas com diferentes mapeamentos. Para fazer isso, basta adicionar outros objetos **DataTableMapping** .  
  
 Quando o método **Fill** recebe uma instância de **DataSet** e um nome de **DataTableMapping**, se existir um mapeamento com esse nome, ele será usado. Caso contrário, um **DataTable** com esse nome será usado.  
  
 Os exemplos a seguir criam um **DataTableMapping** com um nome de **Customers** e um nome de **DataTable** de **BizTalkSchema**. Em seguida, o exemplo mapeia as linhas retornadas pela instrução SELECT ao **DataTable** do **BizTalkSchema**.  
  
```vb  
Dim mapping As ITableMapping = _  
  adapter.TableMappings.Add("Customers", "BizTalkSchema")  
mapping.ColumnMappings.Add("CustomerID", "ClientID")  
mapping.ColumnMappings.Add("CompanyName", "ClientName")  
mapping.ColumnMappings.Add("ContactName", "Contact")  
mapping.ColumnMappings.Add("PostalCode", "ZIP")  
  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
ITableMapping mapping =
  adapter.TableMappings.Add("Customers", "BizTalkSchema");  
mapping.ColumnMappings.Add("CustomerID", "ClientID");  
mapping.ColumnMappings.Add("CompanyName", "ClientName");  
mapping.ColumnMappings.Add("ContactName", "Contact");  
mapping.ColumnMappings.Add("PostalCode", "ZIP");  
  
adapter.Fill(custDS, "Customers");  
```  
  
> [!NOTE]
> Se o nome de uma coluna de origem não for fornecido para um mapeamento de coluna ou se o nome de uma tabela de origem não for fornecido para um mapeamento de tabela, os nomes padrão serão gerados automaticamente. Se nenhuma coluna de origem for fornecida para um mapeamento de coluna, o mapeamento de coluna receberá um nome padrão incremental de **SourceColumn** *N,* começando com **SourceColumn1**. Se nenhum nome de tabela de origem for fornecido para um mapeamento de tabela, o mapeamento de tabela receberá um nome padrão incremental de **SourceTable** *N*, começando com **SourceTable1**.  
  
> [!NOTE]
> É recomendável evitar a convenção de nomenclatura de **SourceColumn** *N* para um mapeamento de coluna ou **SourceTable** *N* para um mapeamento de tabela, porque o nome que você fornece pode entrar em conflito com um nome padrão de mapeamento de coluna existente no **ColumnMappingCollection** ou um nome de mapeamento de tabela existente no **DataTableMappingCollection**. Se o nome fornecido já existir, será gerada uma exceção.  
  
## <a name="handling-multiple-result-sets"></a>Manipulando vários conjuntos de resultados  

 Se o comando **SelectCommand** retornar várias tabelas, o **Fill** vai gerar automaticamente nomes de tabelas com valores incrementais para as tabelas do **DataSet**, começando com o nome da tabela especificado e continuando no formato **TableName** *N*, começando com **TableName1**. Você pode usar mapeamentos de tabela para mapear o nome de tabela gerado automaticamente para um nome que você deseja especificado para a tabela no **DataSet**. Por exemplo, para um **SelectCommand** que retorne duas tabelas, **Customers** e **Orders**, emita a seguinte chamada para **Fill**.  
  
```vb  
adapter.Fill(customersDataSet, "Customers")  
```  

```csharp  
adapter.Fill(customersDataSet, "Customers");  
```  

 Duas tabelas são criadas no **DataSet**: **Customers** e **Customers1**. Você pode usar mapeamentos de tabela para que a segunda tabela seja denominada **Orders** em vez de **Customers1**. Para fazer isso, mapeie a tabela de origem de **Customers1** para a tabela do **DataSet** **Orders**, conforme mostrado no exemplo a seguir.  
  
```vb  
adapter.TableMappings.Add("Customers1", "Orders")  
adapter.Fill(customersDataSet, "Customers")  
```  

```csharp  
adapter.TableMappings.Add("Customers1", "Orders");  
adapter.Fill(customersDataSet, "Customers");  
```
  
## <a name="see-also"></a>Confira também

- [DataAdapters e DataReaders](dataadapters-and-datareaders.md)
- [Recuperando e modificando dados no ADO.NET](retrieving-and-modifying-data.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
