---
description: 'Saiba mais sobre: 1028-CompleteTransactionContextWorkItem'
title: 1028 - CompleteTransactionContextWorkItem
ms.date: 03/30/2017
ms.assetid: 95423f9d-d29a-460e-bcd8-096e80af5bd0
ms.openlocfilehash: ae66072769c24ce8d44f92a88cd4232d20bde5f6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755454"
---
# <a name="1028---completetransactioncontextworkitem"></a>1028 - CompleteTransactionContextWorkItem

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1028|  
|Palavras-chave|WFRuntime|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um TransactionContextWorkItem terminado.  
  
## <a name="message"></a>Mensagem  

 Um TransactionContextWorkItem concluiu para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Atividade|xs:string|O nome do tipo de atividade.|  
|DisplayName|xs:string|O nome para exibição de atividade.|  
|InstanceId|xs:string|A identificação de instância de atividade.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
