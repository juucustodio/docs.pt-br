---
description: 'Saiba mais sobre: como recuperar informações como Read-Only'
title: 'Como: recuperar informações como somente leitura'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: fb09e298-0b53-47e5-97fb-ab318bcd4fad
ms.openlocfilehash: 7743e555bcc3f6371ca601d02313e30895e57961
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99723446"
---
# <a name="how-to-retrieve-information-as-read-only"></a>Como: recuperar informações como somente leitura

Quando você não pretende modificar os dados, você pode aumentar o desempenho de consultas buscando resultados somente leitura.  
  
 Você implementar o processamento somente leitura <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> definindo a `false`.  
  
> [!NOTE]
> Quando <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> é definido como `false`, <xref:System.Data.Linq.DataContext.DeferredLoadingEnabled%2A> é definido implicitamente a `false`.  
  
## <a name="example"></a>Exemplo  

 O código a seguir recupera uma coleção somente leitura de datas de admissão de funcionários.  
  
 [!code-csharp[DLinqQuerying#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#2)]
 [!code-vb[DLinqQuerying#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- [Consulte conceitos](query-concepts.md)
- [Consultando o banco de dados](querying-the-database.md)
- [Adiado contra a carga immediate](deferred-versus-immediate-loading.md)
