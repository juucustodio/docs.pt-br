---
description: 'Saiba mais sobre: namespaces (Entity SQL)'
title: Namespaces (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 83991c21-60db-4af9-aca3-b416f6cae98e
ms.openlocfilehash: 70ef0021c3015fd661b42becb5371dcfd958f20f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99696549"
---
# <a name="namespaces-entity-sql"></a>Namespaces (Entity SQL)

[!INCLUDE[esql](../../../../../../includes/esql-md.md)] apresenta namespaces para evitar conflitos de nome para identificadores globais como nomes de tipo, conjuntos de entidades, funções, e assim por diante. O suporte a namespace no [!INCLUDE[esql](../../../../../../includes/esql-md.md)] é semelhante ao suporte de namespace no .NET Framework.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornece dois formulários que a cláusula group UTILIZAÇÃO: namespaces qualificadas (onde um alias mais curtas são fornecidas para o namespace), e namespaces não qualificado, como ilustrado no exemplo a seguir:  
  
 `USING System.Data;`  
  
 `USING tsql = System.Data;`  
  
## <a name="name-resolution-rules"></a>Regras de resolução de nomes  

 Se um identificador não puder ser resolvido nos escopos locais, o [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tentará localizar o nome nos escopos globais (os namespaces). [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tenta corresponder primeiro o identificador (prefixo) com uma namespaces qualificadas. Se houver uma correspondência, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] o tentará resolver o restante do identificador no namespace especificado. Se nenhuma correspondência for encontrada, uma exceção é lançada.  
  
 Em seguida, o [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tenta pesquisar todos os namespaces não qualificados (especificados no prólogo) para o identificador. Se o identificador pode ser localizado em exatamente um namespace, esse local é retornado. Se mais de um namespace tiver uma correspondência para o identificador, uma exceção é lançada. Se nenhum namespace puder ser identificado para o identificador, o [!INCLUDE[esql](../../../../../../includes/esql-md.md)] passará o nome para o próximo escopo externo (o <xref:System.Data.Common.DbCommand> <xref:System.Data.Common.DbConnection> objeto ou), conforme ilustrado no exemplo a seguir:  
  
```sql  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)  
```  
  
## <a name="differences-from-the-net-framework"></a>Diferenças do .NET Framework  

 No .NET Framework, você pode usar namespaces parcialmente qualificados. [!INCLUDE[esql](../../../../../../includes/esql-md.md)] não permite isso.  
  
## <a name="adonet-usage"></a>Uso do ADO.NET  

 Consultas são expressos por meio de objetos ADO.NET <xref:System.Data.Common.DbCommand> . os objetos de<xref:System.Data.Common.DbCommand> podem ser compilados sobre objetos de <xref:System.Data.Common.DbConnection> . Namespaces também podem ser especificadas como parte de objetos de <xref:System.Data.Common.DbCommand> e de <xref:System.Data.Common.DbConnection> . Se [!INCLUDE[esql](../../../../../../includes/esql-md.md)] o não puder resolver um identificador dentro da própria consulta, os namespaces externos serão investigados (com base em regras semelhantes).  
  
## <a name="see-also"></a>Consulte também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Visão geral da Entity SQL](entity-sql-overview.md)
