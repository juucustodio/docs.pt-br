---
description: 'Saiba mais sobre: comunicações principais: canais de transporte HTTP/HTTPS'
title: 'Comunicações de núcleo: canais de transporte HTTP-HTTPS'
ms.date: 03/30/2017
ms.assetid: 6c0a23c9-a663-461c-bdab-58b4d3e23642
ms.openlocfilehash: 585e7511a8c3291c09b40f5895bd700534e6faad
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99635898"
---
# <a name="core-communications-httphttps-transport-channels"></a>Comunicações principais: Canais de transporte HTTP/HTTPS

Este tópico lista todas as exceções geradas por canais HTTP/HTTPS de transporte do Windows Communication Foundation (WCF).  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|DigestExplicitCredsImpersonationLevel|O nível de representação especificado foi especificado. A autenticação HTTP Digest só dá suporte ao nível de ' representação ' quando usada com uma credencial explícita.|  
|FramingContentTypeMismatch|O tipo de conteúdo especificado não era suportado pelo serviço especificado. As associações de cliente e serviço podem ser incompatíveis.|  
|Hosting_SslSettingsMisconfigured|As configurações de protocolo SSL para o serviço especificado não correspondem às do Serviços de Informações da Internet.|  
|HttpAuthSchemeAndClientCert|O HTTPS Listener Factory foi configurado para exigir um certificado de cliente e o esquema de autenticação especificado. No entanto, apenas uma forma de autenticação de cliente pode ser necessária ao mesmo tempo.|  
|HttpReceiveFailure|Ocorreu um erro ao receber a resposta HTTP para o especificado. A associação de ponto de extremidade de serviço não pode estar usando o protocolo HTTP. Outra possibilidade é que um contexto de solicitação HTTP seja encerrado pelo servidor devido a um desligamento do serviço. Consulte os logs do servidor para obter mais detalhes.|  
|HttpRegistrationAccessDenied|O HTTP não pode registrar a URL especificada. Seu processo não tem direitos de acesso a este namespace (consulte [reservas de namespace, registros e roteamento](/windows/desktop/http/namespace-reservations-registrations-and-routing) para obter detalhes).|  
|HttpRegistrationAlreadyExists|O HTTP não pode registrar a URL especificada. Outro aplicativo já registrou essa URL com HTTP.SYS.|  
|HttpRegistrationPortInUse|O HTTP não pode registrar a URL especificada porque a porta TCP especificada está sendo usada por outro aplicativo.|  
|HttpSendFailure|Ocorreu um erro ao fazer a solicitação HTTP para o especificado. Verifique se a causa não é uma incompatibilidade de associação de segurança. Verifique também se o serviço não está configurado para protocolo SSL.|  
|MessageXmlProtocolError|Ocorreu um problema com o XML recebido da rede. Consulte a exceção interna para obter mais detalhes.|  
|MissingContentType|O receptor retornou um erro que indica que o tipo de conteúdo estava ausente na solicitação para o especificado. Consulte a exceção interna para obter mais informações.|  
|ProxyAuthenticationLevelMismatch|A credencial de autenticação de proxy HTTP especificou um requisito de autenticação mútua que é mais estrito do que o requisito para a autenticação do servidor de destino.|  
|ProxyImpersonationLevelMismatch|A credencial de autenticação de proxy HTTP especificou uma restrição de nível de representação mais estrita que a restrição para a autenticação do servidor de destino.|  
|SecureChannelFailure|Um canal seguro não pode ser estabelecido para segurança de camada de soquete/transporte de SSL com a autoridade especificada.|  
|TrustFailure|Uma relação de confiança não pode ser estabelecida para o canal seguro de segurança da camada de soquete/transporte com a autoridade especificada.|  
|UseDefaultWebProxyCantBeUsedWithExplicitProxyAddress|Você não pode especificar um endereço de proxy explícito, bem como UseDefaultWebProxy = true no seu elemento HttpTransportBinding.|
