---
description: 'Saiba mais sobre: 2576-TryCatchExceptionFromTry'
title: 2576 - TryCatchExceptionFromTry
ms.date: 03/30/2017
ms.assetid: 47e48973-b17c-4a16-8338-c84b54aa0a6e
ms.openlocfilehash: 83e26726377a9f8bbedda2a310dcf4ee6928d3a2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631510"
---
# <a name="2576---trycatchexceptionfromtry"></a>2576 - TryCatchExceptionFromTry

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|2576|  
|Palavras-chave|WFActivities|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que a atividade de TryCatch capturou uma exceção.  
  
## <a name="message"></a>Mensagem  

 A atividade “%1 " de TryCatch capturou uma exceção “%2 ".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|DisplayName|xs:string|O nome para exibição de atividade.|  
|Exceção|xs:string|O nome do tipo de exceção.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
