---
title: Migrar uma solução WCF para o gRPC-gRPC para desenvolvedores do WCF
description: Como migrar diferentes tipos de serviços WCF para o equivalente em gRPC.
ms.date: 12/15/2020
ms.openlocfilehash: 3bd35cb6119368ff3db3be9ab5fabf89f2652b29
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97937955"
---
# <a name="migrate-a-wcf-solution-to-grpc"></a>Migrar uma solução WCF para o gRPC

Este capítulo descreverá como trabalhar com projetos ASP.NET Core 5,0 gRPC e demonstrar a migração de diferentes tipos de serviços de Windows Communication Foundation (WCF) para o equivalente gRPC:

- Crie um projeto ASP.NET Core gRPC 5,0.
- Operações simples de solicitação-resposta para RPC unário gRPC.
- Operações unidirecionais para RPC de streaming de cliente gRPC.
- Serviços Full duplex para RPC de streaming bidirecional gRPC.

Também há uma comparação entre usar os serviços de streaming versus campos repetidos para retornar conjuntos de valores, e há uma discussão sobre o uso de bibliotecas de cliente no final do capítulo.

O aplicativo WCF de exemplo é um stub mínimo de um conjunto de serviços de comércio de estoque. Ele usa a biblioteca de contêineres IoC (inversão de controle de código aberto) chamada Autofac para injeção de dependência. Ele inclui três serviços, um para cada tipo de serviço do WCF. Os serviços serão discutidos mais detalhadamente nas seções a seguir. Você pode baixar as soluções de [dotnet-Architecture/grpc-for-WCF-Developers](https://github.com/dotnet-architecture/grpc-for-wcf-developers) no github. Os serviços usam dados falsos para minimizar dependências externas.

Os exemplos incluem as implementações do WCF e do gRPC de cada serviço.

>[!div class="step-by-step"]
>[Anterior](ws-protocols.md) 
> [Avançar](create-project.md)
