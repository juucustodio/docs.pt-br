---
description: 'Saiba mais sobre: rastreamento analítico com ETW'
title: Rastreamento analítico com ETW
ms.date: 03/30/2017
helpviewer_keywords:
- diagnostics [WCF], analytic tracing
- administration [WCF], analytic tracing
- analytic tracing [WCF]
ms.assetid: 1d518e47-a38d-41e8-93d7-8c3b361f6a56
ms.openlocfilehash: fd40d40de2508fd251c793e4455c1e656a1cbbf6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798791"
---
# <a name="analytic-tracing-with-etw"></a>Rastreamento analítico com ETW

O rastreamento analítico do Windows Communication Foundation (WCF) oferece uma maneira de capturar informações de diagnóstico durante a execução de um serviço WCF. Os eventos de rastreamento analítico do WCF são emitidos em pontos-chave na pilha do WCF para permitir a solução de problemas de serviços WCF em um ambiente de produção. O rastreamento analítico para serviços WCF tem um impacto mínimo sobre o desempenho de um servidor de produtos que hospeda [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] Serviços WCF, pois esses eventos são emitidos com muita eficiência para uma sessão do ETW (rastreamento de eventos para Windows).  
  
## <a name="in-this-section"></a>Nesta seção  

 [Visão geral de rastreamento analítico](analytic-tracing-overview.md)  
 Discute como o rastreamento analítico do WCF funciona no [!INCLUDE[netfx_current_long](../../../../../includes/netfx-current-long-md.md)] .  
  
 [Rastreamento analítico habilitado dinamicamente](dynamically-enabling-analytic-tracing.md)  
 Discute como habilitar ou desabilitar o rastreamento dinamicamente usando o ETW.  
  
 [Configurando rastreamento de fluxo de mensagem](configuring-message-flow-tracing.md)  
 Descreve como configurar o rastreamento de fluxo de mensagens.  
  
 [Referência de evento de rastreamento analítico](analytic-trace-event-reference.md)  
 Mostra uma tabela de IDs de evento com seus níveis de evento, mensagens de evento e palavras-chave.  
  
## <a name="see-also"></a>Consulte também

- [Serviços e rastreamento de eventos WCF para Windows](../../samples/wcf-services-and-event-tracing-for-windows.md)
- [Eventos de rastreamento no rastreamento de evento no Windows](../../../windows-workflow-foundation/samples/tracking-events-into-event-tracing-in-windows.md)
