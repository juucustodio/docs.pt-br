---
description: 'Saiba mais sobre: 1014-ScheduleCompletionWorkItem'
title: 1014 - ScheduleCompletionWorkItem
ms.date: 03/30/2017
ms.assetid: 84203735-478d-42d8-a320-c175dbddcb38
ms.openlocfilehash: 85bbd9b749c1dd34d026d90d708ea7f880665fbb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792928"
---
# <a name="1014---schedulecompletionworkitem"></a>1014 - ScheduleCompletionWorkItem

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1014|  
|Palavras-chave|WFRuntime|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um CompletionWorkItem foi agendada.  
  
## <a name="message"></a>Mensagem  

 Um CompletionWorkItem foi agendado para a atividade pai ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  Atividade counting “%4 ", DisplayName: “%5", InstanceId: “%6".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|ParentActivity|xs:string|O nome do tipo de atividade pai.|  
|ParentDisplayName|xs:string|O nome para exibição de atividade pai.|  
|ParentInstanceId|xs:string|A identificação de instância de atividade pai.|  
|CompletedActivity|xs:string|O nome do tipo de atividade concluída.|  
|CompletedActivityDisplayName|xs:string|O nome para exibição de atividade concluída.|  
|CompletedActivityInstanceId|xs:string|A identificação de instância de atividade concluída.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
