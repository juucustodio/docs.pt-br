---
description: 'Saiba mais sobre: 205-OperationInvoked'
title: 205 - OperationInvoked
ms.date: 03/30/2017
ms.assetid: 9c8d6c90-dfa5-4ae0-a589-96679a8fb3ba
ms.openlocfilehash: 09afe4c29c5f56b06bbf524dd13d88ddf2319063
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644964"
---
# <a name="205---operationinvoked"></a>205 - OperationInvoked

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|205|  
|Palavras-chave|Solução de problemas, ServiceModel|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido logo antes de o padrão do modelo de serviço `OperationInvoker` iniciar uma chamada para um método.  
  
## <a name="message"></a>Mensagem  

 Um OperationInvoker invocou o método ' %1 '. Informações do chamador: ' %2 '.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Nome do método|`xs:string`|O nome do CLR do método que foi invocado pelo `OperationInvoker` .|  
|Informações de chamador|`xs:string`|O endereço IP e o número da porta do cliente no formato ' IPAddress: PortNumber '. Os dois valores são recuperados da propriedade de mensagem ' System. ServiceModel. Channels. RemoteEndpointMessageProperty ' dentro do contexto de operação. Observe que, para associações não TCP, esse valor `null` .|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
