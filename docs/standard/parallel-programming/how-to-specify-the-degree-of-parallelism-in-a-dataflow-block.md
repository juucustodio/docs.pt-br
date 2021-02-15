---
description: 'Saiba mais sobre: como especificar o grau de paralelismo em um bloco de Dataflow'
title: 'Como: especificar o grau de paralelismo em um bloco de fluxo de dados'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- dataflow block, specifying parallelism in TPL
- Task Parallel Library, dataflows
- TPL dataflow library, specifying parallelism
ms.assetid: e4088541-ee05-40db-95f5-147cfe62fde7
ms.openlocfilehash: 7d2a6d93e4f167975f3ec55a7472f7e81d2f6697
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99641623"
---
# <a name="how-to-specify-the-degree-of-parallelism-in-a-dataflow-block"></a>Como: especificar o grau de paralelismo em um bloco de fluxo de dados

Este documento descreve como definir a propriedade <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A?displayProperty=nameWithType> para habilitar um bloco de fluxo de execução a processar mais de uma mensagem por vez. Fazer isso é útil quando você possui um bloco de fluxo de dados que executa uma computação de longa duração e pode se beneficiar do processamento de mensagens em paralelo. Este exemplo usa a classe <xref:System.Threading.Tasks.Dataflow.ActionBlock%601?displayProperty=nameWithType> para executar várias operações de fluxo de dados simultaneamente; no entanto, você pode especificar o grau máximo de paralelismo em qualquer um dos tipos de bloco de execução predefinidos que a biblioteca de dados TPL fornece, <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>, <xref:System.Threading.Tasks.Dataflow.TransformBlock%602?displayProperty=nameWithType> e <xref:System.Threading.Tasks.Dataflow.TransformManyBlock%602?displayProperty=nameWithType>.

[!INCLUDE [tpl-install-instructions](../../../includes/tpl-install-instructions.md)]

## <a name="example"></a>Exemplo  

 O exemplo a seguir executa dois cálculos de fluxo de dados e imprime o tempo decorrido que é necessário para cada computação. O primeiro cálculo especifica um grau máximo de paralelismo de 1, que é o padrão. Um grau máximo de paralelismo de 1 faz com que o bloco de fluxo de dados processe mensagens em série. A segunda computação lembra a primeira, exceto que especifica um grau máximo de paralelismo igual ao número de processadores disponíveis. Isso permite que o bloco de fluxo de dados execute múltiplas operações em paralelo.  
  
 [!code-csharp[TPLDataflow_DegreeOfParallelism#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_degreeofparallelism/cs/dataflowdegreeofparallelism.cs#1)]
 [!code-vb[TPLDataflow_DegreeOfParallelism#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_degreeofparallelism/vb/dataflowdegreeofparallelism.vb#1)]  
  
## <a name="robust-programming"></a>Programação robusta  

 Por padrão, cada bloco de fluxo de dados predefinido propaga mensagens na ordem em que as mensagens são recebidas.  Embora várias mensagens sejam processadas simultaneamente quando você especifica um grau máximo de paralelismo superior a 1, elas ainda são propagadas na ordem em que são recebidas.  
  
 Como a propriedade <xref:System.Threading.Tasks.Dataflow.ExecutionDataflowBlockOptions.MaxDegreeOfParallelism%2A> representa o grau máximo de paralelismo, o bloco de fluxo de dados pode executar com um menor grau de paralelismo do que o especificado. O bloco de fluxo de dados pode usar um menor grau de paralelismo para atender aos requisitos funcionais ou para explicar a falta de recursos do sistema disponíveis. Um bloco de fluxo de dados nunca escolhe um maior grau de paralelismo do que o especificado por você.  
  
## <a name="see-also"></a>Consulte também

- [Fluxo de dados](dataflow-task-parallel-library.md)
