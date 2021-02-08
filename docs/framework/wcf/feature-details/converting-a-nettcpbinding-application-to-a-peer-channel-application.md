---
description: 'Saiba mais sobre: convertendo um aplicativo NetTcpbinding em um aplicativo de canal par'
title: Convertendo um aplicativo NetTcpBinding em um aplicativo de canal par
ms.date: 03/30/2017
ms.assetid: d4137292-a923-4b8f-8594-42276f2d3ce2
ms.openlocfilehash: 828ffce38fb05acff851c9fe5a6fbb38fffad6aa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780408"
---
# <a name="converting-a-nettcpbinding-application-to-a-peer-channel-application"></a>Convertendo um aplicativo NetTcpBinding em um aplicativo de canal par

Você pode criar conexões entre clientes usando o WinFX usando associações que descrevem os parâmetros da conexão. Converter um aplicativo .NET Framework para usar conexões ponto a ponto requer uma associação que dá suporte a essa tecnologia ao fazer conexões de cliente. O canal par fornece uma associação chamada <xref:System.ServiceModel.NetPeerTcpBinding> , que pode ser usada de forma semelhante ao <xref:System.ServiceModel.NetTcpBinding> . As principais diferenças incluem a especificação de um serviço de resolvedor e a definição de configurações de segurança.  
  
 Se um aplicativo estiver usando o resolvedor padrão e as configurações de segurança, converter um aplicativo normal baseado em cliente/servidor para usar o canal de pares envolve alterar o nome da Associação de "NetTcpbinding" para "NetPeerTcpBinding" no arquivo de configuração do aplicativo — você não precisa alterar a base de código do aplicativo.  
  
## <a name="see-also"></a>Consulte também

- [Compilando um aplicativo de canal par](building-a-peer-channel-application.md)
- [Associações fornecidas pelo sistema](../system-provided-bindings.md)
