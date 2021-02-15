---
description: 'Saiba mais sobre: System. ServiceModel. MessageClosedAgain'
title: System.ServiceModel.MessageClosedAgain
ms.date: 03/30/2017
ms.assetid: 24c274d4-65cd-4c91-9869-bc6eb34ef979
ms.openlocfilehash: 40e6dcc8974440bd7d7f10ca30e36447c4ae790a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99716192"
---
# <a name="systemservicemodelmessageclosedagain"></a>System.ServiceModel.MessageClosedAgain

System.ServiceModel.MessageClosedAgain  
  
## <a name="description"></a>Descrição  

 Uma mensagem foi fechada novamente.  
  
 Uma mensagem deve ser fechada apenas uma vez. Se esse rastreamento estiver sendo emitido no código de extensão do usuário, ele indica que o código de extensão do usuário está fechando uma mensagem que já foi fechada. Se esse rastreamento estiver sendo emitido por meio do código do produto, ele indica que o código de extensão do usuário pode estar fechando uma mensagem muito cedo.  
  
## <a name="see-also"></a>Consulte também

- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
