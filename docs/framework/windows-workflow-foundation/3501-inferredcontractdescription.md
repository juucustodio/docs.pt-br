---
description: 'Saiba mais sobre: 3501-InferredContractDescription'
title: 3501 - InferredContractDescription
ms.date: 03/30/2017
ms.assetid: 21a70849-4fc0-41d2-b9a4-db5aa2acdf1a
ms.openlocfilehash: 2eab180780a1475bff421441b7cef23f58f627c6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99778081"
---
# <a name="3501---inferredcontractdescription"></a>3501 - InferredContractDescription

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|3501|  
|Palavras-chave|WFServices|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Indica que um ContractDescription foi inferido de WorkflowService.  
  
## <a name="message"></a>Mensagem  

 ContractDescription com Name='%1 e Namespace='%2 foi inferido de WorkflowService.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Nome|xs:string|O nome de ContractDescription.|  
|Namespace|xs:string|O namespace de ContractDescription.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
