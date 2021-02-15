---
description: 'Saiba mais sobre: 3503-DuplicateCorrelationQuery'
title: 3503 - DuplicateCorrelationQuery
ms.date: 03/30/2017
ms.assetid: b857f8e6-ce4d-4da4-bc9d-6cd63fa558a4
ms.openlocfilehash: a8e1e41aad3aa1b273d8f8a5d7b0768fabe4e658
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99778068"
---
# <a name="3503---duplicatecorrelationquery"></a>3503 - DuplicateCorrelationQuery

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|3503|  
|Palavras-chave|WFServices|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Indica que um CorrelationQuery duplicado foi encontrado. A consulta duplicado não será usada para calcular correlação.  
  
## <a name="message"></a>Mensagem  

 Um CorrelationQuery duplicado foi encontrado com Where='%1. Essa consulta duplicada não será usada no cálculo de correlação.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Where|xs:string|Onde parte da consulta de correlação.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
