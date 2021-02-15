---
description: 'Saiba mais sobre: matrizes'
title: Matrizes
ms.date: 10/22/2008
helpviewer_keywords:
- class library design guidelines [.NET Framework], arrays
- arrays [.NET Framework], usage guidelines
- empty arrays
ms.assetid: 66a1b3d8-6f3f-4715-b235-e1ff95e32d8e
ms.openlocfilehash: 2d919d5e13a03ed1c5d090339f8f0fd9c1a79190
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99642429"
---
# <a name="arrays"></a>Matrizes

✔️ preferir usar coleções em matrizes em APIs públicas. A seção [coleções](guidelines-for-collections.md) fornece detalhes sobre como escolher entre coleções e matrizes.

 ❌ Não use campos de matriz somente leitura. O próprio campo é somente leitura e não pode ser alterado, mas os elementos na matriz podem ser alterados.

 ✔️ Considere o uso de matrizes denteadas em vez de matrizes multidimensionais.

 Uma matriz denteada é uma matriz com elementos que também são matrizes. As matrizes que compõem os elementos podem ser de tamanhos diferentes, levando a menos espaço desperdiçado para alguns conjuntos de dados (por exemplo, matriz esparsa) em comparação com matrizes multidimensionais. Além disso, o CLR otimiza as operações de índice em matrizes denteadas, para que possam apresentar um melhor desempenho de tempo de execução em alguns cenários.

 *Partes © 2005, 2009 Microsoft Corporation. Todos os direitos reservados.*

 *Reimpresso com permissão da Pearson Education, Inc. das [Diretrizes de Design do Framework: convenções, linguagens e padrões para bibliotecas do .NET reutilizável, 2ª edição](https://www.informit.com/store/framework-design-guidelines-conventions-idioms-and-9780321545619) por Krzysztof Cwalina e Brad Abrams, publicado em 22 de outubro de 2008 por Addison-Wesley Professional como parte da série de desenvolvimento do Microsoft Windows.*

## <a name="see-also"></a>Confira também

- <xref:System.Array>
- [Diretrizes de design de estrutura](index.md)
- [Diretrizes de uso](usage-guidelines.md)
