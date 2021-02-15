---
description: 'Saiba mais sobre: System. ServiceModel. Channels. FailedAcceptFromPool'
title: System.ServiceModel.Channels.FailedAcceptFromPool
ms.date: 03/30/2017
ms.assetid: d535b1b5-ee58-45e8-b400-7d9570f4eb9a
ms.openlocfilehash: 1b3c15594611726fd4872197b97ad4ed56c085c4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99635253"
---
# <a name="systemservicemodelchannelsfailedacceptfrompool"></a>System.ServiceModel.Channels.FailedAcceptFromPool

Falha ao tentar reutilizar uma conexão em pool. Outra tentativa é feita dentro do período de tempo limite especificado.  
  
## <a name="description"></a>Descrição  

 Esse rastreamento informativo indica que ocorreu um erro ao tentar reutilizar uma conexão em pool. Isso pode acontecer porque a conexão em pool não era compatível, pronta ou ainda está ativa. As tentativas adicionais de reutilização de outra conexão em pool são feitas dentro de um determinado tempo limite e uma nova conexão é criada caso não sejam encontradas conexões utilizáveis.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
