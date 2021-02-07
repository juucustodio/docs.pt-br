---
description: 'Saiba mais sobre: provedores de serviço de dados personalizados (WCF Data Services)'
title: Provedores de serviço de dados personalizados (WCF Data Services)
ms.date: 03/30/2017
helpviewer_keywords:
- WCF Data Services, providers
ms.assetid: e702ecdb-3419-4743-92a9-c3c0e7d44082
ms.openlocfilehash: df0cafae46cfdbd71a96341686a9200f032a9938
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99766147"
---
# <a name="custom-data-service-providers-wcf-data-services"></a>Provedores de serviço de dados personalizados (WCF Data Services)

[!INCLUDE [wcf-deprecated](~/includes/wcf-deprecated.md)]

WCF Data Services inclui um conjunto de provedores que permite que você defina um modelo de dados com base em tipos de dados de associação tardia.  
  
|Provedor|Descrição|  
|--------------|-----------------|  
|Provedor de metadados|Este é o principal provedor de serviços de dados personalizados que permite que você defina um modelo de dados personalizado em tempo de execução implementando a <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> interface.|  
|Provedor de consultas|Esse provedor permite que você execute consultas em um modelo de dados personalizado que é definido usando a <xref:System.Data.Services.Providers.IDataServiceMetadataProvider> interface. O provedor de consultas é criado com a implementação da <xref:System.Data.Services.Providers.IDataServiceQueryProvider> interface.|  
|Atualizar provedor|Esse provedor permite que você faça atualizações em tipos expostos em um provedor de serviços de dados personalizado e gerencie a simultaneidade. Um provedor de atualização é criado com a implementação da <xref:System.Data.Services.Providers.IDataServiceUpdateProvider> interface|  
|Provedor de paginação|Esse provedor é usado com o provedor de serviços de dados personalizado para habilitar o suporte de paginação controlado por servidor. Um provedor de paginação para um serviço de dados personalizado é criado com a implementação da <xref:System.Data.Services.Providers.IDataServicePagingProvider> interface.|  
|Provedor de streaming|Esse provedor permite expor tipos de dados de objeto binário grande como um fluxo. Um provedor de streaming é criado com a implementação da interface <xref:System.Data.Services.Providers.IDataServiceStreamProvider>. O provedor de streaming também pode ser usado com provedores de fonte de dados Entity Framework e Reflection. Para obter mais informações, consulte [streaming Provider](streaming-provider-wcf-data-services.md).|  
  
## <a name="see-also"></a>Consulte também

- [Provedores de serviços de dados](data-services-providers-wcf-data-services.md)
- [Provedor de Entity Framework](entity-framework-provider-wcf-data-services.md)
- [Provedor de reflexão](reflection-provider-wcf-data-services.md)
