---
description: 'Saiba mais sobre: 2577-TryCatchExceptionDuringCancelation'
title: 2577 - TryCatchExceptionDuringCancelation
ms.date: 03/30/2017
ms.assetid: 35ee9f55-227f-4566-bcb4-4c7c75dea85b
ms.openlocfilehash: e02e7722dadfe38b9fc1fbb92e809ae8f80cbd2f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99778094"
---
# <a name="2577---trycatchexceptionduringcancelation"></a>2577 - TryCatchExceptionDuringCancelation

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|2577|  
|Palavras-chave|WFActivities|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que uma atividade filho de atividade de TryCatch apresentou uma exceção durante o cancelar.  
  
## <a name="message"></a>Mensagem  

 Uma atividade filho da atividade “%1 " de TryCatch apresentou uma exceção durante o cancelar.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|DisplayName|xs:string|O nome para exibição de atividade.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
