---
description: 'Saiba mais sobre: 201-ClientMessageInspectorAfterReceiveInvoked'
title: 201 - ClientMessageInspectorAfterReceiveInvoked
ms.date: 03/30/2017
ms.assetid: 9ff637f1-cc26-4400-ab9b-546f70e5057d
ms.openlocfilehash: 511f8bd039219d031c311f7def7b360b74df1a0a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99645146"
---
# <a name="201---clientmessageinspectorafterreceiveinvoked"></a>201 - ClientMessageInspectorAfterReceiveInvoked

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|201|  
|Palavras-chave|Solução de problemas, ServiceModel|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido depois que o modelo de serviço invoca o `AfterReceiveReply` método em um inspetor de mensagem do cliente.  
  
## <a name="message"></a>Mensagem  

 O Dispatcher invocou ' AfterReceiveReply ' em um ClientMessageInspector do tipo ' %1 '.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|TypeName|`xs:string`|O CLR FullName do tipo do Inspetor invocado.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
