---
description: 'Saiba mais sobre: Modificando dados com um DbDataAdapter'
title: Modificar dados com um DbDataAdapter
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: e35c7f9e-648b-4fcc-9361-d365c3e42c9a
ms.openlocfilehash: 749c56e8db76a469d7ebf0e503508665c2fdbd94
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786245"
---
# <a name="modifying-data-with-a-dbdataadapter"></a>Modificar dados com um DbDataAdapter

O <xref:System.Data.Common.DbProviderFactory.CreateDataAdapter%2A> método de um <xref:System.Data.Common.DbProviderFactory> objeto fornece a você um <xref:System.Data.Common.DbDataAdapter> objeto fortemente tipado para o provedor de dados subjacente especificado no momento em que você cria a fábrica. Você pode usar um <xref:System.Data.Common.DbCommandBuilder> para criar comandos para inserir, atualizar e excluir dados de um <xref:System.Data.DataSet> para uma fonte de dados.  
  
## <a name="retrieving-data-with-a-dbdataadapter"></a>Recuperando dados com um DbDataAdapter  

 Este exemplo demonstra como criar um tipo fortemente tipado `DbDataAdapter` com base em um nome de provedor e cadeia de conexão. O código usa o <xref:System.Data.Common.DbProviderFactory.CreateConnection%2A> método do <xref:System.Data.Common.DbProviderFactory> para criar um <xref:System.Data.Common.DbConnection> . Em seguida, o código usa o <xref:System.Data.Common.DbProviderFactory.CreateCommand%2A> método para criar um <xref:System.Data.Common.DbCommand> para selecionar dados definindo suas `CommandText` `Connection` Propriedades e. Por fim, o código cria um <xref:System.Data.Common.DbDataAdapter> objeto usando o <xref:System.Data.Common.DbProviderFactory.CreateDataAdapter%2A> método e define sua `SelectCommand` propriedade. O `Fill` método do `DbDataAdapter` carrega os dados em um <xref:System.Data.DataTable> .  
  
 [!code-csharp[DataWorks DbProviderFactories.DbDataAdapter#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbDataAdapter/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.DbDataAdapter#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbDataAdapter/VB/source.vb#1)]  
  
## <a name="modifying-data-with-a-dbdataadapter"></a>Modificar dados com um DbDataAdapter  

 Este exemplo demonstra como modificar dados em um `DataTable` usando um usando <xref:System.Data.Common.DbDataAdapter> um <xref:System.Data.Common.DbCommandBuilder> para gerar os comandos necessários para atualizar os dados na fonte de dados. O <xref:System.Data.Common.DbDataAdapter.SelectCommand%2A> de `DbDataAdapter` é definido para recuperar CustomerID e CompanyName da tabela Customers. O <xref:System.Data.Common.DbCommandBuilder.GetInsertCommand%2A> método é usado para definir a <xref:System.Data.Common.DbDataAdapter.InsertCommand%2A> propriedade, o <xref:System.Data.Common.DbCommandBuilder.GetUpdateCommand%2A> método é usado para definir a <xref:System.Data.Common.DbDataAdapter.UpdateCommand%2A> propriedade e o <xref:System.Data.Common.DbCommandBuilder.GetDeleteCommand%2A> método é usado para definir a <xref:System.Data.Common.DbDataAdapter.DeleteCommand%2A> propriedade. O código adiciona uma nova linha à tabela Customers e atualiza a fonte de dados. Em seguida, o código localiza a linha adicionada pesquisando no CustomerID, que é a chave primária definida para a tabela Customers. Ele altera o CompanyName e atualiza a fonte de dados. Por fim, o código exclui a linha.  
  
 [!code-csharp[DataWorks DbProviderFactories.DbDataAdapterModify#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbDataAdapterModify/CS/source.cs#1)]
 [!code-vb[DataWorks DbProviderFactories.DbDataAdapterModify#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks DbProviderFactories.DbDataAdapterModify/VB/source.vb#1)]  
  
## <a name="handling-parameters"></a>Manipulando parâmetros  

 O .NET Framework provedores de dados manipulam a nomenclatura e a especificação de parâmetros e espaços reservados de parâmetros de forma diferente. Essa sintaxe é personalizada para uma fonte de dados específica, conforme descrito na tabela a seguir.  
  
|Provedor de dados|Sintaxe de nomeação de parâmetro|  
|-------------------|-----------------------------|  
|`SqlClient`|Usa parâmetros nomeados no formato `@` *ParameterName*.|  
|`OracleClient`|Usa parâmetros nomeados no formato `:` *parmname* (ou *parmname*).|  
|`OleDb`|Usa os marcadores de parâmetros posicionais indicados por um ponto de interrogação (`?`).|  
|`Odbc`|Usa os marcadores de parâmetros posicionais indicados por um ponto de interrogação (`?`).|  
  
 O modelo de fábrica não é útil para criar `DbCommand` objetos e com parâmetros `DbDataAdapter` . Você precisará ramificar em seu código para criar parâmetros que são personalizados para seu provedor de dados.  
  
> [!IMPORTANT]
> Evitar os parâmetros específicos do provedor usando a concatenação de cadeia de caracteres para construir instruções SQL diretas não é recomendado por motivos de segurança. Usar a concatenação de cadeia de caracteres em vez de parâmetros deixa seu aplicativo vulnerável a ataques de injeção de SQL.  
  
## <a name="see-also"></a>Consulte também

- [DbProviderFactories](dbproviderfactories.md)
- [Obtendo um DbProviderFactory](obtaining-a-dbproviderfactory.md)
- [DbConnection, DbCommand e DbException](dbconnection-dbcommand-and-dbexception.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
