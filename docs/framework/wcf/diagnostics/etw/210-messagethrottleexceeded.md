---
description: 'Saiba mais sobre: 210-MessageThrottleExceeded'
title: 210 - MessageThrottleExceeded
ms.date: 03/30/2017
ms.assetid: 24ca08ea-c11c-4753-946e-98aa820f8711
ms.openlocfilehash: e02a115995fa0e18a2ed4582710881d30bb4b846
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794436"
---
# <a name="210---messagethrottleexceeded"></a>210 - MessageThrottleExceeded

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|210|  
|Palavras-chave|EndToEndMonitoring, HealthMonitoring, solução de problemas, ServiceModel|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido quando uma das três restrições de serviço principais tiver sido excedida. Observe que esse evento só é emitido quando o limite de limitação é inicialmente excedido. Por exemplo, se o limite de limitação para chamadas simultâneas for 10, a chamada simultânea 11 resultará em um `MessageThrottleExceeded` evento. A chamada de 12, não resulta em outro evento. Além disso, para evitar um fluxo de eventos barulhento, a atividade que focaliza o limite não resulta em outro evento. Neste exemplo, se duas chamadas forem concluídas, haverá 9 chamadas simultâneas. Se posteriormente mais duas chamadas chegarem, o valor atual será novamente 11. Isso não resulta em outro evento. Quando o valor atual cai para 70% do limite de limitação, um evento diferente é emitido, indicando que a atividade foi retardada. Atividade futura que excede o limite resulta em outro `MessageThrottleExceeded` evento sendo emitido. Neste exemplo, se a quantidade de chamadas simultâneas cair para 7 e, novamente, chegar a 11 e outro `MessageThrottleExceeded` evento for emitido.  
  
## <a name="message"></a>Mensagem  

 O limite de ' %2 ' do acelerador ' %1 ' foi atingido.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Nome do acelerador|`xs:string`|O nome do limite que foi excedido. `MaxConcurrentCalls`Ou, `MaxConcurrentInstances` , ou `MaxConcurrentSessions` ,|  
|Limite|`xs:long`|O limite atualmente configurado da limitação.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
