---
description: 'Saiba mais sobre: como iterar diretórios de arquivos com a classe Parallel'
title: 'Como: fazer iterações de diretórios de arquivos com a Classe Paralela'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- parallel loops, how to iterate directories
ms.assetid: 555e9f48-f53d-4774-9bcf-3e965c732ec5
ms.openlocfilehash: 9e1eac634b1a8b50ea938a7de945265ab884895e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99701853"
---
# <a name="how-to-iterate-file-directories-with-the-parallel-class"></a>Como: fazer iterações de diretórios de arquivos com a Classe Paralela

Em muitos casos, a iteração de arquivo é uma operação que pode ser facilmente paralelizada. O tópico [Como iterar diretórios de arquivos com o PLINQ](how-to-iterate-file-directories-with-plinq.md) mostra a maneira mais fácil de executar essa tarefa para muitos cenários. No entanto, podem surgir complicações quando seu código precisa lidar com vários tipos de exceções ao acessar o sistema de arquivos. O exemplo a seguir mostra uma abordagem para o problema. Ele usa uma iteração baseada em pilha para transportar todos os arquivos e pastas para um diretório especificado, e permite que seu código capture e trate várias exceções. É claro que a forma como você manipula as exceções fica a seu critério.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir itera os diretórios sequencialmente, mas processa os arquivos em paralelo. Essa é provavelmente a melhor abordagem quando você tem uma proporção de arquivo para diretório grande. Também é possível paralelizar a iteração de diretórios e acessar cada arquivo em sequência. Provavelmente, não é eficiente paralelizar os dois loops, a menos que você esteja direcionando especificamente a uma máquina com muitos processadores. No entanto, como em todos os casos, você deve testar cuidadosamente seu aplicativo para determinar a melhor abordagem.  
  
 [!code-csharp[TPL_Parallel#08](../../../samples/snippets/csharp/VS_Snippets_Misc/tpl_parallel/cs/parallel_file.cs#08)]
 [!code-vb[TPL_Parallel#08](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpl_parallel/vb/fileiteration08.vb#08)]  
  
 Neste exemplo, a E/S do arquivo é executada de maneira síncrona. Ao lidar com arquivos grandes ou conexões de rede lentas, talvez seja preferível acessar os arquivos de forma assíncrona. Você pode combinar as técnicas de E/S assíncronas com a iteração paralela. Para obter mais informações, consulte [tpl e programação assíncrona .NET tradicional](tpl-and-traditional-async-programming.md).  
  
 O exemplo usa a variável local `fileCount` para manter uma contagem do número total de arquivos processados. Como a variável pode ser acessada simultaneamente por várias tarefas, o acesso a ela é sincronizado chamando o método <xref:System.Threading.Interlocked.Add%2A?displayProperty=nameWithType>.  
  
 Observe que se uma exceção for lançada no thread principal, os threads iniciados pelo método <xref:System.Threading.Tasks.Parallel.ForEach%2A> poderão continuar a executar. Para interromper esses threads, você pode definir uma variável booliana em seus manipuladores de exceção, e verificar seu valor em cada iteração do loop paralelo. Se o valor indica que uma exceção foi lançada, use a variável <xref:System.Threading.Tasks.ParallelLoopState> para interromper ou sair do loop. Para saber mais, confira [Como parar ou sair de um loop Parallel.For](/previous-versions/dotnet/netframework-4.0/dd460721(v=vs.100)).  
  
## <a name="see-also"></a>Consulte também

- [Paralelismo de dados](data-parallelism-task-parallel-library.md)
