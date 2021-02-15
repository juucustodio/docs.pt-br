---
description: 'Saiba mais sobre: 3502-InferredOperationDescription'
title: 3502 - InferredOperationDescription
ms.date: 03/30/2017
ms.assetid: 6aebb614-3c72-4537-ba11-3cc7200ef1f1
ms.openlocfilehash: 5068a3553484b38242951ef985886190f8027035
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631483"
---
# <a name="3502---inferredoperationdescription"></a>3502 - InferredOperationDescription

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|3502|  
|Palavras-chave|WFServices|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Indica que um OperationDescription foi inferido de WorkflowService.  
  
## <a name="message"></a>Mensagem  

 OperationDescription com o Name='%1 no contrato “%2 " foi inferido de WorkflowService. IsOneWay=%3.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|OperationName|xs:string|O nome da operação.|  
|ContractName|xs:string|O nome do contrato.|  
|IsOneWay|xs:string|Retifique ou falso indicando se o contrato é unidirecional.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
