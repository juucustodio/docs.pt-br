---
description: 'Saiba mais sobre: como interceptar mensagens do serviço de dados (WCF Data Services)'
title: Como interceptar mensagens de serviço de dados (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, customizing
- query interceptors [WCF Data Services]
ms.assetid: 24b9df1b-b54b-4795-a033-edf333675de6
ms.openlocfilehash: 6768fa9f0c7ca9a5a6ed6faa318675f2c2c51543
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765276"
---
# <a name="how-to-intercept-data-service-messages-wcf-data-services"></a>Como interceptar mensagens de serviço de dados (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Com WCF Data Services, você pode interceptar mensagens de solicitação para poder adicionar lógica personalizada a uma operação. Para interceptar uma mensagem, você usa métodos especialmente atribuídos no serviço de dados. Para obter mais informações, consulte [Interceptors](interceptors-wcf-data-services.md).  
  
 O exemplo neste tópico usa o serviço de dados de exemplo Northwind. Esse serviço é criado quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
### <a name="to-define-a-query-interceptor-for-the-orders-entity-set"></a>Para definir um interceptor de consulta para o conjunto de entidades Orders  
  
1. No projeto do serviço de dados Northwind, abra o arquivo Northwind.svc.  
  
2. Na página de código para a classe `Northwind`, adicione a instrução `using` a seguir (`Imports` no Visual Basic).  
  
     [!code-csharp[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#usinglinqexpressions)]
     [!code-vb[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#usinglinqexpressions)]  
  
3. Na classe `Northwind`, defina um método de operação de serviço chamado `OnQueryOrders` da seguinte maneira:  
  
     [!code-csharp[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#queryinterceptordef)]
     [!code-vb[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#queryinterceptordef)]  
  
### <a name="to-define-a-change-interceptor-for-the-products-entity-set"></a>Para definir um interceptor de alteração para o conjunto de entidades Products  
  
1. No projeto do serviço de dados Northwind, abra o arquivo Northwind.svc.  
  
2. Na classe `Northwind`, defina um método de operação de serviço chamado `OnChangeProducts` da seguinte maneira:  
  
     [!code-csharp[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#changeinterceptordef)]
     [!code-vb[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#changeinterceptordef)]  
  
## <a name="example"></a>Exemplo  

 Este exemplo define um método de interceptor de consulta para o conjunto de entidades `Orders` que retorna uma expressão lambda. Esta expressão contém um delegado que filtra `Orders` solicitado com base em `Customers` relacionado que tem um nome de contato específico. O nome, por sua vez, é determinado com base no usuário solicitante. Este exemplo presume que o serviço de dados esteja hospedado dentro de um aplicativo ASP.NET que usa WCF, e a autenticação esteja habilitada. A classe <xref:System.Web.HttpContext> é usada para recuperar o princípio da solicitação atual.  
  
 [!code-csharp[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#queryinterceptor)]
 [!code-vb[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#queryinterceptor)]  
  
## <a name="example"></a>Exemplo  

 Este exemplo define um método de interceptador de alteração para o conjunto de entidades `Products`. Este método valida a entrada para o serviço para uma operação <xref:System.Data.Services.UpdateOperations.Add> ou <xref:System.Data.Services.UpdateOperations.Change> e gera uma exceção se uma alteração está sendo feita a um produto descontinuado. Ele também bloqueia a exclusão dos produtos como uma operação sem suporte.  
  
 [!code-csharp[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#changeinterceptor)]
 [!code-vb[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#changeinterceptor)]  
  
## <a name="see-also"></a>Consulte também

- [Como: definir uma operação de serviço](how-to-define-a-service-operation-wcf-data-services.md)
- [Configurando WCF Data Services](defining-wcf-data-services.md)
