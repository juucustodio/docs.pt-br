---
description: 'Saiba mais sobre: como desativar o carregamento adiado'
title: 'Como: desligar o carregamento adiado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 1b84b852-3cad-41a7-8077-149a70d50c8b
ms.openlocfilehash: 739c9b0b65eda73d6c504409395eb805b0c02873
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99785829"
---
# <a name="how-to-turn-off-deferred-loading"></a>Como: desligar o carregamento adiado

Você pode desativar a carga adiada definindo <xref:System.Data.Linq.DataContext.DeferredLoadingEnabled%2A> a `false`. Para obter mais informações, veja [carregamento deferido versus imediato](deferred-versus-immediate-loading.md).  
  
> [!NOTE]
> A carga adiada é desativada implicitamente quando o rastreamento de objeto é desativado. Para obter mais informações, consulte [como recuperar informações como somente leitura](how-to-retrieve-information-as-read-only.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como desativar a carga adiada definindo <xref:System.Data.Linq.DataContext.DeferredLoadingEnabled%2A> a `false`.  
  
 [!code-csharp[DLinqQuerying#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqQuerying/cs/Program.cs#3)]
 [!code-vb[DLinqQuerying#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqQuerying/vb/Module1.vb#3)]  
  
## <a name="see-also"></a>Consulte também

- [Consulte conceitos](query-concepts.md)
- [Consultando o banco de dados](querying-the-database.md)
