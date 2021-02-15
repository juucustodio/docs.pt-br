---
title: Migrar do Newtonsoft.Json para o System.Text.Json .net
description: Saiba como migrar do Newtonsoft.Json para o System.Text.Json . Inclui o código de exemplo.
author: tdykstra
ms.author: tdykstra
no-loc:
- System.Text.Json
- Newtonsoft.Json
ms.date: 12/14/2020
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 3c9383aed97ed3b22f8fccdd55a9fa5664edef2d
ms.sourcegitcommit: 38999dc0ec4f7c4404de5ce0951b64c55997d9ab
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/02/2021
ms.locfileid: "99426925"
---
# <a name="how-to-migrate-from-newtonsoftjson-to-systemtextjson"></a>Como migrar do Newtonsoft.Json para o System.Text.Json

Este artigo mostra como migrar do [Newtonsoft.Json](https://www.newtonsoft.com/json) para o <xref:System.Text.Json> .

O `System.Text.Json` namespace fornece a funcionalidade para serializar e desserializar de JavaScript Object Notation (JSON). A `System.Text.Json` biblioteca está incluída no tempo de execução para [.net Core 3,1](https://dotnet.microsoft.com/download/dotnet-core/3.1) e versões posteriores. Para outras estruturas de destino, instale o [System.Text.Json](https://www.nuget.org/packages/System.Text.Json) pacote NuGet. O pacote dá suporte a:

* .NET Standard 2,0 e versões posteriores
* .NET Framework 4.7.2 e versões posteriores
* .NET Core 2,0, 2,1 e 2,2

`System.Text.Json` concentra-se principalmente em desempenho, segurança e conformidade de padrões. Ele tem algumas diferenças importantes no comportamento padrão e não tem como objetivo ter paridade de recursos com o `Newtonsoft.Json` . Para alguns cenários, o `System.Text.Json` não tem funcionalidade interna, mas há soluções alternativas recomendadas. Para outros cenários, as soluções alternativas são impraticável. Se seu aplicativo depende de um recurso ausente, considere o [arquivamento de um problema](https://github.com/dotnet/runtime/issues/new) para descobrir se o suporte para seu cenário pode ser adicionado.

A maior parte deste artigo é sobre como usar a <xref:System.Text.Json.JsonSerializer> API, mas também inclui orientação sobre como usar o <xref:System.Text.Json.JsonDocument> (que representa os tipos modelo de objeto do documento ou dom), <xref:System.Text.Json.Utf8JsonReader> e <xref:System.Text.Json.Utf8JsonWriter> .

## <a name="table-of-differences-between-newtonsoftjson-and-systemtextjson"></a>Tabela de diferenças entre Newtonsoft.Json e System.Text.Json

A tabela a seguir lista os `Newtonsoft.Json` recursos e `System.Text.Json` equivalentes. Os equivalentes se enquadram nas seguintes categorias:

* Com suporte pela funcionalidade interna. Obter comportamento semelhante do `System.Text.Json` pode exigir o uso de um atributo ou uma opção global.
* Sem suporte, a solução alternativa é possível. As soluções alternativas são [conversores personalizados](system-text-json-converters-how-to.md), que podem não fornecer paridade completa com `Newtonsoft.Json` funcionalidade. Para alguns deles, o código de exemplo é fornecido como exemplos. Se você depender desses `Newtonsoft.Json` recursos, a migração exigirá modificações em seus modelos de objeto .net ou em outras alterações de código.
* Sem suporte, a solução alternativa não é prática ou possível. Se você depender desses `Newtonsoft.Json` recursos, a migração não será possível sem alterações significativas.

::: zone pivot="dotnet-5-0"
| Recurso do Newtonsoft.Json                               | System.Text.Json equivalente |
|-------------------------------------------------------|-----------------------------|
| Desserialização não diferencia maiúsculas de minúsculas por padrão           | [configuração global](#case-insensitive-deserialization) do ✔️ PropertyNameCaseInsensitive |
| Nomes de Propriedade do camel case                             | [configuração global](system-text-json-customize-properties.md#use-camel-case-for-all-json-property-names) do ✔️ PropertyNamingPolicy |
| Escape de caractere mínimo                            | ✔️ [escape de caractere estrito, configurável](#minimal-character-escaping) |
| `NullValueHandling.Ignore` configuração global             | ✔️ [opção global DefaultIgnoreCondition](system-text-json-ignore-properties.md#ignore-all-null-value-properties) |[Ignorar condicionalmente uma propriedade](#conditionally-ignore-a-property)
| Permitir comentários                                        | [configuração global](#comments) do ✔️ ReadCommentHandling |
| Permitir vírgulas à direita                                 | [configuração global](#trailing-commas) do ✔️ AllowTrailingCommas |
| Registro do conversor personalizado                         | ✔️ [ordem de precedência difere](#converter-registration-precedence) |
| Sem profundidade máxima por padrão                           | ✔️ [profundidade máxima padrão 64, configurável](#maximum-depth) |
| `PreserveReferencesHandling` configuração global           | [configuração global](#preserve-object-references-and-handle-loops) do ✔️ ReferenceHandling |
| Serializar ou desserializar números entre aspas            | ✔️ [configuração global do NumberHandling, atributo [JsonNumberHandling]](#allow-or-write-numbers-in-quotes) |
| Desserializar para classes e structs imutáveis          | ✔️ [JsonConstructor, C# 9 registros](#deserialize-to-immutable-classes-and-structs) |
| Suporte para campos                                    | ✔️ [configuração global do IncludeFields, atributo [JsonInclude]](#public-and-non-public-fields) |
| `DefaultValueHandling` configuração global                 | [configuração global](#conditionally-ignore-a-property) do ✔️ DefaultIgnoreCondition |
| `NullValueHandling` configuração em `[JsonProperty]`       | ✔️ [atributo JsonIgnore](#conditionally-ignore-a-property)  |
| `DefaultValueHandling` configuração em `[JsonProperty]`    | ✔️ [atributo JsonIgnore](#conditionally-ignore-a-property)  |
| Desserializar `Dictionary` com chave não cadeia de caracteres          | ✔️ [com suporte](#dictionary-with-non-string-key) |
| Suporte para setters e getters de propriedade não pública   | ✔️ [atributo JsonInclude](#non-public-property-setters-and-getters) |
| Atributo `[JsonConstructor]`                         | [atributo ✔️ [JsonConstructor]](#specify-constructor-to-use-when-deserializing) |
| Suporte para uma ampla variedade de tipos                    | ⚠️[Alguns tipos exigem conversores personalizados](#types-without-built-in-support) |
| Serialização polimórfica                             | ⚠️[Sem suporte, solução alternativa, exemplo](#polymorphic-serialization) |
| Desserialização polimórfica                           | ⚠️[Sem suporte, solução alternativa, exemplo](#polymorphic-deserialization) |
| Desserializar tipo inferido para `object` Propriedades      | ⚠️[Sem suporte, solução alternativa, exemplo](#deserialization-of-object-properties) |
| Desserializar `null` literal JSON para tipos de valores não anuláveis | ⚠️[Sem suporte, solução alternativa, exemplo](#deserialize-null-to-non-nullable-type) |
| `Required` Configurando no `[JsonProperty]` atributo        | ⚠️[Sem suporte, solução alternativa, exemplo](#required-properties) |
| `DefaultContractResolver` para ignorar Propriedades       | ⚠️[Sem suporte, solução alternativa, exemplo](#conditionally-ignore-a-property) |
| `DateTimeZoneHandling`, `DateFormatString` configurações   | ⚠️[Sem suporte, solução alternativa, exemplo](#specify-date-format) |
| Retornos de chamada                                             | ⚠️[Sem suporte, solução alternativa, exemplo](#callbacks) |
| Método `JsonConvert.PopulateObject`                   | ⚠️[Sem suporte, solução alternativa](#populate-existing-objects) |
| `ObjectCreationHandling` configuração global               | ⚠️[Sem suporte, solução alternativa](#reuse-rather-than-replace-properties) |
| Adicionar a coleções sem setters                    | ⚠️[Sem suporte, solução alternativa](#add-to-collections-without-setters) |
| `ReferenceLoopHandling` configuração global                | ❌ [Sem suporte](#preserve-object-references-and-handle-loops) |
| Suporte para `System.Runtime.Serialization` atributos | ❌ [Sem suporte](#systemruntimeserialization-attributes) |
| `MissingMemberHandling` configuração global                | ❌ [Sem suporte](#missingmemberhandling) |
| Permitir nomes de propriedade sem aspas                   | ❌ [Sem suporte](#json-strings-property-names-and-string-values) |
| Permitir aspas simples em vez de valores de cadeia de caracteres              | ❌ [Sem suporte](#json-strings-property-names-and-string-values) |
| Permitir valores JSON que não são de cadeia de caracteres para propriedades de cadeia de caracteres    | ❌ [Sem suporte](#non-string-values-for-string-properties) |
| `TypeNameHandling.All` configuração global                 | ❌ [Sem suporte](#typenamehandlingall-not-supported) |
::: zone-end

::: zone pivot="dotnet-core-3-1"
| Recurso do Newtonsoft.Json                               | System.Text.Json equivalente |
|-------------------------------------------------------|-----------------------------|
| Desserialização não diferencia maiúsculas de minúsculas por padrão           | [configuração global](#case-insensitive-deserialization) do ✔️ PropertyNameCaseInsensitive |
| Nomes de Propriedade do camel case                             | [configuração global](system-text-json-customize-properties.md#use-camel-case-for-all-json-property-names) do ✔️ PropertyNamingPolicy |
| Escape de caractere mínimo                            | ✔️ [escape de caractere estrito, configurável](#minimal-character-escaping) |
| `NullValueHandling.Ignore` configuração global             | ✔️ [opção global IgnoreNullValues](system-text-json-ignore-properties.md#ignore-all-null-value-properties) |
| Permitir comentários                                        | [configuração global](#comments) do ✔️ ReadCommentHandling |
| Permitir vírgulas à direita                                 | [configuração global](#trailing-commas) do ✔️ AllowTrailingCommas |
| Registro do conversor personalizado                         | ✔️ [ordem de precedência difere](#converter-registration-precedence) |
| Sem profundidade máxima por padrão                           | ✔️ [profundidade máxima padrão 64, configurável](#maximum-depth) |
| Suporte para uma ampla variedade de tipos                    | ⚠️[Alguns tipos exigem conversores personalizados](#types-without-built-in-support) |
| Desserializar cadeias de caracteres como números                        | ⚠️[Sem suporte, solução alternativa, exemplo](#allow-or-write-numbers-in-quotes) |
| Desserializar `Dictionary` com chave não cadeia de caracteres          | ⚠️[Sem suporte, solução alternativa, exemplo](#dictionary-with-non-string-key) |
| Serialização polimórfica                             | ⚠️[Sem suporte, solução alternativa, exemplo](#polymorphic-serialization) |
| Desserialização polimórfica                           | ⚠️[Sem suporte, solução alternativa, exemplo](#polymorphic-deserialization) |
| Desserializar tipo inferido para `object` Propriedades      | ⚠️[Sem suporte, solução alternativa, exemplo](#deserialization-of-object-properties) |
| Desserializar `null` literal JSON para tipos de valores não anuláveis | ⚠️[Sem suporte, solução alternativa, exemplo](#deserialize-null-to-non-nullable-type) |
| Desserializar para classes e structs imutáveis          | ⚠️[Sem suporte, solução alternativa, exemplo](#deserialize-to-immutable-classes-and-structs) |
| Atributo `[JsonConstructor]`                         | ⚠️[Sem suporte, solução alternativa, exemplo](#specify-constructor-to-use-when-deserializing) |
| `Required` Configurando no `[JsonProperty]` atributo        | ⚠️[Sem suporte, solução alternativa, exemplo](#required-properties) |
| `NullValueHandling` Configurando no `[JsonProperty]` atributo | ⚠️[Sem suporte, solução alternativa, exemplo](#conditionally-ignore-a-property)  |
| `DefaultValueHandling` Configurando no `[JsonProperty]` atributo | ⚠️[Sem suporte, solução alternativa, exemplo](#conditionally-ignore-a-property)  |
| `DefaultValueHandling` configuração global                 | ⚠️[Sem suporte, solução alternativa, exemplo](#conditionally-ignore-a-property) |
| `DefaultContractResolver` para ignorar Propriedades       | ⚠️[Sem suporte, solução alternativa, exemplo](#conditionally-ignore-a-property) |
| `DateTimeZoneHandling`, `DateFormatString` configurações   | ⚠️[Sem suporte, solução alternativa, exemplo](#specify-date-format) |
| Retornos de chamada                                             | ⚠️[Sem suporte, solução alternativa, exemplo](#callbacks) |
| Suporte para campos públicos e não públicos              | ⚠️[Sem suporte, solução alternativa](#public-and-non-public-fields) |
| Suporte para setters e getters de propriedade não pública   | ⚠️[Sem suporte, solução alternativa](#non-public-property-setters-and-getters) |
| Método `JsonConvert.PopulateObject`                   | ⚠️[Sem suporte, solução alternativa](#populate-existing-objects) |
| `ObjectCreationHandling` configuração global               | ⚠️[Sem suporte, solução alternativa](#reuse-rather-than-replace-properties) |
| Adicionar a coleções sem setters                    | ⚠️[Sem suporte, solução alternativa](#add-to-collections-without-setters) |
| `PreserveReferencesHandling` configuração global           | ❌ [Sem suporte](#preserve-object-references-and-handle-loops) |
| `ReferenceLoopHandling` configuração global                | ❌ [Sem suporte](#preserve-object-references-and-handle-loops) |
| Suporte para `System.Runtime.Serialization` atributos | ❌ [Sem suporte](#systemruntimeserialization-attributes) |
| `MissingMemberHandling` configuração global                | ❌ [Sem suporte](#missingmemberhandling) |
| Permitir nomes de propriedade sem aspas                   | ❌ [Sem suporte](#json-strings-property-names-and-string-values) |
| Permitir aspas simples em vez de valores de cadeia de caracteres              | ❌ [Sem suporte](#json-strings-property-names-and-string-values) |
| Permitir valores JSON que não são de cadeia de caracteres para propriedades de cadeia de caracteres    | ❌ [Sem suporte](#non-string-values-for-string-properties) |
| `TypeNameHandling.All` configuração global                 | ❌ [Sem suporte](#typenamehandlingall-not-supported) |
::: zone-end

Esta não é uma lista completa de `Newtonsoft.Json` recursos. A lista inclui muitos dos cenários que foram solicitados em [problemas do GitHub](https://github.com/dotnet/runtime/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json) ou postagens do [StackOverflow](https://stackoverflow.com/questions/tagged/system.text.json) . Se você implementar uma solução alternativa para um dos cenários listados aqui que não tem um código de exemplo, e se você quiser compartilhar sua solução, selecione **esta página** na seção de **comentários** na parte inferior desta página. Isso cria um problema no repositório GitHub da documentação e o lista na seção de **comentários** nesta página também.

## <a name="differences-in-default-jsonserializer-behavior-compared-to-newtonsoftjson"></a>Diferenças no comportamento padrão de JsonSerializer em comparação com Newtonsoft.Json

<xref:System.Text.Json> é estrito por padrão e evita qualquer adivinhação ou interpretação em nome do chamador, enfatizando o comportamento determinístico. A biblioteca foi projetada intencionalmente dessa forma para desempenho e segurança. `Newtonsoft.Json` é flexível por padrão. Essa diferença fundamental no design está por trás de muitas das diferenças específicas a seguir no comportamento padrão.

### <a name="case-insensitive-deserialization"></a>Desserialização não diferencia maiúsculas de minúsculas

Durante a desserialização, `Newtonsoft.Json` o nome da propriedade que não diferencia maiúsculas de minúsculas corresponde por padrão. O <xref:System.Text.Json> padrão diferencia maiúsculas de minúsculas, o que proporciona melhor desempenho, pois está fazendo uma correspondência exata. Para obter informações sobre como fazer a correspondência que não diferencia maiúsculas de minúsculas, consulte [correspondência de propriedade](system-text-json-character-casing.md)que não diferencia maiúsculas de minúsculas.

Se você estiver usando `System.Text.Json` indiretamente usando ASP.NET Core, não precisará fazer nada para obter o comportamento como `Newtonsoft.Json` . ASP.NET Core especifica as configurações para os [nomes de Propriedade do Camel](system-text-json-customize-properties.md#use-camel-case-for-all-json-property-names) case e a correspondência que não diferencia maiúsculas de minúsculas quando ela usa `System.Text.Json` .

::: zone pivot="dotnet-5-0"
O ASP.NET Core também permite a desserialização de [números entre aspas](#allow-or-write-numbers-in-quotes) por padrão.
::: zone-end

### <a name="minimal-character-escaping"></a>Escape de caractere mínimo

Durante a serialização, `Newtonsoft.Json` é relativamente permissivo de permitir caracteres sem escape. Ou seja, ele não os substitui por `\uxxxx` Where `xxxx` é o ponto de código do caractere. Em que ele faz escape, ele faz isso emitindo um `\` antes do caractere (por exemplo, `"` se torna `\"` ). <xref:System.Text.Json> escapa mais caracteres por padrão para fornecer proteções de defesa profunda contra XSS (script entre sites) ou ataques de divulgação de informações e faz isso usando a sequência de seis caracteres. `System.Text.Json` escapa todos os caracteres não ASCII por padrão, portanto, você não precisa fazer nada se estiver usando o `StringEscapeHandling.EscapeNonAscii` no `Newtonsoft.Json` . `System.Text.Json` também escapa caracteres com distinção de HTML, por padrão. Para obter informações sobre como substituir o `System.Text.Json` comportamento padrão, consulte [Personalizar codificação de caracteres](system-text-json-character-encoding.md).

### <a name="comments"></a>Comentários

Durante a desserialização, o `Newtonsoft.Json` ignora comentários no JSON por padrão. O <xref:System.Text.Json> padrão é gerar exceções para comentários porque a especificação [RFC 8259](https://tools.ietf.org/html/rfc8259) não os inclui. Para obter informações sobre como permitir comentários, consulte [permitir comentários e vírgulas à direita](system-text-json-invalid-json.md).

### <a name="trailing-commas"></a>Vírgula à direita

Durante a desserialização, o `Newtonsoft.Json` ignora vírgulas à direita por padrão. Ele também ignora várias vírgulas à direita (por exemplo, `[{"Color":"Red"},{"Color":"Green"},,]` ). O <xref:System.Text.Json> padrão é lançar exceções para vírgulas à direita porque a especificação [RFC 8259](https://tools.ietf.org/html/rfc8259) não as permite. Para obter informações sobre como fazer com que `System.Text.Json` sejam aceitas, consulte [permitir comentários e vírgulas à direita](system-text-json-invalid-json.md). Não há como permitir várias vírgulas à direita.

### <a name="converter-registration-precedence"></a>Precedência de registro do conversor

A `Newtonsoft.Json` precedência de registro para conversores personalizados é a seguinte:

* Atributo na propriedade
* Atributo no tipo
* Coleção de [conversores](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonSerializerSettings_Converters.htm)

Essa ordem significa que um conversor personalizado na `Converters` coleção é substituído por um conversor registrado pela aplicação de um atributo no nível de tipo. Ambos os registros são substituídos por um atributo no nível de propriedade.

A <xref:System.Text.Json> precedência de registro para conversores personalizados é diferente:

* Atributo na propriedade
* <xref:System.Text.Json.JsonSerializerOptions.Converters> Cole
* Atributo no tipo

A diferença aqui é que um conversor personalizado na `Converters` coleção substitui um atributo no nível de tipo. A intenção por trás dessa ordem de precedência é fazer com que as alterações em tempo de execução substituam as opções de tempo de design. Não há como alterar a precedência.

Para obter mais informações sobre o registro de conversor personalizado, consulte [registrar um conversor personalizado](system-text-json-converters-how-to.md#register-a-custom-converter).

### <a name="maximum-depth"></a>Profundidade máxima

`Newtonsoft.Json` Não tem um limite de profundidade máximo por padrão. <xref:System.Text.Json>Há um limite padrão de 64 e é configurável pela configuração <xref:System.Text.Json.JsonSerializerOptions.MaxDepth?displayProperty=nameWithType> .

Se você estiver usando `System.Text.Json` indiretamente usando ASP.NET Core, o limite máximo de profundidade padrão será 32. O valor padrão é o mesmo para a associação de modelo e é definido na [classe jsonoptions](https://github.com/dotnet/aspnetcore/blob/1f56888ea03f6a113587a6c4ac4d8b2ded326ffa/src/Mvc/Mvc.Core/src/JsonOptions.cs#L17-L20).

### <a name="json-strings-property-names-and-string-values"></a>Cadeias JSON (nomes de propriedade e valores de cadeia de caracteres)

Durante a desserialização, o `Newtonsoft.Json` aceita nomes de propriedade entre aspas duplas, aspas simples ou sem aspas. Ele aceita valores de cadeia de caracteres entre aspas duplas ou aspas simples. Por exemplo, `Newtonsoft.Json` aceita o seguinte JSON:

```json
{
  "name1": "value",
  'name2': "value",
  name3: 'value'
}
```

`System.Text.Json` aceita somente nomes de propriedade e valores de cadeia de caracteres entre aspas duplas porque esse formato é exigido pela especificação [RFC 8259](https://tools.ietf.org/html/rfc8259) e é o único formato considerado JSON válido.

Um valor entre aspas simples resulta em uma [jsonexception](xref:System.Text.Json.JsonException) com a seguinte mensagem:

```output
''' is an invalid start of a value.
```

### <a name="non-string-values-for-string-properties"></a>Valores que não são de cadeia de caracteres para propriedades de cadeia de caracteres

`Newtonsoft.Json` aceita valores que não são de cadeia de caracteres, como um número ou literais `true` e `false` , para desserialização para propriedades do tipo cadeia de caracteres. Aqui está um exemplo de JSON que é `Newtonsoft.Json` desserializado com êxito para a seguinte classe:

```json
{
  "String1": 1,
  "String2": true,
  "String3": false
}
```

```csharp
public class ExampleClass
{
    public string String1 { get; set; }
    public string String2 { get; set; }
    public string String3 { get; set; }
}
```

`System.Text.Json` Não desserializa os valores que não são de cadeia de caracteres em Propriedades de cadeia de caracteres. Um valor de não cadeia de caracteres recebido para um campo de cadeia de caracteres resulta em uma [jsonexception](xref:System.Text.Json.JsonException) com a seguinte mensagem:

```output
The JSON value could not be converted to System.String.
```

## <a name="scenarios-using-jsonserializer"></a>Cenários usando JsonSerializer

Alguns dos cenários a seguir não têm suporte da funcionalidade interna, mas as soluções alternativas são possíveis. As soluções alternativas são [conversores personalizados](system-text-json-converters-how-to.md), que podem não fornecer paridade completa com `Newtonsoft.Json` funcionalidade. Para alguns deles, o código de exemplo é fornecido como exemplos. Se você depender desses `Newtonsoft.Json` recursos, a migração exigirá modificações em seus modelos de objeto .net ou em outras alterações de código.

Para alguns dos cenários a seguir, as soluções alternativas não são práticas ou possíveis. Se você depender desses `Newtonsoft.Json` recursos, a migração não será possível sem alterações significativas.

### <a name="allow-or-write-numbers-in-quotes"></a>Permitir ou gravar números entre aspas

::: zone pivot="dotnet-5-0"
`Newtonsoft.Json` pode serializar ou desserializar números representados por cadeias de caracteres JSON (entre aspas). Por exemplo, ele pode aceitar: `{"DegreesCelsius":"23"}` em vez de `{"DegreesCelsius":23}` . Para habilitar esse comportamento no <xref:System.Text.Json> , defina <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A?displayProperty=nameWithType> como <xref:System.Text.Json.Serialization.JsonNumberHandling.WriteAsString> ou ou <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString> use o atributo [[JsonNumberHandling]](xref:System.Text.Json.Serialization.JsonNumberHandlingAttribute) .

Se você estiver usando `System.Text.Json` indiretamente usando ASP.NET Core, não precisará fazer nada para obter o comportamento como `Newtonsoft.Json` . ASP.NET Core especifica [os padrões da Web](system-text-json-configure-options.md#web-defaults-for-jsonserializeroptions) quando ele usa `System.Text.Json` , e os padrões da Web permitem números entre aspas.

Para obter mais informações, consulte [permitir ou gravar números entre aspas](system-text-json-invalid-json.md).
::: zone-end

::: zone pivot="dotnet-core-3-1"
`Newtonsoft.Json` pode serializar ou desserializar números representados por cadeias de caracteres JSON (entre aspas). Por exemplo, ele pode aceitar: `{"DegreesCelsius":"23"}` em vez de `{"DegreesCelsius":23}` . Para habilitar esse comportamento no <xref:System.Text.Json> no .NET Core 3,1, implemente um conversor personalizado como o exemplo a seguir. O conversor manipula as propriedades definidas como `long` :

* Ele os serializa como cadeias de caracteres JSON.
* Ele aceita números JSON e números entre aspas durante a desserialização.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/LongToStringConverter.cs":::

Registre esse conversor personalizado [usando um atributo](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-property) em propriedades individuais `long` ou [adicionando o conversor](system-text-json-converters-how-to.md#registration-sample---converters-collection) à <xref:System.Text.Json.JsonSerializerOptions.Converters> coleção.
::: zone-end

### <a name="specify-constructor-to-use-when-deserializing"></a>Especificar o Construtor a ser usado ao desserializar

O `Newtonsoft.Json` `[JsonConstructor]` atributo permite que você especifique qual Construtor chamar ao desserializar para um poco.

::: zone pivot="dotnet-5-0"
`System.Text.Json` também tem um atributo [[JsonConstructor]](xref:System.Text.Json.Serialization.JsonConstructorAttribute) . Para obter mais informações, consulte [tipos e registros imutáveis](system-text-json-immutability.md).
::: zone-end

::: zone pivot="dotnet-core-3-1"
<xref:System.Text.Json> no .NET Core 3,1 dá suporte apenas a construtores sem parâmetros. Como alternativa, você pode chamar qualquer Construtor necessário em um conversor personalizado. Consulte o exemplo para [desserializar classes e structs imutáveis](#deserialize-to-immutable-classes-and-structs).
::: zone-end

### <a name="conditionally-ignore-a-property"></a>Ignorar condicionalmente uma propriedade

`Newtonsoft.Json` o tem várias maneiras de ignorar condicionalmente uma propriedade na serialização ou desserialização:

* `DefaultContractResolver` permite selecionar propriedades a serem incluídas ou ignoradas, com base em critérios arbitrários.
* As `NullValueHandling` `DefaultValueHandling` configurações e em `JsonSerializerSettings` permitem que você especifique que todas as propriedades de valor nulo ou valor padrão devem ser ignoradas.
* As `NullValueHandling` `DefaultValueHandling` configurações e no `[JsonProperty]` atributo permitem especificar propriedades individuais que devem ser ignoradas quando definidas como NULL ou o valor padrão.

::: zone pivot="dotnet-5-0"

<xref:System.Text.Json> fornece as seguintes maneiras de ignorar Propriedades ou campos ao serializar:

* O atributo [[JsonIgnore]](system-text-json-ignore-properties.md#ignore-individual-properties) em uma propriedade faz com que a propriedade seja omitida do JSON durante a serialização.
* A opção global [IgnoreReadOnlyProperties](system-text-json-ignore-properties.md#ignore-all-read-only-properties) permite ignorar todas as propriedades somente leitura.
* Se você estiver [incluindo campos](system-text-json-how-to.md#include-fields), a <xref:System.Text.Json.JsonSerializerOptions.IgnoreReadOnlyFields%2A?displayProperty=nameWithType> opção global permitirá ignorar todos os campos somente leitura.
* A `DefaultIgnoreCondition` opção global permite [ignorar todas as propriedades de tipo de valor que têm valores padrão](system-text-json-ignore-properties.md#ignore-all-default-value-properties)ou [ignorar todas as propriedades de tipo de referência que têm valores nulos](system-text-json-ignore-properties.md#ignore-all-null-value-properties).

::: zone-end

::: zone pivot="dotnet-core-3-1"

<xref:System.Text.Json> no .NET Core 3,1 fornece as seguintes maneiras de ignorar Propriedades ao serializar:

* O atributo [[JsonIgnore]](system-text-json-ignore-properties.md#ignore-individual-properties) em uma propriedade faz com que a propriedade seja omitida do JSON durante a serialização.
* A opção global [IgnoreNullValues](system-text-json-ignore-properties.md#ignore-all-null-value-properties) permite ignorar todas as propriedades de valor nulo.
* A opção global [IgnoreReadOnlyProperties](system-text-json-ignore-properties.md#ignore-all-read-only-properties) permite ignorar todas as propriedades somente leitura.
::: zone-end

Essas opções **não** permitem que você:

::: zone pivot="dotnet-5-0"

* Ignorar as propriedades selecionadas com base em critérios arbitrários avaliados em tempo de execução.

::: zone-end

::: zone pivot="dotnet-core-3-1"

* Ignore todas as propriedades que têm o valor padrão para o tipo.
* Ignore as propriedades selecionadas que têm o valor padrão para o tipo.
* Ignorar propriedades selecionadas se seu valor for nulo.
* Ignorar as propriedades selecionadas com base em critérios arbitrários avaliados em tempo de execução.

::: zone-end

Para essa funcionalidade, você pode escrever um conversor personalizado. Aqui está um exemplo de POCO e um conversor personalizado para ele que ilustra essa abordagem:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecastRuntimeIgnoreConverter.cs":::

O conversor faz com que a `Summary` propriedade seja omitida da serialização se seu valor for NULL, uma cadeia de caracteres vazia ou "N/A".

Registre esse conversor personalizado [usando um atributo na classe](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-type) ou [adicionando o conversor](system-text-json-converters-how-to.md#registration-sample---converters-collection) à <xref:System.Text.Json.JsonSerializerOptions.Converters> coleção.

Essa abordagem requer lógica adicional se:

* O POCO inclui propriedades complexas.
* Você precisa manipular atributos como, por `[JsonIgnore]` exemplo, ou opções como codificadores personalizados.

### <a name="public-and-non-public-fields"></a>Campos públicos e não públicos

`Newtonsoft.Json` pode serializar e desserializar campos, bem como propriedades.

::: zone pivot="dotnet-5-0"
No <xref:System.Text.Json> , use a <xref:System.Text.Json.JsonSerializerOptions.IncludeFields?displayProperty=nameWithType> configuração global ou o atributo [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) para incluir campos públicos ao serializar ou desserializar. Para obter um exemplo, consulte [incluir campos](system-text-json-how-to.md#include-fields).
::: zone-end

::: zone pivot="dotnet-core-3-1"
<xref:System.Text.Json> no .NET Core 3,1 funciona apenas com propriedades públicas. Conversores personalizados podem fornecer essa funcionalidade.
::: zone-end

### <a name="preserve-object-references-and-handle-loops"></a>Preservar referências de objeto e manipular loops

Por padrão, o `Newtonsoft.Json` serializa por valor. Por exemplo, se um objeto contiver duas propriedades que contêm uma referência ao mesmo `Person` objeto, os valores das `Person` Propriedades desse objeto serão duplicados no JSON.

`Newtonsoft.Json` tem uma `PreserveReferencesHandling` configuração no `JsonSerializerSettings` que permite serializar por referência:

* Um identificador de metadados é adicionado ao JSON criado para o primeiro `Person` objeto.
* O JSON que é criado para o segundo `Person` objeto contém uma referência a esse identificador em vez de valores de propriedade.

`Newtonsoft.Json` também tem uma `ReferenceLoopHandling` configuração que permite ignorar referências circulares em vez de gerar uma exceção.

::: zone pivot="dotnet-5-0"
Para preservar referências e manipular referências circulares no <xref:System.Text.Json> , defina <xref:System.Text.Json.JsonSerializerOptions.ReferenceHandler%2A?displayProperty=nameWithType> como <xref:System.Text.Json.Serialization.ReferenceHandler.Preserve%2A> . A `ReferenceHandler.Preserve` configuração é equivalente a `PreserveReferencesHandling`  =  `PreserveReferencesHandling.All` em `Newtonsoft.Json` .

Como o Newtonsoft.Json [ReferenceResolver](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonSerializer_ReferenceResolver.htm), a <xref:System.Text.Json.Serialization.ReferenceResolver?displayProperty=fullName> classe define o comportamento de preservar referências na serialização e desserialização. Crie uma classe derivada para especificar o comportamento personalizado. Para obter um exemplo, consulte [GuidReferenceResolver](https://github.com/dotnet/docs/blob/9d5e88edbd7f12be463775ffebbf07ac8415fe18/docs/standard/serialization/snippets/system-text-json-how-to-5-0/csharp/GuidReferenceResolverExample.cs).

`Newtonsoft.Json`Não há suporte para alguns recursos relacionados:

* [JsonPropertyAttribute. IsReference](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonPropertyAttribute_IsReference.htm)
* [JsonPropertyAttribute. ReferenceLoopHandling](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonPropertyAttribute_ReferenceLoopHandling.htm)
* [JsonSerializerSettings. ReferenceLoopHandling](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonSerializerSettings_ReferenceLoopHandling.htm)

Para obter mais informações, consulte [preservar referências e manipular referências circulares](system-text-json-preserve-references.md).
::: zone-end

::: zone pivot="dotnet-core-3-1"
<xref:System.Text.Json> no .NET Core 3,1 dá suporte apenas a serialização por valor e gera uma exceção para referências circulares.
::: zone-end

### <a name="dictionary-with-non-string-key"></a>Dicionário com chave não cadeia de caracteres

::: zone pivot="dotnet-5-0"
`Newtonsoft.Json`E as `System.Text.Json` coleções de suporte do tipo `Dictionary<TKey, TValue>` .

> [!CAUTION]
> A desserialização para um `Dictionary<TKey, TValue>` onde `TKey` é digitada como algo diferente de `string` pode introduzir uma vulnerabilidade de segurança no aplicativo de consumo. Para obter mais informações, consulte [dotnet/tempo de execução # 4761](https://github.com/dotnet/runtime/issues/4761).

::: zone-end

::: zone pivot="dotnet-core-3-1"
`Newtonsoft.Json` dá suporte a coleções do tipo `Dictionary<TKey, TValue>` . O suporte interno para coleções de dicionário no <xref:System.Text.Json> .NET Core 3,1 é limitado a `Dictionary<string, TValue>` . Ou seja, a chave deve ser uma cadeia de caracteres.

Para dar suporte a um dicionário com um inteiro ou algum outro tipo como a chave no .NET Core 3,1, crie um conversor como o exemplo em [como escrever conversores personalizados](system-text-json-converters-how-to.md#support-dictionary-with-non-string-key).
::: zone-end

### <a name="types-without-built-in-support"></a>Tipos sem suporte interno

<xref:System.Text.Json> o não fornece suporte interno para os seguintes tipos:

* <xref:System.Data.DataTable> e tipos relacionados
::: zone pivot="dotnet-5-0"
* Tipos F #, como [uniões discriminadas](../../fsharp/language-reference/discriminated-unions.md). [Tipos de registro](../../fsharp/language-reference/records.md) e [tipos de registros anônimos](../../fsharp/language-reference/anonymous-records.md) são tratados como imutáveis POCOs e, portanto, têm suporte.
::: zone-end
::: zone pivot="dotnet-core-3-1"
* Tipos F #, como [uniões discriminadas](../../fsharp/language-reference/discriminated-unions.md), [tipos de registro](../../fsharp/language-reference/records.md)e [tipos de registros anônimos](../../fsharp/language-reference/anonymous-records.md).
::: zone-end
* <xref:System.Dynamic.ExpandoObject>
* <xref:System.TimeZoneInfo>
* <xref:System.Numerics.BigInteger>
* <xref:System.TimeSpan>
* <xref:System.DBNull>
* <xref:System.Type>
* <xref:System.ValueTuple> e seus tipos genéricos associados

Conversores personalizados podem ser implementados para tipos que não têm suporte interno.

### <a name="polymorphic-serialization"></a>Serialização polimórfica

`Newtonsoft.Json` automaticamente a serialização polimórfica. Para obter informações sobre os recursos limitados de serialização polimórfico do <xref:System.Text.Json> , consulte [serializar Propriedades de classes derivadas](system-text-json-polymorphism.md).

A solução alternativa descrita aqui é definir as propriedades que podem conter classes derivadas como tipo `object` . Se isso não for possível, outra opção é criar um conversor com um `Write` método para a hierarquia de tipo de herança inteira, como o exemplo em [como escrever conversores personalizados](system-text-json-converters-how-to.md#support-polymorphic-deserialization).

### <a name="polymorphic-deserialization"></a>Desserialização polimórfica

`Newtonsoft.Json` tem uma `TypeNameHandling` configuração que adiciona metadados de nome de tipo ao JSON durante a serialização. Ele usa os metadados durante a desserialização para fazer a desserialização polimórfica. <xref:System.Text.Json> pode fazer um intervalo limitado de [serialização polimórfica](system-text-json-polymorphism.md) , mas não desserialização polimórfica.

Para dar suporte à desserialização polimórfica, crie um conversor como o exemplo em [como escrever conversores personalizados](system-text-json-converters-how-to.md#support-polymorphic-deserialization).

### <a name="deserialization-of-object-properties"></a>Desserialização de propriedades de objeto

Quando o `Newtonsoft.Json` desserializa para <xref:System.Object> , ele:

* Infere o tipo de valores primitivos no conteúdo JSON (diferente de `null` ) e retorna o armazenado `string` , `long` , `double` , `boolean` ou `DateTime` como um objeto em caixa. *Os valores primitivos* são valores JSON únicos, como um número JSON, Cadeia de caracteres,, `true` `false` ou `null` .
* Retorna um `JObject` ou `JArray` para valores complexos na carga JSON. *Valores complexos* são coleções de pares chave-valor JSON entre chaves ( `{}` ) ou listas de valores entre colchetes ( `[]` ). As propriedades e os valores dentro das chaves ou colchetes podem ter propriedades ou valores adicionais.
* Retorna uma referência nula quando a carga tem o `null` literal JSON.

<xref:System.Text.Json> Armazena um Boxed `JsonElement` para valores primitivos e complexos sempre que a desserialização para <xref:System.Object> , por exemplo:

* Uma `object` propriedade.
* Um `object` valor de dicionário.
* Um `object` valor de matriz.
* Uma raiz `object` .

No entanto, `System.Text.Json` `null` o trata o mesmo que `Newtonsoft.Json` e retorna uma referência nula quando a carga tem o `null` literal JSON nela.

Para implementar a inferência de tipos para `object` Propriedades, crie um conversor como o exemplo em [como escrever conversores personalizados](system-text-json-converters-how-to.md#deserialize-inferred-types-to-object-properties).

### <a name="deserialize-null-to-non-nullable-type"></a>Desserializar NULL para tipo não anulável

`Newtonsoft.Json` o não gera uma exceção no cenário a seguir:

* `NullValueHandling` é definido como `Ignore` e
* Durante a desserialização, o JSON contém um valor nulo para um tipo de valor não anulável.

No mesmo cenário, o <xref:System.Text.Json> gera uma exceção. (A configuração de manipulação nula correspondente no `System.Text.Json` é <xref:System.Text.Json.JsonSerializerOptions.IgnoreNullValues?displayProperty=nameWithType>  =  `true` .)

Se você possui o tipo de destino, a melhor solução alternativa é tornar a propriedade em questão anulável (por exemplo, alterar `int` para `int?` ).

Outra solução alternativa é criar um conversor para o tipo, como o exemplo a seguir, que manipula valores nulos para `DateTimeOffset` tipos:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/DateTimeOffsetNullHandlingConverter.cs":::

Registre esse conversor personalizado [usando um atributo na propriedade](system-text-json-converters-how-to.md#registration-sample---jsonconverter-on-a-property) ou [adicionando o conversor](system-text-json-converters-how-to.md#registration-sample---converters-collection) à <xref:System.Text.Json.JsonSerializerOptions.Converters> coleção.

**Observação:** O conversor anterior **manipula valores nulos de forma diferente** `Newtonsoft.Json` do que o faz para POCOs que especificam valores padrão. Por exemplo, suponha que o código a seguir represente o objeto de destino:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithDefault":::

E suponha que o JSON a seguir seja desserializado usando o conversor anterior:

```json
{
  "Date": null,
  "TemperatureCelsius": 25,
  "Summary": null
}
```

Após a desserialização, a `Date` propriedade tem 1/1/0001 ( `default(DateTimeOffset)` ), ou seja, o valor definido no construtor é substituído. Considerando o mesmo POCO e JSON, a `Newtonsoft.Json` desserialização deixaria 1/1/2001 na `Date` propriedade.

### <a name="deserialize-to-immutable-classes-and-structs"></a>Desserializar para classes e structs imutáveis

`Newtonsoft.Json` pode desserializar para classes e structs imutáveis porque pode usar construtores com parâmetros.

::: zone pivot="dotnet-5-0"
No <xref:System.Text.Json> , use o atributo [[JsonConstructor]](xref:System.Text.Json.Serialization.JsonConstructorAttribute) para especificar o uso de um construtor com parâmetros. Os registros em C# 9 também são imutáveis e têm suporte como destinos de desserialização. Para obter mais informações, consulte [tipos e registros imutáveis](system-text-json-immutability.md).
::: zone-end

::: zone pivot="dotnet-core-3-1"
<xref:System.Text.Json> no .NET Core 3,1 dá suporte apenas a construtores públicos sem parâmetros. Como alternativa, você pode chamar um construtor com parâmetros em um conversor personalizado.

Aqui está um struct imutável com vários parâmetros de construtor:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/ImmutablePoint.cs" id="ImmutablePoint":::

E aqui está um conversor que serializa e desserializa essa estrutura:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/ImmutablePointConverter.cs":::

Registre esse conversor personalizado [adicionando o conversor](system-text-json-converters-how-to.md#registration-sample---converters-collection) à <xref:System.Text.Json.JsonSerializerOptions.Converters> coleção.

Para obter um exemplo de um conversor semelhante que manipula propriedades genéricas abertas, consulte o [conversor interno para pares de chave-valor](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/libraries/System.Text.Json/src/System/Text/Json/Serialization/Converters/JsonValueConverterKeyValuePair.cs).
::: zone-end

### <a name="required-properties"></a>Propriedades obrigatórias

No `Newtonsoft.Json` , você especifica que uma propriedade é exigida pela configuração `Required` no `[JsonProperty]` atributo. `Newtonsoft.Json` gera uma exceção se nenhum valor for recebido no JSON para uma propriedade marcada como necessária.

<xref:System.Text.Json> Não lançará uma exceção se nenhum valor for recebido para uma das propriedades do tipo de destino. Por exemplo, se você tiver uma `WeatherForecast` classe:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WF":::

O JSON a seguir é desserializado sem erro:

```json
{
    "TemperatureCelsius": 25,
    "Summary": "Hot"
}
```

Para fazer a desserialização falhar se nenhuma `Date` propriedade estiver no JSON, implemente um conversor personalizado. O código de conversor de exemplo a seguir gera uma exceção se a `Date` propriedade não estiver definida após a desserialização ser concluída:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecastRequiredPropertyConverter.cs":::

Registre esse conversor personalizado [adicionando o conversor](system-text-json-converters-how-to.md#registration-sample---converters-collection) à <xref:System.Text.Json.JsonSerializerOptions.Converters?displayProperty=nameWithType> coleção.

Esse padrão de chamar recursivamente o conversor exige que você registre o conversor usando <xref:System.Text.Json.JsonSerializerOptions> , não usando um atributo. Se você registrar o conversor usando um atributo, o conversor personalizado chamará recursivamente a si mesmo. O resultado é um loop infinito que termina em uma exceção de estouro de pilha.

Quando você registra o conversor usando o objeto Options, evite um loop infinito não passando o objeto Options ao chamar <xref:System.Text.Json.JsonSerializer.Serialize%2A> ou <xref:System.Text.Json.JsonSerializer.Deserialize%2A> . O objeto Options contém a <xref:System.Text.Json.JsonSerializerOptions.Converters%2A> coleção. Se você passá-lo para `Serialize` ou `Deserialize` , o conversor personalizado chamará a si mesmo, fazendo um loop infinito que resulta em uma exceção de estouro de pilha. Se as opções padrão não forem viáveis, crie uma nova instância das opções com as configurações necessárias. Essa abordagem será lenta, pois cada nova instância armazena em cache de forma independente.

Há um padrão alternativo que pode usar `JsonConverterAttribute` o registro na classe a ser convertida. Nessa abordagem, o código do conversor chama `Serialize` ou `Deserialize` em uma classe que deriva da classe a ser convertida. A classe derivada não tem uma `JsonConverterAttribute` aplicada a ela. No exemplo a seguir dessa alternativa:

* `WeatherForecastWithRequiredPropertyConverterAttribute` é a classe a ser desserializada e está `JsonConverterAttribute` aplicada a ela.
* `WeatherForecastWithoutRequiredPropertyConverterAttribute` é a classe derivada que não tem o atributo de conversor.
* O código no conversor chama `Serialize` e `Deserialize` em `WeatherForecastWithoutRequiredPropertyConverterAttribute` para evitar um loop infinito. Há um custo de desempenho para essa abordagem na serialização devido a uma instanciação de objeto extra e à cópia de valores de propriedade.

Estes são os `WeatherForecast*` tipos:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecast.cs" id="WFWithReqPptyConverterAttr":::

E aqui está o conversor:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecastRequiredPropertyConverterForAttributeRegistration.cs":::

O conversor de propriedades necessárias exigiria lógica adicional se você precisar manipular atributos como [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute) ou opções diferentes, como codificadores personalizados. Além disso, o código de exemplo não manipula Propriedades para as quais um valor padrão é definido no construtor. E essa abordagem não diferencia os seguintes cenários:

* Uma propriedade está ausente no JSON.
* Uma propriedade para um tipo não anulável está presente no JSON, mas o valor é o padrão para o tipo, como zero para um `int` .
* Uma propriedade para um tipo de valor anulável está presente no JSON, mas o valor é NULL.

### <a name="specify-date-format"></a>Especificar formato de data

`Newtonsoft.Json` fornece várias maneiras de controlar como as propriedades `DateTime` de `DateTimeOffset` tipos e são serializadas e desserializadas:

* A `DateTimeZoneHandling` configuração pode ser usada para serializar todos os `DateTime` valores como datas UTC.
* A `DateFormatString` configuração e os `DateTime` conversores podem ser usados para personalizar o formato de cadeias de caracteres de data.

<xref:System.Text.Json> dá suporte a ISO 8601-1:2019, incluindo o perfil RFC 3339. Esse formato é amplamente adotado, não ambíguo e faz viagens de ida e volta com precisão. Para usar qualquer outro formato, crie um conversor personalizado. Para obter mais informações, consulte [suporte a DateTime e System.Text.Json DateTimeOffset no ](../datetime/system-text-json-support.md).

### <a name="callbacks"></a>Retornos de chamada

`Newtonsoft.Json` permite executar código personalizado em vários pontos no processo de serialização ou desserialização:

* OnDeserializing (ao começar a desserializar um objeto)
* OnDeserialized (quando terminar de desserializar um objeto)
* Onserializando (ao começar a serializar um objeto)
* OnSerialized (ao concluir a serialização de um objeto)

No <xref:System.Text.Json> , você pode simular retornos de chamada escrevendo um conversor personalizado. O exemplo a seguir mostra um conversor personalizado para um POCO. O conversor inclui um código que exibe uma mensagem em cada ponto correspondente a um `Newtonsoft.Json` retorno de chamada.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/WeatherForecastCallbacksConverter.cs":::

Registre esse conversor personalizado [adicionando o conversor](system-text-json-converters-how-to.md#registration-sample---converters-collection) à <xref:System.Text.Json.JsonSerializerOptions.Converters> coleção.

Se você usar um conversor personalizado que segue o exemplo anterior:

* O `OnDeserializing` código não tem acesso à nova instância poco. Para manipular a nova instância POCO no início da desserialização, coloque esse código no Construtor POCO.
* Evite um loop infinito registrando o conversor no objeto Options e não passando o objeto Options ao chamar de forma recursiva `Serialize` ou `Deserialize` .

Para obter mais informações sobre conversores personalizados que chamam de forma recursiva `Serialize` ou `Deserialize` , consulte a seção [Propriedades necessárias](#required-properties) anteriormente neste artigo.

### <a name="non-public-property-setters-and-getters"></a>Setters e getters de propriedade não pública

`Newtonsoft.Json` pode usar setters e propriedades de propriedade privada e interna por meio do `JsonProperty` atributo.

::: zone pivot="dotnet-5-0"
<xref:System.Text.Json> dá suporte a setters e predefinidores de propriedade interna e privada por meio do atributo [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) . Para obter o código de exemplo, consulte [acessadores de propriedade não pública](system-text-json-immutability.md).
::: zone-end

::: zone pivot="dotnet-core-3-1"
<xref:System.Text.Json> no .NET Core 3,1 dá suporte apenas a setters públicos. Conversores personalizados podem fornecer essa funcionalidade.
::: zone-end

### <a name="populate-existing-objects"></a>Popular objetos existentes

O `JsonConvert.PopulateObject` método em `Newtonsoft.Json` desserializa um documento JSON para uma instância existente de uma classe, em vez de criar uma nova instância. <xref:System.Text.Json> sempre cria uma nova instância do tipo de destino usando o construtor público sem parâmetros padrão. Conversores personalizados podem desserializar em uma instância existente.

### <a name="reuse-rather-than-replace-properties"></a>Reutilização em vez de substituir Propriedades

A `Newtonsoft.Json` `ObjectCreationHandling` configuração permite especificar que os objetos nas propriedades devem ser reutilizados em vez de substituídos durante a desserialização. <xref:System.Text.Json> sempre substitui objetos em Propriedades.  Conversores personalizados podem fornecer essa funcionalidade.

### <a name="add-to-collections-without-setters"></a>Adicionar a coleções sem setters

Durante a desserialização, `Newtonsoft.Json` o adiciona objetos a uma coleção, mesmo que a propriedade não tenha nenhum setter. <xref:System.Text.Json> ignora as propriedades que não têm setters. Conversores personalizados podem fornecer essa funcionalidade.

### <a name="systemruntimeserialization-attributes"></a>Atributos System. Runtime. Serialization

<xref:System.Text.Json> Não dá suporte a atributos do `System.Runtime.Serialization` namespace, como `DataMemberAttribute` e `IgnoreDataMemberAttribute` .

### <a name="octal-numbers"></a>Números octais

`Newtonsoft.Json` Trata os números com um zero à esquerda como números octais. <xref:System.Text.Json> Não permite zeros à esquerda porque a especificação [RFC 8259](https://tools.ietf.org/html/rfc8259) não permite.

### <a name="missingmemberhandling"></a>MissingMemberHandling

`Newtonsoft.Json` pode ser configurado para gerar exceções durante a desserialização se o JSON incluir propriedades que estão ausentes no tipo de destino. <xref:System.Text.Json> ignora propriedades extras no JSON, exceto quando você usa o [atributo [JsonExtensionData]](system-text-json-handle-overflow.md). Não há nenhuma solução alternativa para o recurso de membro ausente.

### <a name="tracewriter"></a>TraceWriter

`Newtonsoft.Json` permite que você depure usando um `TraceWriter` para exibir logs gerados pela serialização ou desserialização. <xref:System.Text.Json> Não faz registro em log.

## <a name="jsondocument-and-jsonelement-compared-to-jtoken-like-jobject-jarray"></a>JsonDocument e Jsonelement em comparação com JToken (como JObject, JArray)

<xref:System.Text.Json.JsonDocument?displayProperty=fullName> fornece a capacidade de analisar e criar um Modelo de Objeto do Documento **somente leitura** (dom) de cargas JSON existentes. O DOM fornece acesso aleatório aos dados em uma carga JSON. Os elementos JSON que compõem a carga podem ser acessados por meio do <xref:System.Text.Json.JsonElement> tipo. O `JsonElement` tipo fornece APIs para converter texto JSON em tipos .net comuns. `JsonDocument` expõe uma <xref:System.Text.Json.JsonDocument.RootElement> propriedade.

### <a name="jsondocument-is-idisposable"></a>JsonDocument é IDisposable

`JsonDocument` Cria uma exibição na memória dos dados em um buffer em pool. Portanto, ao `JObject` contrário `JArray` de ou de `Newtonsoft.Json` , o `JsonDocument` tipo implementa `IDisposable` e precisa ser usado dentro de um bloco Using.

Retorne apenas uma `JsonDocument` da sua API se você quiser transferir a propriedade de tempo de vida e descartar a responsabilidade para o chamador. Na maioria dos cenários, isso não é necessário. Se o chamador precisar trabalhar com o documento JSON inteiro, retorne o <xref:System.Text.Json.JsonElement.Clone%2A> do <xref:System.Text.Json.JsonDocument.RootElement%2A> , que é um <xref:System.Text.Json.JsonElement> . Se o chamador precisar trabalhar com um elemento específico dentro do documento JSON, retorne o <xref:System.Text.Json.JsonElement.Clone%2A> <xref:System.Text.Json.JsonElement> . Se você retornar o `RootElement` ou um subelemento diretamente sem fazer um `Clone` , o chamador não poderá acessar o retornado `JsonElement` depois `JsonDocument` que o proprietário for descartado.

Aqui está um exemplo que exige que você faça um `Clone` :

```csharp
public JsonElement LookAndLoad(JsonElement source)
{
    string json = File.ReadAllText(source.GetProperty("fileName").GetString());

    using (JsonDocument doc = JsonDocument.Parse(json))
    {
        return doc.RootElement.Clone();
    }
}
```

O código anterior espera um `JsonElement` que contém uma `fileName` propriedade. Ele abre o arquivo JSON e cria um `JsonDocument` . O método pressupõe que o chamador deseja trabalhar com o documento inteiro e, portanto, retorna o `Clone` do `RootElement` .

Se você receber um `JsonElement` e estiver retornando um subelemento, não será necessário retornar um `Clone` do subelemento. O chamador é responsável por manter a vida o `JsonDocument` que o passado `JsonElement` pertence. Por exemplo:

```csharp
public JsonElement ReturnFileName(JsonElement source)
{
   return source.GetProperty("fileName");
}
```

### <a name="jsondocument-is-read-only"></a>JsonDocument é somente leitura

O <xref:System.Text.Json> dom não pode adicionar, remover ou modificar elementos JSON. Ele foi projetado dessa forma para o desempenho e para reduzir as alocações para a análise de tamanhos de carga JSON comuns (ou seja, < 1 MB). Se seu cenário usa atualmente um DOM modificável, uma das seguintes soluções alternativas pode ser viável:

* Para criar um `JsonDocument` do zero (ou seja, sem passar um conteúdo JSON existente para o `Parse` método), grave o texto JSON usando o `Utf8JsonWriter` e analise a saída de para criar um novo `JsonDocument` .
* Para modificar um existente `JsonDocument` , use-o para gravar texto JSON, fazer alterações enquanto você escreve e analisar a saída do para criar um novo `JsonDocument` .
* Para mesclar documentos JSON existentes, equivalentes `JObject.Merge` às `JContainer.Merge` APIs ou do `Newtonsoft.Json` , consulte [este problema do GitHub](https://github.com/dotnet/corefx/issues/42466#issuecomment-570475853).

### <a name="jsonelement-is-a-union-struct"></a>Jsonelement é uma struct Union

`JsonDocument` expõe o `RootElement` como uma propriedade do tipo <xref:System.Text.Json.JsonElement> , que é um tipo Union, struct que abrange qualquer elemento JSON. `Newtonsoft.Json` usa tipos hierárquicos dedicados como `JObject` , `JArray` , `JToken` e assim por diante. `JsonElement` é o que você pode pesquisar e enumerar e pode usar `JsonElement` para materializar elementos JSON em tipos .net.

### <a name="how-to-search-a-jsondocument-and-jsonelement-for-sub-elements"></a>Como pesquisar um JsonDocument e um Jsonelement para subelementos

Procura tokens JSON usando `JObject` ou `JArray` de `Newtonsoft.Json` tendem a ser relativamente rápidos, pois são pesquisas em algum dicionário. Por comparação, as pesquisas em `JsonElement` exigem uma pesquisa sequencial das propriedades e, portanto, são relativamente lentas (por exemplo, ao usar `TryGetProperty` ). <xref:System.Text.Json> foi projetado para minimizar o tempo de análise inicial em vez da hora de pesquisa. Portanto, use as seguintes abordagens para otimizar o desempenho ao pesquisar por um `JsonDocument` objeto:

* Use os enumeradores internos ( <xref:System.Text.Json.JsonElement.EnumerateArray%2A> e <xref:System.Text.Json.JsonElement.EnumerateObject%2A> ) em vez de fazer sua própria indexação ou loops.
* Não faça uma pesquisa seqüencial no todo `JsonDocument` por meio de cada propriedade usando `RootElement` . Em vez disso, pesquise objetos JSON aninhados com base na estrutura conhecida dos dados JSON. Por exemplo, se você estiver procurando uma `Grade` propriedade em `Student` objetos, faça um loop pelos `Student` objetos e obtenha o valor de `Grade` para cada um, em vez de Pesquisar por todos os `JsonElement` objetos procurando por `Grade` Propriedades. Fazer o último resultará em passagens desnecessárias nos mesmos dados.

Para obter um exemplo de código, consulte [usar JsonDocument para acessar dados](write-custom-serializer-deserializer.md#use-jsondocument-for-access-to-data).

## <a name="utf8jsonreader-compared-to-jsontextreader"></a>Utf8JsonReader em comparação com JsonTextReader

<xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName>é um leitor de alto desempenho, de baixa alocação e somente de encaminhamento para texto JSON codificado em UTF-8, lido de um [ReadOnlySpan \<byte> ](xref:System.ReadOnlySpan%601) ou [ReadOnlySequence \<byte> ](xref:System.Buffers.ReadOnlySequence%601). O `Utf8JsonReader` é um tipo de baixo nível que pode ser usado para criar analisadores e desserializadores personalizados.

As seções a seguir explicam os padrões de programação recomendados para o uso do `Utf8JsonReader` .

### <a name="utf8jsonreader-is-a-ref-struct"></a>Utf8JsonReader é um struct de referência

Como o `Utf8JsonReader` tipo é uma *struct de referência*, ele tem [determinadas limitações](../../csharp/language-reference/builtin-types/struct.md#ref-struct). Por exemplo, ele não pode ser armazenado como um campo em uma classe ou struct diferente de um struct de referência. Para obter alto desempenho, esse tipo deve ser um, uma `ref struct` vez que ele precisa armazenar em cache a entrada [ReadOnlySpan \<byte> ](xref:System.ReadOnlySpan%601), que é um struct de referência. Além disso, esse tipo é mutável, pois mantém o estado. Portanto, **passe-o por ref** em vez de por valor. Passá-lo por valor resultaria em uma cópia de struct e as alterações de estado não seriam visíveis para o chamador. Isso `Newtonsoft.Json` é diferente desde que o `Newtonsoft.Json` `JsonTextReader` é uma classe. Para obter mais informações sobre como usar structs de referência, consulte [escrever código C# seguro e eficiente](../../csharp/write-safe-efficient-code.md).

### <a name="read-utf-8-text"></a>Ler texto UTF-8

Para obter o melhor desempenho possível ao usar o `Utf8JsonReader` , leia as cargas JSON já codificadas como texto UTF-8, e não como cadeias de caracteres UTF-16. Para obter um exemplo de código, consulte [filtrar dados usando Utf8JsonReader](write-custom-serializer-deserializer.md#filter-data-using-utf8jsonreader).

### <a name="read-with-a-stream-or-pipereader"></a>Ler com um fluxo ou PipeReader

O `Utf8JsonReader` oferece suporte à leitura de um [ \<byte> READONLYSPAN](xref:System.ReadOnlySpan%601) codificado em UTF-8 ou [ReadOnlySequence \<byte> ](xref:System.Buffers.ReadOnlySequence%601) (que é o resultado da leitura de um <xref:System.IO.Pipelines.PipeReader> ).

Para leitura síncrona, você pode ler a carga JSON até o final do fluxo em uma matriz de bytes e passá-la para o leitor. Para ler de uma cadeia de caracteres (que é codificada como UTF-16), chame <xref:System.Text.Encoding.UTF8> .<xref:System.Text.Encoding.GetBytes%2A> para primeiro transcodificar a cadeia de caracteres em uma matriz de bytes codificada em UTF-8. Em seguida, passe-o para o `Utf8JsonReader` .

Como o `Utf8JsonReader` considera a entrada como texto JSON, uma bom (marca de ordem de byte) UTF-8 é considerada JSON inválido. O chamador precisa filtrar isso antes de passar os dados para o leitor.

Para obter exemplos de código, consulte [usar Utf8JsonReader](write-custom-serializer-deserializer.md#use-utf8jsonreader).

### <a name="read-with-multi-segment-readonlysequence"></a>Ler com ReadOnlySequence de vários segmentos

Se a entrada JSON for um [ReadOnlySpan \<byte> ](xref:System.ReadOnlySpan%601), cada elemento JSON poderá ser acessado da `ValueSpan` propriedade no leitor à medida que você passar pelo loop de leitura. No entanto, se sua entrada for um [ \<byte> ReadOnlySequence](xref:System.Buffers.ReadOnlySequence%601) (que é o resultado da leitura de um <xref:System.IO.Pipelines.PipeReader> ), alguns elementos JSON poderão se ampliar de vários segmentos do `ReadOnlySequence<byte>` objeto. Esses elementos não podem ser acessados <xref:System.Text.Json.Utf8JsonReader.ValueSpan%2A> em um bloco de memória contíguo. Em vez disso, sempre que você tiver um multithread `ReadOnlySequence<byte>` como entrada, pesquise a <xref:System.Text.Json.Utf8JsonReader.HasValueSequence%2A> propriedade no leitor para descobrir como acessar o elemento JSON atual. Aqui está um padrão recomendado:

```csharp
while (reader.Read())
{
    switch (reader.TokenType)
    {
        // ...
        ReadOnlySpan<byte> jsonElement = reader.HasValueSequence ?
            reader.ValueSequence.ToArray() :
            reader.ValueSpan;
        // ...
    }
}
```

### <a name="use-valuetextequals-for-property-name-lookups"></a>Usar ValueTextEquals para pesquisas de nome de propriedade

Não use para fazer comparações de <xref:System.Text.Json.Utf8JsonReader.ValueSpan%2A> byte por byte chamando <xref:System.MemoryExtensions.SequenceEqual%2A> pesquisas de nome de propriedade. Chame <xref:System.Text.Json.Utf8JsonReader.ValueTextEquals%2A> em vez disso, porque esse método desescapa quaisquer caracteres que tenham escape no JSON. Aqui está um exemplo que mostra como procurar uma propriedade denominada "Name":

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/ValueTextEqualsExample.cs" id="DefineUtf8Var":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/ValueTextEqualsExample.cs" id="UseUtf8Var" highlight="9":::

### <a name="read-null-values-into-nullable-value-types"></a>Ler valores nulos em tipos de valores anuláveis

`Newtonsoft.Json` fornece APIs que retornam <xref:System.Nullable%601> , como `ReadAsBoolean` , que lidam com a `Null` `TokenType` para você retornando um `bool?` . As `System.Text.Json` APIs internas retornam apenas tipos de valores não anuláveis. Por exemplo, <xref:System.Text.Json.Utf8JsonReader.GetBoolean%2A?displayProperty=nameWithType> retorna um `bool` . Ele lançará uma exceção se encontrar `Null` no JSON. Os exemplos a seguir mostram duas maneiras de lidar com nulos, um retornando um tipo de valor anulável e um retornando o valor padrão:

```csharp
public bool? ReadAsNullableBoolean()
{
    _reader.Read();
    if (_reader.TokenType == JsonTokenType.Null)
    {
        return null;
    }
    if (_reader.TokenType != JsonTokenType.True && _reader.TokenType != JsonTokenType.False)
    {
        throw new JsonException();
    }
    return _reader.GetBoolean();
}
```

```csharp
public bool ReadAsBoolean(bool defaultValue)
{
    _reader.Read();
    if (_reader.TokenType == JsonTokenType.Null)
    {
        return defaultValue;
    }
    if (_reader.TokenType != JsonTokenType.True && _reader.TokenType != JsonTokenType.False)
    {
        throw new JsonException();
    }
    return _reader.GetBoolean();
}
```

### <a name="multi-targeting"></a>Multiplataforma

Se você precisar continuar a usar `Newtonsoft.Json` para determinadas estruturas de destino, você pode ter vários destinos e ter duas implementações. No entanto, isso não é trivial e exigiria uma `#ifdefs` duplicação de origem. Uma maneira de compartilhar o máximo de código possível é criar um `ref struct` wrapper em volta de `Utf8JsonReader` e `Newtonsoft.Json` `JsonTextReader` . Esse wrapper unificaria a área de superfície pública ao isolar as diferenças comportamentais. Isso permite isolar as alterações principalmente na construção do tipo, juntamente com a passagem do novo tipo por referência. Esse é o padrão que a biblioteca [Microsoft. Extensions. DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/3.1.0/) segue:

* [UnifiedJsonReader.JsonTextReader.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonReader.JsonTextReader.cs)
* [UnifiedJsonReader.Utf8JsonReader.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonReader.Utf8JsonReader.cs)

## <a name="utf8jsonwriter-compared-to-jsontextwriter"></a>Utf8JsonWriter em comparação com JsonTextWriter

<xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> é uma maneira de alto desempenho para escrever texto JSON codificado em UTF-8 de tipos comuns do .NET como `String` , `Int32` e `DateTime` . O gravador é um tipo de baixo nível que pode ser usado para criar serializadores personalizados.

As seções a seguir explicam os padrões de programação recomendados para o uso do `Utf8JsonWriter` .

### <a name="write-with-utf-8-text"></a>Gravar com texto UTF-8

Para obter o melhor desempenho possível ao usar o `Utf8JsonWriter` , grave as cargas JSON já codificadas como texto UTF-8, e não como cadeias de caracteres UTF-16. Use <xref:System.Text.Json.JsonEncodedText> para armazenar em cache e codificar previamente nomes de propriedade de cadeia de caracteres e valores como estáticos e passá-los para o gravador, em vez de usar literais de cadeia de caracteres UTF-16. Isso é mais rápido do que armazenar em cache e usar matrizes de bytes UTF-8.

Essa abordagem também funcionará se você precisar fazer escapes personalizados. `System.Text.Json` Não permite desabilitar o escape durante a gravação de uma cadeia de caracteres. No entanto, você pode passar seu próprio personalizado <xref:System.Text.Encodings.Web.JavaScriptEncoder> como uma opção para o gravador, ou criar seu próprio `JsonEncodedText` que usa o `JavascriptEncoder` para fazer a saída e, em seguida, escrever o `JsonEncodedText` em vez da cadeia de caracteres. Para obter mais informações, consulte [Personalizar codificação de caracteres](system-text-json-character-encoding.md).

### <a name="write-raw-values"></a>Gravar valores brutos

O `Newtonsoft.Json` `WriteRawValue` método grava JSON bruto onde um valor é esperado. <xref:System.Text.Json> Não tem equivalente direto, mas aqui está uma solução alternativa que garante que apenas JSON válido seja gravado:

```csharp
using JsonDocument doc = JsonDocument.Parse(string);
doc.WriteTo(writer);
```

### <a name="customize-character-escaping"></a>Personalizar a saída de caracteres

A configuração [StringEscapeHandling](https://www.newtonsoft.com/json/help/html/T_Newtonsoft_Json_StringEscapeHandling.htm) de `JsonTextWriter` oferece opções para escapar de todos os caracteres não ASCII **ou** caracteres HTML. Por padrão, o `Utf8JsonWriter` escapa todos os caracteres não ASCII **e** HTML. Essa saída é feita para motivos de segurança de defesa intensa. Para especificar uma política de saída diferente, crie um <xref:System.Text.Encodings.Web.JavaScriptEncoder> e defina <xref:System.Text.Json.JsonWriterOptions.Encoder?displayProperty=nameWithType> . Para obter mais informações, consulte [Personalizar codificação de caracteres](system-text-json-character-encoding.md).

### <a name="customize-json-format"></a>Personalizar o formato JSON

`JsonTextWriter` inclui as seguintes configurações, para as quais `Utf8JsonWriter` não tem equivalente:

* [Recuo](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_Indentation.htm) – especifica o número de caracteres a serem recuados. `Utf8JsonWriter` sempre faz recuo de 2 caracteres.
* [IndentChar](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_IndentChar.htm) -especifica o caractere a ser usado para recuo.  `Utf8JsonWriter` sempre usa espaço em branco.
* [QuoteChar](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_QuoteChar.htm) -especifica o caractere a ser usado para envolver valores de cadeia de caracteres.  `Utf8JsonWriter` sempre usa aspas duplas.
* [QUOTENAME](https://www.newtonsoft.com/json/help/html/P_Newtonsoft_Json_JsonTextWriter_QuoteName.htm) – especifica se os nomes de propriedade devem ser circundados com aspas.  `Utf8JsonWriter` sempre circunda-os com aspas.

Não há soluções alternativas que permitam personalizar o JSON produzido por `Utf8JsonWriter` essas maneiras.

### <a name="write-null-values"></a>Gravar valores nulos

Para gravar valores nulos usando `Utf8JsonWriter` , chame:

* <xref:System.Text.Json.Utf8JsonWriter.WriteNull%2A> para gravar um par chave-valor com NULL como o valor.
* <xref:System.Text.Json.Utf8JsonWriter.WriteNullValue%2A> para gravar NULL como um elemento de uma matriz JSON.

Para uma propriedade de cadeia de caracteres, se a cadeia de caracteres for nula e <xref:System.Text.Json.Utf8JsonWriter.WriteString%2A> <xref:System.Text.Json.Utf8JsonWriter.WriteStringValue%2A> for equivalente a `WriteNull` e `WriteNullValue` .

### <a name="write-timespan-uri-or-char-values"></a>Gravar valores de TimeSpan, URI ou Char

`JsonTextWriter` fornece `WriteValue` métodos para valores de [TimeSpan](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_18.htm), [URI](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_22.htm)e [Char](https://www.newtonsoft.com/json/help/html/M_Newtonsoft_Json_JsonTextWriter_WriteValue_3.htm) . `Utf8JsonWriter` Não tem métodos equivalentes. Em vez disso, formate esses valores como cadeias de caracteres (chamando `ToString()` , por exemplo) e chame <xref:System.Text.Json.Utf8JsonWriter.WriteStringValue%2A> .

### <a name="multi-targeting"></a>Multiplataforma

Se você precisar continuar a usar `Newtonsoft.Json` para determinadas estruturas de destino, você pode ter vários destinos e ter duas implementações. No entanto, isso não é trivial e exigiria uma `#ifdefs` duplicação de origem. Uma maneira de compartilhar o máximo de código possível é criar um wrapper em volta de `Utf8JsonWriter` e `Newtonsoft` `JsonTextWriter` . Esse wrapper unificaria a área de superfície pública ao isolar as diferenças comportamentais. Isso permite isolar as alterações principalmente na construção do tipo. A biblioteca [Microsoft. Extensions. DependencyModel](https://www.nuget.org/packages/Microsoft.Extensions.DependencyModel/3.1.0/) segue:

* [UnifiedJsonWriter.JsonTextWriter.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonWriter.JsonTextWriter.cs)
* [UnifiedJsonWriter.Utf8JsonWriter.cs](https://github.com/dotnet/runtime/blob/81bf79fd9aa75305e55abe2f7e9ef3f60624a3a1/src/installer/managed/Microsoft.Extensions.DependencyModel/UnifiedJsonWriter.Utf8JsonWriter.cs)

## <a name="typenamehandlingall-not-supported"></a>TypeNameHandling. All sem suporte

A decisão de excluir `TypeNameHandling.All` a funcionalidade equivalente do `System.Text.Json` era intencional. Permitir que um conteúdo JSON especifique suas próprias informações de tipo é uma fonte comum de vulnerabilidades em aplicativos Web. Em particular, a configuração do `Newtonsoft.Json` com `TypeNameHandling.All` permite que o cliente remoto incorpore um aplicativo executável inteiro na própria carga JSON, de modo que durante a desserialização, o aplicativo Web extrai e executa o código inserido. Para obter mais informações, confira [sexta-feira os ataques JSON 13 PowerPoint](https://www.blackhat.com/docs/us-17/thursday/us-17-Munoz-Friday-The-13th-Json-Attacks.pdf) e [sexta-feira aos detalhes dos ataques JSON 13](https://www.blackhat.com/docs/us-17/thursday/us-17-Munoz-Friday-The-13th-JSON-Attacks-wp.pdf).

## <a name="additional-resources"></a>Recursos adicionais

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
* [Personalizar codificação de caracteres](system-text-json-character-encoding.md)
* [Escrever serializadores personalizados e desserializadores](write-custom-serializer-deserializer.md)
* [Gravar conversores personalizados para serialização JSON](system-text-json-converters-how-to.md)
* [Suporte a DateTime e DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
* [System.Text.Json. Referência de API de serialização](xref:System.Text.Json.Serialization)
