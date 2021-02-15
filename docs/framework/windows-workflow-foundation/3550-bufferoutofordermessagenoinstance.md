---
description: 'Saiba mais sobre: 3550-BufferOutOfOrderMessageNoInstance'
title: 3550 - BufferOutOfOrderMessageNoInstance
ms.date: 03/30/2017
ms.assetid: 1299d294-99b8-430e-98b1-55f5f17002f3
ms.openlocfilehash: cb51f9fa32de1b56560f9593dae2ec82c100dc65
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631444"
---
# <a name="3550---bufferoutofordermessagenoinstance"></a>3550 - BufferOutOfOrderMessageNoInstance

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|3550|  
|Palavras-chave|WFServices|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Indica que um armazenados em buffer recebe falhou. A operação será tentada novamente quando a instância do serviço está pronta para processar esta operação específico.  
  
## <a name="message"></a>Mensagem  

 A operação “%1 " não pode ser executada no momento. Outra tentativa será feita quando a instância de serviço estiver pronta para processar esse operação específica.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|OperationName|xs:string|O nome da operação.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
