---
description: 'Saiba mais sobre: como enviar alterações ao banco de dados'
title: 'Como: enviar alterações para o banco de dados'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c7cba174-9d40-491d-b32c-f2d73b7e9eab
ms.openlocfilehash: 31d85d94c74315a127b18bd41b4d1d1a7fe7d0b2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785842"
---
# <a name="how-to-submit-changes-to-the-database"></a>Como: enviar alterações para o banco de dados

Independentemente de quantas você faz alterações aos objetos, as alterações são feitas somente para réplicas de memória. Você não tiver nenhuma alteração nos dados reais na base de dados. Suas alterações não são passadas para o servidor até que você chama explicitamente <xref:System.Data.Linq.DataContext.SubmitChanges%2A> em <xref:System.Data.Linq.DataContext>.  
  
 Quando você fizer essa chamada, <xref:System.Data.Linq.DataContext> tenta converter suas alterações em comandos SQL equivalentes. Você pode usar sua própria lógica personalizada para substituir essas ações, mas a ordem de envio é orquestrada por um serviço do <xref:System.Data.Linq.DataContext> conhecido como processador de *alteração*. A sequência de eventos é a seguinte:  
  
1. Quando você chama <xref:System.Data.Linq.DataContext.SubmitChanges%2A>, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] examina o conjunto de objetos conhecidos para determinar se as novas instâncias eles foram anexadas. Se eles tiverem, essas novas instâncias são adicionadas ao conjunto de objetos rastreadas.  
  
2. Todos os objetos que possuem durante alterações são ordenados em uma sequência de objetos com base nas dependências entre eles. Os objetos cujas ambas as alterações depende de outros objetos são arranjados seqüencialmente após as suas dependências.  
  
3. Imediatamente antes todas as alterações reais são passadas, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] inicia uma transação para encapsular a série de comandos individuais.  
  
4. As alterações para os objetos são traduzidas um por um para comandos SQL e enviadas ao servidor.  
  
 Neste ponto, todos os erros detectados por base de dados fazem com que o processo de envio parar, e uma exceção é gerada. Todas as alterações a base de dados são revertidas como se nenhuma envio ocorreu nunca. <xref:System.Data.Linq.DataContext> ainda tem uma gravação completa de todas as alterações. Portanto você pode tentar corrigir o problema e chamar novamente <xref:System.Data.Linq.DataContext.SubmitChanges%2A> , como no exemplo de código que segue.  
  
## <a name="example"></a>Exemplo  

 Quando a transação em torno do envio é concluída com êxito, <xref:System.Data.Linq.DataContext> aceita as alterações aos objetos ignorando as informações de controle de alterações.  
  
 [!code-csharp[DLinqSubmittingChanges#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSubmittingChanges/cs/Program.cs#1)]
 [!code-vb[DLinqSubmittingChanges#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSubmittingChanges/vb/Module1.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Como: detectar e resolver submissões com conflito](how-to-detect-and-resolve-conflicting-submissions.md)
- [Como: gerenciar conflitos de alteração](how-to-manage-change-conflicts.md)
- [Baixar bancos de dados de amostra](downloading-sample-databases.md)
- [Fazendo e enviando alterações de dados](making-and-submitting-data-changes.md)
