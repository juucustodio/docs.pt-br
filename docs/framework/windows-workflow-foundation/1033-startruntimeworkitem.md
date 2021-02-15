---
description: 'Saiba mais sobre: 1033-StartRuntimeWorkItem'
title: 1033 - StartRuntimeWorkItem
ms.date: 03/30/2017
ms.assetid: 172b5346-9f3b-46ae-bc06-39872022376a
ms.openlocfilehash: 31e664070b7592d3350a2f6f84f0493cc8f11ea1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99668000"
---
# <a name="1033---startruntimeworkitem"></a>1033 - StartRuntimeWorkItem

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1046|  
|Palavras-chave|WFRuntime|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um RuntimeWorkItem está sendo a execução.  
  
## <a name="message"></a>Mensagem  

 Iniciar a execução de um item de trabalho de runtime para atividades “%1 ", DisplayName: “%2", InstanceId: “%3".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Atividade|xs:string|O nome do tipo de atividade.|  
|DisplayName|xs:string|O nome para exibição de atividade.|  
|InstanceId|xs:string|A identificação de instância de atividade.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
