---
description: 'Saiba mais sobre: 110-CustomTrackingRecordWarning'
title: 110 - CustomTrackingRecordWarning
ms.date: 03/30/2017
ms.assetid: 3bc093de-be47-4ed0-983f-05b4246446fc
ms.openlocfilehash: d127b0fbf8fa4f2d7285068486a900452685346d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99667597"
---
# <a name="110---customtrackingrecordwarning"></a>110 - CustomTrackingRecordWarning

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|110|  
|Palavras-chave|UserEvents, EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Este evento é emitido pelo participante de rastreamento de ETW quando uma atividade em uma instância de fluxo de trabalho se emite CustomTrackingRecord com aviso nivelado  
  
## <a name="message"></a>Mensagem  

 TrackRecord = CustomTrackingRecord, InstanceID = %1, RecordNumber=%2, EventTime=%3, Name=%4, ActivityName=%5, ActivityId=%6, ActivityInstanceId=%7, ActivityTypeName=%8, Data=%9, Annotations=%10, ProfileName = %11  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|A identificação de instância para o fluxo de trabalho|  
|RecordNumber|xs:long|O número de sequência do registro emitido|  
|EventTime|xs:dateTime|A hora UTC quando o evento foi emitido|  
|Nome|xs:string|O nome de CustomTrackingRecord|  
|ActivityName|xs:string|O nome da atividade que se emitiu o CustomTrackingRecord|  
|ActivityId|xs:string|A identificação da atividade que se emitiu o CustomTrackingRecord|  
|ActivityInstanceId|xs:string|A identificação de instância de atividade que se emitiu o CustomTrackingRecord|  
|ActivityTypeName|xs:string|O nome da atividade que se emitiu o CustomTrackingRecord|  
|Dados|xs:string|Os dados que foram rastreadas com esse evento.  Os valores são armazenados em um elemento XML no formato \<items> \< item  name = "dataName" type="System.String"> DataValue \</item> \</items> .  Se nenhum dado foi acompanhado, a cadeia de caracteres contém \<items/> . O tamanho do evento de ETW é limitado pelo tamanho do buffer de ETW ou pela carga máxima útil para um evento de ETW. Se o tamanho do evento exceder os limites de ETW, o evento será truncado descartando as anotações e substituindo o valor dos dados por \<items> ... \</items> .  Os tipos a seguir são armazenados como seu valor, conforme retornado por ToString (); String, Char, bool, int, short, Long, uint, ushort, ulong, System. single, float, Double, System. GUID, System. DateTimeOffset, System. DateTime.  Todos os outros tipos são serializados usando System.Runtime.Serialization.NetDataContractSerializer.|  
|Anotações|xs:string|As anotações que foram adicionadas a este evento.  Os valores são armazenados em um elemento XML no formato \<items> \< item  name = "annotationName" type="System.String"> annotationvalue \</item> \</items> .  Se nenhuma anotação for especificada, a cadeia de caracteres conterá \<items/> . O tamanho do evento de ETW é limitado pelo tamanho do buffer de ETW ou pela carga máxima útil para um evento de ETW. Se o tamanho do evento exceder os limites de ETW, o evento será truncado descartando as anotações e substituindo o valor da anotação por \<items> ... \</items> .|  
|ProfileName|xs:string|O nome ou o perfil de rastreamento que levam a este evento que está sendo emitido|  
|HostReference|xs:string|Hospedados para serviços da Web, este campo identifica unicamente o serviço na hierarquia da Web.  O formato é definido como ' nome do site aplicativo caminho virtual do serviço&#124;caminho virtual Service&#124;nome do provedor ' exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
