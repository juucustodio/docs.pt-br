---
title: Segurança em aplicativos gRPC – gRPC para desenvolvedores do WCF
description: Visão geral de autenticação e autorização de canal e chamada no gRPC.
ms.date: 12/15/2020
ms.openlocfilehash: a5c16a4a4f7567e23bf4f9e3049fe116086daf12
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938085"
---
# <a name="security-in-grpc-applications"></a>Segurança em aplicativos gRPC

Em qualquer cenário do mundo real, a proteção de aplicativos e serviços é essencial. A segurança abrange três áreas principais:

* Criptografar o tráfego de rede para impedir que hackers mal-intencionados o interceptem.
* Autenticar clientes e servidores para estabelecer identidade e confiança.
* Autorizar clientes a controlar o acesso a sistemas e aplicar permissões com base na identidade.

> [!NOTE]
> A *autenticação* se preocupa com o estabelecimento da identidade de um cliente ou servidor. A *autorização* está preocupada com a determinação se um cliente tem permissão para acessar um recurso ou emitir um comando.

Este capítulo abordará as instalações de autenticação e autorização no gRPC para ASP.NET Core. Ele também discutirá a segurança de rede por meio de conexões criptografadas por TLS.

## <a name="wcf-authentication-and-authorization"></a>Autenticação e autorização do WCF

No Windows Communication Foundation (WCF), a autenticação e a autorização foram manipuladas de maneiras diferentes, dependendo dos transportes e das associações que estão sendo usadas. O WCF dá suporte a vários padrões WS- \* Security. Também há suporte para a autenticação do Windows para serviços HTTP em execução no IIS ou em serviços NetTCP entre sistemas Windows.

## <a name="grpc-authentication-and-authorization"></a>autenticação e autorização do gRPC

a autenticação e a autorização do gRPC funcionam em dois níveis:

* A autenticação/autorização em nível de chamada geralmente é manipulada por meio de tokens que são aplicados nos metadados quando a chamada é feita.
* A autenticação no nível do canal usa um certificado de cliente que é aplicado no nível de conexão. Ele também pode incluir credenciais de autenticação/autorização em nível de chamada para serem aplicadas a cada chamada no canal automaticamente.

Você pode usar um ou ambos os mecanismos para ajudar a proteger seu serviço.

A implementação de ASP.NET Core do gRPC dá suporte à autenticação e autorização por meio da maioria dos mecanismos de ASP.NET Core padrão:

- Chamar autenticação
  - Azure Active Directory
  - IdentityServer
  - Token de portador JWT
  - OAuth 2.0
  - OpenID Connect
  - O certificado do provedor de identidade do Web Services Federation
- Autenticação de canal
  - Certificado do cliente

Os métodos de autenticação de chamada são todos baseados em *tokens*. A única diferença real é como os tokens são gerados e as bibliotecas que são usadas para validar os tokens no serviço de ASP.NET Core.

Para obter mais informações, consulte o artigo [autenticação e autorização](/aspnet/core/grpc/authn-and-authz) .

> [!NOTE]
> Quando você estiver usando o gRPC em uma conexão HTTP/2 criptografada por TLS, todo o tráfego entre clientes e servidores será criptografado, mesmo que você não use a autenticação no nível do canal.

Este capítulo mostrará como aplicar credenciais de chamada e credenciais de canal a um serviço gRPC. Ele também mostrará como usar credenciais de um cliente .NET gRPC para se autenticar com o serviço.

>[!div class="step-by-step"]
>[Anterior](client-libraries.md) 
> [Avançar](call-credentials.md)
