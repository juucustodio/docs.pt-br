---
title: Tipos de coleção com suporte no System.Text.Json
description: Saiba quais tipos de coleção têm suporte para serialização pelas APIs no System.Text.Json namespace.
ms.date: 02/01/2021
no-loc:
- System.Text.Json
ms.topic: reference
zone_pivot_groups: dotnet-version
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: 5a5016c70e86124510a4778aafb9fb14b1890add
ms.sourcegitcommit: 4df8e005c074ceb1f978f007b222fe253be2baf3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99547649"
---
# <a name="supported-collection-types-in-systemtextjson"></a>Tipos de coleção com suporte no System.Text.Json

Este artigo fornece uma visão geral de quais coleções têm suporte para serialização e desserialização. <xref:System.Text.Json.JsonSerializer?displayProperty=nameWithType> oferece suporte a um tipo de coleção para serialização se:

* Deriva de <xref:System.Collections.IEnumerable>.
* Contém elementos que são serializáveis.

O serializador chama o <xref:System.Collections.IEnumerable.GetEnumerator> método e grava os elementos.

A desserialização é mais complicada e não tem suporte para alguns tipos de coleção.

As seções a seguir são organizadas por namespace e mostram quais tipos têm suporte para serialização e desserialização.

## <a name="systemarray-namespace"></a>Namespace System. array

| Tipo                                                                                            | Serialização | Desserialização |
|-------------------------------------------------------------------------------------------------|---------------|-----------------|
| [Matrizes unidimensionais](../../csharp/programming-guide/arrays/single-dimensional-arrays.md) | ✔️           | ✔️              |
| [Matrizes multidimensionais](../../csharp/programming-guide/arrays/multidimensional-arrays.md)    | ❌           | ❌              |
| [Matrizes denteadas](../../csharp/programming-guide/arrays/jagged-arrays.md)                         | ✔️           | ✔️              |

## <a name="systemcollections-namespace"></a>Namespace System.Collections

| Tipo                                      | Serialização | Desserialização |
|-------------------------------------------|---------------|-----------------|
| <xref:System.Collections.ArrayList>       | ✔️           | ✔️              |
| <xref:System.Collections.BitArray>        | ✔️           | ❌              |
| <xref:System.Collections.DictionaryEntry> | ✔️           | ✔️              |
| <xref:System.Collections.Hashtable>       | ✔️           | ✔️              |
| <xref:System.Collections.Queue>           | ✔️           | ✔️              |
| <xref:System.Collections.SortedList>      | ✔️           | ✔️              |
| <xref:System.Collections.Stack>           | ✔️           | ✔️              |
| <xref:System.Collections.ICollection>     | ✔️           | ✔️              |
| <xref:System.Collections.IDictionary>     | ✔️           | ✔️              |
| <xref:System.Collections.IEnumerable>     | ✔️           | ✔️              |
| <xref:System.Collections.IList>           | ✔️           | ✔️              |

## <a name="systemcollectionsgeneric-namespace"></a>Namespace System.Collections.Generic

::: zone pivot="dotnet-5-0"

| Tipo                                                      | Serialização | Desserialização |
|-----------------------------------------------------------|---------------|-----------------|
| <xref:System.Collections.Generic.Dictionary%602> \*       | ✔️           | ✔️              |
| <xref:System.Collections.Generic.HashSet%601>             | ✔️           | ✔️              |
| <xref:System.Collections.Generic.KeyValuePair%602>        | ✔️           | ✔️              |
| <xref:System.Collections.Generic.LinkedList%601>          | ✔️           | ✔️              |
| <xref:System.Collections.Generic.LinkedListNode%601>      | ✔️           | ❌              |
| <xref:System.Collections.Generic.List%601>                | ✔️           | ✔️              |
| <xref:System.Collections.Generic.Queue%601>               | ✔️           | ✔️              |
| <xref:System.Collections.Generic.SortedDictionary%602> \* | ✔️           | ✔️              |
| <xref:System.Collections.Generic.SortedList%602> \*       | ✔️           | ✔️              |
| <xref:System.Collections.Generic.SortedSet%601>           | ✔️           | ✔️              |
| <xref:System.Collections.Generic.Stack%601>               | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IAsyncEnumerable%601>    | ❌           | ❌              |
| <xref:System.Collections.Generic.ICollection%601>         | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IDictionary%602> \*      | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IEnumerable%601>         | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IList%601>               | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IReadOnlyCollection%601> | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IReadOnlyDictionary%602> \* | ✔️        | ✔️              |
| <xref:System.Collections.Generic.IReadOnlyList%601>       | ✔️           | ✔️              |
| <xref:System.Collections.Generic.ISet%601>                | ✔️           | ✔️              |

::: zone-end

::: zone pivot="dotnet-core-3-1"

| Tipo                                                                                            | Serialização | Desserialização |
|-------------------------------------------------------------------------------------------------|---------------|-----------------|
| [Dicionário \<string, TValue> ](xref:System.Collections.Generic.Dictionary%602) do\*                | ✔️           | ✔️              |
| <xref:System.Collections.Generic.HashSet%601>                                                   | ✔️           | ✔️              |
| <xref:System.Collections.Generic.KeyValuePair%602>                                              | ✔️           | ✔️              |
| <xref:System.Collections.Generic.LinkedList%601>                                                | ✔️           | ✔️              |
| <xref:System.Collections.Generic.LinkedListNode%601>                                            | ✔️           | ❌              |
| <xref:System.Collections.Generic.List%601>                                                      | ✔️           | ✔️              |
| <xref:System.Collections.Generic.Queue%601>                                                     | ✔️           | ✔️              |
| [SortedDictionary \<string, TValue> ](xref:System.Collections.Generic.SortedDictionary%602)\*    | ✔️           | ✔️              |
| [ \<string, TValue> Classificadolist](xref:System.Collections.Generic.SortedList%602)\*                | ✔️           | ✔️              |
| <xref:System.Collections.Generic.SortedSet%601>                                                 | ✔️           | ✔️              |
| <xref:System.Collections.Generic.Stack%601>                                                     | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IAsyncEnumerable%601>                                          | ❌           | ❌              |
| <xref:System.Collections.Generic.ICollection%601>                                               | ✔️           | ✔️              |
| [IDictionary\<string, TValue> ](xref:System.Collections.Generic.IDictionary%602) \*              | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IEnumerable%601>                                               | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IList%601>                                                     | ✔️           | ✔️              |
| <xref:System.Collections.Generic.IReadOnlyCollection%601>                                       | ✔️           | ✔️              |
| [IReadOnlyDictionary \<string, TValue> ](xref:System.Collections.Generic.IReadOnlyDictionary%602)\* | ✔️        | ✔️              |
| <xref:System.Collections.Generic.IReadOnlyList%601>                                             | ✔️           | ✔️              |
| <xref:System.Collections.Generic.ISet%601>                                                      | ✔️           | ✔️              |

::: zone-end

\* Consulte [tipos de chave com suporte](#supported-key-types).

## <a name="systemcollectionsimmutable-namespace"></a>Namespace System. Collections. imutável

::: zone pivot="dotnet-5-0"

| Tipo                                                              | Serialização | Desserialização |
|-------------------------------------------------------------------|---------------|-----------------|
| <xref:System.Collections.Immutable.ImmutableArray%601>            | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.ImmutableDictionary%602> \*\*  | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.ImmutableHashSet%601>          | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableList%601>            | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.ImmutableQueue%601>            | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.ImmutableSortedDictionary%602> \*\* | ✔️      | ✔️              |
| <xref:System.Collections.Immutable.ImmutableSortedSet%601>        | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.ImmutableStack%601> \*         | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableDictionary%602> \*\* | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableList%601>            | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableQueue%601>           | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableSet%601>             | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableStack%601> \*        | ✔️           | ✔️              |

::: zone-end

::: zone pivot="dotnet-core-3-1"

| Tipo                                                                                                          | Serialização | Desserialização |
|---------------------------------------------------------------------------------------------------------------|---------------|-----------------|
| <xref:System.Collections.Immutable.ImmutableArray%601>                                                        | ✔️           | ✔️              |
| [ImmutableDictionary \<string, TValue> ](xref:System.Collections.Immutable.ImmutableDictionary%602)\*\*        | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.ImmutableHashSet%601>                                                      | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableList%601>                                                        | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.ImmutableQueue%601>                                                        | ✔️           | ✔️              |
| [ImmutableSortedDictionary \<string, TValue> ](xref:System.Collections.Immutable.ImmutableSortedDictionary%602)\*\*| ✔️       | ✔️              |
| <xref:System.Collections.Immutable.ImmutableSortedSet%601>                                                    | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.ImmutableStack%601> \*                                                     | ✔️           | ✔️              |
| [IImmutableDictionary \<string, TValue> ](xref:System.Collections.Immutable.IImmutableDictionary%602)\*\*      | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableList%601>                                                        | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableQueue%601>                                                       | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableSet%601>                                                         | ✔️           | ✔️              |
| <xref:System.Collections.Immutable.IImmutableStack%601> \*                                                    | ✔️           | ✔️              |

::: zone-end

\*Consulte [dar suporte à viagem de \<T> ida e volta para a pilha](system-text-json-converters-how-to.md#support-round-trip-for-stackt).

\*\* Consulte [tipos de chave com suporte](#supported-key-types).

## <a name="systemcollectionsspecialized-namespace"></a>Namespace System.Collections.Specialized

| Tipo                                                      | Serialização | Desserialização |
|-----------------------------------------------------------|---------------|-----------------|
| <xref:System.Collections.Specialized.BitVector32>         | ✔️           | ❌\*            |
| <xref:System.Collections.Specialized.HybridDictionary>    | ✔️           | ✔️              |
| <xref:System.Collections.Specialized.IOrderedDictionary>  | ✔️           | ❌              |
| <xref:System.Collections.Specialized.ListDictionary>      | ✔️           | ✔️              |
| <xref:System.Collections.Specialized.StringCollection>    | ✔️           | ❌              |
| <xref:System.Collections.Specialized.StringDictionary>    | ✔️           | ❌              |
| <xref:System.Collections.Specialized.NameValueCollection> | ✔️           | ❌              |

\* Quando <xref:System.Collections.Specialized.BitVector32> é desserializado, a <xref:System.Collections.Specialized.BitVector32.Data> propriedade é ignorada porque não tem um setter público. Nenhuma exceção é gerada.

## <a name="systemcollectionsconcurrent-namespace"></a>Namespace System.Collections.Concurrent

::: zone pivot="dotnet-5-0"

| Tipo                                                          | Serialização | Desserialização |
|---------------------------------------------------------------|---------------|-----------------|
| <xref:System.Collections.Concurrent.BlockingCollection%601>   | ✔️           | ❌              |
| <xref:System.Collections.Concurrent.ConcurrentBag%601>        | ✔️           | ❌              |
| <xref:System.Collections.Concurrent.ConcurrentDictionary%602> \*\* | ✔️      | ✔️              |
| <xref:System.Collections.Concurrent.ConcurrentQueue%601>      | ✔️           | ✔️              |
| <xref:System.Collections.Concurrent.ConcurrentStack%601> \*   | ✔️           | ✔️              |

::: zone-end

::: zone pivot="dotnet-core-3-1"

| Tipo                                                        | Serialização | Desserialização |
|-------------------------------------------------------------|---------------|-----------------|
| <xref:System.Collections.Concurrent.BlockingCollection%601> | ✔️           | ❌              |
| <xref:System.Collections.Concurrent.ConcurrentBag%601>      | ✔️           | ❌              |
| [ConcurrentDictionary \<string, TValue> ](xref:System.Collections.Concurrent.ConcurrentDictionary%602)\*\* |✔️|✔️|
| <xref:System.Collections.Concurrent.ConcurrentQueue%601>    | ✔️           | ✔️              |
| <xref:System.Collections.Concurrent.ConcurrentStack%601> \* | ✔️           | ✔️              |

::: zone-end

\*Consulte [dar suporte à viagem de \<T> ida e volta para a pilha](system-text-json-converters-how-to.md#support-round-trip-for-stackt).

\*\* Consulte [tipos de chave com suporte](#supported-key-types).

## <a name="systemcollectionsobjectmodel-namespace"></a>Namespace System.Collections.ObjectModel

::: zone pivot="dotnet-5-0"

| Tipo                                                           | Serialização | Desserialização |
|----------------------------------------------------------------|---------------|-----------------|
| <xref:System.Collections.ObjectModel.Collection%601>           | ✔️            | ✔️             |
| [ \<string, TValue> Chaveid](xref:System.Collections.ObjectModel.KeyedCollection%602)\* |✔️|❌|
| <xref:System.Collections.ObjectModel.ObservableCollection%601> | ✔️            | ✔️             |
| <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>   | ✔️            | ❌             |
| <xref:System.Collections.ObjectModel.ReadOnlyDictionary%602>   | ✔️            | ❌             |
| <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601> | ✔️    | ❌             |

\* Não há `string` suporte para chaves.

::: zone-end

::: zone pivot="dotnet-core-3-1"

| Tipo                                                           | Serialização | Desserialização |
|----------------------------------------------------------------|---------------|-----------------|
| <xref:System.Collections.ObjectModel.Collection%601>           | ✔️            | ✔️             |
| [ \<string, TValue> Chaveid](xref:System.Collections.ObjectModel.KeyedCollection%602)\* |✔️|❌|
| <xref:System.Collections.ObjectModel.ObservableCollection%601> | ✔️            | ✔️             |
| <xref:System.Collections.ObjectModel.ReadOnlyCollection%601>   | ✔️            | ❌             |
| [ReadOnlyDictionary \<string, TValue> ](xref:System.Collections.ObjectModel.ReadOnlyDictionary%602)\* |✔️|❌|
| <xref:System.Collections.ObjectModel.ReadOnlyObservableCollection%601>| ✔️     | ❌             |

\* Consulte [tipos de chave com suporte](#supported-key-types).

::: zone-end

## <a name="custom-collections"></a>Coleções personalizadas

Qualquer tipo de coleção que não esteja em um dos namespaces anteriores é considerado uma coleção personalizada. Esses tipos incluem tipos definidos pelo usuário e tipos definidos por ASP.NET Core. Por exemplo, <xref:Microsoft.Extensions.Primitives?displayProperty=fullName> está nesse grupo.

Todas as coleções personalizadas (tudo que deriva de `IEnumerable` ) têm suporte para serialização, contanto que seus tipos de elementos tenham suporte.

### <a name="custom-collections-with-deserialization-support"></a>Coleções personalizadas com suporte à desserialização

Uma coleção personalizada tem suporte para desserialização se:

::: zone pivot="dotnet-5-0"

* Não é uma interface ou abstrata.
* Tem um construtor sem parâmetros.
* Contém tipos de elementos que são suportados pelo <xref:System.Text.Json.JsonSerializer> .
* Implementa ou herda uma ou mais das seguintes interfaces ou classes:
  * <xref:System.Collections.Concurrent.ConcurrentQueue%601>
  * <xref:System.Collections.Concurrent.ConcurrentStack%601> \*
  * <xref:System.Collections.Generic.ICollection%601>
  * <xref:System.Collections.IDictionary>
  * <xref:System.Collections.Generic.IDictionary%602> \*\*
  * <xref:System.Collections.IList>
  * <xref:System.Collections.Generic.IList%601>
  * <xref:System.Collections.Queue>
  * <xref:System.Collections.Generic.Queue%601>
  * <xref:System.Collections.Stack> \*
  * <xref:System.Collections.Generic.Stack%601> \*

::: zone-end

::: zone pivot="dotnet-core-3-1"

* Não é uma interface ou abstrata.
* Tem um construtor sem parâmetros.
* Contém tipos de elementos que são suportados pelo <xref:System.Text.Json.JsonSerializer> .
* Implementa ou herda uma ou mais das seguintes interfaces ou classes:
  * <xref:System.Collections.Concurrent.ConcurrentQueue%601>
  * <xref:System.Collections.Concurrent.ConcurrentStack%601> \*
  * <xref:System.Collections.Generic.ICollection%601>
  * <xref:System.Collections.IDictionary>
  * [IDictionary\<string, TValue>](xref:System.Collections.Generic.IDictionary%602) \* \*
  * <xref:System.Collections.IList>
  * <xref:System.Collections.Generic.IList%601>
  * <xref:System.Collections.Queue>
  * <xref:System.Collections.Generic.Queue%601>
  * <xref:System.Collections.Stack> \*
  * <xref:System.Collections.Generic.Stack%601> \*

::: zone-end

  \*Consulte [dar suporte à viagem de \<T> ida e volta para a pilha](system-text-json-converters-how-to.md#support-round-trip-for-stackt).

  \*\* Consulte [tipos de chave com suporte](#supported-key-types).

### <a name="custom-collections-with-known-issues"></a>Coleções personalizadas com problemas conhecidos

Há problemas conhecidos com as seguintes coleções personalizadas:

- <xref:System.Dynamic.ExpandoObject>: Consulte [dotnet/tempo de execução # 29690](https://github.com/dotnet/runtime/issues/29690).
- <xref:System.Dynamic.DynamicObject>: Consulte [dotnet/tempo de execução # 1808](https://github.com/dotnet/runtime/issues/1808).
- <xref:System.Data.DataTable>: Consulte [dotnet/docs # 21366](https://github.com/dotnet/docs/issues/21366).
- <xref:Microsoft.AspNetCore.Http.FormFile?displayProperty=fullName>: Consulte [dotnet/tempo de execução # 1559](https://github.com/dotnet/runtime/issues/1559).
- <xref:Microsoft.AspNetCore.Http.IFormCollection?displayProperty=fullName>: Consulte [dotnet/tempo de execução # 1559](https://github.com/dotnet/runtime/issues/1559).

Para obter mais informações sobre problemas conhecidos, consulte os [problemas em System.Text.Json aberto em ](https://github.com/dotnet/runtime/issues?q=is%3Aopen+is%3Aissue+label%3Aarea-System.Text.Json).

## <a name="supported-key-types"></a>Tipos de chave com suporte

::: zone pivot="dotnet-5-0"

Os tipos com suporte para as chaves de `Dictionary` e `SortedList` tipos incluem o seguinte:

* `Boolean`
* `Byte`
* `DateTime`
* `DateTimeOffset`
* `Decimal`
* `Double`
* `Enum`
* `Guid`
* `Int16`
* `Int32`
* `Int64`
* `Object` (Somente na serialização e se o tipo de tempo de execução for um dos tipos com suporte nesta lista.)
* `SByte`
* `Single`
* `String`
* `UInt16`
* `UInt32`
* `UInt64`

::: zone-end

::: zone pivot="dotnet-core-3-1"

\*\* Não `string` há suporte para os tipos e não-chaves `Dictionary` `SortedList` no .NET Core 3,1.

::: zone-end

## <a name="see-also"></a>Confira também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Instanciar instâncias JsonSerializerOptions](system-text-json-configure-options.md)
* [Habilitar a correspondência sem diferenciação de maiúsculas e minúsculas](system-text-json-character-casing.md)
* [Personalizar nomes e valores da propriedade](system-text-json-customize-properties.md)
* [Ignorar propriedades](system-text-json-ignore-properties.md)
* [Permitir JSON inválido](system-text-json-invalid-json.md)
* [Manipular JSON de estouro](system-text-json-handle-overflow.md)
* [Preservar referências](system-text-json-preserve-references.md)
* [Tipos imutáveis e acessadores não públicos](system-text-json-immutability.md)
* [Serialização polimórfica](system-text-json-polymorphism.md)
* [Migrar do Newtonsoft.Jspara o System.Text.Json](system-text-json-migrate-from-newtonsoft-how-to.md)
* [Personalizar codificação de caracteres](system-text-json-character-encoding.md)
* [Escrever serializadores personalizados e desserializadores](write-custom-serializer-deserializer.md)
* [Gravar conversores personalizados para serialização JSON](system-text-json-converters-how-to.md)
* [Suporte a DateTime e DateTimeOffset](../datetime/system-text-json-support.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
* [System.Text.Json. Referência de API de serialização](xref:System.Text.Json.Serialization)
