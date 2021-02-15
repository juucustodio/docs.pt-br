---
description: 'Saiba mais sobre: 214-OperationCompleted'
title: 214 - OperationCompleted
ms.date: 03/30/2017
ms.assetid: a6287eef-023f-4816-813c-1802c82366df
ms.openlocfilehash: aad1ac49667a2ebbf172b5132507584e05d0f03e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794384"
---
# <a name="214---operationcompleted"></a>214 - OperationCompleted

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|214|  
|Palavras-chave|HealthMonitoring, EndToEndMonitoring, solução de problemas, ServiceModel|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido quando o padrão do modelo de serviço `OperationInvoker` concluiu uma chamada para um método sem que esse método emita uma exceção.  
  
## <a name="message"></a>Mensagem  

 Um OperationInvoker concluiu a chamada para o método ' %1 '. A duração da chamada do método era ' %2 ' MS.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Nome do método|`xs:string`|O nome do CLR do método que foi invocado pelo `OperationInvoker` .|  
|Duration|`xs:long`|O tempo, em milissegundos, necessário `OperationInvoker` para invocar o método.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
