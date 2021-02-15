---
title: Associações e transportes do WCF – gRPC para desenvolvedores do WCF
description: Saiba como as diferentes associações e transportes do WCF se comparam ao gRPC.
ms.date: 12/15/2020
ms.openlocfilehash: 7a50e3e4468d86a6140066502a765818119642d4
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938501"
---
# <a name="wcf-bindings-and-transports"></a>Associações e transportes do WCF

O Windows Communication Foundation (WCF) tem *ligações* internas que especificam diferentes protocolos de rede, formatos de conexão e outros detalhes de implementação. gRPC efetivamente tem apenas um protocolo de rede e um formato de conexão. (Tecnicamente, você *pode* personalizar o formato de conexão, mas está além do escopo deste livro.) É provável que você descubra que o gRPC oferece a melhor solução na maioria dos casos.

O que vem a seguir é uma breve discussão sobre as associações do WCF mais relevantes e como elas se comparam com seus equivalentes no gRPC.

## <a name="nettcp"></a>NetTCP

A associação NetTCP do WCF permite conexões persistentes, mensagens pequenas e mensagens de duas vias. Mas só funciona entre clientes e servidores .NET. o gRPC permite a mesma funcionalidade, mas tem suporte em várias linguagens de programação e plataformas.

o gRPC tem muitos recursos da Associação NetTCP do WCF, mas eles nem sempre são implementados da mesma maneira. Por exemplo, no WCF, a criptografia é controlada por meio da configuração e manipulada na estrutura. No gRPC, a criptografia é obtida no nível de conexão por meio de HTTP/2 por TLS.

## <a name="http"></a>HTTP

A associação do WCF chamada BasicHttpBinding geralmente é baseada em texto e usa SOAP como o formato de conexão. Isso é lento em comparação com a associação NetTCP. Ele é usado para fornecer interoperabilidade entre plataformas ou conexão pela infra-estrutura da Internet.

O equivalente em gRPC usa HTTP/2 como a camada de transporte subjacente com o formato de conexão de Protobuf binário para mensagens. Portanto, ele pode oferecer desempenho no nível de serviço NetTCP e interoperabilidade completa entre plataformas com todas as linguagens e estruturas de programação modernas.

## <a name="named-pipes"></a>Pipes nomeados

O WCF forneceu uma associação de *pipes nomeados* para comunicação entre processos no mesmo computador físico. A primeira versão do ASP.NET Core gRPC não dá suporte a pipes nomeados. Adicionar suporte de cliente e servidor para pipes nomeados (e soquetes de domínio do UNIX) é uma meta para uma versão futura.

## <a name="msmq"></a>MSMQ

O MSMQ é uma fila de mensagens do Windows proprietária. A ligação do WCF com o MSMQ permite solicitações "disparar e esquecer" de clientes que podem ser processados a qualquer momento no futuro. o gRPC não fornece uma funcionalidade de fila de mensagens nativamente.

A melhor alternativa é usar diretamente um sistema de mensagens como o barramento de serviço do Azure, RabbitMQ ou Kafka. Você pode implementar essa funcionalidade com o cliente que está colocando as mensagens diretamente na fila ou um serviço de streaming de cliente gRPC que enfileira as mensagens.

## <a name="webhttpbinding"></a>WebHttpBinding

WebHttpBinding (também conhecido como WCF REST), com os `WebGet` `WebInvoke` atributos e, habilitou você a desenvolver APIs RESTful que poderiam falar JSON por vez quando esse comportamento fosse menos comum. Se você tiver uma API RESTful criada com o WCF REST, considere migrá-la para um aplicativo de API Web do MVC regular ASP.NET Core. Essa migração forneceria a mesma funcionalidade que uma conversão em gRPC.

>[!div class="step-by-step"]
>[Anterior](wcf-endpoints-grpc-methods.md) 
> [Avançar](rpc-types.md)
