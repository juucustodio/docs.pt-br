---
description: 'Saiba mais sobre: usando um delegado AsyncCallback para finalizar uma operação assíncrona'
title: Usando um delegado AsyncCallback para finalizar uma operação assíncrona
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- ending asynchronous operations
- asynchronous programming, ending operations
- AsyncCallback delegate
- stopping asynchronous operations
ms.assetid: 9d97206c-8917-406c-8961-7d0909d84eeb
ms.openlocfilehash: c97be1b9dbf225cfb76f8d9392269297fc1d123c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99732183"
---
# <a name="using-an-asynccallback-delegate-to-end-an-asynchronous-operation"></a>Usando um delegado AsyncCallback para finalizar uma operação assíncrona

Os aplicativos que podem executar outras tarefas enquanto aguardam os resultados de uma operação assíncrona não devem bloquear a espera até que a operação seja concluída. Use uma das opções a seguir para continuar a execução das instruções ao aguardar a conclusão de uma operação assíncrona:  
  
- Use um representante do <xref:System.AsyncCallback> para processar os resultados da operação assíncrona em um thread separado. Esta abordagem será demonstrada neste tópico.  
  
- Use a propriedade <xref:System.IAsyncResult.IsCompleted%2A> do <xref:System.IAsyncResult> retornado do método **Begin**_OperationName_ da operação assíncrona para determinar se a operação foi concluída. Veja um exemplo que demonstra essa abordagem em [Sondagem do status de uma operação assíncrona](polling-for-the-status-of-an-asynchronous-operation.md).  
  
## <a name="example"></a>Exemplo  

 O exemplo de código a seguir demonstra como usar métodos assíncronos na classe <xref:System.Net.Dns> para recuperar informações do DNS (Sistema de Nomes de Domínio) de computadores especificados pelo usuário. Este exemplo cria um representante <xref:System.AsyncCallback> que referencia o método `ProcessDnsInformation`. Esse método é chamado uma vez para cada solicitação assíncrona para obter informações de DNS.  
  
 Observe que o host especificado pelo usuário é passado para o parâmetro <xref:System.Net.Dns.BeginGetHostByName%2A><xref:System.Object>. Para obter um exemplo que demonstra a definição e uso de um objeto de estado mais complexo, veja [Usar um representante AsyncCallback e um objeto de estado](using-an-asynccallback-delegate-and-state-object.md).  
  
 [!code-csharp[AsyncDesignPattern#4](../../../samples/snippets/csharp/VS_Snippets_CLR/AsyncDesignPattern/CS/AsyncDelegateNoStateObject.cs#4)]
 [!code-vb[AsyncDesignPattern#4](../../../samples/snippets/visualbasic/VS_Snippets_CLR/AsyncDesignPattern/VB/AsyncDelegateNoState.vb#4)]  
  
## <a name="see-also"></a>Consulte também

- [Padrão assíncrono baseado em evento (EAP)](event-based-asynchronous-pattern-eap.md)
- [Visão geral do padrão assíncrono baseado em evento](event-based-asynchronous-pattern-overview.md)
- [Chamando métodos assíncronos usando IAsyncResult](calling-asynchronous-methods-using-iasyncresult.md)
- [Usando um delegado AsyncCallback e um objeto de estado](using-an-asynccallback-delegate-and-state-object.md)
