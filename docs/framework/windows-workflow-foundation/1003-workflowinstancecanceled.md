---
description: 'Saiba mais sobre: 1003-WorkflowInstanceCanceled'
title: 1003 - WorkflowInstanceCanceled
ms.date: 03/30/2017
ms.assetid: 64754dc2-c160-4bf3-869a-13d56694e2dc
ms.openlocfilehash: ef7b7c6849e96866204fe53deadce8302d18e0d8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99703361"
---
# <a name="1003---workflowinstancecanceled"></a>1003 - WorkflowInstanceCanceled

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1003|  
|Palavras-chave|WFRuntime|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que uma instância de fluxo de trabalho concluído no estado cancelado.  
  
## <a name="message"></a>Mensagem  

 Identificação de WorkflowInstance: “%1 " terminou no estado cancelado.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|WorkflowInstanceId|`xs:string`|A identificação de instância para o fluxo de trabalho|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
