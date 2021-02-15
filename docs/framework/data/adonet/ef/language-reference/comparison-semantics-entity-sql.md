---
description: 'Saiba mais sobre: semântica de comparação (Entity SQL)'
title: Semântica de comparação (Entity SQL)
ms.date: 03/30/2017
ms.assetid: b36ce28a-2fe4-4236-b782-e5f7c054deae
ms.openlocfilehash: b1c832cb6f2903073b1c6be806c73823b1f4a220
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99786427"
---
# <a name="comparison-semantics-entity-sql"></a>Semântica de comparação (Entity SQL)

Executar alguns dos seguintes operadores de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] envolve a comparação de instâncias do tipo:  
  
## <a name="explicit-comparison"></a>Comparação explícita  

 Operações de igualdade:  
  
- =  
  
- !=  
  
 Ordenando operações:  
  
- <  
  
- \<=  
  
- \>  
  
- \>=  
  
 Operações de nulidade:  
  
- IS NULL  
  
- IS NOT NULL  
  
## <a name="explicit-distinction"></a>Distinção explícita  

 Distinção de igualdade:  
  
- DISTINTO  
  
- GROUP BY  
  
 Classificação a distinção:  
  
- ORDER BY  
  
## <a name="implicit-distinction"></a>Distinção implícita  

 Definir operações e predicados (igualdade):  
  
- UNION  
  
- INTERSECT  
  
- EXCEPT  
  
- SET  
  
- OVERLAPS  
  
 Predicados de item (igual):  
  
- IN  
  
## <a name="supported-combinations"></a>Combinações com suporte  

 A tabela a seguir mostra todas as combinações suportados operadores de comparação para cada tipo do tipo:  
  
|**Tipo**|**=**<br /><br /> **!=**|**GROUP BY**<br /><br /> **DISTINCT**|**UNION**<br /><br /> **INTERSECT**<br /><br /> **EXCEPT**<br /><br /> **SET**<br /><br /> **OVERLAPS**|**IN**|**<   <=**<br /><br /> **>   >=**|**ORDER BY**|**IS NULL**<br /><br /> **NÃO É NULO**|  
|-|-|-|-|-|-|-|-|  
|Tipo de entidade|Ref<sup>1</sup>|Todas as propriedades<sup>2</sup>|Todas as propriedades<sup>2</sup>|Todas as propriedades<sup>2</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Ref<sup>1</sup>|  
|Tipo complexo|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|  
|Linha|Todas as propriedades<sup>4</sup>|Todas as propriedades<sup>4</sup>|Todas as propriedades<sup>4</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Todas as propriedades<sup>4</sup>|Lançamento<sup>3</sup>|  
|Tipo primitivo|Específica do provedor|Específica do provedor|Específica do provedor|Específica do provedor|Específica do provedor|Específica do provedor|Específica do provedor|  
|Multiset|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|  
|Ref|Sim<sup>5</sup>|Sim<sup>5</sup>|Sim<sup>5</sup>|Sim<sup>5</sup>|Throw|Throw|Sim<sup>5</sup>|  
|Associação<br /><br /> type|Lançamento<sup>3</sup>|Throw|Throw|Throw|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|Lançamento<sup>3</sup>|  
  
 <sup>1</sup> As referências das instâncias de tipo de entidade fornecidas são implicitamente comparadas, conforme mostrado no exemplo a seguir:  
  
```sql  
SELECT p1, p2
FROM AdventureWorksEntities.Product AS p1
     JOIN AdventureWorksEntities.Product AS p2
WHERE p1 != p2 OR p1 IS NULL  
```  
  
 Uma instância de entidade não pode ser comparado a uma referência explícita. Se isso for tentada, uma exceção é lançada. Por exemplo, a seguinte consulta irá acionar uma exceção:  
  
```sql  
SELECT p1, p2
FROM AdventureWorksEntities.Product AS p1
     JOIN AdventureWorksEntities.Product AS p2
WHERE p1 != REF(p2)  
```  
  
 <sup>2</sup> As propriedades de tipos complexos são achatadas antes de serem enviadas para o armazenamento, de modo que se tornem comparáveis (desde que todas as suas propriedades sejam comparáveis). Consulte também <sup>4.</sup>  
  
 <sup>3</sup> O tempo de execução do Entity Framework detecta o caso sem suporte e gera uma exceção significativa sem envolver o provedor/repositório.  
  
 <sup>4</sup> É feita uma tentativa de comparar todas as propriedades. Se houver uma propriedade que é de um tipo não comparável, como texto, o ntext, ou imagem, uma exceção de servidor pode ser lançada.  
  
 <sup>5</sup> Todos os elementos individuais das referências são comparados (isso inclui o nome do conjunto de entidades e todas as propriedades de chave do tipo de entidade).  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da Entity SQL](entity-sql-overview.md)
