---
description: 'Saiba mais sobre: 1150-Remunerable'
title: 1150 - CompensationState
ms.date: 03/30/2017
ms.assetid: eb015842-cc5a-47be-bce5-6af39e567723
ms.openlocfilehash: 4adc246cbe46dee3594bc6c0330c8e0306489219
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99703335"
---
# <a name="1150---compensationstate"></a>1150 - CompensationState

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1150|  
|Palavras-chave|WFActivities|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica uma alteração de estado em um CompensableActivity.  
  
## <a name="message"></a>Mensagem  

 CompensableActivity “%1 " está em “%2 " estado.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|DisplayName|xs:string|O nome para exibição de atividade.|  
|Estado|xs:string|O estado da compensação.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
