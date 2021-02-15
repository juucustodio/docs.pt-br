---
title: Threading gerenciado
description: Consulte links para artigos sobre threads gerenciados no .NET que abrangem as noções básicas, práticas recomendadas, objetos de Threading & recursos, páginas de referência & mais.
ms.date: 03/30/2017
helpviewer_keywords:
- threading [.NET], about threading
- managed threading
ms.assetid: 7b46a7d9-c6f1-46d1-a947-ae97471bba87
ms.openlocfilehash: 28ba05c345d22b14512d280f3855934d727b3142
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95728440"
---
# <a name="managed-threading"></a>Threading gerenciado

Independentemente de você estar desenvolvendo para computadores com um processador ou vários, você deseja que seu aplicativo forneça a interação mais responsiva com o usuário, mesmo que o aplicativo esteja fazendo outro trabalho no momento. Usar vários threads de execução é uma das maneiras mais eficazes de manter seu aplicativo responsivo ao usuário e, ao mesmo tempo, usar o processador entre ou, até mesmo, durante os eventos do usuário. Embora esta seção introduza os conceitos básicos de threading, ele se concentra nos conceitos de threading gerenciado e em como usá-lo.  
  
> [!NOTE]
> A partir do .NET Framework 4, a programação multithread é bastante simplificada com as <xref:System.Threading.Tasks.Parallel?displayProperty=nameWithType> <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> classes e, o [Parallel LINQ (PLINQ)](../parallel-programming/introduction-to-plinq.md), as classes de coleção simultâneas no <xref:System.Collections.Concurrent?displayProperty=nameWithType> namespace e um modelo de programação baseado no conceito de tarefas em vez de threads. Para obter mais informações, consulte [programação paralela](../parallel-programming/index.md).  
  
## <a name="in-this-section"></a>Nesta seção  

 [Noções básicas de threading gerenciado](managed-threading-basics.md)  
 Fornece uma visão geral de threading gerenciado e descreve quando usar vários threads.  
  
 [Usando threads e threading](using-threads-and-threading.md)  
 Explica como criar, iniciar, pausar, retomar e abortar threads.  
  
 [Práticas recomendadas de threading gerenciado](managed-threading-best-practices.md)  
 Aborda os níveis de sincronização, como evitar deadlocks e condições de corrida, além de outros problemas de threading.  
  
 [Threading de objetos e recursos](threading-objects-and-features.md)  
 Descreve as classes gerenciadas que você pode usar para sincronizar as atividades de threads e os dados de objetos acessados em threads diferentes, bem como fornece uma visão geral dos threads de pool do thread.  
  
## <a name="reference"></a>Referência  

 <xref:System.Threading>  
 Contém classes para uso e sincronização de threads gerenciados.  
  
 <xref:System.Collections.Concurrent>  
 Contém classes de coleção que são seguras para uso com vários threads.  
  
 <xref:System.Threading.Tasks>  
 Contém classes para criação e agendamento de tarefas de processamento simultâneo.  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Domínios do aplicativo](../../framework/app-domains/application-domains.md)  
 Fornece uma visão geral de domínios do aplicativo e seu uso pelo Common Language Infrastructure.  
  
 [E/s de arquivo assíncrono](../io/asynchronous-file-i-o.md)  
 Descreve as vantagens de desempenho e a operação básica da E/S assíncrona.  
  
 [Padrão assíncrono baseado em tarefa (TAP)](../asynchronous-programming-patterns/task-based-asynchronous-pattern-tap.md)  
 Fornece uma visão geral do padrão recomendado para programação assíncrona no .NET.  
  
 [Chamando métodos síncronos de forma assíncrona](../asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 Explica como chamar métodos nos threads de pool do thread usando recursos internos de representantes.  
  
 [Programação paralela](../parallel-programming/index.md)  
 Descreve as bibliotecas de programação paralela, que simplificam o uso de vários threads em aplicativos.  
  
 [LINQ paralelo (PLINQ)](../parallel-programming/introduction-to-plinq.md)  
 Descreve um sistema para executar consultas paralelamente, de modo a aproveitar vários processadores.
