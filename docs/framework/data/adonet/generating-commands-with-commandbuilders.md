---
description: 'Saiba mais sobre: gerando comandos com CommandBuilders'
title: Gerando comandos com CommandBuilders
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 6e3fb8b5-373b-4f9e-ab03-a22693df8e91
ms.openlocfilehash: 495312f57d497421182384eff23b621130447940
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724096"
---
# <a name="generating-commands-with-commandbuilders"></a>Gerando comandos com CommandBuilders

Quando a propriedade `SelectCommand` é especificada dinamicamente em tempo de execução, como através de uma ferramenta de consulta que usa um comando textual do usuário, você não poderá especificar o `InsertCommand`, `UpdateCommand` ou `DeleteCommand` apropriado em tempo de design. Se seu <xref:System.Data.DataTable> mapear para ou for gerado a partir de uma única tabela do banco de dados, você poderá aproveitar o objeto <xref:System.Data.Common.DbCommandBuilder> para gerar automaticamente o `DeleteCommand`, `InsertCommand` e `UpdateCommand` do <xref:System.Data.Common.DbDataAdapter>.  
  
 Como um requisito mínimo, você deverá definir a propriedade `SelectCommand` para que a geração automática de comando funcione. O esquema da tabela recuperado pela propriedade `SelectCommand` determina a sintaxe das instruções INSERT, UPDATE e DELETE geradas automaticamente.  
  
 O <xref:System.Data.Common.DbCommandBuilder> deve executar o `SelectCommand` na ordem para retornar os metadados necessários para construir os comandos SQL INSERT, UPDATE e DELETE. Como resultado, uma viagem extra à fonte de dados é necessária e isso pode comprometer o desempenho. Para obter o desempenho ideal, especifique seus comandos explicitamente em vez de usar o <xref:System.Data.Common.DbCommandBuilder>.  
  
 O `SelectCommand` também deve retornar pelo menos uma chave primária ou coluna exclusivo. Se nenhum estiver presente, uma exceção de `InvalidOperation` será gerada e os comandos não serão gerados.  
  
 Quando estiver associado com um `DataAdapter`, o <xref:System.Data.Common.DbCommandBuilder> gera automaticamente as propriedades `InsertCommand`, `UpdateCommand` e `DeleteCommand` do `DataAdapter` se forem referências nulas. Se um `Command` já existir para uma propriedade, o `Command` existente será usado.  
  
 As exibições de banco de dados que são criadas juntando duas ou mais tabelas não são consideradas uma única tabela de banco de dados. Nesse caso, você não pode usar o <xref:System.Data.Common.DbCommandBuilder> para gerar comandos automaticamente; você deve especificar seus comandos explicitamente. Para obter informações sobre como definir explicitamente os comandos para resolver atualizações de `DataSet` volta para a fonte de dados, consulte [Atualizando fontes de dados com dataadaptadores](updating-data-sources-with-dataadapters.md).  
  
 Você pode desejar mapear parâmetros de saída de volta para a linha atualizada de um `DataSet`. Uma tarefa comum é recuperar o valor de um campo de identidade ou um carimbo de data/hora gerado automaticamente da fonte de dados. O <xref:System.Data.Common.DbCommandBuilder> não mapeará parâmetros de saída para colunas em uma linha atualizada por padrão. Nesse caso, você deve especificar explicitamente o comando. Para obter um exemplo de mapeamento de um campo de identidade gerado automaticamente de volta para uma coluna de uma linha inserida, consulte [recuperando identidade ou valores autonumerados](retrieving-identity-or-autonumber-values.md).  
  
## <a name="rules-for-automatically-generated-commands"></a>Regras comandos gerados automaticamente  

 A tabela a seguir mostra as regras para como os comandos gerados automaticamente são gerados.  
  
|Comando|Regra|  
|-------------|----------|  
|`InsertCommand`|Insere uma linha na fonte de dados para todas as linhas na tabela com um <xref:System.Data.DataRow.RowState%2A> de <xref:System.Data.DataRowState.Added>. Insere valores para todas as colunas que são atualizáveis (mas não colunas como identidades, expressões ou carimbos de data/hora).|  
|`UpdateCommand`|Atualiza linhas na fonte de dados para todas as linhas na tabela com um `RowState` de <xref:System.Data.DataRowState.Modified>. Atualiza os valores de todas as colunas exceto as que não são atualizáveis, como identidades ou expressões. Atualiza todas as linhas onde os valores de coluna na fonte de dados correspondem aos valores de coluna de chave primária da linha, e onde as colunas restantes na fonte de dados correspondem aos valores originais da linha. Para obter mais informações, consulte “Modelo de simultaneidade otimista para atualizações e exclusões”, posteriormente neste tópico.|  
|`DeleteCommand`|Exclui linhas na fonte de dados para todas as linhas na tabela com um `RowState` de <xref:System.Data.DataRowState.Deleted>. Exclui todas as linhas onde os valores de coluna correspondem aos valores de coluna de chave primária da linha, e onde as colunas restantes na fonte de dados correspondem aos valores originais da linha. Para obter mais informações, consulte “Modelo de simultaneidade otimista para atualizações e exclusões”, posteriormente neste tópico.|  
  
## <a name="optimistic-concurrency-model-for-updates-and-deletes"></a>Modelo de simultaneidade otimista para atualizações e exclusões  

 A lógica para gerar comandos automaticamente para instruções UPDATE e DELETE baseia-se na *simultaneidade otimista*, ou seja, os registros não são bloqueados para edição e podem ser modificados por outros usuários ou processos a qualquer momento. Como um registro pode ter sido modificado após ter sido retornado da instrução SELECT, mas antes de a instrução UPDATE ou DELETE ser emitida, a instrução UPDATE ou DELETE gerada automaticamente contém uma cláusula WHERE, especificando que uma linha estará atualizada apenas se contiver todos os valores originais e não tiver sido excluída da fonte de dados. Isso é feito para evitar sobrescrever novos dados. Onde uma atualização gerada automaticamente tentar atualizar uma linha que foi excluída ou que não contém os valores originais localizados no <xref:System.Data.DataSet>, o comando não afetará nenhum registro e uma <xref:System.Data.DBConcurrencyException> será gerada.  
  
 Se você desejar que a instrução UPDATE ou DELETE seja concluída independentemente dos valores originais, você deverá definir explicitamente o `UpdateCommand` para o `DataAdapter` e não depender da geração de comando automática.  
  
## <a name="limitations-of-automatic-command-generation-logic"></a>Limitações da lógica de geração automática de comando  

 As seguintes limitações aplicam-se à geração automática de comando.  
  
### <a name="unrelated-tables-only"></a>Somente tabelas não relacionadas  

 A lógica de geração automática de comando gera instruções INSERT, UPDATE ou DELETE para tabelas autônomas sem levar em consideração as relações com outras tabelas em uma fonte de dados. Como resultado, você pode encontrar uma falha ao chamar `Update` para enviar alterações para uma coluna que participa em uma restrição de chave estrangeira no banco de dados. Para evitar essa exceção, não use o <xref:System.Data.Common.DbCommandBuilder> para atualizar as colunas envolvidas em uma restrição de chave estrangeira; em vez disso, especifique explicitamente as instruções usadas para executar a operação.  
  
### <a name="table-and-column-names"></a>Nomes de tabelas e colunas  

 A lógica da geração automática de comando poderá falhar se os nomes de colunas ou tabelas contiverem algum caractere especial, como espaços, pontos, aspas ou outros caracteres não alfanuméricos, mesmo se estiver limitado por colchetes. Dependendo do provedor, definir os parâmetros QuotePrefix e QuoteSuffix pode permitir que a lógica de geração processe os espaços, mas não será possível substituir caracteres especiais. Os nomes de tabela totalmente qualificados na forma de *catalog.schema.table* têm suporte.  
  
## <a name="using-the-commandbuilder-to-automatically-generate-an-sql-statement"></a>Usando o CommandBuilder para gerar automaticamente uma instrução SQL  

 Para gerar automaticamente as instruções SQL para um `DataAdapter`, primeiro defina a propriedade `SelectCommand` de `DataAdapter`, em seguida, crie um objeto `CommandBuilder` e especifique como argumento o `DataAdapter` para o qual o `CommandBuilder` gerará instruções SQL automaticamente.  
  
```vb  
' Assumes that connection is a valid SqlConnection object
' inside of a Using block.  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers", connection)  
Dim builder As SqlCommandBuilder = New SqlCommandBuilder(adapter)  
builder.QuotePrefix = "["  
builder.QuoteSuffix = "]"  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object  
// inside of a using block.  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers", connection);  
SqlCommandBuilder builder = new SqlCommandBuilder(adapter);  
builder.QuotePrefix = "[";  
builder.QuoteSuffix = "]";  
```  
  
## <a name="modifying-the-selectcommand"></a>Alterando o SelectCommand  

 Se você alterar o `CommandText` do `SelectCommand` após os comandos INSERT, UPDATE ou DELETE terem sido gerados automaticamente, uma exceção poderá ocorrer. Se o `SelectCommand.CommandText` modificado contiver informações de esquema que forem inconsistentes com o `SelectCommand.CommandText` usado quando os comandos de inserção, atualização ou exclusão foram gerados automaticamente, as chamadas futuras para o método `DataAdapter.Update` poderão tentar acessar as colunas que não existem mais na tabela atual referenciada pelo `SelectCommand` e uma exceção será gerada.  
  
 Você pode atualizar as informações de esquema usadas pelo `CommandBuilder` para gerar automaticamente comandos chamando o método `RefreshSchema` do `CommandBuilder`.  
  
 Se você quiser saber qual comando foi gerado automaticamente, poderá obter uma referência para comandos gerados automaticamente usando os métodos `GetInsertCommand`, `GetUpdateCommand` e `GetDeleteCommand` do objeto `CommandBuilder` e verificando a propriedade `CommandText` do comando associado.  
  
 O exemplo de código a seguir grava no console o comando de atualização que foi gerado automaticamente.  
  
```vb
Console.WriteLine(builder.GetUpdateCommand().CommandText)  
```

```csharp
Console.WriteLine(builder.GetUpdateCommand().CommandText);
```
  
 O exemplo a seguir recria a tabela `Customers` no conjunto de dados do `custDS`. O método **RefreshSchema** é chamado para atualizar os comandos gerados automaticamente com as informações dessa nova coluna.  
  
```vb  
' Assumes an open SqlConnection and SqlDataAdapter inside of a Using block.  
adapter.SelectCommand.CommandText = _  
  "SELECT CustomerID, ContactName FROM dbo.Customers"  
builder.RefreshSchema()  
  
custDS.Tables.Remove(custDS.Tables("Customers"))  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
// Assumes an open SqlConnection and SqlDataAdapter inside of a using block.  
adapter.SelectCommand.CommandText =
  "SELECT CustomerID, ContactName FROM dbo.Customers";  
builder.RefreshSchema();  
  
custDS.Tables.Remove(custDS.Tables["Customers"]);  
adapter.Fill(custDS, "Customers");  
```  
  
## <a name="see-also"></a>Confira também

- [Comandos e parâmetros](commands-and-parameters.md)
- [Executando um comando](executing-a-command.md)
- [DbConnection, DbCommand e DbException](dbconnection-dbcommand-and-dbexception.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
