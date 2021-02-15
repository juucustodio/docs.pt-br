---
description: 'Saiba mais sobre: como recuperar informações de conflito de entidade'
title: 'Como: recuperar informações de conflito de entidade'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9a02b608-e7bb-4041-a452-a7fed26fd008
ms.openlocfilehash: dde11a431ae977595b9845444e48705a4552fb23
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767746"
---
# <a name="how-to-retrieve-entity-conflict-information"></a>Como: recuperar informações de conflito de entidade

Você pode usar objetos de classe de <xref:System.Data.Linq.ObjectChangeConflict> para fornecer informações sobre os conflitos revelados por exceções de <xref:System.Data.Linq.ChangeConflictException> . Para obter mais informações, consulte [simultaneidade otimista: visão geral](optimistic-concurrency-overview.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir efetua iterações através de uma lista de conflitos acumulados.  
  
 [!code-csharp[System.Data.Linq.ObjectChangeConflict#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.objectchangeconflict/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.ObjectChangeConflict#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.objectchangeconflict/vb/module1.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Como: gerenciar conflitos de alteração](how-to-manage-change-conflicts.md)
