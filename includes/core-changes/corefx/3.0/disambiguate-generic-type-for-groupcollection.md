---
ms.openlocfilehash: 97fab784acac4331894547eea27fc21b485597fb
ms.sourcegitcommit: fcbe432482464b1639decad78cc4dc8387c6269e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/12/2020
ms.locfileid: "97366861"
---
### <a name="passing-groupcollection-to-extension-methods-taking-ienumerablet-requires-disambiguation"></a>Passar GroupCollection para métodos de extensão assumindo IEnumerable \<T> requer ambiguidade

Ao chamar um método de extensão que usa um `IEnumerable<T>` em um <xref:System.Text.RegularExpressions.GroupCollection> , você deve eliminar a ambiguidade do tipo usando uma conversão.

#### <a name="change-description"></a>Descrição das alterações

A partir do .NET Core 3,0, <xref:System.Text.RegularExpressions.GroupCollection?displayProperty=nameWithType> implementa `IEnumerable<KeyValuePair<String,Group>>` -se além dos outros tipos que ele implementa, incluindo `IEnumerable<Group>` . Isso resulta em ambiguidade ao chamar um método de extensão que usa um <xref:System.Collections.Generic.IEnumerable%601> . Se você chamar esse método de extensão em uma <xref:System.Text.RegularExpressions.GroupCollection> instância, por exemplo, <xref:System.Linq.Enumerable.Count%2A?displayProperty=nameWithType> você verá o seguinte erro do compilador:

**CS1061: ' GroupCollection ' não contém uma definição para ' count ' e nenhum método de extensão acessível ' count ' aceitando um primeiro argumento do tipo ' GroupCollection ' foi encontrado (está faltando uma diretiva using ou uma referência de assembly?)**

Nas versões anteriores do .NET, não havia nenhuma ambiguidade e nenhum erro do compilador.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="reason-for-change"></a>Motivo da alteração

Essa foi uma [alteração sem intenção](https://github.com/dotnet/corefx/pull/30077). Por ter sido assim por algum tempo, não planejamos revertê-la. Além disso, essa alteração seria interrompida.

#### <a name="recommended-action"></a>Ação recomendada

Para <xref:System.Text.RegularExpressions.GroupCollection> instâncias, desambiguar chamadas para métodos de extensão que aceitam um `IEnumerable<T>` com uma conversão.

```csharp
// Without a cast - causes CS1061.
match.Groups.Count(_ => true)

// With a disambiguating cast.
((IEnumerable<Group>)m.Groups).Count(_ => true);
```

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

Qualquer método de extensão que aceita um <xref:System.Collections.Generic.IEnumerable%601> é afetado. Por exemplo:

- <xref:System.Collections.Immutable.ImmutableArray.ToImmutableArray%60%601(System.Collections.Generic.IEnumerable{%60%600})?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableDictionary.ToImmutableDictionary%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableHashSet.ToImmutableHashSet%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableList.ToImmutableList%60%601(System.Collections.Generic.IEnumerable{%60%600})?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableSortedDictionary.ToImmutableSortedDictionary%2A?displayProperty=fullName>
- <xref:System.Collections.Immutable.ImmutableSortedSet.ToImmutableSortedSet%2A?displayProperty=fullName>
- <xref:System.Data.DataTableExtensions.CopyToDataTable%2A?displayProperty=fullName>
- A maioria dos `System.Linq.Enumerable` métodos, por exemplo, <xref:System.Linq.Enumerable.Count%2A?displayProperty=fullName>
- <xref:System.Linq.ParallelEnumerable.AsParallel%2A?displayProperty=fullName>
- <xref:System.Linq.Queryable.AsQueryable%2A?displayProperty=fullName>

<!--

#### Affected APIs

- ``M:System.Collections.Immutable.ImmutableArray.ToImmutableArray``1(System.Collections.Generic.IEnumerable{``0})``
- `Overload:System.Collections.Immutable.ImmutableDictionary.ToImmutableDictionary`
- `Overload:System.Collections.Immutable.ImmutableHashSet.ToImmutableHashSet`
- ``M:System.Collections.Immutable.ImmutableList.ToImmutableList``1(System.Collections.Generic.IEnumerable{``0})``
- `Overload:System.Collections.Immutable.ImmutableSortedDictionary.ToImmutableSortedDictionary`
- `Overload:System.Collections.Immutable.ImmutableSortedSet.ToImmutableSortedSet`
- `Overload:System.Data.DataTableExtensions.CopyToDataTable`
- `Overload:System.Linq.Enumerable.Count`
- `Overload:System.Linq.ParallelEnumerable.AsParallel`
- `Overload:System.Linq.Queryable.AsQueryable`

-->
