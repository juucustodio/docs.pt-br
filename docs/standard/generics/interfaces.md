---
description: 'Saiba mais sobre: interfaces genéricas'
title: Interfaces genéricas
ms.date: 03/30/2017
helpviewer_keywords:
- generic interfaces [.NET]
- equality comparisons [.NET]
- generics [.NET], interfaces
- ordering comparisons [.NET]
ms.assetid: 88bf5b04-d371-4edb-ba38-01ec7cabaacf
ms.openlocfilehash: 18822ec29ac0905d1f177c5888cac6121ac36a95
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99702399"
---
# <a name="generic-interfaces"></a>Interfaces genéricas

Este artigo fornece uma visão geral das interfaces genéricas que fornecem funcionalidade comum em famílias de tipos genéricos.  
  
As interfaces genéricas fornecem contrapartes fortemente tipadas para interfaces não genéricas para fins de comparações de ordenação e de igualdade, e para a funcionalidade que é compartilhada por tipos de coleção genérica.  
  
> [!NOTE]
> Os parâmetros de tipo de várias interfaces genéricas são marcados como covariant ou contravariant, fornecendo maior flexibilidade na atribuição e no uso de tipos que implementam essas interfaces. Consulte [Covariância e contravariância](covariance-and-contravariance.md).  
  
## <a name="equality-and-ordering-comparisons"></a>Comparações de ordem e igualdade  

 No namespace <xref:System>, as interfaces genéricas <xref:System.IComparable%601?displayProperty=nameWithType> e <xref:System.IEquatable%601?displayProperty=nameWithType>, assim como suas contrapartes não genéricas, definem métodos para comparações de classificação e de igualdade, respectivamente. Os tipos implementam essas interfaces para permitir a execução dessas comparações.  
  
 No namespace <xref:System.Collections.Generic>, as interfaces genéricas <xref:System.Collections.Generic.IComparer%601> e <xref:System.Collections.Generic.IEqualityComparer%601> oferecem uma maneira de definir uma comparação de classificação ou de igualdade para tipos que não implementam a interface genérica <xref:System.IComparable%601?displayProperty=nameWithType> ou <xref:System.IEquatable%601?displayProperty=nameWithType>, e fornecem uma maneira de redefinir esses relacionamentos para tipos que implementam. Essas interfaces são usadas pelos métodos e construtores de muitas classes de coleção genérica. Por exemplo, você pode passar um objeto <xref:System.Collections.Generic.IComparer%601> genérico para o construtor da classe <xref:System.Collections.Generic.SortedDictionary%602>, a fim de especificar uma ordem de classificação para um tipo que não implementa um <xref:System.IComparable%601?displayProperty=nameWithType> genérico. Há sobrecargas do método estático genérico <xref:System.Array.Sort%2A?displayProperty=nameWithType> e do método de instância <xref:System.Collections.Generic.List%601.Sort%2A?displayProperty=nameWithType> para classificar matrizes e listas usando implementações <xref:System.Collections.Generic.IComparer%601> genéricas.  
  
 As classes genéricas <xref:System.Collections.Generic.Comparer%601> e <xref:System.Collections.Generic.EqualityComparer%601> fornecem classes base para implementações das interfaces genéricas <xref:System.Collections.Generic.IComparer%601> e <xref:System.Collections.Generic.IEqualityComparer%601>, e também fornecem comparações padrão de ordem e de igualdade por meio de suas respectivas propriedades <xref:System.Collections.Generic.Comparer%601.Default%2A?displayProperty=nameWithType> e <xref:System.Collections.Generic.EqualityComparer%601.Default%2A?displayProperty=nameWithType>.  
  
## <a name="collection-functionality"></a>Funcionalidade de coleção  

 A interface genérica <xref:System.Collections.Generic.ICollection%601> é a interface básica para tipos de coleção genérica. Ela fornece a funcionalidade básica para adicionar, remover, copiar e enumerar elementos. <xref:System.Collections.Generic.ICollection%601> herda da <xref:System.Collections.Generic.IEnumerable%601> genérica e da <xref:System.Collections.IEnumerable> não genérica.  
  
 A interface genérica <xref:System.Collections.Generic.IList%601> estende a interface genérica <xref:System.Collections.Generic.ICollection%601> com métodos para recuperação indexada.  
  
 A interface genérica <xref:System.Collections.Generic.IDictionary%602> estende a interface genérica <xref:System.Collections.Generic.ICollection%601> com métodos para recuperação codificada. Os tipos de dicionário genérico na base class library do .NET também implementam a interface não genérica <xref:System.Collections.IDictionary> .  
  
 A interface genérica <xref:System.Collections.Generic.IEnumerable%601> fornece uma estrutura de enumerador genérico. A interface genérica <xref:System.Collections.Generic.IEnumerator%601> implementada pelos enumeradores genéricos herda a interface não genérica <xref:System.Collections.IEnumerator>; os membros <xref:System.Collections.IEnumerator.MoveNext%2A> e <xref:System.Collections.IEnumerator.Reset%2A>, que não dependem do parâmetro de tipo `T`, só aparecem na interface não genérica. Isso significa que qualquer consumidor da interface não genérica também poderá consumir a interface genérica.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Collections.Generic?displayProperty=nameWithType>
- <xref:System.Collections.ObjectModel?displayProperty=nameWithType>
- [Genéricos](index.md)
- [Coleções genéricas no .NET](collections.md)
- [Delegados genéricos para manipular matrizes e listas](delegates-for-manipulating-arrays-and-lists.md)
- [Covariância e contravariância](covariance-and-contravariance.md)
