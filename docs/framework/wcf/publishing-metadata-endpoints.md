---
description: 'Saiba mais sobre: publicando pontos de extremidade de metadados'
title: Publicando pontos de extremidade de metadados
ms.date: 03/30/2017
ms.assetid: 29cd8a60-dfb7-460c-bf5a-c2b31b782671
ms.openlocfilehash: 8204a62413e09c0fbc6effaae1fd752aee397147
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99726670"
---
# <a name="publishing-metadata-endpoints"></a>Publicando pontos de extremidade de metadados

Os serviços Windows Communication Foundation (WCF) publicam metadados publicando um ou mais pontos de extremidade de metadados. A publicação de metadados de serviço torna os metadados disponíveis usando protocolos padronizados, como WS-MetadataExchange (MEX) e solicitações HTTP/GET. Os pontos de extremidade de metadados são semelhantes a outros pontos de extremidade de serviço, pois têm um endereço, uma associação e um contrato, e podem ser adicionados a um host de serviço por meio da configuração ou no código. Para habilitar a publicação de pontos de extremidade de metadados, você deve adicionar o <xref:System.ServiceModel.Description.ServiceMetadataBehavior> comportamento do serviço ao serviço.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Como: publicar metadados para um serviço usando um arquivo de configuração](./feature-details/how-to-publish-metadata-for-a-service-using-a-configuration-file.md)  
 Demonstra como configurar um serviço WCF para publicar metadados para que os clientes possam recuperar os metadados usando uma WS-MetadataExchange ou uma solicitação HTTP/GET usando a `?wsdl` cadeia de caracteres de consulta.  
  
 [Como: publicar metadados utilizando código para um serviço](./feature-details/how-to-publish-metadata-for-a-service-using-code.md)  
 Demonstra como habilitar a publicação de metadados para um serviço WCF no código para que os clientes possam recuperar os metadados usando uma WS-MetadataExchange ou uma solicitação HTTP/GET usando a `?wsdl` cadeia de caracteres de consulta.  
  
## <a name="see-also"></a>Consulte também

- [Publicando metadados](./feature-details/publishing-metadata.md)
