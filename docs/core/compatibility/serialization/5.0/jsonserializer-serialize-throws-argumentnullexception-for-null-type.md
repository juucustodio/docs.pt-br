---
title: 'Alteração significativa: Serialize gera uma exceção quando o parâmetro de tipo é nulo'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que os métodos de serialização JsonSerialize que têm um parâmetro de tipo agora lançam uma exceção sempre que NULL é passado para esse parâmetro.
ms.date: 10/18/2020
ms.openlocfilehash: af2885394418072ad7efec5855490b5b80152fe6
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760503"
---
# <a name="jsonserializerserialize-throws-argumentnullexception-when-type-parameter-is-null"></a>JsonSerializer. Serialize gera ArgumentNullException quando o parâmetro de tipo é nulo

<xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType>, <xref:System.Text.Json.JsonSerializer.SerializeAsync%2A?displayProperty=nameWithType> e <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=nameWithType> sobrecargas que têm um parâmetro do tipo <xref:System.Type> agora lançam um <xref:System.ArgumentNullException> sempre que `null` é passado para esse parâmetro.

## <a name="change-description"></a>Descrição das alterações

No .NET Core 3,1, as <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> <xref:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)?displayProperty=nameWithType> <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=nameWithType> sobrecargas que têm um <xref:System.Type> parâmetro geram um <xref:System.ArgumentNullException> quando `null` é passado para o `Type inputType` parâmetro, mas não se o `Object value` parâmetro também for `null` . A partir do .NET 5,0, esses métodos *sempre* lançam um <xref:System.ArgumentNullException> quando `null` é passado para o <xref:System.Type> parâmetro.

Comportamento no .NET Core 3,1:

```csharp
// Returns a string with value "null".
JsonSerializer.Serialize(null, null);

// Returns a byte array with value "null".
JsonSerializer.SerializeToUtf8Bytes(null, null);
```

Comportamento no .NET 5,0 e posterior:

```csharp
// Throws ArgumentNullException: "Value cannot be null. (Parameter 'inputType')".
JsonSerializer.Serialize(null, null);

// Throws ArgumentNullException: "Value cannot be null. (Parameter 'inputType')".
JsonSerializer.SerializeToUtf8Bytes(null, null);
```

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="reason-for-change"></a>Motivo da alteração

A passagem `null` para o `Type inputType` parâmetro é inaceitável e sempre deve lançar um <xref:System.ArgumentNullException> .

## <a name="recommended-action"></a>Ação recomendada

Certifique-se de que você não está passando `null` para o `Type inputType` parâmetro desses métodos.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Text.Json.JsonSerializer.Serialize(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.Serialize(System.Text.Json.Utf8JsonWriter,System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)?displayProperty=fullName>

<!--

### Affected APIs

- `M:System.Text.Json.JsonSerializer.Serialize(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`
- `M:System.Text.Json.JsonSerializer.Serialize(System.Text.Json.Utf8JsonWriter,System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`
- `M:System.Text.Json.JsonSerializer.SerializeAsync(System.IO.Stream,System.Object,System.Type,System.Text.Json.JsonSerializerOptions,System.Threading.CancellationToken)`
- `M:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes(System.Object,System.Type,System.Text.Json.JsonSerializerOptions)`

### Category

Serialization

-->
