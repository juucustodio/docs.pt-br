---
title: Como personalizar a codificação de caracteres com System.Text.Json
description: Saiba como personalizar a codificação de caracteres ao serializar e desserializar do JSON no .NET.
ms.date: 01/22/2021
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 136a75ab73767fd79f99caa1d1387706ab655473
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99215973"
---
# <a name="how-to-customize-character-encoding-with-no-locsystemtextjson"></a>Como personalizar a codificação de caracteres com System.Text.Json

Por padrão, o serializador escapa todos os caracteres não ASCII. Ou seja, ele substitui por `\uxxxx` onde `xxxx` está o código Unicode do caractere. Por exemplo, se a `Summary` propriedade no JSON a seguir estiver definida como cirílico `жарко` , o `WeatherForecast` objeto será serializado, conforme mostrado neste exemplo:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "\u0436\u0430\u0440\u043A\u043E"
}
```

## <a name="serialize-language-character-sets"></a>Serializar conjuntos de caracteres de idioma

Para serializar os conjuntos de caracteres de um ou mais idiomas sem saída, especifique os [intervalos Unicode](xref:System.Text.Unicode.UnicodeRanges) ao criar uma instância do <xref:System.Text.Encodings.Web.JavaScriptEncoder?displayProperty=fullName> , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="Usings":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="LanguageSets":::

Este código não sai de escape de caracteres cirílico ou grego. Se a `Summary` propriedade for definida como cirílico `жарко` , o `WeatherForecast` objeto será serializado, conforme mostrado neste exemplo:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "жарко"
}
```

Por padrão, o codificador é inicializado com o <xref:System.Text.Unicode.UnicodeRanges.BasicLatin> intervalo.

Para serializar todos os conjuntos de idiomas sem saída, use <xref:System.Text.Unicode.UnicodeRanges.All?displayProperty=nameWithType> .

## <a name="serialize-specific-characters"></a>Serializar caracteres específicos

Uma alternativa é especificar os caracteres individuais que você deseja permitir sem ter escape. O exemplo a seguir serializa apenas os dois primeiros caracteres de `жарко` :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="Usings":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="SelectedCharacters":::

Aqui está um exemplo de JSON produzido pelo código anterior:

```json
{
  "Date": "2019-08-01T00:00:00-07:00",
  "TemperatureCelsius": 25,
  "Summary": "жа\u0440\u043A\u043E"
}
```

## <a name="block-lists"></a>Listas de bloqueios

As seções anteriores mostram como especificar as listas de permissões de pontos de código ou intervalos para os quais você não deseja ter escape. No entanto, há listas de blocos globais e específicas do codificador que podem substituir determinados pontos de código na lista de permissões. Pontos de código em uma lista de blocos são sempre de escape, mesmo que estejam incluídos na sua lista de permissões.

### <a name="global-block-list"></a>Lista de blocos globais

A lista de blocos globais inclui itens como caracteres de uso particular, caracteres de controle, pontos de código indefinidos e determinadas categorias Unicode, como a [Space_Separator categoria](https://util.unicode.org/UnicodeJsps/list-unicodeset.jsp?a=%5B:General_Category=Space_Separator:%5D), exceto `U+0020 SPACE` . Por exemplo, `U+3000 IDEOGRAPHIC SPACE` é escapado mesmo se você especificar [símbolos CJK do intervalo Unicode e pontuação (U +3000-u + 303F)](xref:System.Text.Unicode.UnicodeRanges.CjkSymbolsandPunctuation) como sua lista de permissões.

A lista de blocos global é um detalhe de implementação que foi alterado em todas as versões do .NET Core e no .NET 5. Não use uma dependência de um caractere que seja membro (ou não seja membro) da lista de blocos global.

### <a name="encoder-specific-block-lists"></a>Listas de blocos específicos do codificador

Exemplos de pontos de código bloqueados específicos do codificador incluem `'<'` e `'&'` para o [codificador HTML](xref:System.Text.Encodings.Web.HtmlEncoder), `'\'` para o [codificador JSON](xref:System.Text.Encodings.Web.JavaScriptEncoder)e `'%'` para o [codificador de URL](xref:System.Text.Encodings.Web.UrlEncoder). Por exemplo, o codificador HTML sempre escapa e comercial ( `'&'` ), mesmo que o e comercial esteja no `BasicLatin` intervalo e todos os codificadores sejam inicializados com `BasicLatin` por padrão.

## <a name="serialize-all-characters"></a>Serializar todos os caracteres

Para minimizar a saída, você pode usar <xref:System.Text.Encodings.Web.JavaScriptEncoder.UnsafeRelaxedJsonEscaping?displayProperty=nameWithType> , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="Usings":::

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/SerializeCustomEncoding.cs" id="UnsafeRelaxed":::

> [!CAUTION]
> Em comparação com o codificador padrão, o `UnsafeRelaxedJsonEscaping` codificador é mais permissivo de permitir que os caracteres passem sem escape:
>
> * Ele não sai de caracteres sensíveis a HTML, como `<` ,, `>` `&` e `'` .
> * Ele não oferece nenhuma proteção adicional de defesa profunda contra ataques XSS ou de divulgação de informações, como aqueles que podem resultar do cliente e do servidor que estão descordando no conjunto de *caracteres*.
>
> Use o codificador não seguro somente quando for conhecido que o cliente irá interpretar a carga resultante como JSON codificado em UTF-8. Por exemplo, você pode usá-lo se o servidor estiver enviando o cabeçalho de resposta `Content-Type: application/json; charset=utf-8` . Nunca permita que a `UnsafeRelaxedJsonEscaping` saída bruta seja emitida em uma página HTML ou em um `<script>` elemento.

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
* [Serialização polimórfica](system-text-json-polymorphism.md)
* [Migrar do Newtonsoft.Json para o System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Escrever serializadores personalizados e desserializadores](write-custom-serializer-deserializer.md)
* [Gravar conversores personalizados para serialização JSON](system-text-json-converters-how-to.md)
* [Suporte a DateTime e DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
* [System.Text.Json. Referência de API de serialização](xref:System.Text.Json.Serialization)
