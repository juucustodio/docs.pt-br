---
description: 'Saiba mais sobre: Implantando aplicativos WCF com o ClickOnce'
title: Implantando aplicativos do WCF com um clique
ms.date: 03/30/2017
ms.assetid: 1a11feee-2a47-4d3e-a28a-ad69d5ff93e0
ms.openlocfilehash: f0a78bab6bbe7ddfd431e8e12bfe1ca9c9143143
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99646082"
---
# <a name="deploying-wcf-applications-with-clickonce"></a>Implantando aplicativos do WCF com um clique

Aplicativos cliente que usam Windows Communication Foundation (WCF) podem ser implantados usando a tecnologia ClickOnce. Essa tecnologia permite que eles aproveitem as proteções de segurança de tempo de execução fornecidas pela segurança de acesso ao código, desde que sejam assinadas digitalmente com um certificado confiável. O certificado usado para assinar o aplicativo ClickOnce deve residir no repositório de fornecedores confiáveis, e a política de segurança local no computador cliente deve ser configurada para conceder permissões de confiança total a aplicativos assinados com o certificado do Publicador.  
  
 Para obter informações sobre como configurar aplicativos ClickOnce e editores confiáveis, consulte [Configurando editores confiáveis do ClickOnce](/previous-versions/dotnet/articles/ms996418(v=msdn.10)).  
  
## <a name="see-also"></a>Consulte também

- [Visão geral da implantação de aplicativos confiáveis](/visualstudio/deployment/trusted-application-deployment-overview)
- [Implantação do ClickOnce para aplicativos Windows Forms](/previous-versions/visualstudio/visual-studio-2008/wh45kb66(v=vs.90))
