---
description: 'Saiba mais sobre: como anexar uma entidade existente ao DataServiceContext (WCF Data Services)'
title: 'Como: anexar uma entidade existente ao DataServiceContext (WCF Data Services)'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, changing data
ms.assetid: e3f2d71d-434c-4e98-91c3-95adae4702b6
ms.openlocfilehash: 039225ec992a4ddd23fd9f7013e04562f6fe72a9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766589"
---
# <a name="how-to-attach-an-existing-entity-to-the-dataservicecontext-wcf-data-services"></a>Como: anexar uma entidade existente ao DataServiceContext (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

Quando uma entidade já existe em um serviço de dados, a biblioteca de cliente do WCF Data Services permite que você anexe um objeto que representa a entidade diretamente ao <xref:System.Data.Services.Client.DataServiceContext> sem primeiro executar uma consulta. Para obter mais informações, consulte [atualizando o serviço de dados](updating-the-data-service-wcf-data-services.md).  
  
 O exemplo deste tópico usa o serviço de dados de exemplo Northwind e as classes de serviço de dados do cliente geradas automaticamente. Esse serviço e as classes de dados do cliente são criados quando você conclui o guia de [início rápido do WCF Data Services](quickstart-wcf-data-services.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como criar um `Customer` objeto existente que contém alterações a serem salvas no serviço de dados. O objeto é anexado ao contexto e o <xref:System.Data.Services.Client.DataServiceContext.UpdateObject%2A> método é chamado para marcar o objeto anexado como <xref:System.Data.Services.Client.EntityStates.Modified> antes de o <xref:System.Data.Services.Client.DataServiceContext.SaveChanges%2A> método ser chamado.  
  
 [!code-csharp[Astoria Northwind Client#AttachObject](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_northwind_client/cs/source.cs#attachobject)]
 [!code-vb[Astoria Northwind Client#AttachObject](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_northwind_client/vb/source.vb#attachobject)]  
  
## <a name="see-also"></a>Consulte também

- [Biblioteca de cliente do WCF Data Services](wcf-data-services-client-library.md)
