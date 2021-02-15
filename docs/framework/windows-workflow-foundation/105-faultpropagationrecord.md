---
description: 'Saiba mais sobre: 105-FaultPropagationRecord'
title: 105 - FaultPropagationRecord
ms.date: 03/30/2017
ms.assetid: 168473b1-b1e5-4e9f-8a2a-35bbdb2ef531
ms.openlocfilehash: 95f82763606bf16219fa4234b5f6e7101c0954fa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99667675"
---
# <a name="105---faultpropagationrecord"></a>105 - FaultPropagationRecord

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|105|  
|Palavras-chave|EndToEndMonitoring, solução de problemas, HealthMonitoring, WFTracking|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Este evento é emitido pelo participante de rastreamento de ETW quando uma atividade com a instância de fluxo de trabalho se emite FaultPropagationRecord.  
  
## <a name="message"></a>Mensagem  

 TrackRecord = FaultPropagationRecord, InstanceID = %1, RecordNumber = %2, EventTime = %3, FaultSourceActivityName = %4, FaultSourceActivityId = %5, FaultSourceActivityInstanceId = %6, FaultSourceActivityTypeName = %7, FaultHandlerActivityName = %8, FaultHandlerActivityId = %9, FaultHandlerActivityInstanceId = %10, FaultHandlerActivityTypeName = %11, a falha = %12, isfaultnames = %13, anotações = %14, ProfileName = %15  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|InstanceId|xs:GUID|A identificação de instância para o fluxo de trabalho|  
|RecordNumber|xs:long|O número de sequência do registro emitido|  
|EventTime|xs:dateTime|A hora UTC quando o evento foi emitido|  
|FaultSourceActivityName|xs:string|O nome da atividade que se emitiu a falha|  
|FaultSourceActivityId|xs:string|A identificação da atividade que se emitiu a falha|  
|FaultSourceActivityInstanceId|xs:string|A identificação de instância de atividade que se emitiu a falha|  
|FaultSourceActivityTypeName|xs:string|O tipo de atividade que se emitiu a falha|  
|FaultHandlerActivityName|xs:string|O nome para exibição de atividade do manipulador de falha|  
|FaultHandlerActivityId|xs:string|A identificação de atividade do manipulador de falha|  
|FaultHandlerActivityInstanceId|xs:string|A identificação de instância de atividade do manipulador de falha|  
|FaultHandlerActivityTypeName|xs:string|O tipo de atividade do manipulador de falha|  
|Falha|xs:string|Os detalhes de falha|  
|IsFaultSource|xs:unsignedByte|Indica se o evento foi emitido de origem de falha|  
|Anotações|xs:string|As anotações que foram adicionadas a este evento.  Os valores são armazenados em um elemento XML no formato \<items> \< item  name = "annotationName" type="System.String"> annotationvalue \</item> \</items> .  Se nenhuma anotação for especificada, a cadeia de caracteres conterá \<items/> . O tamanho do evento de ETW é limitado pelo tamanho do buffer de ETW ou pela carga máxima útil para um evento de ETW. Se o tamanho do evento exceder os limites de ETW, o evento será truncado descartando as anotações e substituindo o valor da anotação por \<items> ... \</items> .|  
|ProfileName|xs:string|O nome ou o perfil de rastreamento que levam a este evento que está sendo emitido|  
|HostReference|xs:string|Hospedados para serviços da Web, este campo identifica unicamente o serviço na hierarquia da Web.  Seu formato é definido como ' nome do site aplicativo caminho virtual do serviço&#124;caminho virtual&#124;ServiceName ' exemplo: ' Default Web site/CalculatorApplication&#124;/CalculatorService.svc&#124;CalculatorService '|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
