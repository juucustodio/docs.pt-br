---
description: 'Saiba mais sobre: 3551-BufferOutOfOrderMessageNoBookmark'
title: 3551 - BufferOutOfOrderMessageNoBookmark
ms.date: 03/30/2017
ms.assetid: 7930d6c4-c843-4a83-933a-cecd71b80d1e
ms.openlocfilehash: 573056fed1753ac55c51d9a074047e8eea15e229
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99777990"
---
# <a name="3551---bufferoutofordermessagenobookmark"></a>3551 - BufferOutOfOrderMessageNoBookmark

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|3551|  
|Palavras-chave|WFServices|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Indica que uma ressunção do indexador falhou. O armazenados em buffer recebe a operação será tentada novamente quando a instância do serviço está pronta para processar esta operação específico.  
  
## <a name="message"></a>Mensagem  

 A operação “%2 " na instância “%1 " do serviço não pode ser executada no momento. Outra tentativa será feita quando a instância de serviço estiver pronta para processar esse operação específica.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|OperationName|xs:string|O nome da operação.|  
|ServiceInstanceId|xs:string|A identificação da instância do serviço.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
