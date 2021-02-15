---
title: Temporizadores
description: Saiba quais temporizadores .NET devem ser usados em um ambiente multi-threaded.
ms.date: 07/03/2018
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- threading [.NET], timers
- timers, about timers
ms.assetid: 7091500d-be18-499b-a942-95366ce185e5
author: pkulikov
ms.openlocfilehash: 1ab612bc32a84c1248d311b0603a01a32a25199f
ms.sourcegitcommit: 965a5af7918acb0a3fd3baf342e15d511ef75188
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/18/2020
ms.locfileid: "94826099"
---
# <a name="timers"></a>Temporizadores

O .NET fornece dois temporizadores a serem usados em um ambiente multi-threaded:

- <xref:System.Threading.Timer?displayProperty=nameWithType>, que executa um único método de retorno de chamada em um thread <xref:System.Threading.ThreadPool> em intervalos regulares.
- <xref:System.Timers.Timer?displayProperty=nameWithType>, que por padrão gera um evento em um thread <xref:System.Threading.ThreadPool> em intervalos regulares.

> [!NOTE]
> Algumas implementações do .NET podem incluir temporizadores adicionais:
>
> - <xref:System.Windows.Forms.Timer?displayProperty=nameWithType>: um componente do Windows Forms que dispara um evento em intervalos regulares. O componente não tem nenhuma interface do usuário e é projetado para ser usado em um ambiente single-threaded.  
> - <xref:System.Web.UI.Timer?displayProperty=nameWithType>: um componente do ASP.NET que executa postbacks de página da Web assíncrona ou síncrona em intervalos regulares.
> - <xref:System.Windows.Threading.DispatcherTimer?displayProperty=nameWithType>: um temporizador que é integrado à fila <xref:System.Windows.Threading.Dispatcher> que é processada em um intervalo de tempo especificado e com uma prioridade especificada.

## <a name="the-systemthreadingtimer-class"></a>A classe System.Threading.Timer

A classe <xref:System.Threading.Timer?displayProperty=nameWithType> permite chamar um delegado continuamente em intervalos de tempo especificado. Você também pode usar essa classe para agendar uma única chamada para um delegado em um intervalo de tempo especificado. O delegado é executado em um thread <xref:System.Threading.ThreadPool>.

Ao criar um objeto <xref:System.Threading.Timer?displayProperty=nameWithType>, você especifica um delegado <xref:System.Threading.TimerCallback> que define o método de retorno de chamada, um objeto de estado opcional que é passado para o retorno de chamada, o período de atraso antes da primeira invocação do retorno de chamada e o intervalo de tempo entre as invocações do retorno de chamada. Para cancelar um temporizador pendente, chame o método <xref:System.Threading.Timer.Dispose%2A?displayProperty=nameWithType>.

O exemplo a seguir cria um temporizador que chama o delegado fornecido pela primeira vez após um segundo (1000 milissegundos) e, em seguida, chama a cada dois segundos. O objeto de estado no exemplo é usado para contar quantas vezes o delegado é chamado. O temporizador é interrompido quando o delegado é chamado pelo menos 10 vezes.

[!code-cpp[System.Threading.Timer#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.Timer/CPP/source2.cpp#2)]
[!code-csharp[System.Threading.Timer#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.Timer/CS/source2.cs#2)]
[!code-vb[System.Threading.Timer#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.Timer/VB/source2.vb#2)]

Para obter mais informações e exemplos, consulte <xref:System.Threading.Timer?displayProperty=nameWithType>.

## <a name="the-systemtimerstimer-class"></a>A classe System.Timers.Timer

Outro temporizador que pode ser usado em um ambiente multi-threaded é o <xref:System.Timers.Timer?displayProperty=nameWithType> que, por padrão, gera um evento em um thread <xref:System.Threading.ThreadPool>.

Ao criar um objeto <xref:System.Timers.Timer?displayProperty=nameWithType>, você pode especificar o intervalo de tempo em que um evento <xref:System.Timers.Timer.Elapsed> deve ser gerado. Use a propriedade <xref:System.Timers.Timer.Enabled%2A> para indicar se um temporizador deve gerar um evento <xref:System.Timers.Timer.Elapsed>. Se você precisar que um evento <xref:System.Timers.Timer.Elapsed> seja gerado apenas uma vez depois que o intervalo especificado for decorrido, defina <xref:System.Timers.Timer.AutoReset%2A> para `false`. O valor padrão da propriedade <xref:System.Timers.Timer.AutoReset%2A> é `true`, o que significa que um evento <xref:System.Timers.Timer.Elapsed> é gerado regularmente no intervalo definido pela propriedade <xref:System.Timers.Timer.Interval%2A>.

Para obter mais informações e exemplos, consulte <xref:System.Timers.Timer?displayProperty=nameWithType>.
  
## <a name="see-also"></a>Confira também

- <xref:System.Threading.Timer?displayProperty=nameWithType>
- <xref:System.Timers.Timer?displayProperty=nameWithType>
- [Threading de objetos e recursos](threading-objects-and-features.md)
