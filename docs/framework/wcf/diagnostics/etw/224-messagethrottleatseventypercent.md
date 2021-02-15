---
description: 'Saiba mais sobre: 224-MessageThrottleAtSeventyPercent'
title: 224 - MessageThrottleAtSeventyPercent
ms.date: 03/30/2017
ms.assetid: 82bbbfd7-10d2-41fd-805d-2443b0c1b96b
ms.openlocfilehash: 14c08371c5db7e6f7deb0a5851a1d24dfc94475e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794267"
---
# <a name="224---messagethrottleatseventypercent"></a>224 - MessageThrottleAtSeventyPercent

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|224|  
|Palavras-chave|EndToEndMonitoring, HealthMonitoring, solução de problemas, ServiceModel|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Quando uma das principais restrições de serviço for excedida, o `MessageThrottleExceeded` evento será emitido. Quando o pico de atividade é lento e o valor atual da limitação está em 70% do limite atual, esse evento é emitido. Observe que esse evento é emitido apenas uma vez, pois a atividade está lenta. Se o valor atual focalizar na marca de porcentagem de 70, (por exemplo, 70, 69, 70, 71, 70, 69), somente a primeira ocorrência de 70% resultará em um evento. Depois que esse evento é emitido, ocorrências futuras de exceder o limite do acelerador resulta em um `MessageThrottleExceeded` evento.  
  
## <a name="message"></a>Mensagem  

 O limite de ' %2 ' do acelerador ' %1 ' está em 70%%.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Nome do acelerador|`xs:string`|O nome do limite que foi excedido. `MaxConcurrentCalls`Ou, `MaxConcurrentInstances` , ou `MaxConcurrentSessions` ,|  
|Limite|`xs:long`|O limite atualmente configurado da limitação.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
