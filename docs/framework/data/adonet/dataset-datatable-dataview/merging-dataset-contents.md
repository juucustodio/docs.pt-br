---
description: 'Saiba mais sobre: mesclando conteúdo do conjunto de informações'
title: Mesclando conteúdo do DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e5e9309a-3ebb-4a9c-9d78-21c4e2bafc5b
ms.openlocfilehash: bdd7184d2b3a46f8ee59a052239dcd472db5e404
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99651867"
---
# <a name="merging-dataset-contents"></a>Mesclando conteúdo do DataSet

Você pode usar o método <xref:System.Data.DataSet.Merge%2A> para mesclar o conteúdo de uma matriz <xref:System.Data.DataSet>, <xref:System.Data.DataTable> ou <xref:System.Data.DataRow> em um `DataSet` existente. Vários fatores e opções afetam a maneira como os novos dados são mesclados em um `DataSet` existente.

## <a name="primary-keys"></a>Chaves primárias

Se a tabela que recebe novos dados e esquemas de uma mesclagem tiver uma chave primária, as novas linhas de dados de entrada coincidirão com linhas existentes que tenham os mesmos valores de chave primária <xref:System.Data.DataRowVersion.Original> que nos dados de entrada. Se as colunas do esquema de entrada coincidem com as do esquema existente, os dados nas linhas existentes são modificados. As colunas que não correspondem ao esquema existente são ignoradas ou adicionadas com base no parâmetro <xref:System.Data.Common.DataAdapter.MissingSchemaAction%2A>. As novas linhas com valores de chave primária que não correspondem a linhas existentes são adicionadas à tabela existente.

Se o estado de linha das linhas novas ou existentes for <xref:System.Data.DataRowState.Added>, seus valores de chave primária serão correspondidos usando o valor de chave primária <xref:System.Data.DataRowVersion.Current> da linha `Added` pois não existe versão da linha `Original`.

Se uma tabela de entrada e uma tabela existente contiverem uma coluna com o mesmo nome, mas tipos de dados diferentes, uma exceção será gerada e o evento <xref:System.Data.DataSet.MergeFailed> de `DataSet` será gerado. Se uma tabela de entrada e uma tabela existente tiverem chaves definidas, mas as chaves primárias forem para colunas diferentes, uma exceção será gerada e o evento `MergeFailed` de `DataSet` será gerado.

Se a tabela que recebe novos dados de uma mesclagem não tem uma chave primária, as novas linhas de dados de entrada não podem coincidir com linhas existentes na tabela e são adicionadas à tabela existente.

## <a name="table-names-and-namespaces"></a>Nomes de tabela e namespaces

Os objetos <xref:System.Data.DataTable> podem opcionalmente receber um valor de propriedade <xref:System.Data.DataTable.Namespace%2A>. Quando os valores <xref:System.Data.DataTable.Namespace%2A> são atribuídos, um <xref:System.Data.DataSet> pode conter vários objetos <xref:System.Data.DataTable> com o mesmo valor <xref:System.Data.DataTable.TableName%2A>. Durante operações de mesclagem, <xref:System.Data.DataTable.TableName%2A> e <xref:System.Data.DataTable.Namespace%2A> são usados para identificar o destino de uma mesclagem. Se nenhum <xref:System.Data.DataTable.Namespace%2A> foi atribuído, somente <xref:System.Data.DataTable.TableName%2A> será usado para identificar o destino de uma mesclagem.

> [!NOTE]
> Esse comportamento mudou no .NET Framework versão 2.0. Na versão 1.1, namespaces tinham suporte, mas eram ignorados durante operações de mesclagem. Por esse motivo, um <xref:System.Data.DataSet> que usa valores de propriedade <xref:System.Data.DataTable.Namespace%2A> terá comportamentos diferentes de acordo com a versão do .NET Framework executada. Por exemplo, digamos que você tenha dois `DataSets` contendo `DataTables` com os mesmos valores de propriedade <xref:System.Data.DataTable.TableName%2A>, mas diferentes valores de propriedades <xref:System.Data.DataTable.Namespace%2A>. No .NET Framework versão 1.1, os nomes diferentes de <xref:System.Data.DataTable.Namespace%2A> serão ignorados na mesclagem dos dois objetos <xref:System.Data.DataSet>. No entanto, a partir da versão 2.0, a mesclagem leva à criação de dois novos `DataTables` no <xref:System.Data.DataSet> de destino. O `DataTables` original não será afetado pela mesclagem.

## <a name="preservechanges"></a>PreserveChanges

Quando você passa uma matriz de `DataSet`, de `DataTable` ou de `DataRow` para o método `Merge`, pode incluir parâmetros opcionais que especificam se as alterações devem ou não ser preservadas no `DataSet` existente, e como tratar novos elementos de esquema encontrados nos dados de entrada. O primeiro desses parâmetros após os dados de entrada é um sinalizador booliano, <xref:System.Data.LoadOption.PreserveChanges>, que especifica se as alterações devem ou não ser preservadas no `DataSet` existente. Se o sinalizador `PreserveChanges` estiver definido como `true`, os valores de entrada não substituirão os valores existentes na versão de linha `Current` da linha existente. Se o sinalizador `PreserveChanges` estiver definido como `false`, os valores de entrada substituirão os valores existentes na versão de linha `Current` da linha existente. Se o sinalizador `PreserveChanges` não for especificado, ele será definido como `false` por padrão. Para obter mais informações sobre versões de linha, consulte [Estados de linha e versões de linha](row-states-and-row-versions.md).

Quando `PreserveChanges` é `true`, os dados da linha existente são mantidos na versão de linha <xref:System.Data.DataRowVersion.Current> da linha existente, enquanto os dados da versão de linha <xref:System.Data.DataRowVersion.Original> da linha existente são substituídos pelos dados da versão de linha `Original` da nova linha. O <xref:System.Data.DataRow.RowState%2A> da linha existente é definido como <xref:System.Data.DataRowState.Modified>. As seguintes exceções se aplicam:

- Se a linha existente tem um `RowState` de `Deleted`, este `RowState` permanece `Deleted` e não é definido como `Modified`. Nesse caso, os dados da nova linha ainda serão armazenados na versão de linha `Original` da linha existente, substituindo a versão de linha `Original` da linha existente (a menos que a nova linha tenha um `RowState` de `Added`).

- Se a nova linha tem `RowState` de `Added`, os dados da versão de linha `Original` da linha existente não serão substituídos pelos dados da nova linha, pois a nova linha não tem uma versão de linha `Original`.

Quando `PreserveChanges` é `false`, as versões de linha `Current` e `Original` na linha existente são substituídas pelos dados da nova linha, e `RowState` da linha existente é definido como o `RowState` da nova linha. As seguintes exceções se aplicam:

- Se a nova linha tem um `RowState` de `Unchanged` e a linha existente tem um `RowState` de `Modified`, de `Deleted` ou de `Added`, o `RowState` da linha existente é definido como `Modified`.

- Se a nova linha tem um `RowState` de `Added` e a linha existente tem um `RowState` de `Unchanged`, de `Modified` ou de `Deleted`, o `RowState` da linha existente é definido como `Modified`. Além disso, os dados da versão de linha `Original` da linha existente não são substituídos pelos dados da nova linha, pois a nova linha não tem uma versão de linha `Original`.

## <a name="missingschemaaction"></a>MissingSchemaAction

Você pode usar o parâmetro opcional <xref:System.Data.MissingSchemaAction> do método `Merge` para especificar como `Merge` tratará os elementos de esquema nos dados de entrada que não fazem parte do `DataSet` existente.

A tabela a seguir descreve as opções de `MissingSchemaAction`.

|Opção MissingSchemaAction|Descrição|
|--------------------------------|-----------------|
|<xref:System.Data.MissingSchemaAction.Add>|Adicionar as novas informações de esquema ao `DataSet` e preencher as novas colunas com os valores de entrada. Este é o padrão.|
|<xref:System.Data.MissingSchemaAction.AddWithKey>|Adicionar as novas informações de esquema e de chave primária ao `DataSet` e preencher as novas colunas com os valores de entrada.|
|<xref:System.Data.MissingSchemaAction.Error>|Gere uma exceção se forem encontradas informações de esquema incompatíveis.|
|<xref:System.Data.MissingSchemaAction.Ignore>|Ignorar as novas informações do esquema.|

## <a name="constraints"></a>Restrições

Com o método `Merge`, as restrições não são verificadas até que todos os novos dados sejam adicionados ao `DataSet` existente. Após a adição dos dados, as restrições são impostas nos valores atuais no `DataSet`. Você deve garantir que seu código trate quaisquer exceções que possam ser geradas por causa de violações de restrição.

Considere um caso onde uma linha existente em um `DataSet` seja uma linha `Unchanged` com um valor de chave primária de 1. Durante uma operação de mesclagem com uma nova linha `Modified` com um valor de chave primária `Original` de 2 e um valor de chave primária `Current` de 1, a linha existente e a nova linha não são consideradas coincidentes porque os valores de chave primária `Original` diferem. Entretanto, quando a mesclagem é concluída e restrições são verificadas, uma exceção é gerada pois os valores de chave primária `Current` violam a restrição exclusiva para a coluna de chave primária.

> [!NOTE]
> Quando linhas são inseridas em uma tabela de banco de dados contendo uma coluna de incremento automático, como uma coluna de identidade, o valor da coluna de identidade retornado pela inserção talvez não corresponda ao valor no `DataSet`, causando as linhas retornados a serem adicionadas, e não mescladas. Para obter mais informações, consulte [recuperando identidade ou valores de numeração automática](../retrieving-identity-or-autonumber-values.md).

O exemplo de código a seguir mescla dois `DataSet` objetos com esquemas diferentes em um `DataSet` com os esquemas combinados dos dois objetos de entrada `DataSet` .

[!code-csharp[DataWorks DataSet.Merge#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.Merge/CS/source.cs#1)]
[!code-vb[DataWorks DataSet.Merge#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.Merge/VB/source.vb#1)]

O exemplo de código a seguir usa um `DataSet` existente com atualizações e passa essas atualizações para um `DataAdapter` a serem processadas na fonte de dados. Os resultados são mesclados no `DataSet` original. Após a rejeição das alterações que resultaram em um erro, as alterações mescladas são confirmadas com `AcceptChanges`.

[!code-csharp[DataWorks DataSet.MergeAcceptChanges#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/CS/source.cs#1)]
[!code-vb[DataWorks DataSet.MergeAcceptChanges#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/VB/source.vb#1)]

[!code-csharp[DataWorks DataSet.MergeAcceptChanges#2](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/CS/source.cs#2)]
[!code-vb[DataWorks DataSet.MergeAcceptChanges#2](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DataSet.MergeAcceptChanges/VB/source.vb#2)]

## <a name="see-also"></a>Consulte também

- [DataSets, DataTables e DataViews](index.md)
- [Estados de linha e versões de linha](row-states-and-row-versions.md)
- [DataAdapters e DataReaders](../dataadapters-and-datareaders.md)
- [Recuperando e modificando dados no ADO.NET](../retrieving-and-modifying-data.md)
- [Recuperando identidade ou valores de Autonumber](../retrieving-identity-or-autonumber-values.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
