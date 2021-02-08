---
description: 'Saiba mais sobre: 225-TraceCorrelationKeys'
title: 225 - TraceCorrelationKeys
ms.date: 03/30/2017
ms.assetid: d9083aaf-3816-4c1c-bae0-2d7f49628345
ms.openlocfilehash: c5fdb9305815cdc4df6bbae3e54209d2b5cffd9d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99778107"
---
# <a name="225---tracecorrelationkeys"></a>225 - TraceCorrelationKeys

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|225|  
|Palavras-chave|Solução de problemas, ServiceModel|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Este evento é emitida quando correlação conteudo base é usada para um serviço de fluxo de trabalho. Contém as chaves de correlação que são aplicadas para correlacionar uma mensagem a uma instância.  
  
## <a name="message"></a>Mensagem  

 Chave calculada “%1 " de correlação usando o %2 " dos valores no escopo pai “%3 ".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Chave de instância|`xs:GUID`|A tecla que foi gerada de correlação avalia.|  
|Valores|`xs:string`|Os valores que foram usados para calcular a chave de instância de correlação.|  
|Escopo pai|`xs:string`||  
|HostReference|`xs:string`|Os serviços hospedados da Web, este campo identificam exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
