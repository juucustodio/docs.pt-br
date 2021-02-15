---
description: 'Saiba mais sobre: Method-Based exemplos de sintaxe de consulta: navegando em relações'
title: 'Exemplos de sintaxe da consulta com base em método: Navegando em relações'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: a0bfa4b1-99e5-4dd1-9912-4b825a9dc25c
ms.openlocfilehash: c209b97704fec86834375ad8c9eee4d717a61294
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99650513"
---
# <a name="method-based-query-syntax-examples-navigating-relationships"></a>Exemplos de sintaxe da consulta com base em método: Navegando em relações

As propriedades de navegação no Entity Framework são propriedades de atalho usadas para localizar as entidades nas extremidades de uma associação. As propriedades de navegação permitem que um usuário navegue de uma entidade para outra, ou uma entidade a entidades relacionadas por um conjunto de associações. Este tópico fornece exemplos de sintaxe de consulta baseada em método de como navegar em relações por meio de propriedades de navegação em LINQ to Entities consultas.  
  
 O Modelo de vendas AdventureWorks usado nesses exemplos é criado a partir das tabelas Contact, Address, Product, SalesOrderHeader e SalesOrderDetail no banco de dados de exemplo AdventureWorks.  
  
 Os exemplos neste tópico usam as seguintes `using` / `Imports` instruções:  
  
 [!code-csharp[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#importsusing)]
 [!code-vb[DP L2E Examples#ImportsUsing](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#importsusing)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir na sintaxe da consulta com base em método usa o método de <xref:System.Linq.Queryable.SelectMany%2A> para obter todos os pedidos de contatos cujo nome é “Zhou”. A propriedade de navegação de `Contact.SalesOrderHeader` é usada para obter a coleção de objetos `SalesOrderHeader` para cada contato.  
  
 [!code-csharp[DP L2E Examples#SelectEachContactsOrders_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selecteachcontactsorders_mq)]
 [!code-vb[DP L2E Examples#SelectEachContactsOrders_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selecteachcontactsorders_mq)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir na sintaxe da consulta com base em método usa o método de <xref:System.Linq.Queryable.Select%2A> para obter todos os IDs de contato e soma total de vencido para cada contato cujo nome é “Zhou”. A propriedade de navegação de `Contact.SalesOrderHeader` é usada para obter a coleção de objetos `SalesOrderHeader` para cada contato. O método de `Sum` usa a propriedade de navegação de `Contact.SalesOrderHeader` para somar o total vencido de todos os pedidos para cada contato.  
  
 [!code-csharp[DP L2E Examples#SelectEachContactsOrders2_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selecteachcontactsorders2_mq)]
 [!code-vb[DP L2E Examples#SelectEachContactsOrders2_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selecteachcontactsorders2_mq)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir na sintaxe da consulta com base em método obtém todos os pedidos de contatos cujo nome é “Zhou”. A propriedade de navegação de `Contact.SalesOrderHeader` é usada para obter a coleção de objetos `SalesOrderHeader` para cada contato. O nome e os pedidos de contato são retornados em um tipo anônimo.  
  
 [!code-csharp[DP L2E Examples#SelectEachContactsOrders3_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#selecteachcontactsorders3_mq)]
 [!code-vb[DP L2E Examples#SelectEachContactsOrders3_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#selecteachcontactsorders3_mq)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa `SalesOrderHeader.Address` e propriedades de navegação de `SalesOrderHeader.Contact` para obter a coleção de `Address` e de `Contact` objeto associado com cada pedido. O primeiro contato, endereço, o número de ordem de venda, e o total vencido para cada pedido a cidade de Seattle são retornados em um tipo anônimo.  
  
 [!code-csharp[DP L2E Examples#GetOrderInfoThruRelationships_MQ](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#getorderinfothrurelationships_mq)]
 [!code-vb[DP L2E Examples#GetOrderInfoThruRelationships_MQ](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#getorderinfothrurelationships_mq)]  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir usa o método `Where` para localizar os pedidos que foram feitos depois de 1° de dezembro de 2003 e, em seguida, usa a propriedade de navegação `order.SalesOrderDetail` para obter os detalhes de cada pedido.  
  
 [!code-csharp[DP L2E Examples#WhereNavProperty](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Examples/CS/Program.cs#wherenavproperty)]
 [!code-vb[DP L2E Examples#WhereNavProperty](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Examples/VB/Module1.vb#wherenavproperty)]  
  
## <a name="see-also"></a>Consulte também

- [Relações, propriedades de navegação e chaves estrangeiras](/ef/ef6/fundamentals/relationships)
- [Consultas no LINQ to Entities](queries-in-linq-to-entities.md)
