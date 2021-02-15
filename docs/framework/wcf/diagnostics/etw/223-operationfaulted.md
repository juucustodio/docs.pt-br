---
description: 'Saiba mais sobre: 223-OperationFaulted'
title: 223 - OperationFaulted
ms.date: 03/30/2017
ms.assetid: 2f7d89d7-3a6a-40fe-9610-5424eb6bbf61
ms.openlocfilehash: e4155516e07568d4ee4ca76d63754ec4171e1064
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99794280"
---
# <a name="223---operationfaulted"></a>223 - OperationFaulted

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|223|  
|Palavras-chave|EndToEndMonitoring, HealthMonitoring, solução de problemas, ServiceModel|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento é emitido quando o padrão do modelo de serviço `OperationInvoker` tiver encontrado uma exceção derivando `FaultException` ao invocar seu método.  
  
## <a name="message"></a>Mensagem  

 O método ' %1 ' lançou uma FaultException quando invocado pelo OperationInvoker. A duração da chamada do método era ' %2 ' MS.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|MethodName|`xs:string`|O nome do CLR do método que foi invocado pelo `OperationInvoker` .|  
|Duration|`xs:long`|O tempo, em milissegundos, necessário `OperationInvoker` para invocar o método.|  
|HostReference|`xs:string`|Para serviços hospedados na Web, esse campo identifica exclusivamente o serviço na hierarquia da Web. Seu formato é definido como ' nome do site aplicativo caminho virtual&#124;serviço caminho virtual&#124;ServiceName '. Exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
