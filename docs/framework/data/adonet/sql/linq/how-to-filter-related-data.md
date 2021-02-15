---
description: 'Saiba mais sobre: como filtrar dados relacionados'
title: 'Como: filtrar dados relacionados'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: ec8b8f97-5d01-4f31-9b97-d1556df6a4bc
ms.openlocfilehash: d44e0805b82c0c58f9ee19808e078f9f9b337050
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738943"
---
# <a name="how-to-filter-related-data"></a>Como: filtrar dados relacionados

Use o método de <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> para especificar subpropriedades consultas para limitar a quantidade de dados recuperados.  
  
## <a name="example"></a>Exemplo  

 No exemplo a seguir, o método de <xref:System.Data.Linq.DataLoadOptions.AssociateWith%2A> limita `Orders` recuperado com aqueles que não foram enviados hoje. Essa abordagem, sem qualquer `Orders` deve ser recuperado mesmo que somente um subconjunto é desejado.  
  
 [!code-csharp[System.Data.Linq.DataLoadOptions#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/system.data.linq.dataloadoptions/cs/program.cs#1)]
 [!code-vb[System.Data.Linq.DataLoadOptions#1](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/system.data.linq.dataloadoptions/vb/module1.vb#1)]  
  
## <a name="see-also"></a>Consulte também

- [Consultando o banco de dados](querying-the-database.md)
