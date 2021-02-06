---
description: 'Saiba mais sobre: 403-SuspendSignpostEvent'
title: 403 - SuspendSignpostEvent
ms.date: 03/30/2017
ms.assetid: fb2e6f29-e556-47b4-b4c1-acd6b8879702
ms.openlocfilehash: 4e601920c94ed99c25a1c969508798f65f5348bc
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99656417"
---
# <a name="403---suspendsignpostevent"></a>403 - SuspendSignpostEvent

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|403|  
|Palavras-chave|Solução de problemas|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Esse evento marca a suspensão de uma atividade de ponta a ponta. Contém o nome da atividade.  
  
## <a name="message"></a>Mensagem  

 Limite de atividade.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Dados estendidos|`xs:string`|O nome da atividade.|  
|AppDomain|`xs:string`|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
