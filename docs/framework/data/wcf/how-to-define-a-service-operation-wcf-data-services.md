---
description: 'Saiba mais sobre: como definir uma operação de serviço (WCF Data Services)'
title: Como definir uma operação de serviço (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- Service Operations [WCF Data Services]
- WCF Data Services, service operations
ms.assetid: dfcd3cb1-2f07-4d0b-b16a-6b056c4f45fa
ms.openlocfilehash: 9fcad3a31ea5b439c248ba103cbf4ddd75b8109a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765614"
---
# <a name="how-to-define-a-service-operation-wcf-data-services"></a>Como definir uma operação de serviço (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

WCF Data Services expor métodos que são definidos no servidor como operações de serviço. As operações de serviço permitem que um serviço de dados forneça acesso por meio de um URI para um método definido no servidor. Para definir uma operação de serviço, aplique o `WebGet]` atributo [ou `[WebInvoke]` ao método. Para dar suporte a operadores de consulta, a operação de serviço deve retornar uma <xref:System.Linq.IQueryable%601> instância. As operações de serviço podem acessar a fonte de dados subjacente por meio da <xref:System.Data.Services.DataService%601.CurrentDataSource%2A> propriedade no <xref:System.Data.Services.DataService%601> . Para obter mais informações, consulte [operações de serviço](service-operations-wcf-data-services.md).

O exemplo neste tópico define uma operação de serviço chamada `GetOrdersByCity` que retorna uma instância filtrada <xref:System.Linq.IQueryable%601> do `Orders` e `Order_Details` objetos relacionados. O exemplo acessa a <xref:System.Data.Objects.ObjectContext> instância que é a fonte de dados para o serviço de dados de exemplo Northwind. Esse serviço é criado quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).

### <a name="to-define-a-service-operation-in-the-northwind-data-service"></a>Para definir uma operação de serviço no serviço de dados Northwind

1. No projeto do serviço de dados Northwind, abra o arquivo Northwind.svc.

2. Na classe `Northwind`, defina um método de operação de serviço chamado `GetOrdersByCity` da seguinte maneira:

     [!code-csharp[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#serviceoperationdef)]
     [!code-vb[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#serviceoperationdef)]

3. No `InitializeService` método da `Northwind` classe, adicione o seguinte código para habilitar o acesso à operação de serviço:

     [!code-csharp[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#serviceoperationconfig)]
     [!code-vb[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#serviceoperationconfig)]

### <a name="to-query-the-getordersbycity-service-operation"></a>Para consultar a operação do serviço GetOrdersByCity

- Em um navegador da Web, insira um dos seguintes URIs para invocar a operação de serviço que é definida no exemplo a seguir:

  - `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'`

  - `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$top=2`

  - `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$expand=Order_Details&$orderby=RequiredDate desc`

## <a name="example"></a>Exemplo

O exemplo a seguir implementa uma operação de serviço chamada `GetOrderByCity` no serviço de dados Northwind. Esta operação usa o Entity Framework ADO.NET para retornar um conjunto de `Orders` objetos e relacionados `Order_Details` como uma <xref:System.Linq.IQueryable%601> instância com base no nome de cidade fornecido.

> [!NOTE]
> Há suporte para operadores de consulta neste ponto de extremidade de operação de serviço porque o método retorna uma <xref:System.Linq.IQueryable%601> instância.

[!code-csharp[Astoria Northwind Service#ServiceOperation](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_service/cs/northwind2.svc.cs#serviceoperation)]
[!code-vb[Astoria Northwind Service#ServiceOperation](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_service/vb/northwind2.svc.vb#serviceoperation)]

## <a name="see-also"></a>Consulte também

- [Configurando WCF Data Services](defining-wcf-data-services.md)
