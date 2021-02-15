---
description: 'Saiba mais sobre: como: usar procedimentos armazenados mapeados para formas de resultados sequenciais'
title: 'Como: usar procedimentos armazenados mapeados para formas sequenciais de resultado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a73530de-5a4e-4d9c-8d66-abb19c225b11
ms.openlocfilehash: 3b5791875a7beb5a0c702e787e775cd528ab2517
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99738761"
---
# <a name="how-to-use-stored-procedures-mapped-for-sequential-result-shapes"></a>Como: usar procedimentos armazenados mapeados para formas sequenciais de resultado

Esse tipo de procedimento armazenado pode gerar mais de uma forma de resultado, mas você souber ordem em que os resultados são retornados. Compare este cenário com o cenário onde você não souber a sequência de retorna. Para obter mais informações, consulte [como: usar procedimentos armazenados mapeados para várias formas de resultado](how-to-use-stored-procedures-mapped-for-multiple-result-shapes.md).  
  
## <a name="example"></a>Exemplo  

 Aqui está T-SQL de um procedimento armazenado que retorna várias formas de resultado em seqüência:  
  
```sql
CREATE PROCEDURE MultipleResultTypesSequentially  
AS  
select * from products  
select * from customers  
```  
  
 [!code-csharp[DLinqSprox#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/northwind-sprox.cs#6)]
 [!code-vb[DLinqSprox#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/northwind-sprox.vb#6)]  
  
## <a name="example"></a>Exemplo  

 Você usaria código semelhante ao seguinte para executar este procedimento armazenado.  
  
 [!code-csharp[DLinqSprox#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqSprox/cs/Program.cs#7)]
 [!code-vb[DLinqSprox#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqSprox/vb/Module1.vb#7)]  
  
## <a name="see-also"></a>Consulte também

- [Procedimentos armazenados](stored-procedures.md)
