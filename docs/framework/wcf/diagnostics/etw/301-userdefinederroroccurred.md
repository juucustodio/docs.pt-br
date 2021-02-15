---
description: 'Saiba mais sobre: 301-UserDefinedErrorOccurred'
title: 301 - UserDefinedErrorOccurred
ms.date: 03/30/2017
ms.assetid: a0285d1c-550f-4c14-9c36-a96e97f1c4e4
ms.openlocfilehash: 15e12bb27e3626f80747498a1387aa90fc461d28
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794241"
---
# <a name="301---userdefinederroroccurred"></a>301 - UserDefinedErrorOccurred

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|301|  
|Palavras-chave|Solução de problemas, HealthMonitoring, UserEvents, ServiceModel, EndToEndMonitoring|  
|Level|Erro do|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido a partir do código do usuário. Os desenvolvedores podem emitir esse evento quando ocorre um erro personalizado definido em seu serviço. Isso pode ser feito usando as <xref:System.Diagnostics.Eventing> APIs. Além disso, há um exemplo do WCF que encapsula essa API e demonstra como emitir esse evento corretamente.  
  
## <a name="message"></a>Mensagem  

 Nome: ' %1 ', referência: ' %2 ', carga: %3  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Nome|`xs:string`|O nome definido pelo usuário do evento.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|Carga útil|`xs:string`|A carga definida pelo usuário do evento.|
