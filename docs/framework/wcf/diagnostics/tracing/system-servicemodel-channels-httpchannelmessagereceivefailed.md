---
description: 'Saiba mais sobre: System. ServiceModel. Channels. HttpChannelMessageReceiveFailed'
title: System.ServiceModel.Channels.HttpChannelMessageReceiveFailed
ms.date: 03/30/2017
ms.assetid: 9eb311da-fdcc-4dd3-9d85-05b3280dfdda
ms.openlocfilehash: 41c31305fabc369faedec460fc3a042426d45e37
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99769865"
---
# <a name="systemservicemodelchannelshttpchannelmessagereceivefailed"></a>System.ServiceModel.Channels.HttpChannelMessageReceiveFailed

Falha ao receber uma mensagem por um canal HTTP.  
  
## <a name="description"></a>Descrição  

 Esse rastreamento pode ser emitido como um aviso ou um erro. Em ambos os casos, o rastreamento é emitido quando um ouvinte compatível não é encontrado para uma solicitação HTTP de entrada e a solicitação HTTP é descartada. Isso pode acontecer porque o verbo HTTP da solicitação não foi reconhecido por nenhum ouvinte HTTP ou porque nenhum ouvinte estava escutando no endereço para o qual a solicitação foi destinada. O rastreamento é emitido como um aviso no caso hospedado automaticamente e como um erro quando o serviço é hospedado no IIS.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
