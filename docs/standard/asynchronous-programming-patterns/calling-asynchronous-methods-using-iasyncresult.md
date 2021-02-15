---
description: 'Saiba mais sobre: chamando métodos assíncronos usando IAsyncResult'
title: Chamando métodos assíncronos usando IAsyncResult
ms.date: 03/30/2017
helpviewer_keywords:
- ending asynchronous operations
- waiting for asynchronous operations
- asynchronous method calling
- calling asynchronous methods
- asynchronous programming, calling asynchronous methods
- IAsyncResult interface, calling asynchronous methods
- stopping asynchronous operations
ms.assetid: 07fba116-045b-473c-a0b7-acdbeb49861f
ms.openlocfilehash: 0fcf71c95fc0170a41ea2ad2085b9308c75264f8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754570"
---
# <a name="calling-asynchronous-methods-using-iasyncresult"></a>Chamando métodos assíncronos usando IAsyncResult

Os tipos nas bibliotecas .NET e bibliotecas de classe de terceiros podem fornecer métodos que permitem que um aplicativo continue a execução enquanto executa operações assíncronas em threads diferentes do thread do aplicativo principal. As seções a seguir descrevem e fornecem exemplos de código que demonstram diferentes maneiras de chamar métodos assíncronos que usam o padrão de design <xref:System.IAsyncResult>.  
  
- [Bloqueio da execução do aplicativo encerrando uma operação assíncrona](blocking-application-execution-by-ending-an-async-operation.md).  
  
- [Bloqueando a execução do aplicativo usando um AsyncWaitHandle](blocking-application-execution-using-an-asyncwaithandle.md).  
  
- [Sondando o status de uma operação assíncrona](polling-for-the-status-of-an-asynchronous-operation.md).  
  
- [Usando um delegado AsyncCallback para finalizar uma operação assíncrona](using-an-asynccallback-delegate-to-end-an-asynchronous-operation.md).  
  
## <a name="see-also"></a>Consulte também

- [Padrão assíncrono baseado em evento (EAP)](event-based-asynchronous-pattern-eap.md)
- [Visão geral do padrão assíncrono baseado em evento](event-based-asynchronous-pattern-overview.md)
