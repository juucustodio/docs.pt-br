---
description: 'Saiba mais sobre: System. ServiceModel. MessageProcessingPaused'
title: System.ServiceModel.MessageProcessingPaused
ms.date: 03/30/2017
ms.assetid: 36b5302a-93cc-478a-9bb2-8a1601fba1df
ms.openlocfilehash: 77e4742bc5617904136b2ddd9cb90fe886d38b10
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716172"
---
# <a name="systemservicemodelmessageprocessingpaused"></a>System.ServiceModel.MessageProcessingPaused

System.ServiceModel.MessageProcessingPaused  
  
## <a name="description"></a>Descrição  

 Os threads foram alternados durante o processamento de uma mensagem.  
  
 O processamento de mensagens pode ser pausado pelos seguintes motivos:  
  
- ConcurrencyMode é Single ou reentrante e o serviço está processando outra mensagem.  
  
- A transação está habilitada e o serviço está processando outra transação.  
  
- O contexto de sincronização não é atual.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
