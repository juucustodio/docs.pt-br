---
description: 'Saiba mais sobre: 3508-TrackingProfileNotFound'
title: 3508 - TrackingProfileNotFound
ms.date: 03/30/2017
ms.assetid: 4cee3c4a-0490-4c94-aa19-ef7ce7287c02
ms.openlocfilehash: 3e97af1689a868fb103b06413a0c4f28b0c1f652
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99778003"
---
# <a name="3508---trackingprofilenotfound"></a>3508 - TrackingProfileNotFound

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|3508|  
|Palavras-chave|WFServices|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Indica que um ou TrackingProfile não está localizado no arquivo de configuração ou o ActivityDefinitionId não corresponde ao perfil.  
  
## <a name="message"></a>Mensagem  

 TrackingProfile “%1 " para o ActivityDefinitionId “%2 " não encontrado. O TrackingProfile não é encontrado no arquivo de configuração ou a ActivityDefinitionId não é correspondente.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|TrackingProfile|xs:string|O nome de perfil de rastreamento.|  
|ActivityDefinitionId|xs:string|A identificação da definição de atividades|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
