---
title: Comandos e parâmetros
description: Saiba como usar objetos de comando para cada provedor de dados de .NET Framework para executar comandos e retornar resultados de uma fonte de dados.
ms.date: 03/30/2017
ms.assetid: b623f810-d871-49a5-b0f5-078cc3c34db6
ms.openlocfilehash: fb7b86dc3c826805e0e1dcec4764be2e484ec40b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91203820"
---
# <a name="commands-and-parameters"></a>Comandos e parâmetros

Depois de estabelecer uma conexão a uma fonte de dados, você pode executar comandos e retornar resultados da fonte de dados usando um objeto <xref:System.Data.Common.DbCommand>. Você pode criar um comando usando um dos construtores de comando do provedor de dados .NET Framework com o qual está trabalhando. Os construtores podem usar argumentos opcionais, como uma instrução SQL para executar na fonte de dados, em um objeto <xref:System.Data.Common.DbConnection> ou em um objeto <xref:System.Data.Common.DbTransaction>. Você também pode configurar esses objetos como propriedades do comando. Pode também criar um comando para uma conexão específica usando o método <xref:System.Data.Common.DbConnection.CreateCommand%2A> de um objeto `DbConnection`. A instrução SQL que está sendo executada pelo comando pode ser configurada usando a propriedade <xref:System.Data.Common.DbCommand.CommandText%2A>.  
  
 Cada provedor de dados .NET Framework incluído com o .NET Framework tem um objeto `Command`. O Provedor de Dados .NET Framework para OLE DB inclui um objeto <xref:System.Data.OleDb.OleDbCommand>, o Provedor de Dados .NET Framework para SQL Server inclui um objeto <xref:System.Data.SqlClient.SqlCommand>, o Provedor de Dados .NET Framework para ODBC inclui um objeto <xref:System.Data.Odbc.OdbcCommand> e o Provedor de Dados .NET Framework para Oracle inclui um objeto <xref:System.Data.OracleClient.OracleCommand>.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Executando um comando](executing-a-command.md)  
 Descreve o objeto `Command` ADO.NET e como usá-lo para executar consultas e comandos em uma fonte de dados.  
  
 [Configurar parâmetros e tipos de dados de parâmetro](configuring-parameters-and-parameter-data-types.md)  
 Descreve como trabalhar com os parâmetros de `Command`, incluindo a direção, os tipos de dados e a sintaxe de parâmetro.  
  
 [Gerando comandos com CommandBuilders](generating-commands-with-commandbuilders.md)  
 Descreve como usar construtores de comando para gerar automaticamente comandos INSERT, UPDATE, e DELETE para um `DataAdapter` que possui um comando SELECT de uma única tabela.  
  
 [Obter um único valor de um banco de dados](obtaining-a-single-value-from-a-database.md)  
 Descreve como usar o método `ExecuteScalar` de um objeto `Command` para retornar um único valor de uma consulta de banco de dados.  
  
 [Usar os comandos para modificar dados](using-commands-to-modify-data.md)  
 Descreve como usar um provedor de dados para executar procedimentos armazenados ou instruções DDL (linguagem de definição de dados).  
  
## <a name="see-also"></a>Veja também

- [DataAdapters e DataReaders](dataadapters-and-datareaders.md)
- [DataSets, DataTables e DataViews](./dataset-datatable-dataview/index.md)
- [Conectando a uma Fonte de Dados](connecting-to-a-data-source.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
