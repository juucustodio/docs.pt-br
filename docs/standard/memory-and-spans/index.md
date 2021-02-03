---
title: Memória e extensão
ms.date: 10/03/2018
helpviewer_keywords:
- Memory<T>
- Span<T>
- buffers"
- pipeline processing
ms.openlocfilehash: b81531d77bae1dce9d6cf58fe1b5439bf79f9e9c
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506364"
---
# <a name="memory--and-span-related-types"></a>Tipos relacionados a memória e extensão

A partir do .NET Core 2,1, o .NET inclui vários tipos inter-relacionados que representam uma região contígua e fortemente tipada de memória arbitrária. Elas incluem:

- <xref:System.Span%601?displayProperty=nameWithType>, um tipo usado para acessar uma região contígua da memória. Uma instância <xref:System.Span%601> pode ser sustentada por uma matriz do tipo `T`, uma <xref:System.String>, um buffer alocado com [stackalloc](../../csharp/language-reference/operators/stackalloc.md) ou um ponteiro para memória não gerenciada. Como ela deve ser alocada na pilha, tem várias restrições. Por exemplo, um campo em uma classe não pode ser do tipo <xref:System.Span%601>, nem a extensão pode ser usada em operações assíncronas.

- <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>, uma versão imutável da estrutura <xref:System.Span%601>.

- <xref:System.Memory%601?displayProperty=nameWithType>, um wrapper em uma região contígua de memória. Uma <xref:System.Memory%601> instância pode ser apoiada por uma matriz do tipo `T` ou um <xref:System.String> Gerenciador de memória ou um. Como pode ser armazenado no heap gerenciado, o não <xref:System.Memory%601> tem nenhuma das limitações do <xref:System.Span%601> .

- <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType>, uma versão imutável da estrutura <xref:System.Memory%601>.

- <xref:System.Buffers.MemoryPool%601?displayProperty=nameWithType>, que aloca blocos fortemente tipados de memória de um pool de memória para um proprietário. Instâncias <xref:System.Buffers.IMemoryOwner%601> podem ser alocadas do pool chamando <xref:System.Buffers.MemoryPool%601.Rent%2A?displayProperty=nameWithType> e lançadas de volta ao pool chamando <xref:System.Buffers.MemoryPool%601.Dispose?displayProperty=nameWithType>.

- <xref:System.Buffers.IMemoryOwner%601?displayProperty=nameWithType>, que representa o proprietário de um bloco de memória e controla o gerenciamento do tempo de vida.

- <xref:System.Buffers.MemoryManager%601>, uma classe base abstrata que pode ser usada para substituir a implementação de <xref:System.Memory%601>, de modo que <xref:System.Memory%601> possa ser sustentada por tipos adicionais, como identificadores seguros. <xref:System.Buffers.MemoryManager%601> destina-se a cenários avançados.

- <xref:System.ArraySegment%601>, um wrapper para determinado número de elementos de matriz, começando em um índice específico.

- <xref:System.MemoryExtensions?displayProperty=nameWithType>, uma coleção de métodos de extensão para converter cadeias de caracteres, matrizes e segmentos de matriz para blocos <xref:System.Memory%601>.

<xref:System.Span%601?displayProperty=nameWithType>, <xref:System.Memory%601?displayProperty=nameWithType> , e suas contrapartes ReadOnly são projetadas para permitir a criação de algoritmos que evitam a cópia da memória ou a alocação no heap gerenciado mais do que o necessário. Criá-los (via `Slice` ou seus construtores) não envolve duplicar os buffers subjacentes: somente as referências e os deslocamentos relevantes, que representam a "exibição" da memória encapsulada, são atualizados.

> [!NOTE]
> Para estruturas anteriores, <xref:System.Span%601> e <xref:System.Memory%601> estão disponíveis no [pacote do System.Memory NuGet](https://www.nuget.org/packages/System.Memory/).

Para obter mais informações, consulte o namespace de <xref:System.Buffers?displayProperty=nameWithType>.

## <a name="working-with-memory-and-span"></a>Como trabalhando com memória e extensão

Como os tipos relacionados a memória e extensão normalmente são usados para armazenar dados em um pipeline de processamento, é importante que os desenvolvedores sigam um conjunto de melhores práticas ao usar <xref:System.Span%601>, <xref:System.Memory%601> e tipos relacionados. Essas práticas recomendadas são documentadas em [memória \<T> e abrangem as \<T> diretrizes de uso](memory-t-usage-guidelines.md).

## <a name="see-also"></a>Confira também

- <xref:System.Memory%601?displayProperty=nameWithType>
- <xref:System.ReadOnlyMemory%601?displayProperty=nameWithType>
- <xref:System.Span%601?displayProperty=nameWithType>
- <xref:System.ReadOnlySpan%601?displayProperty=nameWithType>
- <xref:System.Buffers?displayProperty=nameWithType>
