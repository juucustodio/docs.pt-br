---
description: 'Saiba mais sobre: 4210-SqlExceptionCaught'
title: 4210 - SqlExceptionCaught
ms.date: 03/30/2017
ms.assetid: f0ce8af3-eb4c-48c8-b3d9-dd2f94b5574b
ms.openlocfilehash: 58846d02b6d1e388e3aef2bff76f51cba4990f2f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99777873"
---
# <a name="4210---sqlexceptioncaught"></a>4210 - SqlExceptionCaught

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|4210|  
|Palavras-chave|WFInstanceStore|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que uma exceção SQL foi detectada.  
  
## <a name="message"></a>Mensagem  

 Mensagem capturada %2 de %1. número de exceção SQL.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|ErrorNumber|xs:string|O número do erro SQL.|  
|ExceptionMessage|xs:string|A mensagem de exceção SQL.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
