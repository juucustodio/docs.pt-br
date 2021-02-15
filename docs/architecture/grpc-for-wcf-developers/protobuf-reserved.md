---
title: Protobuf campos reservados – gRPC para desenvolvedores do WCF
description: Saiba mais sobre os campos reservados para compatibilidade entre versões.
ms.date: 12/15/2020
ms.openlocfilehash: d82043d619c5b3b81091ae4ea381e4778c1cf6ba
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938514"
---
# <a name="protobuf-reserved-fields"></a>Campos reservados de Protobuf

As garantias de compatibilidade com versões anteriores no buffer de protocolo (Protobuf) dependem de números de campo sempre representando o mesmo item de dados. Se um campo for removido de uma mensagem em uma nova versão do serviço, esse número de campo nunca deverá ser reutilizado. Você pode impor esse comportamento usando a `reserved` palavra-chave.

Se os `displayName` `marketId` campos e tiverem sido removidos da `Stock` mensagem definida anteriormente, os números de campos deverão ser reservados como no exemplo a seguir.

```protobuf
syntax "proto3";

message Stock {

    reserved 3, 4;
    int32 id = 1;
    string symbol = 2;

}
```

Você também pode usar a `reserved` palavra-chave como um espaço reservado para campos que podem ser adicionados no futuro. Você pode expressar números de campo contíguos como um intervalo usando a `to` palavra-chave.

```protobuf
syntax "proto3";

message Info {

    reserved 2, 9 to 11, 15;
    // ...
}
```

>[!div class="step-by-step"]
>[Anterior](protobuf-repeated.md) 
> [Avançar](protobuf-any-oneof.md)
