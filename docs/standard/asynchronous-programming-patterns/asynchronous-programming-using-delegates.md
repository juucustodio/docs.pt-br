---
description: 'Saiba mais sobre: programação assíncrona usando delegados'
title: Programação assíncrona usando delegados
ms.date: 03/30/2017
helpviewer_keywords:
- BeginInvoke method
- asynchronous programming, delegates
- asynchronous delegates
- calling synchronous methods in asynchronous manner
- EndInvoke method
- calling asynchronous methods
- delegates [.NET], asynchronous
- synchronous calling in asynchronous manner
ms.assetid: 38a345ca-6963-4436-9608-5c9defef9c64
ms.openlocfilehash: 5315324fa79ce4658c255dbc09cd71a09afc614c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99703101"
---
# <a name="asynchronous-programming-using-delegates"></a>Programação assíncrona usando delegados

Os representantes permitem que você chame um método síncrono de maneira assíncrona. Quando você chama um representante de forma síncrona, o método `Invoke` chama o método de destino diretamente no thread atual. Se o método `BeginInvoke` for chamado, o CLR (Common Language Runtime) enfileira a solicitação e retorna imediatamente ao chamador. O método de destino é chamado de forma assíncrona em um thread a partir do pool de threads. O thread original, que enviou a solicitação, permanece livre para continuar a executar em paralelo com o método de destino. Se um método de retorno de chamada foi especificado na chamada para o método `BeginInvoke`, o método de retorno de chamada é chamado quando termina o método de destino. O método de retorno de chamada, o método `EndInvoke` obtém o valor retornado e os parâmetros de entrada/saída ou somente de saída. Se nenhum método de retorno de chamada for especificado ao chamar `BeginInvoke`, `EndInvoke` pode ser chamado do thread que chamou `BeginInvoke`.  
  
> [!IMPORTANT]
> Os compiladores devem emitir classes de representante com os métodos `Invoke`, `BeginInvoke` e `EndInvoke` usando a assinatura de representante especificada pelo usuário. Os métodos `BeginInvoke` e `EndInvoke` devem ser decorados como nativos. Como esses métodos são marcados como nativos, o CLR fornece automaticamente a implementação no tempo de carregamento da classe. O carregador garante que eles não sejam substituídos.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Chamando métodos síncronos de forma assíncrona](calling-synchronous-methods-asynchronously.md)  
 Discute o uso de representantes para fazer chamadas assíncronas a métodos comuns e fornece exemplos de código simples que mostram quatro maneiras de aguardar o retorno de uma chamada assíncrona.  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Padrão assíncrono baseado em evento (EAP)](event-based-asynchronous-pattern-eap.md)  
 Descreve a programação assíncrona no .NET.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Delegate>
