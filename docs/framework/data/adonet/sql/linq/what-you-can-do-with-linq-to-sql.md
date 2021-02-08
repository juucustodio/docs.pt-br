---
description: 'Saiba mais sobre: o que você pode fazer com LINQ to SQL'
title: O que você pode fazer com LINQ to SQL
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 061d98b2-baa7-4336-8ad2-c14de8134d91
ms.openlocfilehash: adf1d8dfab69db27d15634a12dbdfbfa287dbb4c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791745"
---
# <a name="what-you-can-do-with-linq-to-sql"></a>O que você pode fazer com LINQ to SQL

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] o oferece suporte a todos os principais recursos que você espera como um desenvolvedor do SQL. Você pode consultar informações, e inserir, atualizar e excluir informações de tabelas.  
  
## <a name="selecting"></a>Seleção  

 Selecionar (*projeção*) é obtido apenas escrevendo uma consulta LINQ em sua própria linguagem de programação e, em seguida, executando essa consulta para recuperar os resultados. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Ele mesmo converte todas as operações necessárias nas operações de SQL necessárias com as quais você está familiarizado. Para obter mais informações, consulte [LINQ to SQL](index.md).  
  
 No exemplo a seguir, os nomes de empresas de clientes de Londres são recuperados e exibidos na janela do console.  
  
 [!code-csharp[DLinqGettingStarted#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#1)]
 [!code-vb[DLinqGettingStarted#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#1)]  
  
## <a name="inserting"></a>Inserindo  

 Para executar um `Insert` do SQL, basta adicionar objetos ao modelo de objetos que você criou e chamar <xref:System.Data.Linq.DataContext.SubmitChanges%2A> em <xref:System.Data.Linq.DataContext>.  
  
 No exemplo a seguir, um novo cliente e informações sobre o cliente são adicionados à tabela `Customers` usando <xref:System.Data.Linq.Table%601.InsertOnSubmit%2A>.  
  
 [!code-csharp[DLinqGettingStarted#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#2)]
 [!code-vb[DLinqGettingStarted#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#2)]  
  
## <a name="updating"></a>Atualizar  

 Para `Update` uma entrada de banco de dados, primeiro recupere o item e edite-o diretamente no modelo de objeto. Depois que você modificou o objeto, chame <xref:System.Data.Linq.DataContext.SubmitChanges%2A> no <xref:System.Data.Linq.DataContext> para atualizar o banco de dados.  
  
 No exemplo a seguir, todos os clientes que são de Londres são recuperados. O nome da cidade é alterado de “Londres” para “Londres - metro”. Finalmente, <xref:System.Data.Linq.DataContext.SubmitChanges%2A> é chamado para enviar as alterações para o banco de dados.  
  
 [!code-csharp[DLinqGettingStarted#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#3)]
 [!code-vb[DLinqGettingStarted#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#3)]  
  
## <a name="deleting"></a>Excluir  

 Para `Delete` um item, remova-o da coleção à qual ele pertence e, em seguida, chame <xref:System.Data.Linq.DataContext.SubmitChanges%2A> no <xref:System.Data.Linq.DataContext> para confirmar a alteração.  
  
> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Não reconhece operações de exclusão em cascata. Se você quiser excluir uma linha em uma tabela que tenha restrições em relação a ela, consulte [como excluir linhas do banco de dados](how-to-delete-rows-from-the-database.md).  
  
 No exemplo a seguir, o cliente que tem `CustomerID` de `98128` é recuperado do banco de dados. Em seguida, após ter confirmado que a linha do cliente foi recuperada, <xref:System.Data.Linq.Table%601.DeleteOnSubmit%2A> é chamado para remover esse objeto da coleção. Finalmente, <xref:System.Data.Linq.DataContext.SubmitChanges%2A> é chamado para encaminhar a exclusão para o banco de dados.  
  
 [!code-csharp[DLinqGettingStarted#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqGettingStarted/cs/Program.cs#4)]
 [!code-vb[DLinqGettingStarted#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqGettingStarted/vb/Module1.vb#4)]  
  
## <a name="see-also"></a>Consulte também

- [Guia de programação](programming-guide.md)
- [Modelo de objeto LINQ to SQL](the-linq-to-sql-object-model.md)
- [Introdução](getting-started.md)
