---
description: 'Saiba mais sobre: provedor EntityClient para o Entity Framework'
title: Provedor EntityClient para Entity Framework
ms.date: 03/30/2017
ms.assetid: 8c5db787-78e6-4a34-8dc1-188bca0aca5e
ms.openlocfilehash: 96c060f3e0b21484e90fcbc2483693abd528dcfb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650866"
---
# <a name="entityclient-provider-for-the-entity-framework"></a>Provedor EntityClient para Entity Framework

O provedor EntityClient é um provedor de dados usado por aplicativos Entity Framework para acessar dados descritos em um modelo conceitual. Para obter informações sobre modelos conceituais, consulte [modelagem e mapeamento](modeling-and-mapping.md). O EntityClient usa outros provedores de dados .NET Framework para acessar a fonte de dados. Por exemplo, o EntityClient usa o Provedor de Dados .NET Framework para SQL Server (SqlClient) ao acessar um banco de dados do SQL Server. Para obter informações sobre o provedor SqlClient, consulte [SqlClient para o Entity Framework](sqlclient-for-the-entity-framework.md). O provedor EntityClient é implementado no namespace <xref:System.Data.EntityClient>.  
  
## <a name="managing-connections"></a>Gerenciando conexões  

 O Entity Framework se baseia em provedores de dados ADO.NET específicos de armazenamento, fornecendo um <xref:System.Data.EntityClient.EntityConnection> para um provedor de dados subjacente e um banco de dado relacional. Para construir um <xref:System.Data.EntityClient.EntityConnection> objeto, você precisa fazer referência a um conjunto de metadados que contém os modelos e o mapeamento necessários, além de um nome de provedor de dados específico de armazenamento e uma cadeia de conexão. Depois que o <xref:System.Data.EntityClient.EntityConnection> estiver em vigor, as entidades poderão ser acessadas por meio das classes geradas do modelo conceitual.  
  
 Você pode especificar uma cadeia de conexão no arquivo app.config.  
  
 O <xref:System.Data.EntityClient> também inclui a classe <xref:System.Data.EntityClient.EntityConnectionStringBuilder>. Essa classe permite aos desenvolvedores criar, programaticamente, cadeias de conexão com sintaxe correta, bem como analisar e reconstruir cadeias de conexão existentes, usando as propriedades e os métodos da classe. Para obter mais informações, consulte [como: criar uma cadeia de conexão de EntityConnection](how-to-build-an-entityconnection-connection-string.md).  
  
## <a name="creating-queries"></a>Criando consultas  

 O [!INCLUDE[esql](../../../../../includes/esql-md.md)] idioma é um dialeto independente de armazenamento do SQL que funciona diretamente com esquemas de entidade conceitual e dá suporte a conceitos de modelo de dados de entidade como a herança e as relações. A <xref:System.Data.EntityClient.EntityCommand> classe é usada para executar um [!INCLUDE[esql](../../../../../includes/esql-md.md)] comando em um modelo de entidade. Quando você constrói objetos <xref:System.Data.EntityClient.EntityCommand>, é possível especificar um nome de procedimento armazenado ou um texto de consulta. O Entity Framework funciona com provedores de dados específicos de armazenamento para converter generic [!INCLUDE[esql](../../../../../includes/esql-md.md)] em consultas específicas de armazenamento. Para obter mais informações sobre como escrever [!INCLUDE[esql](../../../../../includes/esql-md.md)] consultas, consulte [Entity SQL Language](./language-reference/entity-sql-language.md).  
  
 O exemplo a seguir cria um <xref:System.Data.EntityClient.EntityCommand> objeto e atribui um [!INCLUDE[esql](../../../../../includes/esql-md.md)] texto de consulta à sua <xref:System.Data.EntityClient.EntityCommand.CommandText%2A?displayProperty=nameWithType> propriedade. Essa [!INCLUDE[esql](../../../../../includes/esql-md.md)] consulta solicita produtos ordenados pelo preço da lista do modelo conceitual. O código a seguir não tem nenhum conhecimento do modelo de armazenamento.  
  
 ```csharp
EntityCommand cmd = conn.CreateCommand();
cmd.CommandText = @"SELECT VALUE p
  FROM AdventureWorksEntities.Product AS p
  ORDER BY p.ListPrice";
```
  
## <a name="executing-queries"></a>Executando consultas  

 Quando uma consulta é executada, ela é analisada e convertida em uma árvore de comandos canônica. Todo processamento subsequente é executado na árvore de comandos. A árvore de comandos é o meio de comunicação entre o <xref:System.Data.EntityClient> e o provedor de dados de .NET Framework subjacente, como <xref:System.Data.SqlClient> .  
  
 O <xref:System.Data.EntityClient.EntityDataReader> expõe os resultados da execução de um <xref:System.Data.EntityClient.EntityCommand> em relação a um modelo conceitual. Para executar o comando que retorna <xref:System.Data.EntityClient.EntityDataReader>, chame <xref:System.Data.EntityClient.EntityCommand.ExecuteReader%2A>. O <xref:System.Data.EntityClient.EntityDataReader> implementa <xref:System.Data.IExtendedDataRecord> para descrever resultados estruturados avançados.  
  
## <a name="managing-transactions"></a>Gerenciando transações  

 No Entity Framework, existem dois modos de usar transações: automático e explícito. As transações automáticas usam o namespace <xref:System.Transactions>, e as transações explícitas usam a classe <xref:System.Data.EntityClient.EntityTransaction>.  
  
 Para atualizar os dados expostos por meio de um modelo conceitual, consulte [como gerenciar transações no Entity Framework](/previous-versions/dotnet/netframework-4.0/bb738523(v=vs.100)).  
  
## <a name="in-this-section"></a>Nesta seção  

 [Como: criar uma cadeia de conexão EntityConnection](how-to-build-an-entityconnection-connection-string.md)  
  
 [Como: executar uma consulta que retorna resultados de PrimitiveType](how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [Como: executar uma consulta que retorna resultados de StructuralType](how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [Como: executar uma consulta que retorna resultados de RefType](how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [Como: executar uma consulta que retorna tipos complexos](how-to-execute-a-query-that-returns-complex-types.md)  
  
 [Como: executar uma consulta que retorna aninhados coleções](how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [Como: executar uma consulta Entity SQL parametrizada usando EntityCommand](how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [Como: executar um procedimento armazenado parametrizado usando EntityCommand](how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [Como: executar uma consulta polimorfo](how-to-execute-a-polymorphic-query.md)  
  
 [Como: navegar em relações com o operador navegar](how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## <a name="see-also"></a>Consulte também

- [Gerenciando conexões e transações](/previous-versions/dotnet/netframework-4.0/bb896325(v=vs.100))
- [ADO.NET Entity Framework](index.md)
- [Referência de linguagem](./language-reference/index.md)
