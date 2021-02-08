---
description: 'Saiba mais sobre: 39457-TrackingRecordRaised'
title: 39457 - TrackingRecordRaised
ms.date: 03/30/2017
ms.assetid: 5a2731d1-c731-4b79-bb69-016cb69ef481
ms.openlocfilehash: 551e13e32dbb690458877ceed0b532799f238966
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99777899"
---
# <a name="39457---trackingrecordraised"></a>39457 - TrackingRecordRaised

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|39457|  
|Palavras-chave|WFRuntime|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um TrackingRecord foi gerado para um TrackingParticipant.  
  
## <a name="message"></a>Mensagem  

 Controlando o registro %1 elevado a %2.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|RecordNumber|xs:string|O número de registro controlando.|  
|ParticipantId|xs:string|O participante de rastreamento.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
