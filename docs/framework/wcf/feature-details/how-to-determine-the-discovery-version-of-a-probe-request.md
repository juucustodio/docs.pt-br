---
description: 'Saiba mais sobre: como determinar a versão de descoberta de uma solicitação de investigação'
title: Como determinar a versão de descoberta de uma solicitação de investigação
ms.date: 03/30/2017
ms.assetid: b3c4e2e2-2957-4074-ae6a-776a5ca84278
ms.openlocfilehash: c41283cb84d75dd2dbf7e86da0dec075ab8b6635
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793786"
---
# <a name="how-todetermine-the-discovery-version-of-a-probe-request"></a>Como determinar a versão de descoberta de uma solicitação de investigação

Um proxy de descoberta pode expor vários pontos de extremidade de descoberta usando diferentes versões de descoberta. Quando uma solicitação de investigação de multicast UDP chega ao proxy, o proxy deve responder com uma mensagem de supressão de multicast. Para fazer isso, seria necessário saber a versão de descoberta da solicitação.

## <a name="to-determine-the-discovery-version-of-a-probe-request"></a>Para determinar a versão de descoberta de uma solicitação de investigação

No método que responde a uma solicitação de investigação (por exemplo <xref:System.ServiceModel.Discovery.DiscoveryProxy.OnBeginFind%2A?displayProperty=nameWithType> ), use a <xref:System.ServiceModel.OperationContext.Current%2A?displayProperty=nameWithType> propriedade estática para pesquisar por um <xref:System.ServiceModel.Discovery.DiscoveryOperationContextExtension> , conforme mostrado no código a seguir.

```csharp
DiscoveryOperationContextExtension doce = OperationContext.Current.Extensions.Find<DiscoveryOperationContextExtension>();
// Access the discovery version from the DiscoveryOperationContextExtension
doce.DiscoveryVersion;
```

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Discovery.Configuration.AnnouncementEndpointElement.DiscoveryVersion%2A>
- [Implementando um proxy de descoberta](implementing-a-discovery-proxy.md)
