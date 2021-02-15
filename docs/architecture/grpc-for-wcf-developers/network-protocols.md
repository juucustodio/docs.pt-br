---
title: Protocolos de rede-gRPC para desenvolvedores do WCF
description: Uma visão geral dos protocolos de rede gRPC.
ms.date: 09/02/2019
ms.openlocfilehash: 801d57c95aec748e5dcf667ca480775ff945b55c
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938553"
---
# <a name="network-protocols"></a>Protocolos de rede

Ao contrário de Windows Communication Foundation (WCF), o gRPC usa HTTP/2 como base para sua rede. Esse protocolo oferece vantagens significativas em relação ao WCF e ao SOAP, que operam somente no HTTP/1.1. Para os desenvolvedores que desejam usar o gRPC, Considerando que não há nenhuma alternativa ao HTTP/2, parece ser o momento ideal para explorar o HTTP/2 mais detalhadamente e identificar os benefícios adicionais do uso do gRPC.

O HTTP/2, lançado pela Internet Engineering Task Force no 2015, foi derivado do protocolo SPDY experimental, que já estava sendo usado pelo Google. Ele foi projetado especificamente para ser mais eficiente, mais rápido e mais seguro do que o HTTP/1.1.

## <a name="key-features-of-http2"></a>Principais recursos do HTTP/2

Esta lista mostra alguns dos principais recursos e vantagens do HTTP/2:

### <a name="binary-protocol"></a>Protocolo binário

Os ciclos de solicitação/resposta não precisam mais de comandos de texto. Essa atividade simplifica e acelera a implementação de comandos. Especificamente, a análise de dados é mais rápida e usa menos memória, a latência de rede é reduzida com melhorias de desempenho óbvias em relação à velocidade, e há um melhor uso geral dos recursos de rede.

### <a name="streams"></a>Fluxos

Os fluxos permitem que você crie conexões de longa duração entre o remetente e o destinatário, em que várias mensagens ou quadros podem ser enviados de forma assíncrona. Vários fluxos podem operar de forma independente em uma única conexão HTTP/2.

### <a name="request-multiplexing-over-a-single-tcp-connection"></a>Solicitação de multiplexação em uma única conexão TCP

Esse recurso é uma das inovações mais importantes do HTTP/2. Como ele permite várias solicitações paralelas de dados, agora é possível baixar arquivos da Web simultaneamente de um único servidor. Os sites são carregados mais rapidamente e a necessidade de otimização é reduzida. Bloqueio de cabeçalho de linha (Chol), em que as respostas que estão prontas devem aguardar para serem enviadas até que uma solicitação anterior seja concluída, também é mitigada (embora o bloqueio de Chol ainda possa ocorrer no nível de transporte de TCP).

### <a name="nettcp-like-performance-cross-platform"></a>Desempenho de net. TCP como, entre plataformas

Fundamentalmente, a combinação de gRPC e HTTP/2 oferece aos desenvolvedores pelo menos a velocidade equivalente e a eficiência das associações de net. TCP para o WCF e, em alguns casos, até maior velocidade e eficiência. Mas, ao contrário de net. TCP, gRPC sobre HTTP/2 não é restrito a aplicativos .NET.

>[!div class="step-by-step"]
>[Anterior](interface-definition-language.md) 
> [Avançar](why-grpc.md)
