---
description: 'Saiba mais sobre: 1007-WorkflowApplicationPersisted'
title: 1007 - WorkflowApplicationPersisted
ms.date: 03/30/2017
ms.assetid: f4ea4452-28e3-4e66-93c6-eb12ee29bcb1
ms.openlocfilehash: 6598f4490d20f84abfc95223f9d5a3f4231b4754
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755571"
---
# <a name="1007---workflowapplicationpersisted"></a>1007 - WorkflowApplicationPersisted

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1007|  
|Palavras-chave|WFRuntime|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um aplicativo de fluxo de trabalho persistiu.  
  
## <a name="message"></a>Mensagem  

 Identificação de WorkflowApplication: “%1 " foi persistente.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|WorkflowApplicationId|`xs:string`|A identificação do aplicativo de fluxo de trabalho|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
