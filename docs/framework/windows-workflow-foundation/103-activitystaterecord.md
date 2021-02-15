---
description: 'Saiba mais sobre: 103-ActivityStateRecord'
title: 103 - ActivityStateRecord
ms.date: 03/30/2017
ms.assetid: 57636a9a-561e-44aa-aef9-1f1894aaa6dd
ms.openlocfilehash: 14afbfdb0869b6ee65e1482fa73aa36ccd58f307
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99668117"
---
# <a name="103---activitystaterecord"></a>103 - ActivityStateRecord

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|103|  
|Palavras-chave|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Este evento é emitido pelo participante de rastreamento de ETW quando uma atividade em uma instância de fluxo de trabalho se emite ActivityStateRecord  
  
## <a name="message"></a>Mensagem  

 TrackRecord = ActivityStateRecord, InstanceID = %1, RecordNumber=%2, EventTime=%3, estado = %4, Name=%5, ActivityId=%6, ActivityInstanceId=%7, ActivityTypeName=%8, Arguments=%9, Variables=%10, Annotations=%11, ProfileName = %12  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|A identificação de instância para o fluxo de trabalho|  
|RecordNumber|xs:long|O número de sequência do registro emitido|  
|EventTime|xs:dateTime|A hora UTC quando o evento foi emitido|  
|Estado|xs:string|O estado de atividades|  
|Nome|xs:string|O nome para exibição de atividade que se emitiu o evento|  
|ActivityId|xs:string|A identificação de atividade de atividade emitindo|  
|ActivityInstanceId|xs:string|A identificação de instância de atividade de atividade emitindo|  
|ActivityTypeName|xs:string|O nome do tipo de atividade emitindo|  
|Argumentos|xs:string|Os argumentos que foram rastreadas com esse evento.  Os valores são armazenados em um elemento XML no formato \<items> \< item  name = "argumentName" type="System.String"> ArgumentValue \</item> \</items> .  Se nenhum argumento tiver sido acompanhado, a cadeia de caracteres conterá \<items/> . O tamanho do evento de ETW é limitado pelo tamanho do buffer de ETW ou pela carga máxima útil para um evento de ETW. Se o tamanho do evento exceder os limites de ETW, o evento será truncado descartando as anotações e substituindo o valor da anotação por \<items> ... \</items> .  Os tipos a seguir são armazenados como seu valor, conforme retornado por ToString (); String, Char, bool, int, short, Long, uint, ushort, ulong, System. single, float, Double, System. GUID, System. DateTimeOffset, System. DateTime.  Todos os outros tipos são serializados usando System.Runtime.Serialization.NetDataContractSerializer.|  
|Variáveis|xs:string|Variáveis que foram rastreadas com esse evento.  Os valores são armazenados em um elemento XML no formato \<items> \< item  name = "variableName" type="System.String"> variableValue \</item> \</items> .  Se nenhuma variável tiver sido rastreada, a cadeia de caracteres conterá \<items/> . O tamanho do evento de ETW é limitado pelo tamanho do buffer de ETW ou pela carga máxima útil para um evento de ETW. Se o tamanho do evento exceder os limites de ETW, o evento será truncado descartando as anotações e substituindo o valor das variáveis por \<items> ... \</items> .  Os tipos a seguir são armazenados como seu valor, conforme retornado por ToString (); String, Char, bool, int, short, Long, uint, ushort, ulong, System. single, float, Double, System. GUID, System. DateTimeOffset, System. DateTime.  Todos os outros tipos são serializados usando System.Runtime.Serialization.NetDataContractSerializer.|  
|Anotações|xs:string|As anotações que foram adicionadas a este evento.  Os valores são armazenados em um elemento XML no formato \<items> \< item  name = "annotationName" type="System.String"> annotationvalue \</item> \</items> .  Se nenhuma anotação for especificada, a cadeia de caracteres conterá \<items/> . O tamanho do evento de ETW é limitado pelo tamanho do buffer de ETW ou pela carga máxima útil para um evento de ETW. Se o tamanho do evento exceder os limites de ETW, o evento será truncado descartando as anotações e substituindo o valor da anotação por \<items> ... \</items> .|  
|ProfileName|xs:string|O nome ou o perfil de rastreamento que levam a este evento que está sendo emitido|  
|HostReference|xs:string|Hospedados para serviços da Web, este campo identifica unicamente o serviço na hierarquia da Web.  Seu formato é definido como ' nome do site aplicativo caminho virtual do serviço&#124;caminho virtual&#124;ServiceName ' exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
