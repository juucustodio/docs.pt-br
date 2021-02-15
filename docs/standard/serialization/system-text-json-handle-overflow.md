---
title: Como lidar com o JSON de estouro com System.Text.Json
description: Saiba como lidar com o JSON de estouro ao serializar e desserializar do JSON no .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 265ce4f77d353720419122d17c36e508a377b68f
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008910"
---
# <a name="how-to-handle-overflow-json-with-no-locsystemtextjson"></a>Como lidar com o JSON de estouro com System.Text.Json

Neste artigo, você aprenderá a manipular o JSON de estouro com o `System.Text.Json` namespace.

## <a name="handle-overflow-json"></a>Manipular JSON de estouro

Durante a desserialização, você pode receber dados no JSON que não são representados pelas propriedades do tipo de destino. Por exemplo, suponha que o tipo de destino seja o seguinte:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

E o JSON a ser desserializado é o seguinte:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "temperatureCelsius": 25,
  "Summary": "Hot",
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

Se você desserializar o JSON mostrado no tipo mostrado, as `DatesAvailable` Propriedades e `SummaryWords` ficarão sem lugar e serão perdidas. Para capturar dados adicionais, como essas propriedades, aplique o atributo [[JsonExtensionData]](xref:System.Text.Json.Serialization.JsonExtensionDataAttribute) a uma propriedade do tipo `Dictionary<string,object>` ou `Dictionary<string,JsonElement>` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithExtensionData":::

Quando você desserializar o JSON mostrado anteriormente neste tipo de exemplo, os dados extras se tornarão pares de chave-valor da `ExtensionData` Propriedade:

| Propriedade | Valor | Observações |
|--|--|--|
| `Date` | `"8/1/2019 12:00:00 AM -07:00"` |  |
| `TemperatureCelsius` | `0` | Incompatibilidade de maiúsculas e minúsculas ( `temperatureCelsius` no JSON), portanto, a propriedade não está definida. |
| `Summary` | `"Hot"` |  |
| `ExtensionData` | `temperatureCelsius: 25` | Como o caso não corresponde, essa propriedade JSON é um extra e se torna um par chave-valor no dicionário. |
| `DatesAvailable` | `[ "8/1/2019 12:00:00 AM -07:00", "8/2/2019 12:00:00 AM -07:00" ]` | A propriedade extra do JSON torna-se um par chave-valor, com uma matriz como o objeto de valor. |
| `SummaryWords` | `[ "Cool", "Windy", "Humid" ]` | A propriedade extra do JSON torna-se um par chave-valor, com uma matriz como o objeto de valor. |

Quando o objeto de destino é serializado, os pares de valor de chave de dados de extensão se tornam propriedades JSON, assim como no JSON de entrada:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 0,
  "Summary": "Hot",
  "temperatureCelsius": 25,
  "DatesAvailable": [
    "2019-08-01T00:00:00-07:00",
    "2019-08-02T00:00:00-07:00"
  ],
  "SummaryWords": [
    "Cool",
    "Windy",
    "Humid"
  ]
}
```

Observe que o `ExtensionData` nome da propriedade não aparece no JSON. Esse comportamento permite que o JSON faça uma viagem de ida e volta sem perder nenhum dado extra que, de outra forma, não seria desserializado.

## <a name="see-also"></a>Confira também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Como serializar e desserializar JSON](system-text-json-how-to.md)
* [Instanciar instâncias JsonSerializerOptions](system-text-json-configure-options.md)
* [Habilitar a correspondência sem diferenciação de maiúsculas e minúsculas](system-text-json-character-casing.md)
* [Personalizar nomes e valores da propriedade](system-text-json-customize-properties.md)
* [Ignorar propriedades](system-text-json-ignore-properties.md)
* [Permitir JSON inválido](system-text-json-invalid-json.md)
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
