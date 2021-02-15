---
description: 'Saiba mais sobre: 1148-FlowchartSwitchCaseNotFound'
title: 1148 - FlowchartSwitchCaseNotFound
ms.date: 03/30/2017
ms.assetid: 9ee7fcee-e040-4306-968e-ed840a1cb00c
ms.openlocfilehash: 067dff850a67f1b235bf9c1903757eefa912bd92
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99720404"
---
# <a name="1148---flowchartswitchcasenotfound"></a>1148 - FlowchartSwitchCaseNotFound

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1148|  
|Palavras-chave|WFActivities|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que nem casos compatíveis ou casos padrão em uma opção do fluxograma podem ser localizados. A execução do fluxograma será finalizada.  
  
## <a name="message"></a>Mensagem  

 O fluxograma “%1 " /FlowSwitch - pôde localizar ou uma atividade dos casos ou casos padrão que correspondem ao resultado da expressão. A execução do fluxograma será finalizada.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Fluxograma|xs:string|O nome para exibição do fluxograma.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
