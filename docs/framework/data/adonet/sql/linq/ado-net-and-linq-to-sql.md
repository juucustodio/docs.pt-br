---
description: 'Saiba mais sobre: ADO.NET e LINQ to SQL'
title: O ADO.NET e LINQ to SQL
titleSuffix: ''
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 49ac6da0-f2e1-46fa-963e-1b6dcb63fef7
ms.openlocfilehash: 1f3f4a50c13af857ecd9f3195c7f431dd46ed3ee
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99712944"
---
# <a name="adonet-and-linq-to-sql"></a>O ADO.NET e LINQ to SQL

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] faz parte da família de tecnologias ADO.NET. Ele se baseia em serviços fornecidos pelo modelo de provedor ADO.NET. Portanto, você pode misturar [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] código com aplicativos ADO.net existentes e migrar soluções ADO.net atuais para o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] . A ilustração a seguir fornece uma exibição de alto nível de relacionamento.  
  
 ![LINQ to SQL e ADO.NET](./media/dlinq-3.png "DLinq_3")  
  
## <a name="connections"></a>conexões  

 Você pode fornecer uma conexão ADO.NET existente ao criar um [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] <xref:System.Data.Linq.DataContext> . Todas as operações em relação ao <xref:System.Data.Linq.DataContext> (incluindo consultas) usam essa conexão fornecida. Se a conexão já estiver aberta, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] deixará como está quando você tiver terminado.  
  
 [!code-csharp[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCommunicatingWithDatabase/cs/Program.cs#4)]
 [!code-vb[DLinqCommunicatingWithDatabase#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCommunicatingWithDatabase/vb/Module1.vb#4)]  
  
 Você sempre pode acessar a conexão e fechá-lo você mesmo usando a propriedade de <xref:System.Data.Linq.DataContext.Connection%2A> , como no código a seguir:  
  
 [!code-csharp[DLinqAdoNet#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#1)]
 [!code-vb[DLinqAdoNet#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#1)]  
  
## <a name="transactions"></a>Transactions  

 Você pode fornecer seu <xref:System.Data.Linq.DataContext> com sua própria transação de base de dados quando seu aplicativo é iniciado na transação e você deseja que o <xref:System.Data.Linq.DataContext> a ser empacotado.  
  
 O método preferencial para fazer transações com o .NET Framework é usar o <xref:System.Transactions.TransactionScope> objeto. Usando essa abordagem, você pode fazer as transações distribuídas que funcionam através de bases de dados e outros gerentes de recurso de memória residente. Os escopos de transação exigem alguns recursos iniciar. Elevam-se a transações distribuídas somente quando há várias conexões no escopo de transação.  
  
 [!code-csharp[DLinqAdoNet#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#2)]
 [!code-vb[DLinqAdoNet#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#2)]  
  
 Você não pode usar essa abordagem para todos os bases de dados. Por exemplo, a conexão SqlClient não pode promover transações do sistema quando ele funciona em um servidor SQL Server 2000. Em vez disso, inscreve-se automaticamente para uma transação completa, distribuído consulta sempre que um escopo de transação que está sendo usado.  
  
## <a name="direct-sql-commands"></a>Comandos SQL diretos  

 Às vezes você pode encontrar situações onde a capacidade de <xref:System.Data.Linq.DataContext> de consulte ou enviar alterações insuficientes para a tarefa específica que você deseja executar. Nesteas circunstâncias você pode usar o método de <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> para emitir comandos SQL a base de dados e para converter os resultados da consulta a objetos.  
  
 Por exemplo, suponha que os dados para a classe de `Customer` são espalhado sobre duas tabelas (customer1 e customer2). A seguinte consulta retorna uma sequência de objetos `Customer` :  
  
 [!code-csharp[DLinqAdoNet#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#3)]
 [!code-vb[DLinqAdoNet#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#3)]  
  
 Desde que os nomes de coluna nos resultados de tabela correspondam às propriedades da coluna de sua classe de entidade, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] cria seus objetos fora de qualquer consulta SQL.  
  
### <a name="parameters"></a>Parâmetros  

 O método de <xref:System.Data.Linq.DataContext.ExecuteQuery%2A> aceita parâmetros. O código a seguir executa uma consulta parametrizada:  
  
 [!code-csharp[DlinqAdoNet#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqAdoNet/cs/Program.cs#4)]
 [!code-vb[DlinqAdoNet#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqAdoNet/vb/Module1.vb#4)]  
  
> [!NOTE]
> Os parâmetros são expressos no texto da consulta usando a mesma notação encaracolado usada por `Console.WriteLine()` e por `String.Format()`. `String.Format()` leva a cadeia de caracteres de consulta que você fornece e substitui os parâmetros encaracolado- apoiados com nomes de parâmetro gerados como `@p0`, `@p1` …, `@p(n)`.  
  
## <a name="see-also"></a>Consulte também

- [Informações gerais](background-information.md)
- [Como: reutilizar uma conexão entre um comando ADO.NET e um DataContext](how-to-reuse-a-connection-between-an-ado-net-command-and-a-datacontext.md)
