---
description: 'Saiba mais sobre: System. ServiceModel. Channels. PeerNodeAuthenticationFailure'
title: System.ServiceModel.Channels.PeerNodeAuthenticationFailure
ms.date: 03/30/2017
ms.assetid: 0b50f782-ca06-4a82-aa7f-71f78ddc5177
ms.openlocfilehash: 751202abd3e199a03fc4ee0bf1252d4a8027e0cb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99634928"
---
# <a name="systemservicemodelchannelspeernodeauthenticationfailure"></a>System.ServiceModel.Channels.PeerNodeAuthenticationFailure

O handshake de segurança com um vizinho potencial não foi bem-sucedido.  
  
## <a name="description"></a>Descrição  

 Esse rastreamento ocorre durante a tentativa de estabelecer uma conexão de vizinho segura. Isso pode ocorrer devido a credenciais insuficientes ou incorretas.  
  
 O PeerChannel reconhece um único tipo de token para certificados de identificação forte, X. 509, que fornecem um modelo de identidade forte baseado no tipo de autenticação e autorização que podem ser implementados. O PeerChannel também oferece suporte a aplicativos simples por meio do uso de senhas. As senhas só podem ser usadas para permitir a entrada na sessão; Eles não podem ser usados para executar a autenticação de mensagens. Isso ocorre porque um token simétrico que um grupo de colegas compartilha é difícil e inadequado para a autenticação de origem.  
  
## <a name="troubleshooting"></a>Solução de problemas  

 Verifique se todos os vizinhos têm as credenciais de segurança apropriadas.  
  
## <a name="see-also"></a>Consulte também

- [Segurança de canal par](../../feature-details/peer-channel-security.md)
- [Rastreamento](index.md)
- [Utilizando o rastreamento para solucionar problemas em seu aplicativo](using-tracing-to-troubleshoot-your-application.md)
- [Administração e diagnósticos](../index.md)
