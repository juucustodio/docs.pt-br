---
title: 'Alteração significativa: as opções PropertyNamingPolicy, PropertyNameCaseInsensitive e Encoder são respeitadas para pares de chave-valor'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que as opções PropertyNamingPolicy, PropertyNameCaseInsensitive e Encoder são respeitadas ao serializar e desserializar os nomes de propriedade de chave e valor de uma instância de par chave-valor.
ms.date: 10/18/2020
ms.openlocfilehash: 5d75cb7feea32cc4b942e5261c5b609e00a5082c
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760502"
---
# <a name="propertynamingpolicy-propertynamecaseinsensitive-and-encoder-options-are-honored-when-serializing-and-deserializing-key-value-pairs"></a>As opções PropertyNamingPolicy, PropertyNameCaseInsensitive e Encoder são respeitadas ao serializar e desserializar pares chave-valor

<xref:System.Text.Json.JsonSerializer> Agora respeita as <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy> Opções e <xref:System.Text.Json.JsonSerializerOptions.Encoder> ao serializar os <xref:System.Collections.Generic.KeyValuePair%602.Key> <xref:System.Collections.Generic.KeyValuePair%602.Value> nomes de propriedade e de uma <xref:System.Collections.Generic.KeyValuePair%602> instância do. Além disso, <xref:System.Text.Json.JsonSerializer> honra as <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy> <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive> Opções e ao desserializar <xref:System.Collections.Generic.KeyValuePair%602> instâncias.

## <a name="change-description"></a>Descrição das alterações

### <a name="serialization"></a>Serialização

Nas versões do .NET Core 3. x e nas versões 4.6.0-4.7.2 do [System.Text.Jsno pacote NuGet](https://www.nuget.org/packages/System.Text.Json), as propriedades das <xref:System.Collections.Generic.KeyValuePair%602> instâncias são sempre serializadas como "chave" e "valor" exatamente, independentemente de qualquer <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> <xref:System.Text.Json.JsonSerializerOptions.Encoder?displayProperty=nameWithType> opção e. O exemplo de código a seguir mostra como as <xref:System.Collections.Generic.KeyValuePair%602.Key> <xref:System.Collections.Generic.KeyValuePair%602.Value> Propriedades e *não* são camel-case após a serialização, mesmo que a política de nomenclatura de propriedade especificada determine isso.

```csharp
var options = new JsonSerializerOptions { PropertyNamingPolicy = JsonNamingPolicy.CamelCase };
KeyValuePair<int, int> kvp = KeyValuePair.Create(1, 1);
Console.WriteLine(JsonSerializer.Serialize(kvp, options));
// Expected: {"key":1,"value":1}
// Actual: {"Key":1,"Value":1}
```

A partir do .NET 5,0, <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy> as <xref:System.Text.Json.JsonSerializerOptions.Encoder> Opções e são respeitadas ao serializar <xref:System.Collections.Generic.KeyValuePair%602> instâncias. O exemplo de código a seguir mostra como as <xref:System.Collections.Generic.KeyValuePair%602.Key> <xref:System.Collections.Generic.KeyValuePair%602.Value> Propriedades e são camel-case após a serialização, de acordo com a política de nomenclatura de propriedade especificada.

```csharp
var options = new JsonSerializerOptions { PropertyNamingPolicy = JsonNamingPolicy.CamelCase };
KeyValuePair<int, int> kvp = KeyValuePair.Create(1, 1);
Console.WriteLine(JsonSerializer.Serialize(kvp, options));
// {"key":1,"value":1}
```

### <a name="deserialization"></a>Desserialização

Nas versões do .NET Core 3. x e nas versões 4.7. x do [System.Text.Jsno pacote NuGet](https://www.nuget.org/packages/System.Text.Json), um <xref:System.Text.Json.JsonException> é gerado quando os nomes de propriedade JSON não são precisamente `Key` e `Value` , por exemplo, se não começam com uma letra maiúscula. A exceção é lançada mesmo que uma política de nomenclatura de propriedade especificada permita expressamente.

```csharp
var options = new JsonSerializerOptions { PropertyNamingPolicy = JsonNamingPolicy.CamelCase };
string json = @"{""key"":1,""value"":1}";
// Throws JsonException.
JsonSerializer.Deserialize<KeyValuePair<int, int>>(json, options);
```

A partir do .NET 5,0, <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy> as <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive> Opções e são respeitadas ao desserializar usando <xref:System.Text.Json.JsonSerializer> . Por exemplo, o trecho de código a seguir mostra a desserialização bem-sucedida de nomes de propriedade e letras minúsculas <xref:System.Collections.Generic.KeyValuePair%602.Key> <xref:System.Collections.Generic.KeyValuePair%602.Value> porque a política de nomenclatura de propriedade especificada permite.

```csharp
var options = new JsonSerializerOptions { PropertyNamingPolicy = JsonNamingPolicy.CamelCase };
string json = @"{""key"":1,""value"":1}";

KeyValuePair<int, int> kvp = JsonSerializer.Deserialize<KeyValuePair<int, int>>(json);
Console.WriteLine(kvp.Key); // 1
Console.WriteLine(kvp.Value); // 1
```

Para acomodar as cargas que foram serializadas com versões anteriores, "chave" e "valor" são especiais para corresponder ao desserializar. Embora os <xref:System.Collections.Generic.KeyValuePair%602.Key> nomes de <xref:System.Collections.Generic.KeyValuePair%602.Value> propriedade e não sejam camel-case de acordo com a <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy> opção in no exemplo de código a seguir, eles são desserializados com êxito.

```csharp
var options = new JsonSerializerOptions { PropertyNamingPolicy = JsonNamingPolicy.CamelCase };
string json = @"{""Key"":1,""Value"":1}";

KeyValuePair<int, int> kvp = JsonSerializer.Deserialize<KeyValuePair<int, int>>(json);
Console.WriteLine(kvp.Key); // 1
Console.WriteLine(kvp.Value); // 1
```

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="reason-for-change"></a>Motivo da alteração

Comentários de clientes substanciais indicaram que o <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy> deve ser respeitado. Para fins de integridade, <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive> as <xref:System.Text.Json.JsonSerializerOptions.Encoder> Opções e também são respeitadas, para que as <xref:System.Collections.Generic.KeyValuePair%602> instâncias sejam tratadas da mesma forma que qualquer outro objeto CLR antigo (POCO).

## <a name="recommended-action"></a>Ação recomendada

Se essa alteração for prejudicial para você, você poderá usar um [conversor personalizado](../../../../standard/serialization/system-text-json-converters-how-to.md) que implementa a semântica desejada.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes%2A?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.SerializeAsync%2A?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A?displayProperty=fullName>

<!--

### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Serialize`
- `Overload:System.Text.Json.JsonSerializer.SerializeAsync`
- `Overload:System.Text.Json.JsonSerializer.SerializeToUtf8Bytes`
- `Overload:System.Text.Json.JsonSerializer.Deserialize`
- `Overload:System.Text.Json.JsonSerializer.DeserializeAsync`

### Category

Serialization

-->
