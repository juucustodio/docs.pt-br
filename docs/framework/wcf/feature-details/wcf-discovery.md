---
description: 'Saiba mais sobre: descoberta do WCF'
title: Descoberta de WCF
ms.date: 03/30/2017
helpviewer_keywords:
- WCF [WCF], discovery
- Windows Communication Foundation [WCF], discovery
- discovery [WCF]
ms.assetid: 462c4913-f388-45a9-9042-28ae96a4e735
ms.openlocfilehash: 67fa5800209676b11e9e49171483bf514b6a190a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99779628"
---
# <a name="wcf-discovery"></a>Descoberta de WCF

O Windows Communication Foundation (WCF) fornece suporte para permitir que os serviços sejam detectáveis em tempo de execução de maneira interoperável usando o protocolo WS-Discovery. Os serviços WCF podem anunciar sua disponibilidade na rede usando uma mensagem multicast ou um servidor proxy de descoberta. Os aplicativos cliente podem pesquisar a rede ou um servidor proxy de descoberta para encontrar serviços que atendam a um conjunto de critérios. Os tópicos nesta seção fornecem uma visão geral e descrevem o modelo de programação para esse recurso em detalhes.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Visão geral de descoberta do WCF](wcf-discovery-overview.md)  
 Fornece uma visão geral do suporte WS-Discovery fornecido pelo WCF.  
  
 [Modelo de objeto de descoberta do WCF](wcf-discovery-object-model.md)  
 Descreve as classes no modelo de objeto e a extensibilidade do suporte a WS-Discovery.  
  
 [Como: adicionar programaticamente a capacidade de descoberta para um cliente e serviço do WCF](how-to-programmatically-add-discoverability-to-a-wcf-service-and-client.md)  
 Mostra como tornar um serviço Windows Communication Foundation (WCF) detectável.  
  
 [Implementando um proxy de descoberta](implementing-a-discovery-proxy.md)  
 Descreve as etapas necessárias para implementar um proxy de descoberta, um serviço detectável que registra com o proxy de descoberta e um cliente que usa o proxy de descoberta para encontrar o serviço detectável.  
  
 [Controle de versão de descoberta](discovery-versioning.md)  
 Fornece uma breve visão geral de uma implementação de protótipo de alguns novos recursos de descoberta. Ele também fornece uma visão geral de como selecionar a versão de descoberta a ser usada.  
  
 [Configurando a descoberta em um arquivo de configuração](configuring-discovery-in-a-configuration-file.md)  
 Mostra como configurar a descoberta na configuração.  
  
 [Usando o canal cliente Discovery](using-the-discovery-client-channel.md)  
 Mostra como usar um canal de cliente de descoberta ao gravar um aplicativo cliente WCF.
