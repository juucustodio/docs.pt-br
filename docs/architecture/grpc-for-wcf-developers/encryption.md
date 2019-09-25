---
title: Criptografia e segurança de rede-gRPC para desenvolvedores do WCF
description: Algumas observações sobre segurança de rede e criptografia no gRPC
author: markrendle
ms.date: 09/02/2019
ms.openlocfilehash: 8a115b59337003669b4e5436edffe239489ca79e
ms.sourcegitcommit: 55f438d4d00a34b9aca9eedaac3f85590bb11565
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2019
ms.locfileid: "71184459"
---
# <a name="encryption-and-network-security"></a><span data-ttu-id="df5fb-103">Criptografia e segurança de rede</span><span class="sxs-lookup"><span data-stu-id="df5fb-103">Encryption and network security</span></span>

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

<span data-ttu-id="df5fb-104">O modelo de segurança de rede do WCF é extensivo e complexo, incluindo segurança em nível de transporte usando HTTPS ou TLS sobre TCP e segurança em nível de mensagem usando a especificação WS-Security para criptografar mensagens individuais.</span><span class="sxs-lookup"><span data-stu-id="df5fb-104">WCF's network security model is extensive and complex, including transport-level security using HTTPS or TLS-over-TCP, and message-level security using the WS-Security specification to encrypt individual messages.</span></span>

<span data-ttu-id="df5fb-105">gRPC deixa a rede segura para o protocolo HTTP/2 subjacente, que pode ser protegido usando certificados TLS regulares.</span><span class="sxs-lookup"><span data-stu-id="df5fb-105">gRPC leaves secure networking to the underlying HTTP/2 protocol, which can be secured using regular TLS certificates.</span></span>

<span data-ttu-id="df5fb-106">Navegadores da Web insistem no uso de conexões TLS para HTTP/2, mas com a maioria dos clientes programáticos, incluindo. `HttpClient`Net, pode usar http/2 em conexões não criptografadas.</span><span class="sxs-lookup"><span data-stu-id="df5fb-106">Web browsers insist on using TLS connections for HTTP/2, but most programmatic clients, including .NET's `HttpClient`, can use HTTP/2 over unencrypted connections.</span></span> <span data-ttu-id="df5fb-107">`HttpClient`*o* requer criptografia por padrão, mas você pode substituí-lo usando <xref:System.AppContext> uma opção.</span><span class="sxs-lookup"><span data-stu-id="df5fb-107">`HttpClient` *does* require encryption by default, but you can override this using an <xref:System.AppContext> switch.</span></span>

```csharp
AppContext.SetSwitch("System.Net.Http.SocketsHttpHandler.Http2UnencryptedSupport", true);
```

<span data-ttu-id="df5fb-108">Para APIs públicas, você sempre deve usar conexões TLS e fornecer certificados válidos para seus serviços de uma autoridade SSL apropriada.</span><span class="sxs-lookup"><span data-stu-id="df5fb-108">For public APIs, you should always use TLS connections and provide valid certificates for your services from a proper SSL authority.</span></span> <span data-ttu-id="df5fb-109">O [LetsEncrypt](https://letsencrypt.org) fornece certificados SSL gratuitos e automatizados, e a maior parte da infraestrutura de hospedagem atualmente dá suporte ao padrão LetsEncrypt com plug-ins ou extensões comuns.</span><span class="sxs-lookup"><span data-stu-id="df5fb-109">[LetsEncrypt](https://letsencrypt.org) provide free, automated SSL certificates, and most hosting infrastructure today supports the LetsEncrypt standard with common plug-ins or extensions.</span></span>

<span data-ttu-id="df5fb-110">Para serviços internos em uma rede corporativa, você ainda deve considerar o uso do TLS para proteger o tráfego de rede de e para seus serviços gRPCs.</span><span class="sxs-lookup"><span data-stu-id="df5fb-110">For internal services across a corporate network, you should still consider using TLS to secure network traffic to and from your gRPC services.</span></span>

<span data-ttu-id="df5fb-111">A comunicação entre os microserviços em um cluster como o kubernetes ou o Docker Swarm é, em geral, criptografada automaticamente pela camada de rede do contêiner, portanto, não é necessário implementar o TLS em serviços executados exclusivamente nesse cluster.</span><span class="sxs-lookup"><span data-stu-id="df5fb-111">Communication between microservices in a cluster like Kubernetes or Docker Swarm is in general automatically encrypted by the container networking layer, so implementing TLS in services running exclusively in such a cluster isn't necessary.</span></span> <span data-ttu-id="df5fb-112">Haverá mais informações sobre esse assunto na seção "malha de serviço" do próximo capítulo.</span><span class="sxs-lookup"><span data-stu-id="df5fb-112">There will be more on this subject in the "Service Mesh" section of the next chapter.</span></span>

<span data-ttu-id="df5fb-113">Se você precisar usar o TLS explícito entre os serviços em execução no kubernetes, considere usar uma autoridade de certificação no cluster e um controlador do Gerenciador de certificados como [CERT-Manager](https://docs.cert-manager.io/en/latest/) para atribuir certificados automaticamente aos serviços no momento da implantação.</span><span class="sxs-lookup"><span data-stu-id="df5fb-113">If you need to use explicit TLS between services running in Kubernetes, consider using an in-cluster Certificate Authority and a Certificate Manager Controller like [cert-manager](https://docs.cert-manager.io/en/latest/) to assign automatically certificates to services at deployment time.</span></span>

>[!div class="step-by-step"]
><span data-ttu-id="df5fb-114">[Anterior](channel-credentials.md)
>[Próximo](grpc-in-production.md)</span><span class="sxs-lookup"><span data-stu-id="df5fb-114">[Previous](channel-credentials.md)
[Next](grpc-in-production.md)</span></span>