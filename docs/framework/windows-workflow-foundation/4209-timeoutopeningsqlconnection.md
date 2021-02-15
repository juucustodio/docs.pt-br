---
description: 'Saiba mais sobre: 4209-TimeoutOpeningSqlConnection'
title: 4209 - TimeoutOpeningSqlConnection
ms.date: 03/30/2017
ms.assetid: f0e56518-9758-41dc-a760-50d1a10fba6e
ms.openlocfilehash: 9c7540e328530fdc01b9f065dfb75b92c467bd43
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787988"
---
# <a name="4209---timeoutopeningsqlconnection"></a>4209 - TimeoutOpeningSqlConnection

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|4209|  
|Palavras-chave|WFInstanceStore|  
|Level|Erro do|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um tempo limite foi encontrado ao tentar abrir uma conexão SQL.  
  
## <a name="message"></a>Mensagem  

 O tempo limite está tentando abrir uma conexão de SQL. A operação não concluiu dentro do tempo limite distribuído de %1. O tempo determinado para essa operação pode ter sido uma parte de um tempo limite maior.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Tempo limite|xs:string|O valor de tempo limite para abrir a conexão SQL.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
