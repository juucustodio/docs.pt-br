---
description: 'Saiba mais sobre: hospedando exceções'
title: Exceções de hospedagem
ms.date: 03/30/2017
ms.assetid: ad9e14f8-fa17-4d59-b365-fe0e7ec17c98
ms.openlocfilehash: ba2ff3d4bd069483ddc620a09bb97eeaddf84a56
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686447"
---
# <a name="hosting-exceptions"></a>Exceções de hospedagem

Este tópico lista todas as exceções geradas pela hospedagem.  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|Hosting_AddressIsAbsoluteUri|O URI completo não é permitido. Não são permitidos URIs completos para a API de ServiceHostingEnvironment. EnsureServiceAvailable. Use um caminho virtual para o serviço correspondente.|  
|Hosting_BuildProviderCouldNotCreateType|O tipo CLR especificado não pode ser carregado durante a compilação do serviço. Verifique se esse tipo está definido em um arquivo de origem localizado no \\ diretório \ App_Code do aplicativo, contido em um assembly compilado localizado no diretório \bin do aplicativo \\ , ou presente em um assembly instalado no cache de assembly global. O nome do tipo diferencia maiúsculas de minúsculas. Os diretórios como \\ \ App_Code e \\ \Bin devem estar localizados no diretório raiz do aplicativo. Os \\ diretórios \ App_Code e \\ \Bin não podem ser aninhados em subdiretórios.|
