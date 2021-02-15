---
description: 'Saiba mais sobre: 104-ActivityScheduledRecord'
title: 104 - ActivityScheduledRecord
ms.date: 03/30/2017
ms.assetid: ae202178-8fb1-4646-a3aa-18beeda8ff93
ms.openlocfilehash: 9d52dac3ec68de0d38959e81294c5c6ead21428e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99667805"
---
# <a name="104---activityscheduledrecord"></a>104 - ActivityScheduledRecord

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|104|  
|Palavras-chave|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Este evento é emitido pelo participante de rastreamento de ETW quando uma atividade em uma instância de fluxo de trabalho se emite ActivityScheduledRecord  
  
## <a name="message"></a>Mensagem  

 TrackRecord = ActivityScheduledRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, nome = %4, ActivityId = %5, ActivityInstanceId = %6, outactivityname = %7, ChildActivityName = %8, ChildActivityId = %9, ChildActivityInstanceId = %10, ChildActivityTypeName = %11, anotações = %12, ProfileName = %13  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|A identificação de instância para o fluxo de trabalho|  
|RecordNumber|xs:long|O número de sequência do registro emitido|  
|EventTime|xs:dateTime|A hora UTC quando o evento foi emitido|  
|Nome|xs:string|O nome da atividade que agendou a atividade filho|  
|ActivityId|xs:string|A identificação da atividade que agendou a atividade filho|  
|ActivityInstanceId|xs:string|A identificação de instância de atividade que agendou a atividade filho|  
|ActivityTypeName|xs:string|O tipo de atividade que solicitou a operação de cancelamento|  
|ChildActivityName|xs:string|O nome da atividade agendada|  
|ChildActivityId|xs:string|A identificação da atividade agendada|  
|ChildActivityInstanceId|xs:string|A identificação de instância de atividade agendada|  
|ChildActivityTypeName|xs:string|O tipo de atividade agendada|  
|Anotações|xs:string|As anotações que foram adicionadas a este evento.  Os valores são armazenados em um elemento XML no formato \<items> \< item  name = "annotationName" type="System.String"> annotationvalue \</item> \</items> .  Se nenhuma anotação for especificada, a cadeia de caracteres conterá \<items/> . O tamanho do evento de ETW é limitado pelo tamanho do buffer de ETW ou pela carga máxima útil para um evento de ETW. Se o tamanho do evento exceder os limites de ETW, o evento será truncado descartando as anotações e substituindo o valor da anotação por \<items> ... \</items> .|  
|ProfileName|xs:string|O nome ou o perfil de rastreamento que levam a este evento que está sendo emitido|  
|HostReference|xs:string|Hospedados para serviços da Web, este campo identifica unicamente o serviço na hierarquia da Web.  Seu formato é definido como ' nome do site aplicativo caminho virtual do serviço&#124;caminho virtual&#124;ServiceName ' exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
