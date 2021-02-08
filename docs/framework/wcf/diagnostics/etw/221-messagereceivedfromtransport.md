---
description: 'Saiba mais sobre: 221-MessageReceivedFromTransport'
title: 221 - MessageReceivedFromTransport
ms.date: 03/30/2017
ms.assetid: 4995f0d5-c182-4d97-981f-6951da6df1fb
ms.openlocfilehash: 0cc15fa95ae321083afa2792810807971e909e6b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99803497"
---
# <a name="221---messagereceivedfromtransport"></a>221 - MessageReceivedFromTransport

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|221|  
|Palavras-chave|EndToEndMonitoring, solução de problemas, ServiceModel|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido quando o modelo de serviço recebe uma mensagem do transporte.  
  
## <a name="message"></a>Mensagem  

 O Dispatcher recebeu uma mensagem do transporte. ID de correlação = = ' %1 '.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|ID de Correlação|`xs:GUID`|A ID da atividade usada para correlacionar um `MessageSentToTransport` evento de um serviço ou cliente ao seu correspondente `MessageReceivedFromTransport` no outro final.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
