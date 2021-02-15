---
description: 'Saiba mais sobre: como implantar um aplicativo de integração COM+'
title: 'Como: implantar um aplicativo de integração COM+'
ms.date: 03/30/2017
ms.assetid: 2e5a0510-db3c-4988-a09c-696285836650
ms.openlocfilehash: 4bf9e72a631c97f3b791ecd01abb5cb74365772d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99734380"
---
# <a name="how-to-deploy-a-com-integration-application"></a>Como: implantar um aplicativo de integração COM+

Depois de escrever um aplicativo de integração COM+, talvez você queira implantá-lo em outro computador. Este tópico descreve como mover um aplicativo de integração COM+ de um computador para outro.  
  
### <a name="moving-a-com-hosted-integration-app"></a>Movendo um aplicativo de integração hospedado COM+  
  
1. Verifique se o WCF está instalado em ambos os computadores.  
  
2. Exporte o aplicativo do computador A.  
  
3. Importe o aplicativo no computador B.  
  
4. Defina o diretório raiz do aplicativo. Por convenção, é% PROGRAMfiles%/ComPlus Applications/{AppGUID}.  
  
5. Copie o Application.config e os arquivos. manifest do aplicativo do diretório raiz do aplicativo no computador A para o diretório raiz do aplicativo no computador B.  
  
6. Edite os endereços de ponto de extremidade de serviço no arquivo de Application.config no computador B para identificar o computador apropriado. Por exemplo, altere `http://machineA/MyService` para `http://machineB/MyService`.  
  
### <a name="moving-a-web-hosted-integration-application"></a>Movendo um aplicativo de integração hospedado na Web  
  
1. Verifique se o WCF está instalado em ambos os computadores.  
  
2. Exporte o aplicativo do computador A.  
  
3. Importe o aplicativo no computador B.  
  
4. Crie uma VRoot do IIS no computador B.  
  
5. Copie o arquivo. svc (ComponentName. svc) e o arquivo Web.config do vroot no computador a para o vroot recentemente criado no computador B.  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da integração com aplicativos COM+](integrating-with-com-plus-applications-overview.md)
- [Como: definir configurações de serviço de COM+](how-to-configure-com-service-settings.md)
- [Como: usar a ferramenta de configuração do modelo de serviço COM+](how-to-use-the-com-service-model-configuration-tool.md)
