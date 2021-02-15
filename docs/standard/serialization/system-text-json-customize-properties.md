---
title: Como personalizar nomes de propriedade e valores com System.Text.Json
description: Saiba como personalizar nomes de propriedade e valores ao serializar com o System.Text.Json no .net.
ms.date: 02/01/2021
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: f38511838fee299880ba7ca50c071aa790a031cd
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100438171"
---
# <a name="how-to-customize-property-names-and-values-with-systemtextjson"></a>Como personalizar nomes de propriedade e valores com System.Text.Json

Por padrão, os nomes de propriedade e as chaves de dicionário são inalterados na saída JSON, incluindo maiúsculas e minúsculas. Os valores de enumeração são representados como números. Neste artigo, você aprenderá a:

> [!NOTE]
> O [padrão da Web](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) é o camel case.

* [Personalizar nomes de propriedade individuais](#customize-individual-property-names)
* [Converter todos os nomes de propriedade em camel case](#use-camel-case-for-all-json-property-names)
* [Implementar uma política de nomenclatura de propriedade personalizada](#use-a-custom-json-property-naming-policy)
* [Converter chaves de dicionário em camel case](#camel-case-dictionary-keys)
* [Converter enums em cadeias de caracteres e camel case](#enums-as-strings)

Para outros cenários que exigem tratamento especial de valores e nomes de propriedade JSON, você pode [implementar conversores personalizados](system-text-json-converters-how-to.md).

## <a name="customize-individual-property-names"></a>Personalizar nomes de propriedade individuais

Para definir o nome de propriedades individuais, use o atributo [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) .

Veja um exemplo de tipo para serializar e o JSON resultante:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "Wind": 35
}
```

O nome da propriedade definido por este atributo:

* Aplica-se em ambas as direções, para serialização e desserialização.
* Tem precedência sobre as políticas de nomenclatura de propriedade.
* [Não afeta a correspondência de nome de parâmetro para construtores com parâmetros](system-text-json-immutability.md#immutable-types-and-records).

## <a name="use-camel-case-for-all-json-property-names"></a>Usar o camel case para todos os nomes de propriedade JSON

Para usar o camel case para todos os nomes de propriedade JSON, defina como <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> `JsonNamingPolicy.CamelCase` , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundTripCamelCasePropertyNames.cs" id="Serialize":::

Aqui está uma classe de exemplo para serializar e a saída JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "summary": "Hot",
  "Wind": 35
}
```

A política de nomenclatura de Propriedade do camel case:

* Aplica-se à serialização e desserialização.
* É substituído por `[JsonPropertyName]` atributos. É por isso que o nome da propriedade JSON `Wind` no exemplo não é camel case.

## <a name="use-a-custom-json-property-naming-policy"></a>Usar uma política de nomenclatura de propriedade JSON personalizada

Para usar uma política de nomenclatura de propriedade JSON personalizada, crie uma classe derivada de <xref:System.Text.Json.JsonNamingPolicy> e substitua o <xref:System.Text.Json.JsonNamingPolicy.ConvertName%2A> método, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/UpperCaseNamingPolicy.cs":::

Em seguida, defina a <xref:System.Text.Json.JsonSerializerOptions.PropertyNamingPolicy?displayProperty=nameWithType> propriedade como uma instância da sua classe de política de nomenclatura:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripPropertyNamingPolicy.cs" id="Serialize":::

Aqui está uma classe de exemplo para serializar e a saída JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPropertyNameAttribute":::

```json
{
  "DATE": "2019-08-01T00:00:00-07:00",
  "TEMPERATURECELSIUS": 25,
  "SUMMARY": "Hot",
  "Wind": 35
}
```

A política de nomenclatura de propriedade JSON:

* Aplica-se à serialização e desserialização.
* É substituído por `[JsonPropertyName]` atributos. É por isso que o nome da propriedade JSON `Wind` no exemplo não é maiúscula.

## <a name="camel-case-dictionary-keys"></a>Chaves de dicionário do camel case

Se uma propriedade de um objeto a ser serializado for do tipo `Dictionary<string,TValue>` , as `string` chaves poderão ser convertidas em camel case. Para fazer isso, defina <xref:System.Text.Json.JsonSerializerOptions.DictionaryKeyPolicy> como `JsonNamingPolicy.CamelCase` , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCamelCaseDictionaryKeys.cs" id="Serialize":::

Serializar um objeto com um dicionário chamado `TemperatureRanges` que tem pares chave-valor `"ColdMinTemp", 20` e `"HotMinTemp", 40` resultaria em uma saída JSON como o exemplo a seguir:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "coldMinTemp": 20,
    "hotMinTemp": 40
  }
}
```

A política de nomenclatura do camel case para chaves de dicionário se aplica somente à serialização. Se você desserializar um dicionário, as chaves corresponderão ao arquivo JSON mesmo que você especifique `JsonNamingPolicy.CamelCase` para o `DictionaryKeyPolicy` .

## <a name="enums-as-strings"></a>Enumerações como cadeias de caracteres

Por padrão, as enumerações são serializadas como números. Para serializar nomes de enumeração como cadeias de caracteres, use o <xref:System.Text.Json.Serialization.JsonStringEnumConverter> .

Por exemplo, suponha que você precise serializar a seguinte classe que tem uma enumeração:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithEnum":::

Se o resumo for `Hot` , por padrão, o JSON serializado terá o valor numérico 3:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": 3
}
```

O código de exemplo a seguir serializa os nomes de enumeração em vez dos valores numéricos e converte os nomes em camel case:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs" id="Serialize":::

O JSON resultante é semelhante ao exemplo a seguir:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "hot"
}
```

Os nomes de cadeias de caracteres de enumeração também podem ser desserializados, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripEnumAsString.cs" id="Deserialize":::

## <a name="see-also"></a>Consulte também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Como serializar e desserializar JSON](system-text-json-how-to.md)
* [Instanciar instâncias JsonSerializerOptions](system-text-json-configure-options.md)
* [Habilitar a correspondência sem diferenciação de maiúsculas e minúsculas](system-text-json-character-casing.md)
* [Ignorar propriedades](system-text-json-ignore-properties.md)
* [Permitir JSON inválido](system-text-json-invalid-json.md)
* [Manipular JSON de estouro](system-text-json-handle-overflow.md)
* [Preservar referências](system-text-json-preserve-references.md)
* [Tipos imutáveis e acessadores não públicos](system-text-json-immutability.md)
* [Serialização polimórfica](system-text-json-polymorphism.md)
* [Migrar do Newtonsoft.Json para o System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Personalizar codificação de caracteres](system-text-json-character-encoding.md)
* [Escrever serializadores personalizados e desserializadores](write-custom-serializer-deserializer.md)
* [Gravar conversores personalizados para serialização JSON](system-text-json-converters-how-to.md)
* [Suporte a DateTime e DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
* [System.Text.Json. Referência de API de serialização](xref:System.Text.Json.Serialization)
