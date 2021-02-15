---
description: 'Saiba mais sobre: 219-ServiceException'
title: 219 - ServiceException
ms.date: 03/30/2017
ms.assetid: 81e2efac-39aa-4ed2-85a9-97eb8793b844
ms.openlocfilehash: b2ac12d6c5c68517b085b39dd7d0f81c39db9ebd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794319"
---
# <a name="219---serviceexception"></a>219 - ServiceException

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|219|  
|Palavras-chave|EndToEndMonitoring, HealthMonitoring, solução de problemas, ServiceModel|  
|Level|Erro do|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido quando um serviço WCF encontra uma exceção sem tratamento. Isso inclui exceções sem tratamento durante a ativação, durante o processamento da mensagem e no código do usuário.  
  
## <a name="message"></a>Mensagem  

 Houve uma exceção sem tratamento do tipo ' %2 ' durante o processamento da mensagem. Exceção ToString completa: %1.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|ExceptionToString|`xs:string`|O resultado de chamada `ToString` () na exceção CLR.|  
|ExceptionTypeName|`xs:string`|O CLR FullName do tipo da exceção.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
