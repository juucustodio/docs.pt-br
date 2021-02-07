---
description: 'Saiba mais sobre: cláusula Group by (Visual Basic)'
title: Cláusula Group By
ms.date: 07/20/2015
f1_keywords:
- vb.QueryGroupByInto
- vb.QueryGroupBy
- vb.QueryGroupRef
- vb.QueryGroupInto
- vb.QueryGroup
helpviewer_keywords:
- queries [Visual Basic], Group By
- Group By statement [Visual Basic]
- Group By clause [Visual Basic]
ms.assetid: b1b5dcea-6654-473b-a2db-01f7e4c265d7
ms.openlocfilehash: f5cfb76b0f4b1d191f959ae1812140c6872e93bb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99700501"
---
# <a name="group-by-clause-visual-basic"></a>Cláusula Group By (Visual Basic)

Agrupa os elementos de um resultado de consulta. Também pode ser usado para aplicar funções de agregação a cada grupo. A operação de agrupamento é baseada em uma ou mais chaves.  
  
## <a name="syntax"></a>Syntax  
  
```vb  
Group [ listField1 [, listField2 [...] ] By keyExp1 [, keyExp2 [...] ]  
  Into aggregateList  
```  
  
## <a name="parts"></a>Partes  
  
- `listField1`, `listField2`  
  
     Opcional. Um ou mais campos da variável de consulta ou variáveis que identificam explicitamente os campos a serem incluídos no resultado agrupado. Se nenhum campo for especificado, todos os campos da variável de consulta ou variáveis serão incluídos no resultado agrupado.  
  
- `keyExp1`  
  
     Obrigatório. Uma expressão que identifica a chave a ser usada para determinar os grupos de elementos. Você pode especificar mais de uma chave para especificar uma chave composta.  
  
- `keyExp2`  
  
     Opcional. Uma ou mais chaves adicionais que são combinadas com `keyExp1` o para criar uma chave composta.  
  
- `aggregateList`  
  
     Obrigatório. Uma ou mais expressões que identificam como os grupos são agregados. Para identificar um nome de membro para os resultados agrupados, use a `Group` palavra-chave, que pode estar em qualquer uma das seguintes formas:  
  
    ```vb  
    Into Group  
    ```  
  
     -ou-  
  
    ```vb  
    Into <alias> = Group  
    ```  
  
     Você também pode incluir funções de agregação para aplicar ao grupo.  
  
## <a name="remarks"></a>Comentários  

 Você pode usar a `Group By` cláusula para dividir os resultados de uma consulta em grupos. O agrupamento é baseado em uma chave ou em uma chave composta que consiste em várias chaves. Os elementos associados aos valores de chave correspondentes são incluídos no mesmo grupo.  
  
 Use o `aggregateList` parâmetro da `Into` cláusula e a `Group` palavra-chave para identificar o nome do membro que é usado para fazer referência ao grupo. Você também pode incluir funções de agregação na `Into` cláusula para computar valores para os elementos agrupados. Para obter uma lista de funções de agregação padrão, consulte [cláusula Aggregate](aggregate-clause.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir agrupa uma lista de clientes com base em seu local (país/região) e fornece uma contagem dos clientes em cada grupo. Os resultados são ordenados por nome de país/região. Os resultados agrupados são ordenados por nome de cidade.  
  
 [!code-vb[VbSimpleQuerySamples#11](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbSimpleQuerySamples/VB/QuerySamples1.vb#11)]  
  
## <a name="see-also"></a>Consulte também

- [Introdução a LINQ no Visual Basic](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [Consultas](index.md)
- [Cláusula SELECT](select-clause.md)
- [Cláusula from](from-clause.md)
- [Cláusula order by](order-by-clause.md)
- [Cláusula Aggregate](aggregate-clause.md)
- [Cláusula Group Join](group-join-clause.md)
