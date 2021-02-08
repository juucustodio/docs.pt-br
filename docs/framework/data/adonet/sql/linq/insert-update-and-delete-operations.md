---
description: 'Saiba mais sobre: inserir, atualizar e excluir operações'
title: Operações de inserção, atualização e exclusão
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 26a43a4f-83c9-4732-806d-bb23aad0ff6b
ms.openlocfilehash: 2d0470ed6abe654ca08f954c3de97de207adb75d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803809"
---
# <a name="insert-update-and-delete-operations"></a>Operações de inserção, atualização e exclusão

Você executa operações `Insert`, `Update` e `Delete` no [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] adicionando, modificando e removendo objetos no seu modelo de objeto. Por padrão, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] converte suas ações para SQL e envia as alterações para o banco de dados.

[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] oferece flexibilidade máxima na manipulação e persistência de alterações feitas em seus objetos. Assim que os objetos de entidade estiverem disponíveis (recuperando-os por meio de uma consulta ou construindo-os do zero), você poderá alterá-los como objetos típicos em seu aplicativo. Isto é, você pode alterar seus valores, adicioná-los às coleções e removê-los das coleções. O [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] controla as alterações e está pronto para transmiti-las de volta para o banco de dados quando você chama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.

> [!NOTE]
> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] Não dá suporte ou reconhece operações de exclusão em cascata. Se você quiser excluir uma linha em uma tabela que tenha restrições em relação a ela, você deve definir a `ON DELETE CASCADE` regra na restrição FOREIGN-KEY no banco de dados ou usar seu próprio código para primeiro excluir os objetos filho que impedem que o objeto pai seja excluído. Caso contrário, uma exceção será gerada. Para obter mais informações, consulte [como: excluir linhas do banco de dados](how-to-delete-rows-from-the-database.md).

Os seguintes trechos usam as classes `Customer` e `Order` do banco de dados de exemplo Northwind. As definições de classe não são mostradas para abreviar.

[!code-csharp[DLinqCRUDOps#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCRUDOps/cs/Program.cs#1)]
[!code-vb[DLinqCRUDOps#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCRUDOps/vb/Module1.vb#1)]

Quando você chama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, o [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] automaticamente gera e executa comandos SQL de que ele deve passar suas alterações de volta para o banco de dados.

> [!NOTE]
> Você pode substituir esse comportamento usando sua própria lógica personalizada, geralmente usando um procedimento armazenado. Para obter mais informações, consulte [responsabilidades do desenvolvedor ao substituir o comportamento padrão](responsibilities-of-the-developer-in-overriding-default-behavior.md).
>
> Os desenvolvedores que usam o Visual Studio podem usar o Object Relational Designer para desenvolver procedimentos armazenados para essa finalidade.

## <a name="see-also"></a>Consulte também

- [Baixar bancos de dados de amostra](downloading-sample-databases.md)
- [Personalizando a inserção, atualiazação, e as operações de exclusão](customizing-insert-update-and-delete-operations.md)
