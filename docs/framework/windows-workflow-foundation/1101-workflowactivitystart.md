---
description: 'Saiba mais sobre: 1101-WorkflowActivityStart'
title: 1101 - WorkflowActivityStart
ms.date: 03/30/2017
ms.assetid: 831cd386-b9b5-47a9-9690-aff6292ff348
ms.openlocfilehash: f84a3de405d05e5f4669244577a4a16c1c53f8d3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99667584"
---
# <a name="1101---workflowactivitystart"></a>1101 - WorkflowActivityStart

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1101|  
|Palavras-chave|WFRuntime|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que uma atividade de fluxo de trabalho foi iniciado.  
  
## <a name="message"></a>Mensagem  

 Identificação de WorkflowInstance: “%1" atividade de E2E  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|WorkflowInstanceId|xs:string|A identificação de instância de fluxo de trabalho|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
