---
description: 'Saiba mais sobre: 203-ClientParameterInspectorAfterCallInvoked'
title: 203 - ClientParameterInspectorAfterCallInvoked
ms.date: 03/30/2017
ms.assetid: b9592212-07e2-43e0-8b00-affd195cf55a
ms.openlocfilehash: bacdc2a74fc2cef6d7e473fa58c0cbbcffffcf16
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99645016"
---
# <a name="203---clientparameterinspectoraftercallinvoked"></a>203 - ClientParameterInspectorAfterCallInvoked

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|203|  
|Palavras-chave|Solução de problemas, ServiceModel|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido depois que o modelo de serviço invoca o `AfterCall` método em um inspetor de parâmetro do cliente.  
  
## <a name="message"></a>Mensagem  

 O Dispatcher invocou ' AfterCall ' em um ClientParameterInspector do tipo ' %1 '.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|TypeName|`xs:string`|O CLR FullName do tipo do Inspetor invocado.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
