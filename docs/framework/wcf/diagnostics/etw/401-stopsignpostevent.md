---
description: 'Saiba mais sobre: 401-StopSignPostEvent'
title: 401- StopSignPostEvent
ms.date: 03/30/2017
ms.assetid: e033d03a-510d-4300-aa65-ef02cb4807f2
ms.openlocfilehash: 99b6151d902f3f8059b0aa01e6cda290debafda6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793942"
---
# <a name="401--stopsignpostevent"></a>401- StopSignPostEvent

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|401|  
|Palavras-chave|Solução de problemas|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento marca o fim de uma atividade de ponta a ponta. Contém o nome da atividade.  
  
## <a name="message"></a>Mensagem  

 Limite de atividade.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Dados estendidos|`xs:string`|O nome da atividade.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
