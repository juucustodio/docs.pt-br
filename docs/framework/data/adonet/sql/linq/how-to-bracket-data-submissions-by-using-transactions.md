---
description: 'Saiba mais sobre: como colocar os envios de dados de colchete usando transações'
title: 'Como: delimitar submissões de dados entre colchetes usando transações'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 94044a31-de90-479b-935a-8159b4ae5c5a
ms.openlocfilehash: a1bbebfcdb4b65e83c4ac6dc9b87b06f33f2cb41
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99739021"
---
# <a name="how-to-bracket-data-submissions-by-using-transactions"></a>Como: delimitar submissões de dados entre colchetes usando transações

Você pode usar <xref:System.Transactions.TransactionScope> para suportar suas submissões a base de dados. Para obter mais informações, consulte [suporte a transações](transaction-support.md).  
  
## <a name="example"></a>Exemplo  

 O código a seguir inclui o envio de base de dados em <xref:System.Transactions.TransactionScope>.  
  
 [!code-csharp[DLinqSubmittingChanges#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#3)]
 [!code-vb[DLinqSubmittingChanges#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- [Baixar bancos de dados de amostra](downloading-sample-databases.md)
- [Fazendo e enviando alterações de dados](making-and-submitting-data-changes.md)
- [Suporte a transações](transaction-support.md)
