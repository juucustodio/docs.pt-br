---
description: 'Saiba mais sobre: executando um comando'
title: Executando um comando
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 40494916-c25a-4cb8-8f7c-fcb8d378464e
ms.openlocfilehash: 7b5fe46bf4d82fcd4f24cc0eb19e85a2ee9aca7b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724317"
---
# <a name="executing-a-command"></a>Executando um comando

Cada provedor de dados do .NET Framework incluído com o .NET Framework tem seu próprio objeto de comando que herda de <xref:System.Data.Common.DbCommand>. O Provedor de Dados .NET Framework para OLE DB inclui um objeto <xref:System.Data.OleDb.OleDbCommand>, o Provedor de Dados .NET Framework para SQL Server inclui um objeto <xref:System.Data.SqlClient.SqlCommand>, o Provedor de Dados .NET Framework para ODBC inclui um objeto <xref:System.Data.Odbc.OdbcCommand> e o Provedor de Dados .NET Framework para Oracle inclui um objeto <xref:System.Data.OracleClient.OracleCommand>. Cada um desses objetos expõe métodos para executar comandos com base no tipo de comando e do valor de retorno desejado, como descrito na tabela a seguir.  
  
|Comando|Valor Retornado|  
|-------------|------------------|  
|`ExecuteReader`|Retorna um objeto `DataReader`.|  
|`ExecuteScalar`|Retorna um único valor escalar.|  
|`ExecuteNonQuery`|Executa um comando que não retorna nenhuma linha.|  
|`ExecuteXMLReader`|Retorna um <xref:System.Xml.XmlReader>. Disponível somente para um objeto do `SqlCommand`.|  
  
 Cada objeto de comando fortemente tipado também dá suporte a uma enumeração de <xref:System.Data.CommandType> que especifica como uma cadeia de caracteres de comando é interpretada, conforme descrito na tabela a seguir.  
  
|CommandType|Descrição|  
|-----------------|-----------------|  
|`Text`|Um comando SQL que define as instruções a serem executado na fonte de dados.|  
|`StoredProcedure`|O nome do procedimento armazenado. Você pode usar a propriedade `Parameters` de um comando para acessar os parâmetros de entrada e saída e os valores de retorno, independentemente do método `Execute` chamado. Ao usar `ExecuteReader`, os valores de retorno e os parâmetros de saída não estarão acessíveis até que o `DataReader` seja fechado.|  
|`TableDirect`|O nome de uma tabela.|  
  
## <a name="example"></a>Exemplo  

 O código de exemplo a seguir demonstra como criar um objeto <xref:System.Data.SqlClient.SqlCommand> para executar um procedimento armazenado definindo suas propriedades. Um objeto <xref:System.Data.SqlClient.SqlParameter> é usado para especificar o parâmetro de entrada para o procedimento armazenado. O comando é executado usando o método <xref:System.Data.SqlClient.SqlCommand.ExecuteReader%2A> e a saída do <xref:System.Data.SqlClient.SqlDataReader> é exibida na janela do console.  
  
 [!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]  
  
### <a name="troubleshooting-commands"></a>Comandos de solução de problemas  

 O provedor de dados .NET Framework para SQL Server adiciona contadores de desempenho para permitir que você detecte os problemas intermitentes relacionados às execuções de comando com falha. Para obter mais informações, consulte [contadores de desempenho](performance-counters.md).  
  
## <a name="see-also"></a>Consulte também

- [Comandos e parâmetros](commands-and-parameters.md)
- [DataAdapters e DataReaders](dataadapters-and-datareaders.md)
- [Visão geral do ADO.NET](ado-net-overview.md)
