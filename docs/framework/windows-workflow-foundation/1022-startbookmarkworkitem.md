---
description: 'Saiba mais sobre: 1022-StartBookmarkWorkItem'
title: 1022 - StartBookmarkWorkItem
ms.date: 03/30/2017
ms.assetid: 4415fbdb-0329-4019-803f-aea66e75f3da
ms.openlocfilehash: 37d1ec1216df26a928b39189ca299dbb5b6c3d4b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792824"
---
# <a name="1022---startbookmarkworkitem"></a>1022 - StartBookmarkWorkItem

## <a name="properties"></a>Propriedades  
  
|||  
|-|-|  
|ID|1022|  
|Palavras-chave|WFRuntime|  
|Nível|Detalhado|  
|Canal|Os aplicativos de servidor de Microsoft-Windows- aplicativo/depuração|  
  
## <a name="description"></a>Descrição  

 Indica que um BookmarkWorkItem está sendo a execução.  
  
## <a name="message"></a>Mensagem  

 Iniciando a execução de um BookmarkWorkItem para a atividade ' %1 ', DisplayName: ' %2 ', InstanceId: ' %3 '.  BookmarkName: %4, BookmarkScope: %5.  
  
## <a name="details"></a>Detalhes  
  
|Nome do item de dados|Tipo de item de dados|Descrição|  
|--------------------|--------------------|-----------------|  
|Atividade|xs:string|O nome do tipo de atividade.|  
|DisplayName|xs:string|O nome para exibição de atividade.|  
|InstanceId|xs:string|A identificação de instância de atividade.|  
|BookmarkName|xs:string|O nome do indicador.|  
|BookmarkScope|xs:string|O escopo do indexador.|  
|AppDomain|xs:string|A cadeia de caracteres retornada por AppDomain.CurrentDomain.FriendlyName.|
