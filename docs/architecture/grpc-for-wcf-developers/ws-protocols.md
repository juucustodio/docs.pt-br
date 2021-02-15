---
title: Protocolos WS-*-gRPC para desenvolvedores do WCF
description: Revisão dos protocolos WS-* com suporte do WCF e das alternativas disponíveis com o gRPC
author: markrendle
ms.date: 12/15/2020
ms.openlocfilehash: d6fffdd5153c799c78ad949a3b16fa72e9612e43
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938475"
---
# <a name="ws--protocols"></a>WS- \* Protocols

Um dos verdadeiros benefícios de trabalhar com o Windows Communication Foundation (WCF) era que ele oferecia suporte a muitos dos protocolos _WS- \*_ Standard existentes. Esta seção explicará brevemente como o gRPC gerencia os mesmos WS- \* Protocols e discute quais opções estão disponíveis quando não há nenhuma alternativa.

## <a name="metadata-exchange-ws-policy-ws-discovery-and-so-on"></a>Troca de metadados: WS-Policy, WS-Discovery e assim por diante

Os serviços SOAP expõem documentos de esquema WSDL (linguagem de descrição de serviços Web) com informações como formatos de dados, operações ou opções de comunicação. Você pode usar este esquema para gerar o código do cliente.

o gRPC funciona melhor quando servidores e clientes são gerados a partir dos mesmos `.proto` arquivos, mas uma extensão opcional de reflexão de servidor fornece uma maneira de expor informações dinâmicas de um servidor em execução. Para obter mais informações, consulte o pacote NuGet [Grpc. Reflection](https://nuget.org/packages/Grpc.Reflection) e o artigo de [reflexão do servidor Grpc C#](https://github.com/grpc/grpc/blob/master/doc/csharp/server_reflection.md) .

O protocolo WS-Discovery é usado para localizar serviços em uma rede local. os serviços gRPCs estão localizados por meio do DNS ou de um registro de serviço, como Consul ou ZooKeeper.

## <a name="security-ws-security-ws-federation-xml-encryption-and-so-on"></a>Segurança: WS-Security, WS-Federation, criptografia XML e assim por diante

A segurança, a autenticação e a autorização são abordadas com muito mais detalhes no [capítulo 6](security.md). Mas vale a pena observar que, ao contrário do WCF, o gRPC não dá suporte a WS-Security, WS-Federation ou criptografia XML. Mesmo assim, o gRPC fornece excelente segurança. Todo o tráfego de rede gRPC é criptografado automaticamente quando está usando HTTP/2 por TLS. Você pode usar certificados X509 para autenticação de cliente/servidor mútuo.

## <a name="ws-reliablemessaging"></a>WS-ReliableMessaging

gRPC não fornece um equivalente a WS-ReliableMessaging. A semântica de repetição deve ser tratada no código, possivelmente com uma biblioteca como [Polly](https://github.com/App-vNext/Polly). Quando você está executando em ambientes de orquestração kubernetes ou similares, as [malhas de serviço](service-mesh.md) também podem ajudar a fornecer mensagens confiáveis entre serviços.

## <a name="ws-transaction-ws-coordination"></a>WS-Transaction, WS-Coordination

A implementação do WCF de transações distribuídas usa o Microsoft Coordenador de Transações Distribuídas (MSDTC). Ele funciona com gerenciadores de recursos que dão suporte especificamente a ele, como SQL Server, MSMQ ou sistemas de arquivos do Windows. Ainda não há nenhum equivalente no mundo de microserviços modernos, em parte devido à maior variedade de tecnologias em uso. Para obter uma discussão sobre transações, consulte [o apêndice a](appendix.md).

>[!div class="step-by-step"]
>[Anterior](error-handling.md) 
> [Avançar](migrate-wcf-to-grpc.md)
