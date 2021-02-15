---
description: 'Saiba mais sobre: 1037-RuntimeTransactionComplete'
title: 1037 - RuntimeTransactionComplete
ms.date: 03/30/2017
ms.assetid: 2c8c31e0-42a9-4f46-865b-2da9ab16a0ba
ms.openlocfilehash: 5784dc1b0eede5ddad0e6aae4cb79c6e859f325e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99667857"
---
# <a name="1037---runtimetransactioncomplete"></a>1037 - RuntimeTransactionComplete

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1037|  
|Palavras-chave|WFRuntime|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que a transação de runtime terminado.  
  
## <a name="message"></a>Mensagem  

 A transação de runtime terminou com o estado “%1 ".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Estado|xs:string|O estado de transação.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
