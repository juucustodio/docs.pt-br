---
description: 'Saiba mais sobre: 1041-WorkflowApplicationPersistableIdle'
title: 1041 - WorkflowApplicationPersistableIdle
ms.date: 03/30/2017
ms.assetid: 966adf2f-e21d-44df-a3ec-a8e285e0a316
ms.openlocfilehash: eb004077a36ed3e78229df92a73972ed5feda665
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99667753"
---
# <a name="1041---workflowapplicationpersistableidle"></a>1041 - WorkflowApplicationPersistableIdle

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1041|  
|Palavras-chave|WFRuntime|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um aplicativo de fluxo de trabalho estiver ocioso e persistable. O aplicativo de fluxo de trabalho será rodado em marcha lento ou persistente.  
  
## <a name="message"></a>Mensagem  

 WorkflowApplication ID: ' %1 ' está ociosa e persistente.  A seguinte ação será executada: %2.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|WorkflowApplicationId|xs:string|A identificação do aplicativo de fluxo de trabalho|  
|ActionTaken|xs:string|A ação a ser tomada no aplicativo de fluxo de trabalho.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
