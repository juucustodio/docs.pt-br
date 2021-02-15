---
title: Comparando o WCF com o gRPC-gRPC para desenvolvedores do WCF
description: Uma comparação das estruturas do WCF e do gRPC para a criação de aplicativos distribuídos.
ms.date: 12/15/2020
ms.openlocfilehash: 7dd41c3d6f248bb1ef5eacb323b1443c7bc575a7
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938488"
---
# <a name="comparing-wcf-to-grpc"></a>Comparando o WCF com o gRPC

O capítulo anterior forneceu uma boa visão sobre Protobuf e como o gRPC lida com mensagens. Antes de você trabalhar com uma conversão detalhada de Windows Communication Foundation (WCF) para gRPC, é importante saber como os recursos disponíveis no WCF são manipulados no gRPC e quais soluções alternativas você pode usar quando não há nenhum equivalente gRPC. Em particular, este capítulo abordará os seguintes assuntos:

- Operações e métodos
- Associações e transportes
- Tipos de RPC
- Metadados
- Tratamento de erros
- WS- \* Protocols

## <a name="grpc-example"></a>exemplo de gRPC

Quando você cria um novo projeto ASP.NET Core 5,0 gRPC no Visual Studio 2019 ou na linha de comando, o equivalente de gRPC de "Olá, Mundo" é gerado para você. Ele consiste em um `greeter.proto` arquivo que define o serviço e suas mensagens, e um `GreeterService.cs` arquivo com uma implementação do serviço.

```protobuf
syntax = "proto3";

option csharp_namespace = "HelloGrpc";

package Greet;

// The greeting service definition.
service Greeter {
  // Sends a greeting
  rpc SayHello (HelloRequest) returns (HelloReply);
}

// The request message that contains the user's name.
message HelloRequest {
  string name = 1;
}

// The response message that contains the greetings.
message HelloReply {
  string message = 1;
}
```

```csharp
using System.Threading.Tasks;
using Grpc.Core;
using Microsoft.Extensions.Logging;

namespace HelloGrpc
{
    public class GreeterService : Greeter.GreeterBase
    {
        private readonly ILogger<GreeterService> _logger;
        public GreeterService(ILogger<GreeterService> logger)
        {
            _logger = logger;
        }

        public override Task<HelloReply> SayHello(HelloRequest request, ServerCallContext context)
        {
            return Task.FromResult(new HelloReply
            {
                Message = "Hello " + request.Name
            });
        }
    }
}
```

Este capítulo fará referência a este código de exemplo ao explicar diferentes conceitos e recursos do gRPC.

>[!div class="step-by-step"]
>[Anterior](protobuf-maps.md) 
> [Avançar](wcf-endpoints-grpc-methods.md)
