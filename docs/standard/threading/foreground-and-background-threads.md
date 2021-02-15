---
title: Threads em primeiro plano e em segundo plano
description: Determinar ou alterar se um thread é um thread em segundo plano ou um thread em primeiro plano usando a propriedade Thread. IsBackground no .NET.
ms.date: 03/30/2017
helpviewer_keywords:
- threading [.NET], foreground
- threading [.NET], background
- foreground threads
- background threads
ms.assetid: cfe0d632-dd35-47e0-91ad-f742a444005e
ms.openlocfilehash: 9f0ea1d53eb2f96b8a56cacc089cf90eb2f079a0
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94819897"
---
# <a name="foreground-and-background-threads"></a>Threads em primeiro e segundo plano

Um thread gerenciado é um thread em segundo plano ou um thread em primeiro plano. Threads em segundo plano são idênticos aos threads em primeiro plano com uma exceção: um thread em segundo plano não mantém o ambiente de execução gerenciado em execução. Uma vez que todos os threads em primeiro plano foram interrompidos em um processo gerenciado (onde o arquivo .exe é um assembly gerenciado), o sistema interrompe todos os threads em segundo plano e desliga.  
  
> [!NOTE]
> Quando o runtime interrompe um thread em segundo plano porque o processo está sendo desligado, nenhuma exceção é lançada no thread. No entanto, quando os threads são interrompidos porque o método <xref:System.AppDomain.Unload%2A?displayProperty=nameWithType> descarrega o domínio do aplicativo, um <xref:System.Threading.ThreadAbortException> é lançado em ambos os threads em primeiro plano e em segundo plano.  
  
 Use a propriedade <xref:System.Threading.Thread.IsBackground%2A?displayProperty=nameWithType> para determinar se um thread é um thread em segundo plano ou em primeiro plano, ou para alterar seu status. Um thread pode ser alterado para um thread em segundo plano a qualquer momento, definindo a propriedade <xref:System.Threading.Thread.IsBackground%2A> para `true`.  
  
> [!IMPORTANT]
> O status em primeiro plano ou em segundo plano de um thread não afeta o resultado de uma exceção sem tratamento no thread. Uma exceção sem tratamento em threads de primeiro plano ou em segundo plano resulta no encerramento do aplicativo. Confira [Exceções em threads gerenciados](exceptions-in-managed-threads.md).  
  
 Threads pertencentes ao pool de threads gerenciados (ou seja, threads cuja propriedade <xref:System.Threading.Thread.IsThreadPoolThread%2A> é `true`) são threads em segundo plano. Todos os threads que entram no ambiente de execução gerenciado do código não gerenciado são marcados como threads em segundo plano. Todos os threads gerados ao criar e iniciar um novo objeto <xref:System.Threading.Thread> são, por padrão, threads em primeiro plano.  
  
 Se você usar um thread para monitorar uma atividade, como uma conexão de soquete, defina sua propriedade <xref:System.Threading.Thread.IsBackground%2A> como `true` para que o thread não impeça o encerramento do processo.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Threading.Thread.IsBackground%2A?displayProperty=nameWithType>
- <xref:System.Threading.Thread>
- <xref:System.Threading.ThreadAbortException>
