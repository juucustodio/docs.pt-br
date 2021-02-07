---
description: 'Saiba mais sobre: controle de versão de descoberta'
title: Controle de versão de descoberta
ms.date: 03/30/2017
ms.assetid: f91c6d0a-3af2-45c5-9a5c-e75390619836
ms.openlocfilehash: 075fefce0477810336c8b857343984070ed89b37
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99743181"
---
# <a name="discovery-versioning"></a>Controle de versão de descoberta

Este tópico fornece uma breve visão geral da implementação de alguns novos recursos de descoberta. Ele também fornece uma visão geral de como selecionar a versão de descoberta a ser usada.

## <a name="discovery-versioning"></a>Controle de versão de descoberta

O recurso de descoberta inclui suporte para três versões do protocolo WS_Discovery. As APIs de descoberta permitem selecionar qual versão do protocolo você deseja usar. Este documento descreve brevemente as configurações relacionadas à versão.

As classes de descoberta a seguir agora têm uma <xref:System.ServiceModel.Discovery.DiscoveryVersion> propriedade e usam um <xref:System.ServiceModel.Discovery.DiscoveryVersion> argumento em seus construtores:

- <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>

- <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>

- <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>

- <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>

### <a name="discoveryversionwsdiscoveryapril2005"></a>DiscoveryVersion.WSDiscoveryApril2005

Fornecer <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryApril2005> como um parâmetro de construtor faz a implementação usar a versão April2005 do protocolo WS-Discovery. Esta versão corresponde à versão publicada da especificação do protocolo de WS-Discovery. Esta versão deve ser usada para interoperar com o aplicativo herdado utilizando a versão April2005 do WS-Discovery.

### <a name="discoveryversionwsdiscovery11"></a>DiscoveryVersion.WSDiscovery11

A versão de descoberta padrão usada pelas APIs é <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscovery11> . Esta é a versão padronizada atual do protocolo de WS-Discovery.

## <a name="discoveryversionwsdiscoverycd1"></a>DiscoveryVersion.WSDiscoveryCD1

Fornecer <xref:System.ServiceModel.Discovery.DiscoveryVersion.WSDiscoveryCD1> como um parâmetro de construtor faz a implementação usar a versão de rascunho 1 do Comitê do protocolo WS-Discovery. Esta versão do protocolo deve ser usada para interoperar com implementações que executam a versão do CD1 do protocolo WS-Discovery.

## <a name="supporting-multiple-udp-discovery-endpoints-for-different-discovery-versions-on-a-single-service-host"></a>Suporte a vários pontos de extremidade de descoberta de UDP para versões de descoberta diferentes em um único host de serviço

Talvez você queira expor vários pontos de extremidade de descoberta de UDP para diferentes versões de descoberta em um único host de serviço. Para fazer isso, você deve especificar um endereço exclusivo para cada ponto de extremidade de descoberta de UDP. O exemplo a seguir mostra como fazer isso.

```csharp
UdpDiscoveryEndpoint newVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscovery11);
UdpDiscoveryEndpoint oldVersionUdpEndpoint = new UdpDiscoveryEndpoint(DiscoveryVersion.WSDiscoveryApril2005);

newVersionUdpEndpoint.Address = new EndpointAddress(newVersionUdpEndpoint.Address.Uri.ToString() + "/version11");
oldVersionUdpEndpoint.Address = new EndpointAddress(oldVersionUdpEndpoint.Address.Uri.ToString() + "/versionApril2005");

serviceHost.AddServiceEndpoint(newVersionUdpEndpoint);
serviceHost.AddServiceEndpoint(oldVersionUdpEndpoint);
```
