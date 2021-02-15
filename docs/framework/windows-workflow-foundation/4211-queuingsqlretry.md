---
description: 'Saiba mais sobre: 4211-QueuingSqlRetry'
title: 4211 - QueuingSqlRetry
ms.date: 03/30/2017
ms.assetid: df569f88-c86b-4503-840d-1399b67f4df7
ms.openlocfilehash: 674914ee105bb0a48f8c32efbd573c685d22d9f7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742700"
---
# <a name="4211---queuingsqlretry"></a>4211 - QueuingSqlRetry

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|4211|  
|Palavras-chave|WFInstanceStore|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica a nova tentativa de enfileiramento SQL.  
  
## <a name="message"></a>Mensagem  

 Nova tentativa SQL fila com atraso %1 milissegundos.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Atrasar|xs:string|O intervalo entre repetições.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
