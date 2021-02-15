---
description: 'Saiba mais sobre: Entity SQL Language'
title: Linguagem Entity SQL
ms.date: 03/30/2017
ms.assetid: 9e7d8837-28c5-429d-a824-7bafb59724cf
ms.openlocfilehash: c05e561e5da3f9ee8788a25f8ca97b22444e109f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99724564"
---
# <a name="entity-sql-language"></a>Linguagem Entity SQL

O Entity SQL é uma linguagem de consulta independente de armazenamento semelhante ao SQL. O Entity SQL permite que você consulte dados de entidade, como objetos ou em forma de tabela. Você deve considerar o uso do Entity SQL nos seguintes casos:  
  
- Quando uma consulta deve ser construída dinamicamente em runtime. Nesse caso, você também deve considerar o uso dos métodos do construtor de consultas de <xref:System.Data.Objects.ObjectQuery%601>, em vez de construir uma cadeia de caracteres de consulta Entity SQL em runtime.  
  
- Quando você deseja definir uma consulta como parte da definição do modelo. Somente o Entity SQL tem suporte em um modelo de dados. Para obter mais informações, consulte [elemento QueryView (MSL)](/ef/ef6/modeling/designer/advanced/edmx/msl-spec#queryview-element-msl)  
  
- Ao usar EntityClient para retornar dados de entidade somente leitura como conjuntos de linhas usando <xref:System.Data.EntityClient.EntityDataReader>. Para obter mais informações, consulte [EntityClient Provider para o Entity Framework](../entityclient-provider-for-the-entity-framework.md).  
  
- Se você já for um especialista em linguagens de consulta baseadas em SQL, o Entity SQL poderá parecer a opção mais natural para você.  
  
## <a name="using-entity-sql-with-the-entityclient-provider"></a>Usando Entity SQL com o provedor EntityClient  

 Se você desejar usar o Entity SQL com o provedor EntityClient, consulte os seguintes tópicos para obter mais informações:  
  
 [Provedor EntityClient para Entity Framework](../entityclient-provider-for-the-entity-framework.md)  
  
 [Como: criar uma cadeia de conexão EntityConnection](../how-to-build-an-entityconnection-connection-string.md)  
  
 [Como: executar uma consulta que retorna resultados de PrimitiveType](../how-to-execute-a-query-that-returns-primitivetype-results.md)  
  
 [Como: executar uma consulta que retorna resultados de StructuralType](../how-to-execute-a-query-that-returns-structuraltype-results.md)  
  
 [Como: executar uma consulta que retorna resultados de RefType](../how-to-execute-a-query-that-returns-reftype-results.md)  
  
 [Como: executar uma consulta que retorna tipos complexos](../how-to-execute-a-query-that-returns-complex-types.md)  
  
 [Como: executar uma consulta que retorna aninhados coleções](../how-to-execute-a-query-that-returns-nested-collections.md)  
  
 [Como: executar uma consulta Entity SQL parametrizada usando EntityCommand](../how-to-execute-a-parameterized-entity-sql-query-using-entitycommand.md)  
  
 [Como: executar um procedimento armazenado parametrizado usando EntityCommand](../how-to-execute-a-parameterized-stored-procedure-using-entitycommand.md)  
  
 [Como: executar uma consulta polimorfo](../how-to-execute-a-polymorphic-query.md)  
  
 [Como: navegar em relações com o operador navegar](../how-to-navigate-relationships-with-the-navigate-operator.md)  
  
## <a name="using-entity-sql-with-object-queries"></a>Usando o Entity SQL com consultas de objetos  

 Se você desejar usar o Entity SQL com consultas de objetos, consulte os seguintes tópicos para obter mais informações:  
  
 [Como executar uma consulta que retorna objetos de tipo de entidade](/previous-versions/dotnet/netframework-4.0/bb738694(v=vs.100))  
  
 [Como executar uma consulta parametrizada](/previous-versions/dotnet/netframework-4.0/bb738521(v=vs.100))  
  
 [Como navegar em relações usando propriedades de navegação](/previous-versions/dotnet/netframework-4.0/bb896321(v=vs.100))  
  
 [Como: chamar uma função User-Defined](/previous-versions/dotnet/netframework-4.0/dd490951(v=vs.100))  
  
 [Como filtrar dados](/previous-versions/dotnet/netframework-4.0/cc716755(v=vs.100))  
  
 [Como classificar dados](/previous-versions/dotnet/netframework-4.0/cc716784(v=vs.100))  
  
 [Como agrupar dados](/previous-versions/dotnet/netframework-4.0/bb896341(v=vs.100))  
  
 [Como agregar dados](/previous-versions/dotnet/netframework-4.0/cc716738(v=vs.100))  
  
 [Como executar uma consulta que retorna objetos de tipo anônimo](/previous-versions/dotnet/netframework-4.0/bb738512(v=vs.100))  
  
 [Como executar uma consulta que retorna uma coleção de tipos primitivos](/previous-versions/dotnet/netframework-4.0/bb738451(v=vs.100))  
  
 [Como consultar objetos relacionados em uma EntityCollection](/previous-versions/dotnet/netframework-4.0/cc716708(v=vs.100))  
  
 [Como ordenar a União de duas consultas](/previous-versions/dotnet/netframework-4.0/bb896299(v=vs.100))  
  
 [Como: paginar os resultados da consulta](/previous-versions/dotnet/netframework-4.0/bb738702(v=vs.100))  
  
## <a name="in-this-section"></a>Nesta seção  

 [Visão geral da Entity SQL](entity-sql-overview.md)  
  
 [Referência de Entity SQL](entity-sql-reference.md)  
  
## <a name="see-also"></a>Consulte também

- [ADO.NET Entity Framework](../index.md)
- [Referência de linguagem](index.md)
