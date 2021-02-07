---
description: 'Saiba mais sobre: 1025-BookmarkScopeInitialized'
title: 1025 - BookmarkScopeInitialized
ms.date: 03/30/2017
ms.assetid: 63584434-e709-471d-9e96-97d3d99e70d6
ms.openlocfilehash: 22e686253fc5d580fba453950825072667247fad
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755493"
---
# <a name="1025---bookmarkscopeinitialized"></a>1025 - BookmarkScopeInitialized

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1025|  
|Palavras-chave|WFRuntime|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um BookmarkScope foi inicializado.  
  
## <a name="message"></a>Mensagem  

 O BookmarkScope que tinha TemporaryId: “%1 " foi inicializado com ID: “%2".  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|TemporaryId|xs:string|A identificação do indexador temporária.|  
|InitializedId|xs:string|A identificação do indexador inicializada.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
