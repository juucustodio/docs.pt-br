---
title: Mapas do Protobuf para dicionários-gRPC para desenvolvedores do WCF
description: Entenda como usar o Protobuf Maps para representar tipos de dicionário no .NET.
ms.date: 12/15/2020
ms.openlocfilehash: d38270d4bc320cf1f758080c18843ed1d716b350
ms.sourcegitcommit: 655f8a16c488567dfa696fc0b293b34d3c81e3df
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/06/2021
ms.locfileid: "97938540"
---
# <a name="protobuf-maps-for-dictionaries"></a>Mapas de Protobuf para dicionários

É importante poder representar coleções arbitrárias de valores nomeados em mensagens. No .NET, essa atividade é comumente manipulada por meio de tipos de dicionário. O equivalente do tipo .NET <xref:System.Collections.Generic.IDictionary%602> no buffer de protocolo (Protobuf) é o `map<key_type, value_type>` tipo. Esta seção mostra como declarar um `map` tipo em Protobuf e como usar o código gerado.

```protobuf
message StockPrices {
    map<string, double> prices = 1;
}
```

No código gerado, os `map` campos são representados por propriedades somente leitura do [`Google.Protobuf.Collections.MapField<TKey, TValue>`][map-field] tipo. Esse tipo implementa as interfaces de coleção do .NET padrão, incluindo <xref:System.Collections.Generic.IDictionary%602> .

Os campos de mapa não podem ser repetidos diretamente em uma definição de mensagem. Mas você pode criar uma mensagem aninhada que contém um mapa e usar `repeated` no tipo de mensagem, como no exemplo a seguir:

```protobuf
message Order {
    message Attributes {
        map<string, string> values = 1;
    }
    repeated Attributes attributes = 1;
}
```

## <a name="using-mapfield-properties-in-code"></a>Usando Propriedades MapField no código

As `MapField` Propriedades geradas a partir de `map` campos são somente leitura e nunca serão `null` . Para definir uma propriedade de mapa, use o `Add(IDictionary<TKey,TValue> values)` método na `MapField` Propriedade Empty para copiar valores de qualquer dicionário .net.

```csharp
public Order CreateOrder(Dictionary<string, string> attributes)
{
    var order = new Order();
    order.Attributes.Add(attributes);
    return order;
}
```

## <a name="further-reading"></a>Leitura adicional

Para obter mais informações sobre o Protobuf, consulte a documentação oficial do [Protobuf](https://developers.google.com/protocol-buffers/docs/overview).

[map-field]: https://developers.google.cn/protocol-buffers/docs/reference/csharp/class/google/protobuf/collections/map-field-t-key-t-value-

>[!div class="step-by-step"]
>[Anterior](protobuf-enums.md) 
> [Avançar](wcf-services-to-grpc-comparison.md)
