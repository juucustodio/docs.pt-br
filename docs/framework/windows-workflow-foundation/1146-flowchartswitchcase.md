---
description: 'Saiba mais sobre: 1146-FlowchartSwitchCase'
title: 1146 - FlowchartSwitchCase
ms.date: 03/30/2017
ms.assetid: 274e9209-1720-4512-a615-e742f00895f4
ms.openlocfilehash: f6e9b33f9c068b51695d3ac46cda51fb6d9f8b3f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99667064"
---
# <a name="1146---flowchartswitchcase"></a>1146 - FlowchartSwitchCase

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1146|  
|Palavras-chave|WFActivities|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que casos foram selecionados em um interruptor do fluxograma.  
  
## <a name="message"></a>Mensagem  

 Fluxograma “%1" /FlowSwitch - os casos “%2" foram selecionados.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Fluxograma|xs:string|O nome para exibição do fluxograma.|  
|Caixa|xs:string|Exemplos de opção que foi selecionado.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
