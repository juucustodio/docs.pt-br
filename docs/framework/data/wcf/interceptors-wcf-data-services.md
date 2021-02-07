---
description: 'Saiba mais sobre: interceptores (WCF Data Services)'
title: Interceptores (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, customizing
- query interceptors [WCF Data Services]
ms.assetid: e33ae8dc-8069-41d0-99a0-75ff28db7050
ms.openlocfilehash: f73ee498d0419df9e083248802ea52ed050a914b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765068"
---
# <a name="interceptors-wcf-data-services"></a>Interceptores (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

WCF Data Services permite que um aplicativo intercepte mensagens de solicitação para que você possa adicionar lógica personalizada a uma operação. Você pode usar essa lógica personalizada para validar dados em mensagens de entrada. Você também pode usá-la para restringir mais o escopo de uma solicitação de consulta, como inserir uma política de autorização personalizada com base na solicitação.  
  
 A interceptação é executada por métodos especialmente atribuídos no serviço de dados. Esses métodos são chamados por WCF Data Services no ponto apropriado do processamento de mensagens. Os interceptores são definidos com base no conjunto de entidades, e os métodos de interceptor não podem aceitar parâmetros da solicitação, como ocorre nas operações de serviço. Os métodos de interceptor de consulta, que são chamados durante o processamento de uma solicitação HTTP GET, devem retornar uma expressão lambda que determina se uma instância do conjunto de entidades do interceptor deve ser retornada pelos resultados da consulta. Esta expressão é usada pelo serviço de dados para refinar mais a operação solicitada. Veja a seguir um exemplo de definição de um interceptor de consulta.  
  
 [!code-csharp[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#queryinterceptordef)]
 [!code-vb[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#queryinterceptordef)]  
  
 Para obter mais informações, consulte [como: interceptar mensagens do serviço de dados](how-to-intercept-data-service-messages-wcf-data-services.md).  
  
 Os interceptores de alteração, que são chamados para processar operações sem consulta, devem retornar `void` (`Nothing` no Visual Basic). Os métodos de interceptor de alteração devem aceitar estes dois parâmetros:  
  
1. Um parâmetro de um tipo que seja compatível com o tipo de entidade do conjunto de entidades. Quando o serviço de dados chamar o interceptor de alteração, o valor desse parâmetro refletirá as informações de entidade enviadas pela solicitação.  
  
2. Um parâmetro do tipo <xref:System.Data.Services.UpdateOperations>. Quando o serviço de dados chamar o interceptor de alteração, o valor desse parâmetro refletirá a operação que a solicitação estiver tentando executar.  
  
 Veja a seguir um exemplo de definição de um interceptor de alteração.  
  
 [!code-csharp[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#changeinterceptordef)]
 [!code-vb[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#changeinterceptordef)]  
  
 Para obter mais informações, consulte [como: interceptar mensagens do serviço de dados](how-to-intercept-data-service-messages-wcf-data-services.md).  
  
 Os atributos a seguir têm suporte para interceptação.  
  
 **[QueryInterceptor (** *EntitySetName* **)]**  
 Os métodos com o atributo <xref:System.Data.Services.QueryInterceptorAttribute> aplicado são chamados quando uma solicitação HTTP GET é recebida para o recurso de destino do conjunto de entidades. Esses métodos devem sempre retornar uma expressão lambda no formato `Expression<Func<T,bool>>`.  
  
 **[ChangeInterceptor (** *EntitySetName* **)]**  
 Os métodos com o atributo <xref:System.Data.Services.ChangeInterceptorAttribute> aplicado são chamados quando uma solicitação HTTP, que não seja HTTP GET, é recebida para o recurso de destino do conjunto de entidades. Esses métodos devem sempre retornar `void` (`Nothing` no Visual Basic).  
  
 Para obter mais informações, consulte [como: interceptar mensagens do serviço de dados](how-to-intercept-data-service-messages-wcf-data-services.md).  
  
## <a name="see-also"></a>Consulte também

- [Operações de serviço](service-operations-wcf-data-services.md)
