---
description: 'Saiba mais sobre: como habilitar o acesso ao serviço de dados (WCF Data Services)'
title: Como habilitar o acesso ao serviço de dados (WCF Data Services)
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF Data Services, configuring
ms.assetid: 3d830bcd-32b4-4f26-9287-d58a071452c6
ms.openlocfilehash: 42be9c4c31da7bbbfef07958deef685d52df597b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99765419"
---
# <a name="how-to-enable-access-to-the-data-service-wcf-data-services"></a>Como habilitar o acesso ao serviço de dados (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

No WCF Data Services, você deve conceder explicitamente acesso aos recursos que são expostos por um serviço de dados. Isso significa que, depois de criar um novo serviço de dados, você ainda deve fornecer acesso explicitamente a recursos individuais como conjuntos de entidades. Este tópico mostra como habilitar o acesso de leitura e gravação para cinco dos conjuntos de entidades no serviço de dados Northwind que é criado quando você conclui o guia de [início rápido](quickstart-wcf-data-services.md). Como a <xref:System.Data.Services.EntitySetRights> enumeração é definida usando o <xref:System.FlagsAttribute> , você pode usar um operador OR lógico para especificar várias permissões para um único conjunto de entidades.  
  
> [!NOTE]
> Qualquer cliente que possa acessar o aplicativo ASP.NET também pode acessar os recursos expostos pelo serviço de dados. Em um serviço de dados de produção, para impedir o acesso não autorizado aos recursos, você também deve proteger o próprio aplicativo. Para obter mais informações, consulte [securing ASP.NET Web sites](/previous-versions/aspnet/91f66yxt(v=vs.100)).  
  
### <a name="to-enable-access-to-the-data-service"></a>Para habilitar o acesso ao serviço de dados  
  
- No código para o serviço de dados, substitua o código de espaço reservado na função `InitializeService` pelo seguinte:  
  
     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria_quickstart_service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria_quickstart_service/vb/northwind.svc.vb#allreadconfig)]  
  
     Isso permite que os clientes tenham acesso de leitura e gravação `Orders` aos `Order_Details` conjuntos de entidades e e acesso somente leitura aos `Customers` conjuntos de entidades.  
  
## <a name="see-also"></a>Consulte também

- [Como: desenvolver um serviço de dados do WCF em execução no IIS](how-to-develop-a-wcf-data-service-running-on-iis.md)
- [Configurar o serviço de dados](configuring-the-data-service-wcf-data-services.md)
