---
description: 'Saiba mais sobre: como determinar o número de entidades retornadas por uma consulta (WCF Data Services)'
title: Como determinar o número de entidades retornadas por uma consulta (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, row count
ms.assetid: 03d41a82-df95-40ac-8439-a6c327d37ba8
ms.openlocfilehash: f8eb305bc515d1d69025ce3bcd0a6a9f3baf8232
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794982"
---
# <a name="how-to-determine-the-number-of-entities-returned-by-a-query-wcf-data-services"></a>Como determinar o número de entidades retornadas por uma consulta (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Com WCF Data Services, você pode determinar o número de entidades que estão no conjunto de entidades especificado por um URI de consulta. Essa contagem pode ser incluída juntamente com o resultado da consulta ou como um valor inteiro. Para obter mais informações, consulte [consultando o serviço de dados](querying-the-data-service-wcf-data-services.md).  
  
 O exemplo deste tópico usa o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  

 Este exemplo executa uma consulta depois de chamar o <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A> método. A <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> propriedade retorna o número de entidades no `Customers` conjunto de entidades.  
  
 [!code-csharp[Astoria Northwind Client#CountAllCustomers](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#countallcustomers)]
 [!code-vb[Astoria Northwind Client#CountAllCustomers](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#countallcustomers)]  
  
## <a name="example"></a>Exemplo  

 Este exemplo chama o <xref:System.Linq.Enumerable.Count%2A> método para retornar apenas um valor inteiro que é o número de entidades no `Customers` conjunto de entidades.  
  
 [!code-csharp[Astoria Northwind Client#CountAllCustomersValueOnly](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#countallcustomersvalueonly)]
 [!code-vb[Astoria Northwind Client#CountAllCustomersValueOnly](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#countallcustomersvalueonly)]  
  
## <a name="see-also"></a>Consulte também

- [Consultar o serviço de dados](querying-the-data-service-wcf-data-services.md)
