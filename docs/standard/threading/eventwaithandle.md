---
description: 'Saiba mais sobre: EventWaitHandle'
title: EventWaitHandle
ms.date: 03/30/2017
helpviewer_keywords:
- threading [.NET], EventWaitHandle class
- EventWaitHandle class
- event wait handles [.NET]
- threading [.NET], cross-process synchronization
ms.assetid: 11ee0b38-d663-4617-b793-35eb6c64e9fc
ms.openlocfilehash: a1c5d9741cdcfa1313f0e7f1c0702954a93c6c09
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99666921"
---
# <a name="eventwaithandle"></a>EventWaitHandle

A classe <xref:System.Threading.EventWaitHandle> permite que os threads se comuniquem entre si por meio da sinalização e aguardando sinais. Identificadores de espera de eventos (conhecidos simplesmente como eventos) são identificadores de espera que podem ser sinalizados a fim de liberar um ou mais threads de espera. Após a sinalização, um identificador de espera de eventos é redefinido manualmente ou automaticamente. A classe <xref:System.Threading.EventWaitHandle> pode representar um identificador de espera de evento local (evento local) ou um identificador de espera evento de evento do sistema nomeado (evento nomeado ou evento do sistema, visível a todos os processos).  
  
> [!NOTE]
> Os identificadores de espera de eventos não são [eventos](../events/index.md) do .NET. Não há delegados ou manipuladores de eventos envolvidos. A palavra "evento" é usada para descrevê-los, pois eles têm sido chamados tradicionalmente de eventos do sistema operacional, e porque o ato de sinalização do identificador de espera indica aos threads de espera que um evento ocorreu.  
  
 Os identificadores de espera de eventos local e nomeado usam objetos de sincronização do sistema, que são protegidos por wrappers <xref:Microsoft.Win32.SafeHandles.SafeWaitHandle> a fim de garantir a liberação de recursos. Você pode usar o método <xref:System.Threading.WaitHandle.Dispose%2A> para liberar os recursos imediatamente ao terminar de usar o objeto.  
  
## <a name="event-wait-handles-that-reset-automatically"></a>Identificadores de espera de eventos redefinidos automaticamente  

 Crie um evento de redefinição automática especificando <xref:System.Threading.EventResetMode.AutoReset?displayProperty=nameWithType> ao criar o objeto <xref:System.Threading.EventWaitHandle>. Como o nome sugere, esse evento de sincronização é redefinido automaticamente quando sinalizado, após a liberação de um thread de espera único. Sinalize o evento chamando seu método <xref:System.Threading.EventWaitHandle.Set%2A>.  
  
 Os eventos de redefinição automática geralmente são usados para fornecer acesso exclusivo a um recurso para um thread por vez. Um thread solicita o recurso chamando o método <xref:System.Threading.WaitHandle.WaitOne%2A>. Se nenhum outro thread estiver usando o identificador de espera, o método retornará `true`, e o thread de chamada terá o controle do recurso.  
  
> [!IMPORTANT]
> Assim como ocorre com todos os mecanismos de sincronização, você deve garantir que todos os caminhos de código aguardem o identificador de espera apropriado antes de acessar um recurso protegido. A sincronização do thread é cooperativa.  
  
 Se um evento de redefinição automática for sinalizado quando não houver threads em espera, ele permanecerá sinalizado até que um thread tente esperar por ele. O evento libera o thread e redefine imediatamente, bloqueando os threads subsequentes.  
  
## <a name="event-wait-handles-that-reset-manually"></a>Identificadores de espera de evento redefinidos automaticamente  

 Crie um evento de redefinição manual especificando <xref:System.Threading.EventResetMode.ManualReset?displayProperty=nameWithType> ao criar o objeto <xref:System.Threading.EventWaitHandle>. Como o nome sugere, esse evento de sincronização deve ser redefinido manualmente após a sinalização. Até a redefinição, ao chamar seu método <xref:System.Threading.EventWaitHandle.Reset%2A>, os threads que aguardam o identificador de evento continuam imediatamente sem bloqueio.  
  
 Um evento de redefinição manual age como a porta de um curral. Quando o evento não é sinalizado, os threads que aguardam por ele ficam bloqueados, como cavalos em um curral. Quando o evento é sinalizado, ao chamar seu método <xref:System.Threading.EventWaitHandle.Set%2A>, todos os threads em espera ficam livres para continuar. O evento permanece sinalizado até que seu método <xref:System.Threading.EventWaitHandle.Reset%2A> seja chamado. Isso torna o evento de redefinição manual a maneira ideal de armazenar threads que precisam aguardar até que um thread conclua uma tarefa.  
  
 Como cavalos deixando um curral, demora até o sistema operacional agendar os threads liberados e continuar a execução. Se o método <xref:System.Threading.EventWaitHandle.Reset%2A> for chamado antes de todos os threads voltarem a operar, os threads restantes serão bloqueados novamente. Os threads que retomam a operação e os threads que são bloqueados depende de fatores aleatórios, como a carga no sistema, o número de threads aguardando o agendador etc. Isso não será um problema se o thread que sinaliza o evento terminar após a sinalização, o que é o padrão de uso mais comum. Se você quiser que o thread que sinalizou o evento comece uma nova tarefa após a continuação de todos threads em espera, você deverá bloqueá-lo até que todos os threads em espera tenham retomado a ação. Caso contrário, você terá uma condição de corrida, e o comportamento do seu código será imprevisível.  
  
## <a name="features-common-to-automatic-and-manual-events"></a>Recursos comuns a eventos automáticos e manuais  

 Normalmente, um ou mais threads ficam bloqueados em um <xref:System.Threading.EventWaitHandle> até que um thread desbloqueado chame o método <xref:System.Threading.EventWaitHandle.Set%2A>, o que libera um dos threads em espera (no caso de eventos de redefinição automática) ou todos eles (no caso de eventos de redefinição manual). Um thread pode sinalizar um <xref:System.Threading.EventWaitHandle> e depois bloqueá-lo, como uma operação atômica, chamando o método <xref:System.Threading.WaitHandle.SignalAndWait%2A?displayProperty=nameWithType> estático.  
  
 Os objetos <xref:System.Threading.EventWaitHandle> podem ser usados com os métodos <xref:System.Threading.WaitHandle.WaitAll%2A?displayProperty=nameWithType> e <xref:System.Threading.WaitHandle.WaitAny%2A?displayProperty=nameWithType> estáticos. Como as classes <xref:System.Threading.EventWaitHandle> e <xref:System.Threading.Mutex> derivam de <xref:System.Threading.WaitHandle>, você pode usar as duas classes com esses métodos.  
  
### <a name="named-events"></a>Eventos nomeados  

 O sistema operacional Windows permite que os identificadores de espera de evento tenham nomes. Um evento nomeado serve para todo o sistema. Ou seja, após a criação de um evento nomeado, ele fica visível para todos os threads em todos os processos. Assim, os eventos nomeados podem ser usados para sincronizar as atividades de processos, bem como os threads.  
  
 Você pode criar um objeto <xref:System.Threading.EventWaitHandle> que representa um evento de sistema nomeado usando um dos construtores que especifica um nome de evento.  
  
> [!NOTE]
> Como os eventos nomeados servem para todo o sistema, é possível ter vários objetos <xref:System.Threading.EventWaitHandle> que representam o mesmo evento nomeado. Cada vez que você chama um construtor ou o método <xref:System.Threading.EventWaitHandle.OpenExisting%2A>, um novo objeto <xref:System.Threading.EventWaitHandle> é criado. Especificar o mesmo nome repetidas vezes cria vários objetos que representam o mesmo evento nomeado.  
  
 Tenha cuidado ao usar eventos nomeados. Como eles servem para todo o sistema, outro processo que usa o mesmo nome pode bloquear seus threads inesperadamente. Código mal-intencionado em execução no mesmo computador pode usar isso como base de um ataque de negação de serviço.  
  
 Use a segurança de controle de acesso para proteger um objeto <xref:System.Threading.EventWaitHandle> que representa um evento nomeado, preferencialmente usando um construtor que especifica um objeto <xref:System.Security.AccessControl.EventWaitHandleSecurity>. Também é possível aplicar a segurança de controle de acesso usando o método <xref:System.Threading.EventWaitHandle.SetAccessControl%2A>, mas isso deixa uma janela de vulnerabilidade entre o momento em que o identificador em espera de evento é criado e o momento em que ele é protegido. Proteger eventos com a segurança de controle de acesso ajuda a impedir ataques mal-intencionados, mas não resolve o problema de colisão de nome não intencional.  
  
> [!NOTE]
> Ao contrário da classe <xref:System.Threading.EventWaitHandle>, as classes derivadas <xref:System.Threading.AutoResetEvent> e <xref:System.Threading.ManualResetEvent> podem representar somente identificadores em espera locais. Eles não podem representar eventos nomeados do sistema.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Threading.EventWaitHandle>
- <xref:System.Threading.WaitHandle>
- <xref:System.Threading.AutoResetEvent>
- <xref:System.Threading.ManualResetEvent>
