---
title: Como criar uma instância de JsonSerializerOptions com System.Text.Json
description: Saiba como evitar problemas de desempenho e como usar construtores disponíveis para instâncias de JsonSerializerOptions.
ms.date: 12/02/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 5f32e1369e58dd9550f28abc822f187dee46c022
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009827"
---
# <a name="how-to-instantiate-jsonserializeroptions-instances-with-no-locsystemtextjson"></a>Como instanciar instâncias JsonSerializerOptions com System.Text.Json

Este artigo explica como evitar problemas de desempenho ao usar o <xref:System.Text.Json.JsonSerializerOptions> . Ele também mostra como usar os construtores com parâmetros que estão disponíveis.

## <a name="reuse-jsonserializeroptions-instances"></a>Reutilizar instâncias JsonSerializerOptions

Se você usar `JsonSerializerOptions` repetidamente com as mesmas opções, não crie uma nova `JsonSerializerOptions` instância toda vez que usá-la. Reutilize a mesma instância para cada chamada. Esta orientação se aplica ao código que você escreve para conversores personalizados e quando você chama <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> ou <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> .

O código a seguir demonstra a penalidade de desempenho para usar novas instâncias de opções.

:::code language="csharp" source="snippets/system-text-json-configure-options/csharp/ReuseOptionsInstances.cs":::

O código anterior serializa um objeto pequeno 100.000 vezes usando a mesma instância de opções. Em seguida, ele serializa o mesmo objeto, o mesmo número de vezes, e cria uma nova instância de opções a cada vez. Uma diferença típica de tempo de execução é 190 em comparação com 40.140 milissegundos. A diferença é ainda maior se você aumentar o número de iterações.

O serializador passa por uma fase de aquecimento durante a primeira serialização de cada tipo no grafo do objeto quando uma nova instância de opções é passada para ele. Esse aquecimento inclui a criação de um cache de metadados que são necessários para a serialização. Os metadados incluem delegados para getters de propriedade, setters, argumentos de construtor, atributos especificados e assim por diante. Esse cache de metadados é armazenado na instância de opções. O mesmo processo e cache de aquecimento aplica-se à desserialização.

O tamanho do cache de metadados em uma `JsonSerializerOptions` instância depende do número de tipos a serem serializados. Se você passar por vários tipos — por exemplo, tipos gerados dinamicamente — para o serializador, o tamanho do cache continuará crescendo e poderá acabar causando um `OutOfMemoryException` .

## <a name="copy-jsonserializeroptions"></a>Copiar JsonSerializerOptions

::: zone pivot="dotnet-5-0"
Há um [Construtor JsonSerializerOptions] (xref: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerOptions)) que permite criar uma nova instância com as mesmas opções de uma instância existente, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/CopyOptions.cs" highlight="29":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
Um `JsonSerializerOptions` Construtor que usa uma instância existente não está disponível no .NET Core 3,1.
::: zone-end

## <a name="web-defaults-for-jsonserializeroptions"></a>Padrões da Web para JsonSerializerOptions

::: zone pivot="dotnet-5-0"
Aqui estão as opções que têm padrões diferentes para aplicativos Web:

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>
* <xref:System.Text.Json.JsonSerializerOptions.NumberHandling%2A> = <xref:System.Text.Json.Serialization.JsonNumberHandling.AllowReadingFromString>

Há um [Construtor JsonSerializerOptions] (xref: System.Text.Json . JsonSerializerOptions .% 23ctor ( System.Text.Json . JsonSerializerDefaults)? View = NET-5,0&preserve-View = true) que permite criar uma nova instância com as opções padrão que ASP.NET Core usa para aplicativos Web, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/system-text-json-how-to-5-0/csharp/OptionsDefaults.cs" highlight="24":::
::: zone-end

::: zone pivot="dotnet-core-3-1"
Aqui estão as opções que têm padrões diferentes para aplicativos Web:

* <xref:System.Text.Json.JsonSerializerOptions.PropertyNameCaseInsensitive%2A> = `true`
* <xref:System.Text.Json.JsonNamingPolicy> = <xref:System.Text.Json.JsonNamingPolicy.CamelCase>

Um `JsonSerializerOptions` Construtor que especifica um conjunto de padrões não está disponível no .NET Core 3,1.
::: zone-end

## <a name="see-also"></a>Confira também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Como serializar e desserializar JSON](system-text-json-how-to.md)
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
* [Gravar conversores personalizados para serialização JSON](system-text-json-converters-how-to.md)
* [Suporte a DateTime e DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
* [System.Text.Json. Referência de API de serialização](xref:System.Text.Json.Serialization)
