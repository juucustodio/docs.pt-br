---
description: 'Saiba mais sobre: como criar um serviço de dados usando o provedor de reflexão (WCF Data Services)'
title: 'Como: criar um serviço de dados usando o provedor de reflexão (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: 7315c6d8-f452-4fb2-a0c1-76ab0593c146
ms.openlocfilehash: 1c4d131b21c69e11dd6d8b574e4c22a6af7c5a25
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766215"
---
# <a name="how-to-create-a-data-service-using-the-reflection-provider-wcf-data-services"></a>Como: criar um serviço de dados usando o provedor de reflexão (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

WCF Data Services permite que você defina um modelo de dados baseado em classes arbitrárias, desde que essas classes sejam expostas como objetos que implementam a <xref:System.Linq.IQueryable%601> interface. Para obter mais informações, consulte [provedores de serviços de dados](data-services-providers-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir define um modelo de dados que inclui `Orders` e `Items` . A classe de contêiner de entidade `OrderItemData` tem dois métodos públicos que retornam <xref:System.Linq.IQueryable%601> interfaces. Essas interfaces são os conjuntos de entidades dos `Orders` `Items` tipos de entidade e. Um `Order` pode incluir vários `Items` , portanto, o `Orders` tipo de entidade tem uma `Items` propriedade de navegação que retorna uma coleção de `Items` objetos. A `OrderItemData` classe de contêiner de entidade é o tipo genérico da <xref:System.Data.Services.DataService%601> classe da qual o `OrderItems` serviço de dados é derivado.  
  
> [!NOTE]
> Como este exemplo demonstra um provedor de dados na memória e as alterações não são mantidas fora das instâncias do objeto atual, não há nenhum benefício derivado da implementação da <xref:System.Data.Services.IUpdatable> interface. Para obter um exemplo que implementa a <xref:System.Data.Services.IUpdatable> interface, consulte [como criar um serviço de dados usando uma fonte de dados LINQ to SQL](create-a-data-service-using-linq-to-sql-wcf.md).  
  
 [!code-csharp[Astoria Reflection Provider#CustomIQueryable](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_reflection_provider/cs/orderitems.svc.cs#customiqueryable)]
 [!code-vb[Astoria Reflection Provider#CustomIQueryable](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_reflection_provider/vb/orderitems.svc.vb#customiqueryable)]  
  
## <a name="see-also"></a>Consulte também

- [Como: criar um serviço de dados usando uma fonte de dados LINQ to SQL](create-a-data-service-using-linq-to-sql-wcf.md)
- [Provedores de serviços de dados](data-services-providers-wcf-data-services.md)
- [Como: criar um serviço de dados usando uma fonte de dados do ADO.NET Entity Framework](create-a-data-service-using-an-adonet-ef-data-wcf.md)
