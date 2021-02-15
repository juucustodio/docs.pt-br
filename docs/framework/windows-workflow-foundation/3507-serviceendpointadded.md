---
description: 'Saiba mais sobre: 3507-ServiceEndpointAdded'
title: 3507 - ServiceEndpointAdded
ms.date: 03/30/2017
ms.assetid: c068fc0e-07ee-4551-9824-ea7216e1fe37
ms.openlocfilehash: 7de51cb8908d3bf4b450c545c1a4c0f2bdc6a453
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631470"
---
# <a name="3507---serviceendpointadded"></a>3507 - ServiceEndpointAdded

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|3507|  
|Palavras-chave|WFServices|  
|Level|Informações|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/analítico|  
  
## <a name="description"></a>Descrição  

 Indica que um ponto final de serviço foi adicionado.  
  
## <a name="message"></a>Mensagem  

 Um ponto final de serviço foi adicionado para o endereço “%1 ", associando “%2 ", e reduz “%3 ".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Endereço|xs:string|O endereço do ponto de extremidade.|  
|Associação|xs:string|A associação de ponto de extremidade.|  
|Contrato|xs:string|O contrato de ponto de extremidade.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
