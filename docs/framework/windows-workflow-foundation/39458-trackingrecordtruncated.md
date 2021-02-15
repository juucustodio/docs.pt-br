---
description: 'Saiba mais sobre: 39458-TrackingRecordTruncated'
title: 39458 - TrackingRecordTruncated
ms.date: 03/30/2017
ms.assetid: 5352f0eb-d571-454a-bab5-e2162888b218
ms.openlocfilehash: bb9a46dc5bd9bc4f4709a740dd0e7ec47ca826e3
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631275"
---
# <a name="39458---trackingrecordtruncated"></a>39458 - TrackingRecordTruncated

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|39458|  
|Palavras-chave|WFTracking|  
|Level|Aviso|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um registro de rastreamento foi truncado. Variáveis/anotações/dados do usuário serem removidos.  
  
## <a name="message"></a>Mensagem  

 Registro truncado %1 de rastreamento gravados para a sessão de ETW com provedor %2. Dados de variáveis/anotações/usuários foram removidos  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|RecordNumber|xs:string|O número de registro controlando.|  
|ProviderId|xs:string|A identificação do provedor de ETW|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
