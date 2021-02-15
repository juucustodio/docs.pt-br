---
description: 'Saiba mais sobre: 1132-InvokeMethodDoesNotUseAsyncPattern'
title: 1132 - InvokeMethodDoesNotUseAsyncPattern
ms.date: 03/30/2017
ms.assetid: 436b3767-4460-46b0-9ea3-fc2963260c11
ms.openlocfilehash: 05bbd1f6047ab4c6451d71a4f6007f3112f9630f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99667272"
---
# <a name="1132---invokemethoddoesnotuseasyncpattern"></a>1132 - InvokeMethodDoesNotUseAsyncPattern

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1132|  
|Palavras-chave|WFRuntime|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Durante a etapa de CacheMetadata, a atividade de InvokeMethod indica que não está usando o padrão de async ao chamar o método.  
  
## <a name="message"></a>Mensagem  

 InvokeMethod “%1" - o método não usa o padrão assíncrono.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|InvokeMethod|xs:string|O nome para exibição de atividade de InvokeMethod.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
