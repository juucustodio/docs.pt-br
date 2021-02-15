---
title: Como usar tipos imutáveis e acessadores não públicos com System.Text.Json
description: Saiba como usar tipos imutáveis e acessadores não públicos ao serializar e desserializar de JSON no .NET.
ms.date: 02/08/2021
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 9fe1e6e96703ba404308c758eca49be6e196ad61
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100438158"
---
# <a name="how-to-use-immutable-types-and-non-public-accessors-with-systemtextjson"></a>Como usar tipos imutáveis e acessadores não públicos com System.Text.Json

Este artigo mostra como usar tipos imutáveis, construtores com parâmetros públicos e acessadores não públicos com o `System.Text.Json` namespace.

## <a name="immutable-types-and-records"></a>Tipos e registros imutáveis

::: zone pivot="dotnet-5-0"
`System.Text.Json` pode usar um construtor com parâmetros públicos, o que torna possível desserializar uma classe ou estrutura imutável. Para uma classe, se o único Construtor for um parametrizado, esse construtor será usado. Para uma struct ou uma classe com vários construtores, especifique o que deve ser usado aplicando o atributo [[JsonConstructor]](xref:System.Text.Json.Serialization.JsonConstructorAttribute) . Quando o atributo não é usado, um construtor público sem parâmetros é sempre usado, se estiver presente. O atributo só pode ser usado com construtores públicos. O exemplo a seguir usa o `[JsonConstructor]` atributo:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/ImmutableTypes.cs" highlight="13":::

Os nomes de parâmetro de um construtor com parâmetros devem corresponder aos nomes de propriedade. A correspondência não diferencia maiúsculas de minúsculas e o parâmetro do construtor deve corresponder ao nome real da propriedade mesmo se você usar [[JsonPropertyName]](xref:System.Text.Json.Serialization.JsonPropertyNameAttribute) para renomear uma propriedade. No exemplo a seguir, o nome da `TemperatureC` propriedade é alterado para `celsius` no JSON, mas o parâmetro do Construtor ainda é nomeado `temperatureC` :

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/ImmutableTypesCtorParms.cs" highlight="10,14-16":::

Além `[JsonPropertyName]` dos atributos a seguir, há suporte para desserialização com construtores com parâmetros:

* [[Jsonconverter]](xref:System.Text.Json.Serialization.JsonConverterAttribute)
* [[JsonIgnore]](xref:System.Text.Json.Serialization.JsonIgnoreAttribute)
* [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute)
* [[JsonNumberHandling]](xref:System.Text.Json.Serialization.JsonNumberHandlingAttribute)

Também há suporte para registros no C# 9, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/Records.cs":::

Para tipos que são imutáveis porque todos os seus setters de propriedade são não públicos, consulte a seção a seguir sobre [acessadores de propriedade não pública](#non-public-property-accessors).
::: zone-end

::: zone pivot="dotnet-core-3-1"
`JsonConstructorAttribute` e o suporte a registros do C# 9 não está disponível no .NET Core 3,1.
::: zone-end

## <a name="non-public-property-accessors"></a>Acessadores de propriedade não pública

::: zone pivot="dotnet-5-0"
Para habilitar o uso de um acessador de propriedade não público, use o atributo [[JsonInclude]](xref:System.Text.Json.Serialization.JsonIncludeAttribute) , conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/NonPublicAccessors.cs" highlight="12,15":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
Não há suporte para acessadores de propriedade não pública no .NET Core 3,1. Para obter mais informações, consulte [o Newtonsoft.Json artigo migrar de](system-text-json-migrate-from-newtonsoft-how-to.md#non-public-property-setters-and-getters).
::: zone-end

## <a name="see-also"></a>Consulte também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Como serializar e desserializar JSON](system-text-json-how-to.md)
* [Instanciar instâncias JsonSerializerOptions](system-text-json-configure-options.md)
* [Habilitar a correspondência sem diferenciação de maiúsculas e minúsculas](system-text-json-character-casing.md)
* [Personalizar nomes e valores da propriedade](system-text-json-customize-properties.md)
* [Ignorar propriedades](system-text-json-ignore-properties.md)
* [Permitir JSON inválido](system-text-json-invalid-json.md)
* [Manipular JSON de estouro](system-text-json-handle-overflow.md)
* [Preservar referências](system-text-json-preserve-references.md)
* [Serialização polimórfica](system-text-json-polymorphism.md)
* [Migrar do Newtonsoft.Json para o System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Personalizar codificação de caracteres](system-text-json-character-encoding.md)
* [Escrever serializadores personalizados e desserializadores](write-custom-serializer-deserializer.md)
* [Gravar conversores personalizados para serialização JSON](system-text-json-converters-how-to.md)
* [Suporte a DateTime e DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
* [System.Text.Json. Referência de API de serialização](xref:System.Text.Json.Serialization)
