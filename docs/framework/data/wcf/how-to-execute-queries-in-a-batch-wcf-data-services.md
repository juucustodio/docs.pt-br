---
description: 'Saiba mais sobre: como executar consultas em um lote (WCF Data Services)'
title: Como executar consultas em um lote (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, batch requests
ms.assetid: 3b4db7df-bd33-43a1-8ea4-63a18e131f97
ms.openlocfilehash: bcd95be57d2f3f2cea075a4b87fb6858c59ea41e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765289"
---
# <a name="how-to-execute-queries-in-a-batch-wcf-data-services"></a>Como executar consultas em um lote (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Usando a biblioteca de cliente WCF Data Services, você pode executar mais de uma consulta no serviço de dados em um único lote. Para obter mais informações, consulte [operações de envio em lote](batching-operations-wcf-data-services.md).  
  
 O exemplo deste tópico usa o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como chamar o <xref:System.Data.Services.Client.DataServiceContext.ExecuteBatch%2A> método para executar uma matriz de <xref:System.Data.Services.Client.DataServiceRequest%601> objetos que contém consultas que retornam ambos os `Customers` `Products` objetos e do serviço de dados Northwind. A coleção de <xref:System.Data.Services.Client.QueryOperationResponse%601> objetos no retornado <xref:System.Data.Services.Client.DataServiceResponse> é enumerada e a coleção de objetos contidos em cada um <xref:System.Data.Services.Client.QueryOperationResponse%601> também é enumerada.  
  
 [!code-csharp[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#batchquery)]
 [!code-vb[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#batchquery)]  
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
