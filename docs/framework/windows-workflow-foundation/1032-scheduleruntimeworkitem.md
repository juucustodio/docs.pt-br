---
description: 'Saiba mais sobre: 1032-ScheduleRuntimeWorkItem'
title: 1032 - ScheduleRuntimeWorkItem
ms.date: 03/30/2017
ms.assetid: 54688101-becf-42f3-80ca-f53a7b527620
ms.openlocfilehash: d96226b4ab0f856218d292c9c2481bca6c463c8a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99668039"
---
# <a name="1032---scheduleruntimeworkitem"></a>1032 - ScheduleRuntimeWorkItem

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1032|  
|Palavras-chave|WFRuntime|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um RuntimeWorkItem foi agendada.  
  
## <a name="message"></a>Mensagem  

 Um item de trabalho de runtime foi agendada para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Atividade|xs:string|O nome do tipo de atividade.|  
|DisplayName|xs:string|O nome para exibição de atividade.|  
|InstanceId|xs:string|A identificação de instância de atividade.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
