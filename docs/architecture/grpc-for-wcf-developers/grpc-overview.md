---
title: Visão geral do gRPC-gRPC para desenvolvedores do WCF
description: Saiba mais sobre o conjunto de princípios que orienta o desenvolvimento do gRPC.
ms.date: 12/15/2020
ms.openlocfilehash: 99e1bdb1f49469f444044027c3ac5d927f9cab13
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938397"
---
# <a name="grpc-overview"></a>Visão geral do gRPC

Depois de examinar o Genesis do Windows Communication Foundation (WCF) e gRPC no último capítulo, este capítulo considera alguns dos principais recursos do gRPC e como eles se comparam ao WCF.

ASP.NET Core 3,0 é a primeira versão do ASP.NET que dá suporte nativamente ao gRPC como cidadão de primeira classe, com as equipes da Microsoft contribuindo para a implementação oficial do .NET do gRPC. É recomendável para a criação de aplicativos distribuídos com o .NET que podem interoperar com todas as outras linguagens de programação e estruturas principais.

## <a name="key-principles"></a>Principais princípios

Conforme discutido no capítulo 1, o Google queria usar a introdução do HTTP/2 para substituir o Stubby, sua infraestrutura de RPC de uso geral interna. o gRPC, com base em Stubby, agora pode aproveitar a padronização e estender sua aplicabilidade à computação móvel, à nuvem e à Internet das Coisas.

Para atingir essa padronização, a [CNCF (nuvem Native Computing Foundation)](https://www.cncf.io/) estabeleceu um conjunto de princípios que governariam o gRPC. A lista a seguir mostra as mais relevantes, que se preocupam principalmente com a maximização da acessibilidade e usabilidade:

- **Gratuito e aberto** – todos os artefatos devem ser de software livre, com licenciamento que não restringe os desenvolvedores de adotar gRPC.
- **Cobertura e simplicidade** – o gRPC deve estar disponível em todas as plataformas populares e é simples o suficiente para criar em qualquer plataforma.
- **Interoperabilidade e alcance** – deve ser possível usar o gRPC em qualquer rede, independentemente da largura de banda ou da latência, usando padrões de rede amplamente disponíveis.
- **Uso geral e desempenho** – a estrutura deve ser utilizável por uma ampla gama de casos de uso possível, sem comprometer o desempenho.
- **Streaming** – o protocolo deve fornecer a semântica de streaming para grandes conjuntos de altos ou mensagens assíncronas.
- **Troca de metadados** – o protocolo permite que dados não comerciais, como tokens de autenticação, sejam tratados separadamente dos dados corporativos reais.
- **Códigos de status padronizados** – a variabilidade dos códigos de erro deve ser reduzida para tornar as decisões de tratamento de erros mais claras. Onde o tratamento de erros adicional e mais rico é necessário, um mecanismo deve ser fornecido para gerenciar o comportamento na troca de metadados.

>[!div class="step-by-step"]
>[Anterior](introduction.md) 
> [Avançar](approach.md)
