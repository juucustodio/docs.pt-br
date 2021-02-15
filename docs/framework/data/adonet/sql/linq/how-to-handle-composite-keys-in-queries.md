---
description: 'Saiba mais sobre: como manipular chaves compostas em consultas'
title: 'Como: manipular chaves compostas em consultas'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ce2f14fd-1038-458a-91e3-a078c61f0d10
ms.openlocfilehash: 9d7c68495810bee6a383d98a75694e7cd24f1015
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738865"
---
# <a name="how-to-handle-composite-keys-in-queries"></a>Como: manipular chaves compostas em consultas

Alguns operadores podem levar apenas um argumento. Se o argumento deve incluir mais de uma coluna de base de dados, você deve criar um tipo anônimo para representar a combinação.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra uma consulta que invoca o operador de `GroupBy` , que pode levar apenas um argumento de `key` .  
  
 [!code-csharp[DLinqCompositeKeys#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCompositeKeys/cs/Program.cs#1)]
 [!code-vb[DLinqCompositeKeys#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCompositeKeys/vb/Module1.vb#1)]  
  
## <a name="example"></a>Exemplo  

 Refere-se a mesma situação join, como no exemplo a seguir:  
  
 [!code-csharp[DLinqCompositeKeys#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqCompositeKeys/cs/Program.cs#2)]
 [!code-vb[DLinqCompositeKeys#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqCompositeKeys/vb/Module1.vb#2)]  
  
## <a name="see-also"></a>Consulte também

- [Consulte conceitos](query-concepts.md)
