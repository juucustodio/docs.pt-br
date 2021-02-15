---
description: 'Saiba mais sobre: 115-WorkflowInstanceAbortedRecordWithId'
title: 115 - WorkflowInstanceAbortedRecordWithId
ms.date: 03/30/2017
ms.assetid: 0293dd4e-e6ae-473a-b3d6-c2d38f9bd875
ms.openlocfilehash: 6d9eb387ba61a646cbf1423d01175b0230272ca5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755428"
---
# <a name="115---workflowinstanceabortedrecordwithid"></a>115 - WorkflowInstanceAbortedRecordWithId

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|115|  
|Palavras-chave|HealthMonitoring, WFTracking|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Este evento é emitido pelo participante de rastreamento de ETW quando uma instância de fluxo de trabalho se emite WorkflowInstanceAbortedRecord.  
  
## <a name="message"></a>Mensagem  

 TrackRecord = WorkflowInstanceAbortedRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, ActivityDefinitionId = %4, razão = %5, anotações = %6 ProfileName, =, %7 WorkflowDefinitionIdentity = %8  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|A identificação de instância para o fluxo de trabalho|  
|RecordNumber|xs:long|O número de sequência do registro emitido|  
|EventTime|xs:dateTime|A hora UTC quando o evento foi emitido|  
|ActivityDefinitionId|xs:string|O nome da atividade raiz no fluxo de trabalho|  
|Estado|xs:string|O estado atual de fluxo de trabalho.|  
|Anotações|xs:string|As anotações que foram adicionadas a este evento. Os valores são armazenados em um elemento XML no formato \<items> \< item name = "annotationName" type="System.String"> annotationvalue \</item> \</items> . Se nenhuma anotação for especificada, a cadeia de caracteres conterá \<items/> . O tamanho do evento de ETW é limitado pelo tamanho do buffer de ETW ou pela carga máxima útil para um evento de ETW. Se o tamanho do evento exceder os limites de ETW, o evento será truncado descartando as anotações e substituindo o valor da anotação por \<items> ... \</items> .|  
|ProfileName|xs:string|O nome ou o perfil de rastreamento que levam a este evento que está sendo emitido|  
|WorkflowDefinitionIdentity|xs:string|A identificação da definição de fluxo de trabalho|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
