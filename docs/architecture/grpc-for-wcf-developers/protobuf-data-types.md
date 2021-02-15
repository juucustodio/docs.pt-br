---
title: Tipos de dados escalares Protobuf-gRPC para desenvolvedores do WCF
description: Saiba mais sobre os tipos de dados básico e conhecido que Protobuf e gRPC dão suporte ao .NET Core.
ms.date: 09/09/2019
ms.openlocfilehash: 5447067b953d257258950d020636e0b38245e20d
ms.sourcegitcommit: 665f8fc55258356f4d2f4a6585b750c974b26675
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/30/2020
ms.locfileid: "91573638"
---
# <a name="protobuf-scalar-data-types"></a>Tipos de dados escalares de Protobuf

O buffer de protocolo (Protobuf) dá suporte a um intervalo de tipos de valores escalares nativos. A tabela a seguir lista todos eles com seu tipo C# equivalente:

| Tipo de Protobuf | Tipo de C#      | Observações |
| ------------- | ------------ | ----- |
| `double`      | `double`     |       |
| `float`       | `float`      |       |
| `int32`       | `int`        | 1     |
| `int64`       | `long`       | 1     |
| `uint32`      | `uint`       |       |
| `uint64`      | `ulong`      |       |
| `sint32`      | `int`        | 1     |
| `sint64`      | `long`       | 1     |
| `fixed32`     | `uint`       | 2     |
| `fixed64`     | `ulong`      | 2     |
| `sfixed32`    | `int`        | 2     |
| `sfixed64`    | `long`       | 2     |
| `bool`        | `bool`       |       |
| `string`      | `string`     | 3     |
| `bytes`       | `ByteString` | 4     |

Observações:

1. A codificação padrão para o `int32` e o `int64` é ineficiente quando você está trabalhando com valores assinados. Se for provável que o campo contenha números negativos, use `sint32` ou `sint64` em vez disso. Esses tipos são mapeados para o C# `int` e `long` tipos, respectivamente.
2. Os `fixed` campos sempre usam o mesmo número de bytes, independentemente do valor. Esse comportamento torna a serialização e a desserialização mais rápidas para valores maiores.
3. As cadeias de caracteres Protobuf são codificadas em UTF-8 (ou ASCII de 7 bits). O comprimento codificado não pode ser maior que 2<sup>32</sup>.
4. O tempo de execução do Protobuf fornece um `ByteString` tipo que mapeia facilmente para e de `byte[]` matrizes C#.

## <a name="other-net-primitive-types"></a>Outros tipos primitivos .NET

### <a name="dates-and-times"></a>Datas e horas

Os tipos escalares nativos não fornecem valores de data e hora, equivalentes a C# <xref:System.DateTimeOffset> , <xref:System.DateTime> e <xref:System.TimeSpan> . Você pode especificar esses tipos usando algumas das extensões "tipos conhecidos" do Google. Essas extensões fornecem geração de código e suporte a tempo de execução para tipos de campo complexos em plataformas com suporte.

A tabela a seguir mostra os tipos de data e hora:

| Tipo de C# | Protobuf tipo bem conhecido |
| ------- | ------------------------ |
| `DateTimeOffset` | `google.protobuf.Timestamp` |
| `DateTime` | `google.protobuf.Timestamp` |
| `TimeSpan` | `google.protobuf.Duration` |

```protobuf  
syntax = "proto3"

import "google/protobuf/duration.proto";  
import "google/protobuf/timestamp.proto";

message Meeting {

    string subject = 1;
    google.protobuf.Timestamp time = 2;
    google.protobuf.Duration duration = 3;

}  
```

As propriedades geradas na classe C# não são os tipos de data e hora do .NET. As propriedades usam as `Timestamp` `Duration` classes e no `Google.Protobuf.WellKnownTypes` namespace. Essas classes fornecem métodos para converter de e para `DateTimeOffset` , `DateTime` e `TimeSpan` .

```csharp
// Create Timestamp and Duration from .NET DateTimeOffset and TimeSpan
var meeting = new Meeting
{
    Time = Timestamp.FromDateTimeOffset(meetingTime), // also FromDateTime()
    Duration = Duration.FromTimeSpan(meetingLength)
};

// Convert Timestamp and Duration to .NET DateTimeOffset and TimeSpan
DateTimeOffset time = meeting.Time.ToDateTimeOffset();
TimeSpan? duration = meeting.Duration?.ToTimeSpan();
```

> [!NOTE]
> O `Timestamp` tipo funciona com horas UTC. `DateTimeOffset` os valores sempre têm um deslocamento de zero e a `DateTime.Kind` propriedade é sempre `DateTimeKind.Utc` .

### <a name="systemguid"></a>System.Guid

O Protobuf não oferece suporte direto ao <xref:System.Guid> tipo, conhecido como `UUID` em outras plataformas. Não há um tipo bem conhecido para ele.

A melhor abordagem é manipular `Guid` valores como um `string` campo, usando o `8-4-4-4-12` formato hexadecimal padrão (por exemplo, `45a9fda3-bd01-47a9-8460-c1cd7484b0b3` ). Todas as linguagens e plataformas podem analisar esse formato.

Não use um `bytes` campo para `Guid` valores. Problemas com a *endian* ([definição da Wikipédia](https://en.wikipedia.org/wiki/Endianness)) podem resultar em comportamento irregular quando o Protobuf está interagindo com outras plataformas, como Java.

### <a name="nullable-types"></a>Tipos anuláveis

A geração de código Protobuf para C# usa os tipos nativos, como `int` para `int32` . Portanto, os valores são sempre incluídos e não podem ser nulos.

Para valores que exigem NULL explícito, como usar `int?` em seu código C#, "tipos conhecidos" de Protobuf incluem wrappers que são compilados para tipos em C# anuláveis. Para usá-los, importe `wrappers.proto` para o `.proto` arquivo, da seguinte maneira:

```protobuf  
syntax = "proto3"

import "google/protobuf/wrappers.proto"

message Person {

    ...
    google.protobuf.Int32Value age = 5;

}
```

Protobuf usará o simples `T?` (por exemplo, `int?` ) para a propriedade Message gerada.

A tabela a seguir mostra a lista completa de tipos de wrapper com seu tipo C# equivalente:

| Tipo de C#   | Wrapper de tipo bem conhecido       |
| --------- | ----------------------------- |
| `double?` | `google.protobuf.DoubleValue` |
| `float?`  | `google.protobuf.FloatValue`  |
| `int?`    | `google.protobuf.Int32Value`  |
| `long?`   | `google.protobuf.Int64Value`  |
| `uint?`   | `google.protobuf.UInt32Value` |
| `ulong?`  | `google.protobuf.UInt64Value` |

Os tipos bem conhecidos `Timestamp` e `Duration` são representados no .net como classes. No C# 8 e além disso, você pode usar tipos de referência anuláveis. Mas é importante verificar se há nulo nas propriedades desses tipos quando você estiver convertendo para `DateTimeOffset` ou `TimeSpan` .

## <a name="decimals"></a>Decimais

O Protobuf não dá suporte nativo ao `decimal` tipo .net, apenas `double` e `float` . Há uma discussão contínua no projeto Protobuf sobre a possibilidade de adicionar um `Decimal` tipo padrão aos tipos conhecidos, com suporte de plataforma para linguagens e estruturas que dão suporte a ele. Nada foi implementado ainda.

É possível criar uma definição de mensagem para representar o `decimal` tipo que funcionaria para a serialização segura entre clientes e servidores .net. Mas os desenvolvedores de outras plataformas teriam que entender o formato que está sendo usado e implementar sua própria manipulação.

### <a name="creating-a-custom-decimal-type-for-protobuf"></a>Criando um tipo decimal personalizado para Protobuf

Uma implementação simples pode ser semelhante ao tipo não padrão `Money` que algumas APIs do Google usam, sem o `currency` campo.

```protobuf
package CustomTypes;

// Example: 12345.6789 -> { units = 12345, nanos = 678900000 }
message DecimalValue {

    // Whole units part of the amount
    int64 units = 1;

    // Nano units of the amount (10^-9)
    // Must be same sign as units
    sfixed32 nanos = 2;
}
```

O `nanos` campo representa valores de `0.999_999_999` a `-0.999_999_999` . Por exemplo, o `decimal` valor `1.5m` seria representado como `{ units = 1, nanos = 500_000_000 }` . É por isso que o `nanos` campo neste exemplo usa o `sfixed32` tipo, que codifica com mais eficiência do que `int32` para valores maiores. Se o `units` campo for negativo, o `nanos` campo também deverá ser negativo.

> [!NOTE]
> Há vários outros algoritmos para codificar `decimal` valores como cadeias de caracteres de byte, mas essa mensagem é mais fácil de entender do que qualquer um deles. Os valores não são afetados pela endian em plataformas diferentes.

A conversão entre esse tipo e o `decimal` tipo de BCL pode ser implementada em C# da seguinte maneira:

```csharp
namespace CustomTypes
{
    public partial class DecimalValue
    {
        private const decimal NanoFactor = 1_000_000_000;
        public DecimalValue(long units, int nanos)
        {
            Units = units;
            Nanos = nanos;
        }

        public long Units { get; }
        public int Nanos { get; }

        public static implicit operator decimal(CustomTypes.DecimalValue grpcDecimal)
        {
            return grpcDecimal.Units + grpcDecimal.Nanos / NanoFactor;
        }

        public static implicit operator CustomTypes.DecimalValue(decimal value)
        {
            var units = decimal.ToInt64(value);
            var nanos = decimal.ToInt32((value - units) * NanoFactor);
            return new CustomTypes.DecimalValue(units, nanos);
        }
    }
}
```

> [!IMPORTANT]
> Sempre que usar tipos de mensagem personalizados como este, você *deve* documentá-los com comentários no `.proto` . Outros desenvolvedores podem então implementar a conversão de e para o tipo equivalente em seu próprio idioma ou estrutura.

>[!div class="step-by-step"]
>[Anterior](protobuf-messages.md) 
> [Avançar](protobuf-nested-types.md)
