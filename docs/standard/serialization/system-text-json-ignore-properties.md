---
title: Como ignorar Propriedades com System.Text.Json
description: Saiba como ignorar Propriedades ao serializar com o System.Text.Json no .net.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 6d703156d50a3e00a33cea5e15be2df911ed7c1b
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008806"
---
# <a name="how-to-ignore-properties-with-no-locsystemtextjson"></a>Como ignorar Propriedades com System.Text.Json

Ao serializar objetos C# para JavaScript Object Notation (JSON), por padrão, todas as propriedades públicas são serializadas. Se não quiser que algumas delas apareçam no JSON resultante, você terá várias opções. Neste artigo, você aprenderá a ignorar Propriedades com base em vários critérios:

::: zone pivot="dotnet-5-0"

* [Propriedades individuais](#ignore-individual-properties)
* [Todas as propriedades somente leitura](#ignore-all-read-only-properties)
* [Todas as propriedades de valor nulo](#ignore-all-null-value-properties)
* [Todas as propriedades de valor padrão](#ignore-all-default-value-properties)
::: zone-end

::: zone pivot="dotnet-core-3-1"

* [Propriedades individuais](#ignore-individual-properties)
* [Todas as propriedades somente leitura](#ignore-all-read-only-properties)
* [Todas as propriedades de valor nulo](#ignore-all-null-value-properties)
::: zone-end

## <a name="ignore-individual-properties"></a>Ignorar propriedades individuais

Para ignorar as propriedades individuais, use o atributo [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) .

Aqui está um tipo de exemplo para serializar e a saída JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithIgnoreAttribute":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
}
```

::: zone pivot="dotnet-5-0"
Você pode especificar a exclusão condicional definindo a propriedade do atributo [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) `Condition` . A <xref:System.Text.Json.Serialization.JsonIgnoreCondition> enumeração fornece as seguintes opções:

* `Always` -A propriedade é sempre ignorada. Se não `Condition` for especificado, essa opção será assumida.
* `Never` -A propriedade é sempre serializada e desserializada, independentemente das `DefaultIgnoreCondition` `IgnoreReadOnlyProperties` `IgnoreReadOnlyFields` configurações globais, e.
* `WhenWritingDefault` -A propriedade será ignorada na serialização se for um tipo de referência `null` , um tipo de valor Anulável `null` ou um tipo de valor `default` .
* `WhenWritingNull` -A propriedade será ignorada na serialização se for um tipo de referência `null` ou um tipo de valor Anulável `null` .

O exemplo a seguir ilustra o uso da Propriedade do atributo [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) `Condition` :

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/JsonIgnoreAttributeExample.cs" highlight="10,13,16":::
::: zone-end

## <a name="ignore-all-read-only-properties"></a>Ignorar todas as propriedades somente leitura

Uma propriedade será somente leitura se ela contiver um getter público, mas não um setter público. Para ignorar todas as propriedades somente leitura ao serializar, defina <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyProperties?displayProperty=nameWithType> como `true` , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeExcludeReadOnlyProperties.cs" id="Serialize":::

Aqui está um tipo de exemplo para serializar e a saída JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithROProperty":::

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

Essa opção se aplica somente à serialização. Durante a desserialização, as propriedades somente leitura são ignoradas por padrão.

::: zone pivot="dotnet-5-0"
Essa opção se aplica somente a propriedades. Para ignorar campos somente leitura ao [serializar campos](system-text-json-how-to.md#include-fields), use a <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> configuração global.
::: zone-end

## <a name="ignore-all-null-value-properties"></a>Ignorar todas as propriedades de valor nulo

::: zone pivot="dotnet-5-0"
Para ignorar todas as propriedades de valor nulo, defina a <xref:System.Text.Json.JsonSerializerOptions.DefaultIgnoreCondition> propriedade como <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingNull> , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/IgnoreNullOnSerialize.cs" highlight="28":::

::: zone-end

::: zone pivot="dotnet-core-3-1"
Para ignorar todas as propriedades de valor nulo ao serializar, defina a <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues> propriedade como `true` , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeExcludeNullValueProperties.cs" id="Serialize":::

Aqui está um objeto de exemplo para serializar e a saída JSON:

| Propriedade             | Valor                         |
|----------------------|-------------------------------|
| `Date`               | `8/1/2019 12:00:00 AM -07:00` |
| `TemperatureCelsius` | `25`                          |
| `Summary`            | `null`                        |

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25
}
```

::: zone-end

## <a name="ignore-all-default-value-properties"></a>Ignorar todas as propriedades de valor padrão

::: zone pivot="dotnet-5-0"
Para evitar a serialização de valores padrão em Propriedades de tipo de valor, defina a <xref:System.Text.Json.JsonSerializerOptions.DefaultIgnoreCondition> propriedade como <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingDefault> , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/IgnoreValueDefaultOnSerialize.cs" highlight="28":::
::: zone-end

A <xref:System.Text.Json.Serialization.JsonIgnoreCondition.WhenWritingDefault> configuração também impede a serialização de tipo de referência de valor nulo e propriedades de tipo de valor anulável.

::: zone pivot="dotnet-core-3-1"
Não há uma maneira interna de impedir a serialização de propriedades com padrões de tipo de valor no `System.Text.Json` .NET Core 3,1.
::: zone-end

## <a name="see-also"></a>Confira também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Como serializar e desserializar JSON](system-text-json-how-to.md)
* [Instanciar instâncias JsonSerializerOptions](system-text-json-configure-options.md)
* [Habilitar a correspondência sem diferenciação de maiúsculas e minúsculas](system-text-json-character-casing.md)
* [Personalizar nomes e valores da propriedade](system-text-json-customize-properties.md)
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
