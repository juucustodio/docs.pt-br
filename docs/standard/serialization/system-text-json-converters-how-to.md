---
title: Como escrever conversores personalizados para serialização JSON-.NET
description: Saiba como criar conversores personalizados para as classes de serialização JSON que são fornecidas no System.Text.Json namespace.
ms.date: 01/22/2021
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
- converters
ms.openlocfilehash: 5406f862eeec83b619f660716e68b85f3d90b28f
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99216350"
---
# <a name="how-to-write-custom-converters-for-json-serialization-marshalling-in-net"></a>Como escrever conversores personalizados para serialização JSON (Marshalling) no .NET

Este artigo mostra como criar conversores personalizados para as classes de serialização JSON que são fornecidas no <xref:System.Text.Json> namespace. Para obter uma introdução ao `System.Text.Json` , consulte [como serializar e desserializar JSON no .net](system-text-json-how-to.md).

Um *conversor* é uma classe que converte um objeto ou um valor de e para JSON. O `System.Text.Json` namespace tem conversores internos para a maioria dos tipos primitivos que mapeiam para primitivas de JavaScript. Você pode escrever conversores personalizados:

* Para substituir o comportamento padrão de um conversor interno. Por exemplo, talvez você queira que `DateTime` os valores sejam representados pelo formato mm/dd/aaaa. Por padrão, o ISO 8601-1:2019 tem suporte, incluindo o perfil RFC 3339. Para obter mais informações, consulte [suporte a DateTime e System.Text.Json DateTimeOffset no ](../datetime/system-text-json-support.md).
* Para dar suporte a um tipo de valor personalizado. Por exemplo, um `PhoneNumber` struct.

Você também pode escrever conversores personalizados para personalizar ou estender `System.Text.Json` com funcionalidade não incluída na versão atual. Os cenários a seguir serão abordados posteriormente neste artigo:

::: zone pivot="dotnet-5-0"

* [Desserializar tipos inferidos para propriedades de objeto](#deserialize-inferred-types-to-object-properties).
* [Suporte à desserialização polimórfico](#support-polymorphic-deserialization).
* [Dar suporte à viagem de ida \<T> e volta para pilha](#support-round-trip-for-stackt).
::: zone-end

::: zone pivot="dotnet-core-3-1"

* [Desserializar tipos inferidos para propriedades de objeto](#deserialize-inferred-types-to-object-properties).
* [Dicionário de suporte com chave não cadeia de caracteres](#support-dictionary-with-non-string-key).
* [Suporte à desserialização polimórfico](#support-polymorphic-deserialization).
* [Dar suporte à viagem de ida \<T> e volta para pilha](#support-round-trip-for-stackt).
::: zone-end

No código que você escreve para um conversor personalizado, esteja ciente da penalidade de desempenho substancial para usar novas <xref:System.Text.Json.JsonSerializerOptions> instâncias. Para obter mais informações, consulte [reutilizar instâncias de JsonSerializerOptions](system-text-json-configure-options.md#reuse-jsonserializeroptions-instances).

## <a name="custom-converter-patterns"></a>Padrões de conversor personalizado

Há dois padrões para a criação de um conversor personalizado: o padrão básico e o padrão de fábrica. O padrão de fábrica é para conversores que manipulam tipos `Enum` ou genéricos abertos. O padrão básico é para tipos genéricos não genéricos e fechados.  Por exemplo, os conversores para os seguintes tipos exigem o padrão de fábrica:

* <xref:System.Collections.Generic.Dictionary%602>
* <xref:System.Enum>
* <xref:System.Collections.Generic.List%601>

Alguns exemplos de tipos que podem ser tratados pelo padrão básico incluem:

* `Dictionary<int, string>`
* `WeekdaysEnum`
* `List<DateTimeOffset>`
* <xref:System.DateTime>
* <xref:System.Int32>

O padrão básico cria uma classe que pode manipular um tipo. O padrão de fábrica cria uma classe que determina, em tempo de execução, qual tipo específico é necessário e cria dinamicamente o conversor apropriado.

## <a name="sample-basic-converter"></a>Conversor básico de exemplo

O exemplo a seguir é um conversor que substitui a serialização padrão para um tipo de dados existente. O conversor usa o formato mm/dd/aaaa para `DateTimeOffset` Propriedades.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DateTimeOffsetConverter.cs":::

## <a name="sample-factory-pattern-converter"></a>Conversor de padrão de fábrica de exemplo

O código a seguir mostra um conversor personalizado que funciona com o `Dictionary<Enum,TValue>` . O código segue o padrão de fábrica porque o primeiro parâmetro de tipo genérico é `Enum` e o segundo é aberto. O `CanConvert` método retorna `true` apenas para um `Dictionary` com dois parâmetros genéricos, o primeiro deles é um `Enum` tipo. O conversor interno Obtém um conversor existente para lidar com qualquer tipo fornecido no tempo de execução para `TValue` .

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs":::

O código anterior é o mesmo que o mostrado no dicionário de [suporte com uma chave que não seja de cadeia de caracteres](#support-dictionary-with-non-string-key) , mais adiante neste artigo.

## <a name="steps-to-follow-the-basic-pattern"></a>Etapas para seguir o padrão básico

As etapas a seguir explicam como criar um conversor seguindo o padrão básico:

* Crie uma classe que derive de <xref:System.Text.Json.Serialization.JsonConverter%601> onde `T` é o tipo a ser serializado e desserializado.
* Substitua o `Read` método para desserializar o JSON de entrada e convertê-lo no tipo `T` . Use o <xref:System.Text.Json.Utf8JsonReader> que é passado para o método para ler o JSON. Você não precisa se preocupar em lidar com dados parciais, pois o serializador passa todos os dados para o escopo JSON atual. Portanto, não é necessário chamar <xref:System.Text.Json.Utf8JsonReader.Skip%2A> ou <xref:System.Text.Json.Utf8JsonReader.TrySkip%2A> ou para validar que <xref:System.Text.Json.Utf8JsonReader.Read%2A> retorna `true` .
* Substitua o `Write` método para serializar o objeto de entrada do tipo `T` . Use o <xref:System.Text.Json.Utf8JsonWriter> que é passado para o método para gravar o JSON.
* Substitua o `CanConvert` método somente se necessário. A implementação padrão retorna `true` quando o tipo a ser convertido é do tipo `T` . Portanto, os conversores que suportam apenas `T` o tipo não precisam substituir esse método. Para obter um exemplo de um conversor que precisa substituir esse método, consulte a seção [desserialização polimórfica](#support-polymorphic-deserialization) mais adiante neste artigo.

Você pode consultar o [código-fonte dos conversores internos](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/) como implementações de referência para escrever conversores personalizados.

## <a name="steps-to-follow-the-factory-pattern"></a>Etapas para seguir o padrão de fábrica

As etapas a seguir explicam como criar um conversor seguindo o padrão de fábrica:

* Crie uma classe que deriva de <xref:System.Text.Json.Serialization.JsonConverterFactory>.
* Substitua o `CanConvert` método para retornar true quando o tipo a ser convertido for aquele que o conversor pode manipular. Por exemplo, se o conversor for para `List<T>` ele, ele só poderá manipular `List<int>` , `List<string>` e `List<DateTime>` .
* Substitua o `CreateConverter` método para retornar uma instância de uma classe de conversor que manipulará o tipo a ser convertido que é fornecido no tempo de execução.
* Crie a classe de conversor `CreateConverter` instanciada pelo método.

O padrão de fábrica é necessário para os genéricos abertos porque o código para converter um objeto de e para uma cadeia de caracteres não é o mesmo para todos os tipos. Um conversor para um tipo genérico aberto ( `List<T>` , por exemplo) precisa criar um conversor para um tipo genérico fechado ( `List<DateTime>` , por exemplo) em segundo plano. O código deve ser gravado para lidar com cada tipo fechado genérico que o conversor pode manipular.

O `Enum` tipo é semelhante a um tipo genérico aberto: um conversor de `Enum` deve criar um conversor para um específico `Enum` ( `WeekdaysEnum` , por exemplo) em segundo plano.

## <a name="error-handling"></a>Tratamento de erros

O serializador Fornece tratamento especial para tipos de exceção <xref:System.Text.Json.JsonException> e <xref:System.NotSupportedException> .

### <a name="jsonexception"></a>Jsonexception

Se você lançar um `JsonException` sem uma mensagem, o serializador criará uma mensagem que inclui o caminho para a parte do JSON que causou o erro. Por exemplo, a instrução `throw new JsonException()` produz uma mensagem de erro semelhante ao exemplo a seguir:

```output
Unhandled exception. System.Text.Json.JsonException:
The JSON value could not be converted to System.Object.
Path: $.Date | LineNumber: 1 | BytePositionInLine: 37.
```

Se você fornecer uma mensagem (por exemplo, `throw new JsonException("Error occurred")` o serializador ainda definirá as <xref:System.Text.Json.JsonException.Path> <xref:System.Text.Json.JsonException.LineNumber> Propriedades, e <xref:System.Text.Json.JsonException.BytePositionInLine> .

### <a name="notsupportedexception"></a>NotSupportedException

Se você lançar um `NotSupportedException` , sempre obterá as informações de caminho na mensagem. Se você fornecer uma mensagem, as informações de caminho serão acrescentadas a ela. Por exemplo, a instrução `throw new NotSupportedException("Error occurred.")` produz uma mensagem de erro semelhante ao exemplo a seguir:

```output
Error occurred. The unsupported member type is located on type
'System.Collections.Generic.Dictionary`2[Samples.SummaryWords,System.Int32]'.
Path: $.TemperatureRanges | LineNumber: 4 | BytePositionInLine: 24
```

### <a name="when-to-throw-which-exception-type"></a>Quando lançar qual tipo de exceção

Quando a carga JSON contém tokens que não são válidos para o tipo que está sendo desserializado, lança um `JsonException` .

Quando você quiser não permitir certos tipos, acione um `NotSupportedException` . Essa exceção é o que o serializador gera automaticamente para tipos que não têm suporte. Por exemplo, `System.Type` o não tem suporte por motivos de segurança, portanto, uma tentativa de desserializar isso resulta em um `NotSupportedException` .

Você pode gerar outras exceções conforme necessário, mas elas não incluem automaticamente informações de caminho JSON.

## <a name="register-a-custom-converter"></a>Registrar um conversor personalizado

*Registre* um conversor personalizado para fazer com `Serialize` que os métodos e o `Deserialize` usem. Escolha uma das seguintes abordagens:

* Adicione uma instância da classe converter à <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> coleção.
* Aplique o atributo [[jsonconverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) às propriedades que exigem o conversor personalizado.
* Aplique o atributo [[jsonconverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute) a uma classe ou a uma struct que represente um tipo de valor personalizado.

## <a name="registration-sample---converters-collection"></a>Amostra de registro – coleção de conversores

Veja um exemplo que torna o <xref:System.ComponentModel.DateTimeOffsetConverter> padrão para propriedades do tipo <xref:System.DateTimeOffset> :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs" id="Serialize":::

Suponha que você Serialize uma instância do seguinte tipo:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

Aqui está um exemplo de saída JSON que mostra que o conversor personalizado foi usado:

```json
{
  "Date": "08/01/2019",
  "TemperatureCelsius": 25,
  "Summary": "Hot"
}
```

O código a seguir usa a mesma abordagem para desserializar usando o `DateTimeOffset` conversor personalizado:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithConvertersCollection.cs" id="Deserialize":::

## <a name="registration-sample---jsonconverter-on-a-property"></a>Exemplo de registro-[Jsonconverter] em uma propriedade

O código a seguir seleciona um conversor personalizado para a `Date` Propriedade:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithConverterAttribute":::

O código a ser serializado `WeatherForecastWithConverterAttribute` não exige o uso de `JsonSerializeOptions.Converters` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs" id="Serialize":::

O código para desserializar também não exige o uso de `Converters` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RegisterConverterWithAttributeOnProperty.cs" id="Deserialize":::

## <a name="registration-sample---jsonconverter-on-a-type"></a>Exemplo de registro-[Jsonconverter] em um tipo

Aqui está o código que cria uma struct e aplica o `[JsonConverter]` atributo a ela:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Temperature.cs":::

Este é o conversor personalizado para o struct anterior:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/TemperatureConverter.cs":::

O `[JsonConvert]` atributo na estrutura registra o conversor personalizado como o padrão para propriedades do tipo `Temperature` . O conversor é usado automaticamente na `TemperatureCelsius` Propriedade do seguinte tipo ao serializar ou desserializar:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithTemperatureStruct":::

## <a name="converter-registration-precedence"></a>Precedência de registro do conversor

Durante a serialização ou desserialização, um conversor é escolhido para cada elemento JSON na seguinte ordem, listada da prioridade mais alta para a mais baixa:

* `[JsonConverter]` aplicado a uma propriedade.
* Um conversor adicionado à `Converters` coleção.
* `[JsonConverter]` aplicado a um tipo de valor personalizado ou POCO.

Se vários conversores personalizados para um tipo forem registrados na `Converters` coleção, o primeiro conversor que retorna true para `CanConvert` será usado.

Um conversor interno será escolhido somente se nenhum conversor personalizado aplicável for registrado.

## <a name="converter-samples-for-common-scenarios"></a>Exemplos de conversor para cenários comuns

As seções a seguir fornecem exemplos de conversor que abordam alguns cenários comuns que a funcionalidade interna não trata.

::: zone pivot="dotnet-5-0"

* [Desserializar tipos inferidos para propriedades de objeto](#deserialize-inferred-types-to-object-properties).
* [Suporte à desserialização polimórfico](#support-polymorphic-deserialization).
* [Dar suporte à viagem de ida \<T> e volta para pilha](#support-round-trip-for-stackt).
::: zone-end

::: zone pivot="dotnet-core-3-1"

* [Desserializar tipos inferidos para propriedades de objeto](#deserialize-inferred-types-to-object-properties).
* [Dicionário de suporte com chave não cadeia de caracteres](#support-dictionary-with-non-string-key).
* [Suporte à desserialização polimórfico](#support-polymorphic-deserialization).
* [Dar suporte à viagem de ida \<T> e volta para pilha](#support-round-trip-for-stackt).
::: zone-end

### <a name="deserialize-inferred-types-to-object-properties"></a>Desserializar tipos inferidos para propriedades de objeto

Ao desserializar para uma propriedade do tipo `object` , um `JsonElement` objeto é criado. O motivo é que o desserializador não sabe qual tipo de CLR deve ser criado e não tenta adivinhar. Por exemplo, se uma propriedade JSON tiver "true", o desserializador não inferirá que o valor é a `Boolean` e, se um elemento tiver "01/01/2019", o desserializador não inferirá que é um `DateTime` .

A inferência de tipos pode ser imprecisa. Se o desserializador analisar um número JSON que não tenha nenhum ponto decimal como um `long` , isso poderá resultar em problemas fora do intervalo se o valor tiver sido originalmente serializado como um `ulong` ou `BigInteger` . A análise de um número que tenha um ponto decimal como `double` pode perder a precisão se o número tiver sido originalmente serializado como um `decimal` .

Para cenários que exigem a inferência de tipos, o código a seguir mostra um conversor personalizado para `object` Propriedades. O código converte:

* `true` e `false` para `Boolean`
* Números sem um decimal para `long`
* Números com um decimal para `double`
* Datas para `DateTime`
* Cadeias de caracteres para `string`
* Tudo o mais a `JsonElement`

::: zone pivot="dotnet-5-0"

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CustomConverterInferredTypesToObject.cs":::

O exemplo mostra o código do conversor e uma `WeatherForecast` classe com `object` Propriedades. O `Main` método desserializa uma cadeia de caracteres JSON em uma `WeatherForecast` instância, primeiro sem usar o conversor e, em seguida, usando o conversor. A saída do console mostra que, sem o conversor, o tipo de tempo de execução da `Date` propriedade é `JsonElement` ; com o conversor, o tipo de tempo de execução é `DateTime` .

A [pasta de testes de unidade](https://github.com/dotnet/runtime/tree/c72b54243ade2e1118ab24476220a2eba6057466/src/libraries/System.Text.Json/tests/Serialization/) no `System.Text.Json.Serialization` namespace tem mais exemplos de conversores personalizados que manipulam a desserialização para `object` Propriedades.

:::zone-end

::: zone pivot="dotnet-core-3-1"

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/ObjectToInferredTypesConverter.cs":::

O código a seguir registra o conversor:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DeserializeInferredTypesToObject.cs" id="Register":::

Aqui está um tipo de exemplo com `object` Propriedades:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithObjectProperties":::

O exemplo a seguir de JSON para desserializar contém valores que serão desserializados como `DateTime` , `long` e `string` :

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
}
```

Sem o conversor personalizado, a desserialização coloca um `JsonElement` em cada propriedade.

A [pasta de testes de unidade](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) no `System.Text.Json.Serialization` namespace tem mais exemplos de conversores personalizados que manipulam a desserialização para `object` Propriedades.

:::zone-end

::: zone pivot="dotnet-core-3-1"

### <a name="support-dictionary-with-non-string-key"></a>Dicionário de suporte com chave não cadeia de caracteres

O suporte interno para coleções de dicionário é para o `Dictionary<string, TValue>` . Ou seja, a chave deve ser uma cadeia de caracteres. Para dar suporte a um dicionário com um inteiro ou algum outro tipo como a chave, um conversor personalizado é necessário.

O código a seguir mostra um conversor personalizado que funciona com `Dictionary<Enum,TValue>` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DictionaryTKeyEnumTValueConverter.cs":::

O código a seguir registra o conversor:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripDictionaryTkeyEnumTValue.cs" id="Register":::

O conversor pode serializar e desserializar a `TemperatureRanges` propriedade da seguinte classe que usa o seguinte `Enum` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithEnumDictionary":::

A saída JSON da serialização é semelhante ao exemplo a seguir:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "Hot",
  "TemperatureRanges": {
    "Cold": 20,
    "Hot": 40
  }
}
```

A [pasta de testes de unidade](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) no `System.Text.Json.Serialization` namespace tem mais exemplos de conversores personalizados que manipulam dicionários que não são de chave de cadeia de caracteres.
::: zone-end

### <a name="support-polymorphic-deserialization"></a>Suporte à desserialização polimórfico

Os recursos internos fornecem um intervalo limitado de [serialização polimórfico](system-text-json-polymorphism.md) , mas não há suporte para desserialização. A desserialização requer um conversor personalizado.

Suponha, por exemplo, que você tenha uma `Person` classe base abstrata, `Employee` com `Customer` classes derivadas e. A desserialização polimórfica significa que, em tempo de design, você pode especificar `Person` como o destino de desserialização e `Customer` `Employee` os objetos no JSON são corretamente desserializados em tempo de execução. Durante a desserialização, você precisa encontrar pistas que identificam o tipo necessário no JSON. Os tipos de pistas disponíveis variam de acordo com cada cenário. Por exemplo, uma propriedade discriminadora pode estar disponível ou talvez você precise contar com a presença ou a ausência de uma determinada propriedade. A versão atual do `System.Text.Json` não fornece atributos para especificar como lidar com cenários de desserialização polimórfico, para que conversores personalizados sejam necessários.

O código a seguir mostra uma classe base, duas classes derivadas e um conversor personalizado para elas. O conversor usa uma propriedade discriminadora para fazer desserialização polimórfica. O discriminador de tipo não está nas definições de classe, mas é criado durante a serialização e é lido durante a desserialização.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Person.cs" id="Person":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/PersonConverterWithTypeDiscriminator.cs":::

O código a seguir registra o conversor:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripPolymorphic.cs" id="Register":::

O conversor pode desserializar o JSON criado usando o mesmo conversor para serializar, por exemplo:

```json
[
  {
    "TypeDiscriminator": 1,
    "CreditLimit": 10000,
    "Name": "John"
  },
  {
    "TypeDiscriminator": 2,
    "OfficeNumber": "555-1234",
    "Name": "Nancy"
  }
]
```

O código do conversor no exemplo anterior lê e grava cada propriedade manualmente. Uma alternativa é chamar `Deserialize` ou `Serialize` fazer parte do trabalho. Para obter um exemplo, consulte [esta postagem de StackOverflow](https://stackoverflow.com/a/59744873/12509023).

### <a name="support-round-trip-for-stackt"></a>Dar suporte à viagem de ida e volta para a pilha\<T>

Se você desserializar uma cadeia de caracteres JSON em um <xref:System.Collections.Generic.Stack%601> objeto e, em seguida, serializar esse objeto, o conteúdo da pilha estará na ordem inversa. Esse comportamento se aplica aos tipos e à interface a seguir e aos tipos definidos pelo usuário que derivam deles:

* <xref:System.Collections.Stack>
* <xref:System.Collections.Generic.Stack%601>
* <xref:System.Collections.Concurrent.ConcurrentStack%601>
* <xref:System.Collections.Immutable.ImmutableStack%601>
* <xref:System.Collections.Immutable.IImmutableStack%601>

Para dar suporte à serialização e desserialização que retém o pedido original na pilha, é necessário um conversor personalizado.

O código a seguir mostra um conversor personalizado que permite a passagem de ida e volta de `Stack<T>` objetos:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonConverterFactoryForStackOfT.cs":::

O código a seguir registra o conversor:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/RoundtripStackOfT.cs" id="Register":::

## <a name="handle-null-values"></a>Manipular valores nulos

Por padrão, o serializador trata valores nulos da seguinte maneira:

* Para tipos de referência e <xref:System.Nullable%601> tipos:

  * Ele não passa `null` para conversores personalizados na serialização.
  * Ele não passa `JsonTokenType.Null` para conversores personalizados na desserialização.
  * Ele retorna uma `null` instância na desserialização.
  * Ele grava `null` diretamente com o gravador na serialização.

* Para tipos de valores não anuláveis:

  * Ele passa `JsonTokenType.Null` para conversores personalizados na desserialização. (Se nenhum conversor personalizado estiver disponível, uma `JsonException` exceção será lançada pelo conversor interno para o tipo.)

Esse comportamento de tratamento nulo é principalmente para otimizar o desempenho, ignorando uma chamada extra para o conversor. Além disso, evita a força de conversores para tipos anuláveis a serem verificados `null` no início de cada `Read` e `Write` substituição de método.

::: zone pivot="dotnet-5-0"
Para habilitar um conversor personalizado para tratar `null` de uma referência ou tipo de valor, substitua <xref:System.Text.Json.Serialization.JsonConverter%601.HandleNull%2A?displayProperty=nameWithType> para retornar `true` , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CustomConverterHandleNull.cs" highlight="18":::
::: zone-end

## <a name="other-custom-converter-samples"></a>Outras amostras de conversor personalizadas

O artigo [migrar de Newtonsoft.Json para System.Text.Json ](system-text-json-migrate-from-newtonsoft-how-to.md) contém exemplos adicionais de conversores personalizados.

A [pasta de testes de unidade](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/) no `System.Text.Json.Serialization` código-fonte inclui outras amostras de conversores personalizadas, como:

* [Conversor de Int32 que converte NULL para 0 em desserializar](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.NullValueType.cs)
* [Conversor de Int32 que permite valores de cadeia de caracteres e de número na desserialização](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Int32.cs)
* [Conversor de enumeração](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Enum.cs)
* [\<T>Conversor de lista que aceita dados externos](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.List.cs)
* [Conversor Long [] que funciona com uma lista de números delimitada por vírgulas](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/tests/Serialization/CustomConverterTests.Array.cs)

Se você precisar criar um conversor que modifique o comportamento de um conversor interno existente, poderá obter [o código-fonte do conversor existente](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters) para servir como ponto de partida para personalização.

## <a name="additional-resources"></a>Recursos adicionais

* [Código-fonte para conversores internos](https://github.com/dotnet/runtime/tree/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters)
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
* [Serialização polimórfica](system-text-json-polymorphism.md)
* [Migrar do Newtonsoft.Json para o System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Personalizar codificação de caracteres](system-text-json-character-encoding.md)
* [Escrever serializadores personalizados e desserializadores](write-custom-serializer-deserializer.md)
* [Suporte a DateTime e DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
* [System.Text.Json. Referência de API de serialização](xref:System.Text.Json.Serialization)
