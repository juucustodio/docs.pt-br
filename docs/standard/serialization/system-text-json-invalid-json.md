---
title: Como permitir alguns tipos de JSON inválido com System.Text.Json
description: Saiba como permitir comentários, vírgulas à direita e números entre aspas ao serializar e desserializar de JSON no .NET.
ms.date: 12/03/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 2559b081010fb0a2fa208b121cb095efdeb8da2e
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009802"
---
# <a name="how-to-allow-some-kinds-of-invalid-json-with-no-locsystemtextjson"></a>Como permitir alguns tipos de JSON inválido com System.Text.Json

Neste artigo, você aprenderá como permitir comentários, vírgulas à direita e números entre aspas em JSON e como escrever números como cadeias de caracteres.

## <a name="allow-comments-and-trailing-commas"></a>Permitir comentários e vírgulas à direita

Por padrão, comentários e vírgulas à direita não são permitidos em JSON. Para permitir comentários no JSON, defina a <xref:System.Text.Json.JsonSerializerOptions.ReadCommentHandling?displayProperty=nameWithType> propriedade como `JsonCommentHandling.Skip` .
E para permitir vírgulas à direita, defina a <xref:System.Text.Json.JsonSerializerOptions.AllowTrailingCommas?displayProperty=nameWithType> propriedade como `true` . O exemplo a seguir mostra como permitir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeCommasComments.cs" id="Deserialize":::

Aqui está um exemplo de JSON com comentários e uma vírgula à direita:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25, // Fahrenheit 77
  "Summary": "Hot", /* Zharko */
  // Comments on
  /* separate lines */
}
```

## <a name="allow-or-write-numbers-in-quotes"></a>Permitir ou gravar números entre aspas

::: zone pivot="dotnet-5-0"

Alguns serializadores codificam números como cadeias de caracteres JSON (entre aspas).

Por exemplo:

```json
{
    "DegreesCelsius": "23"
}
```

Em vez de:

```json
{
    "DegreesCelsius": 23
}
```

Para serializar números entre aspas ou aceitar números entre aspas em todo o grafo de objeto de entrada, defina <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A?displayProperty=nameWithType> conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/QuotedNumbers.cs" highlight="27-29":::

Quando você usa `System.Text.Json` indiretamente por meio de ASP.NET Core, são permitidos números entre aspas ao desserializar porque ASP.NET Core especifica [opções padrão da Web](xref:System.Text.Json.JsonSerializerDefaults.Web).

Para permitir ou gravar números entre aspas para propriedades, campos ou tipos específicos, use o atributo [[JsonNumberHandling]](xref:System.Text.Json.Serialization.JsonNumberHandlingAttribute) .
::: zone-end

::: zone pivot="dotnet-core-3-1"
`System.Text.Json` no .NET Core 3,1 não dá suporte à serialização ou desserialização de números entre aspas. Para obter mais informações, consulte [permitir ou gravar números entre aspas](system-text-json-migrate-from-newtonsoft-how-to.md#allow-or-write-numbers-in-quotes).
::: zone-end

## <a name="see-also"></a>Confira também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Como serializar e desserializar JSON](system-text-json-how-to.md)
* [Instanciar instâncias JsonSerializerOptions](system-text-json-configure-options.md)
* [Habilitar a correspondência sem diferenciação de maiúsculas e minúsculas](system-text-json-character-casing.md)
* [Personalizar nomes e valores da propriedade](system-text-json-customize-properties.md)
* [Ignorar propriedades](system-text-json-ignore-properties.md)
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
