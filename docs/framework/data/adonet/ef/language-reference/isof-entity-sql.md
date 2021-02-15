---
description: 'Saiba mais sobre: ISOF (Entity SQL)'
title: ISOF (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5b2b0d34-d0a7-4bcd-baf2-58aa8456d00b
ms.openlocfilehash: 4a44ddc74ef16ec16285132f6567ca2500e173a0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99748343"
---
# <a name="isof-entity-sql"></a>ISOF (Entity SQL)

Determina se o tipo de uma expressão é do tipo especificado ou um de seus subtipos.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
expression IS [ NOT ] OF ( [ ONLY ] type )  
```  
  
## <a name="arguments"></a>Argumentos  

 `expression`  
 Qualquer expressão de consulta válida para determinar o tipo de.  
  
 NOT  
 Nega o resultado de EDM.Boolean de ESTÁ DE.  
  
 ONLY  
 Especifica que É returns `true` somente se `expression` é do tipo `type` e não qualquer um de seus subtipos.  
  
 `type`  
 O tipo para testar `expression` contra. O tipo URL deve ser qualificada.  
  
## <a name="return-value"></a>Valor retornado  

 `true` se `expression` é do tipo T e T é um tipo base, ou um tipo derivado de `type`; se `expression` nulo é nulo em runtime; caso contrário, `false`.  
  
## <a name="remarks"></a>Comentários  

 As expressões `expression IS NOT OF (type)` e `expression IS NOT OF (ONLY type)` são sintaticamente equivalentes a `NOT (expression IS OF (type))` e `NOT (expression IS OF (ONLY type))` , respectivamente.  
  
 A tabela a seguir mostra o comportamento do operador de `IS OF` sobre alguns padrões e típicos do canto. Todas as exceções são geradas do lado do cliente antes que o provedor obtenha chamado:  
  
|Padrão|Comportamento|  
|-------------|--------------|  
|o zero ESTÁ DE (EntityType)|Gera|  
|o zero ESTÁ DE (ComplexType)|Gera|  
|o zero ESTÁ DE (RowType)|Gera|  
|O DELEITE (zero) COMO EntityType ESTÁ DE (EntityType)|Retorna DBNull|  
|O DELEITE (zero) COMO ComplexType ESTÁ DE (ComplexType)|Gera|  
|O DELEITE (zero) COMO RowType ESTÁ DE (RowType)|Gera|  
|EntityType ESTÁ DE (EntityType)|Retorna retificam/falso|  
|ComplexType ESTÁ DE (ComplexType)|Gera|  
|RowType ESTÁ DE (RowType)|Gera|  
  
## <a name="example"></a>Exemplo  

 A consulta a seguir [!INCLUDE[esql](../../../../../../includes/esql-md.md)] usa o operador is of para determinar o tipo de uma expressão de consulta e, em seguida, usa o operador Treat para converter um objeto do tipo curso em uma coleção de objetos do tipo OnsiteCourse. A consulta é baseada no [modelo escolar](/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)).  
  
 [! Code-SQL [conceitos de entidade de DP # TREAT_ISOF] ~/Samples/Snippets/TSQL/VS_Snippets_Data/DP entityservices Concepts/TSQL/entitysql. SQL # treat_isof)]  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
