---
title: Exceções em threads gerenciados
description: Veja como as exceções não tratadas são tratadas no .NET. A maioria das exceções de thread sem tratamento prossegue naturalmente e leva ao encerramento do aplicativo.
ms.date: 03/30/2017
helpviewer_keywords:
- unhandled exceptions,in managed threads
- threading [.NET],unhandled exceptions
- threading [.NET],exceptions in managed threads
- managed threading
ms.assetid: 11294769-2e89-43cb-890e-ad4ad79cfbee
ms.openlocfilehash: 740cd1b78b96c2fcaecf39a725973d738037f403
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95723747"
---
# <a name="exceptions-in-managed-threads"></a>Exceções em threads gerenciados

O Common Language Runtime permite que a maioria das exceções não tratadas em threads prossiga naturalmente. Na maioria dos casos, isso significa que a exceção sem tratamento causa o encerramento do aplicativo.
  
O common language runtime fornece uma barreira para certas exceções sem tratamento que são usados para controlar o fluxo do programa:  
  
- Uma <xref:System.Threading.ThreadAbortException> é gerada em um thread porque <xref:System.Threading.Thread.Abort%2A> foi chamado.  
  
- Um <xref:System.AppDomainUnloadedException> é gerado em um thread, pois o domínio do aplicativo no qual o thread está em execução está sendo descarregado.  
  
- O Common Language Runtime ou um processo de host encerra o thread lançando uma exceção interna.  
  
 Se qualquer uma dessas exceções não tiver tratamento em threads criados pelo common language runtime, a exceção encerrará o thread, mas o common language runtime não permitirá que a exceção prossiga.  
  
 Se essas exceções não tiverem tratamento no thread principal, ou em threads que entraram no runtime a partir do código não gerenciado, elas prosseguirão normalmente, resultando no encerramento do aplicativo.  
  
> [!NOTE]
> É possível que o runtime lance uma exceção não tratada antes que qualquer código gerenciado tenha a oportunidade de instalar um manipulador de exceção. Mesmo que o código gerenciado não tivesse possibilidade de manipular essa exceção, a exceção recebe a permissão para prosseguir naturalmente.  
  
## <a name="exposing-threading-problems-during-development"></a>Exposição de problemas de threading durante o desenvolvimento  

 Quando os threads recebem a permissão para falhar em modo silencioso, sem encerrar o aplicativo, problemas graves de programação podem passar sem detecção. Esse é um problema específico para serviços e outros aplicativos que são executados por longos períodos. À medida que os threads falham, o estado do programa se torna cada vez mais corrompido. O desempenho do aplicativo pode piorar ou o aplicativo pode parar de responder.  
  
 Permitir que exceções sem tratamento em threads prossigam naturalmente, até que o sistema operacional encerre o programa, expõe esses problemas durante o desenvolvimento e teste. Relatórios de erros em depuração de suporte de encerramentos do programa.  
  
## <a name="change-from-previous-versions"></a>Alterar de versões anteriores

No .NET Framework versões 1,0 e 1,1, o Common Language Runtime fornece um Backstop para exceções sem tratamento nas seguintes situações:  
  
- Não existe exceção sem tratamento em um thread de pool de threads. Quando uma tarefa gera uma exceção sem tratamento, o runtime imprime o rastreamento de pilha da exceção para o console e, depois, retorna o thread para o pool de threads.  
  
- Não existe exceção sem tratamento em um thread criado com o método <xref:System.Threading.Thread.Start%2A> da classe <xref:System.Threading.Thread>. Quando um código em execução em um thread como esse gera uma exceção sem tratamento, o runtime imprime o rastreamento de pilha da exceção para o console e, depois, encerra normalmente o thread.  
  
- Não existe exceção sem tratamento no thread finalizador. Quando um finalizar gera uma exceção sem tratamento, o runtime imprime o rastreamento de pilha da exceção para o console e, depois, permite que o thread finalizador retome a execução dos finalizadores.  
  
 O status de primeiro plano ou segundo plano de um thread gerenciado não afeta esse comportamento.  
  
 Para as exceções sem tratamento em threads com origem em código não gerenciado, a diferença é mais sutil. A caixa de diálogo de anexação JIT do runtime impede a caixa de diálogo do sistema operacional para exceções gerenciadas ou exceções nativas em threads que passaram por código nativo. O processo é encerrado em todos os casos.

### <a name="migration"></a>Migração

Se você estiver migrando do .NET Framework 1,0 ou 1,1 e tirar proveito da backstop de tempo de execução, por exemplo, para encerrar threads, considere uma das seguintes estratégias de migração:  
  
- Reestruturar o código para que o thread feche normalmente quando receber um sinal.  
  
- Use o método <xref:System.Threading.Thread.Abort%2A?displayProperty=nameWithType> para anular o thread.  
  
- Se um thread precisar ser interrompido para que o encerramento do processo possa continuar, torne o thread um thread em segundo plano para que ela seja encerrado automaticamente no encerramento do processo.  
  
Em todos os casos, a estratégia deve seguir as diretrizes de design para exceções. Confira [Diretrizes de design para exceções](../design-guidelines/exceptions.md).  
  
Como uma medida temporária de compatibilidade, os administradores podem colocar um sinalizador de compatibilidade na seção `<runtime>` do arquivo de configuração do aplicativo. Isso faz com que o common language runtime reverta para o comportamento das versões 1.0 e 1.1.  
  
```xml  
<legacyUnhandledExceptionPolicy enabled="1"/>  
```  
  
## <a name="host-override"></a>Substituição do host

Um host não gerenciado pode usar a interface [ICLRPolicyManager](../../framework/unmanaged-api/hosting/iclrpolicymanager-interface.md) na API de hospedagem para substituir a política de exceção padrão sem tratamento do Common Language Runtime. A função [ICLRPolicyManager::SetUnhandledExceptionPolicy](../../framework/unmanaged-api/hosting/iclrpolicymanager-setunhandledexceptionpolicy-method.md) é usada para definir a política para exceções sem tratamento.  
  
## <a name="see-also"></a>Confira também

- [Noções básicas de threading gerenciado](managed-threading-basics.md)
