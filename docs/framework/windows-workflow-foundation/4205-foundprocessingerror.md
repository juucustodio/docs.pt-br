---
description: 'Saiba mais sobre: 4205-FoundProcessingError'
title: 4205 - FoundProcessingError
ms.date: 03/30/2017
ms.assetid: f2235a15-dd87-439e-8cb9-8b1b89a3dacf
ms.openlocfilehash: 847535af51cae8723f06d33b3b5c5c64cf3c5dd7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99676281"
---
# <a name="4205---foundprocessingerror"></a>4205 - FoundProcessingError

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|4205|  
|Palavras-chave|WFInstanceStore|  
|Level|Erro do|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que comando do provedor SQL falhou.  
  
## <a name="message"></a>Mensagem  

 Comando falhou: %1  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|ExceptionMessage|xs:string|A mensagem de exceção SQL.|  
|Exceção|xs:string|Os detalhes de exceção para a exceção|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
