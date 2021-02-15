---
title: Como serializar Propriedades de classes derivadas com System.Text.Json
description: Saiba como serializar objetos polimórficos ao serializar e desserializar de JSON no .NET.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: c0bc16c60d3bf96a380bc29bbf7f4765f752b320
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97008741"
---
# <a name="how-to-serialize-properties-of-derived-classes-with-no-locsystemtextjson"></a>Como serializar Propriedades de classes derivadas com System.Text.Json

Neste artigo, você aprenderá a serializar Propriedades de classes derivadas com o `System.Text.Json` namespace.

## <a name="serialize-properties-of-derived-classes"></a>Serializar Propriedades de classes derivadas

_Não_ há suporte para a serialização de uma hierarquia de tipo polimórfico. Por exemplo, se uma propriedade for definida como uma interface ou uma classe abstrata, somente as propriedades definidas na interface ou na classe abstrata serão serializadas, mesmo que o tipo de tempo de execução tenha propriedades adicionais. As exceções a esse comportamento são explicadas nesta seção.

Por exemplo, suponha que você tenha uma `WeatherForecast` classe e uma classe derivada `WeatherForecastDerived` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFDerived":::

E suponha que o argumento de tipo do `Serialize` método em tempo de compilação seja `WeatherForecast` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeDefault":::

Nesse cenário, a `WindSpeed` propriedade não é serializada, mesmo que o `weatherForecast` objeto seja, na verdade, um `WeatherForecastDerived` objeto. Somente as propriedades da classe base são serializadas:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

Esse comportamento destina-se a ajudar a evitar a exposição acidental de dados em um tipo criado de tempo de execução derivado.

Para serializar as propriedades do tipo derivado no exemplo anterior, use uma das seguintes abordagens:

* Chame uma sobrecarga de <xref:System.Text.Json.JsonSerializer.Serialize%2A> que permite especificar o tipo em tempo de execução:

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeGetType":::

* Declare o objeto a ser serializado como `object` .

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeObject":::

No cenário de exemplo anterior, ambas as abordagens fazem com que a `WindSpeed` propriedade seja incluída na saída JSON:

```json
{
  "WindSpeed": 35,
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

> [!IMPORTANT]
> Essas abordagens fornecem serialização polimórfica somente para o objeto raiz a ser serializado, não para propriedades desse objeto raiz.

Você pode obter a serialização polimórfica para objetos de nível inferior se defini-los como tipo `object` . Por exemplo, suponha que sua `WeatherForecast` classe tenha uma propriedade chamada `PreviousForecast` que possa ser definida como tipo `WeatherForecast` ou `object` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPrevious":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithPreviousAsObject":::

Se a `PreviousForecast` Propriedade contiver uma instância de `WeatherForecastDerived` :

* A saída JSON da serialização `WeatherForecastWithPrevious` **não inclui** `WindSpeed` .
* A saída JSON da serialização `WeatherForecastWithPreviousAsObject` **inclui** `WindSpeed` .

Para serializar `WeatherForecastWithPreviousAsObject` , não é necessário chamar `Serialize<object>` ou `GetType` porque o objeto raiz não é aquele que pode ser de um tipo derivado. O exemplo de código a seguir não chama `Serialize<object>` ou `GetType` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeSecondLevel":::

O código anterior serializa corretamente `WeatherForecastWithPreviousAsObject` :

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "PreviousForecast": {
    "WindSpeed": 35,
    "Date": "2019-08-01T00:00:00-07:00",
    "TemperatureCelsius": 25,
    "Summary": "Hot"
  }
}
```

A mesma abordagem de definir propriedades como `object` funciona com interfaces. Suponha que você tenha a seguinte interface e implementação e queira serializar uma classe com propriedades que contêm instâncias de implementação:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/IForecast.cs":::

Quando você serializa uma instância do `Forecasts` , `Tuesday` o mostra apenas a `WindSpeed` propriedade, porque `Tuesday` é definido como `object` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializePolymorphic.cs" id="SerializeInterface":::

O exemplo a seguir mostra o JSON que resulta do código anterior:

```json
{
  "Monday": {
    "Date": "2020-01-06T00:00:00-08:00",
    "TemperatureCelsius": 10,
    "Summary": "Cool"
  },
  "Tuesday": {
    "Date": "2020-01-07T00:00:00-08:00",
    "TemperatureCelsius": 11,
    "Summary": "Rainy",
    "WindSpeed": 10
  }
}
```

Para obter mais informações sobre a **serialização** polimórfica e informações sobre a **desserialização**, consulte [como migrar do Newtonsoft.Json para System.Text.Json o](system-text-json-migrate-from-newtonsoft-how-to.md#polymorphic-serialization).

## <a name="see-also"></a>Confira também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Como serializar e desserializar JSON](system-text-json-how-to.md)
* [Instanciar instâncias JsonSerializerOptions](system-text-json-configure-options.md)
* [Habilitar a correspondência sem diferenciação de maiúsculas e minúsculas](system-text-json-character-casing.md)
* [Personalizar nomes e valores da propriedade](system-text-json-customize-properties.md)
* [Ignorar propriedades](system-text-json-ignore-properties.md)
* [Permitir JSON inválido](system-text-json-invalid-json.md)
* [Manipular JSON de estouro](system-text-json-handle-overflow.md)
* [Preservar referências](system-text-json-preserve-references.md)
* [Tipos imutáveis e acessadores não públicos](system-text-json-immutability.md)
* [Migrar do Newtonsoft.Json para o System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Personalizar codificação de caracteres](system-text-json-character-encoding.md)
* [Escrever serializadores personalizados e desserializadores](write-custom-serializer-deserializer.md)
* [Gravar conversores personalizados para serialização JSON](system-text-json-converters-how-to.md)
* [Suporte a DateTime e DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
* [System.Text.Json. Referência de API de serialização](xref:System.Text.Json.Serialization)
