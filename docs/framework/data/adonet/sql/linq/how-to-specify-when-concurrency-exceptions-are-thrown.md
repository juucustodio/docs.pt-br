---
description: 'Saiba mais sobre: como especificar quando exceções de simultaneidade são geradas'
title: 'Como: especificar quando exceções de simultaneidade são geradas'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 344ae068-ff63-4a2e-8b00-af22e143675f
ms.openlocfilehash: d445cabfd2498f3599d874c2b7983a86c2c36c7d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785868"
---
# <a name="how-to-specify-when-concurrency-exceptions-are-thrown"></a>Como: especificar quando exceções de simultaneidade são geradas

Em [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], uma exceção é lançada de <xref:System.Data.Linq.ChangeConflictException> quando os objetos não atualizarão devido a conflitos de concorrência otimista. Para obter mais informações, consulte [simultaneidade otimista: visão geral](optimistic-concurrency-overview.md).  
  
 Antes de enviar as alterações para base de dados, você pode especificar quando exceções concorrentes devem ser lançadas:  
  
- Lance a exceção na primeira falha (<xref:System.Data.Linq.ConflictMode.FailOnFirstConflict>).  
  
- Concluir todas as tentativas de atualização, se acumule quaisquer falhas, e relatar falhas criadas na exceção (<xref:System.Data.Linq.ConflictMode.ContinueOnConflict>).  
  
 Quando lançada, a exceção de <xref:System.Data.Linq.ChangeConflictException> fornece acesso a uma coleção de <xref:System.Data.Linq.ChangeConflictCollection> . Essa coleção fornece detalhes para cada conflito (mapeado para uma tentativa única falha de atualização), incluindo o acesso à coleção de <xref:System.Data.Linq.ObjectChangeConflict.MemberConflicts%2A> . Mapas de cada conflito de membro a um único membro na atualização que falhou a verificação de simultaneidade.  
  
## <a name="example"></a>Exemplo  

 O código a seguir mostra exemplos de ambos os valores.  
  
 [!code-csharp[System.Data.Linq.ConflictModeEnumeration#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.conflictmodeenumeration/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.ConflictModeEnumeration#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.conflictmodeenumeration/vb/module1.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Como: gerenciar conflitos de alteração](how-to-manage-change-conflicts.md)
- [Fazendo e enviando alterações de dados](making-and-submitting-data-changes.md)
