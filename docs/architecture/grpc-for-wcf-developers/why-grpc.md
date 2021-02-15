---
title: Por que recomendamos o gRPC para desenvolvedores do WCF – gRPC para desenvolvedores do WCF
description: Uma discussão sobre por que o gRPC é uma boa opção para desenvolvedores do WCF que desejam migrar para arquiteturas e plataformas modernas.
ms.date: 12/15/2020
ms.openlocfilehash: 058f85297610116e96c8580fcefb10ee6dfcf935
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97937968"
---
# <a name="why-we-recommend-grpc-for-wcf-developers"></a>Por que recomendamos o gRPC para desenvolvedores do WCF

Antes de nos aprofundarmos na linguagem e nas técnicas de gRPC, vale a pena discutir por que gRPC é a solução certa para desenvolvedores de Windows Communication Foundation (WCF) que desejam migrar para o .NET.

## <a name="similarity-to-wcf"></a>Similaridade para o WCF

Embora a implementação e a abordagem sejam diferentes para gRPC, a experiência de desenvolvimento e consumo de serviços com o gRPC deve ser intuitiva para desenvolvedores do WCF. A meta subjacente é a mesma: tornar possível codificar como se o cliente e o servidor estiverem na mesma plataforma, sem a necessidade de se preocupar com a rede.

Ambas as plataformas compartilham o princípio de declarar e, em seguida, implementar uma interface, mesmo que o processo para declarar essa interface seja diferente. E, como você verá no capítulo 5, os diferentes tipos de chamadas RPC que o gRPC dá suporte ao MAP bem para as associações disponíveis para os serviços WCF.

## <a name="benefits-of-grpc"></a>Benefícios do gRPC

gRPC significa outras soluções pelos seguintes motivos.

### <a name="performance"></a>Desempenho

Usar HTTP/2 em vez de HTTP/1.1 elimina a necessidade de mensagens legíveis e, em vez disso, usa o protocolo binário menor e mais rápido. Isso é mais eficiente para os computadores analisarem. O HTTP/2 também dá suporte à multiplexação de solicitações em uma única conexão. Esse suporte permite que as respostas sejam enviadas assim que estiverem prontas sem a necessidade de aguardar em uma fila. (No HTTP/1.1, esse problema é conhecido como "bloqueio de cabeçote de linha (Chol)".) Você precisa de menos recursos ao usar o gRPC, o que o torna uma boa solução a ser usada para dispositivos móveis e em redes mais lentas.

### <a name="interoperability"></a>Interoperabilidade

Há ferramentas e bibliotecas de gRPC para todas as principais linguagens de programação e plataformas, incluindo .NET, Java, Python, go, C++, Node.js, Swift, Dart, Ruby e PHP. Graças ao formato de cabo binário dos buffers de protocolo e à geração de código eficiente para cada plataforma, os desenvolvedores podem criar aplicativos de alto desempenho enquanto ainda aproveitam o suporte completo a várias plataformas.

### <a name="usability-and-productivity"></a>Usabilidade e produtividade

gRPC é uma solução RPC abrangente. Ele funciona consistentemente em vários idiomas e plataformas. Ele também fornece ferramentas excelentes, com a maior parte do código clichê necessário gerado automaticamente. Portanto, mais tempo de desenvolvedor é liberado para se concentrar na lógica de negócios.

### <a name="streaming"></a>Streaming

o gRPC tem streaming bidirecional completo, que fornece funcionalidade semelhante aos serviços Full-duplex do WCF. o streaming gRPC pode operar em conexões de Internet regulares, balanceadores de carga e malhas de serviço.

### <a name="deadlinetimeouts-and-cancellation"></a>Prazo/tempos limite e cancelamento

gRPC permite que os clientes especifiquem um tempo máximo para que um RPC seja concluído. Se o prazo especificado for excedido, o servidor poderá cancelar a operação independentemente do cliente. Os prazos finais e cancelamentos podem ser propagados por meio de chamadas gRPC adicionais para ajudar a reforçar os limites de uso de recursos. Os clientes também podem parar as operações quando um prazo é excedido ou antes, se necessário (por exemplo, devido a uma interação do usuário).

### <a name="security"></a>Segurança

o gRPC é implicitamente seguro quando está usando HTTP/2 em uma conexão criptografada de ponta a ponta TLS. O suporte para autenticação de certificado de cliente (consulte o [capítulo 6](security.md)) aumenta ainda mais a segurança e a confiança entre o cliente e o servidor.

>[!div class="step-by-step"]
>[Anterior](network-protocols.md) 
> [Avançar](protocol-buffers.md)
