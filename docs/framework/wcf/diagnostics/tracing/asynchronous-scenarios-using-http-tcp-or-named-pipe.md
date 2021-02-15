---
description: 'Saiba mais sobre: cenários assíncronos usando HTTP, TCP ou Named-Pipe'
title: Cenários assíncronos usando HTTP, TCP ou pipe nomeado
ms.date: 03/30/2017
ms.assetid: a4d62402-43a4-48a4-9ced-220633ebc4ce
ms.openlocfilehash: 5e01866cd20d63796741a097a6d7d774ea45d3d9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99770944"
---
# <a name="asynchronous-scenarios-using-http-tcp-or-named-pipe"></a>Cenários assíncronos usando HTTP, TCP ou pipe nomeado

Este tópico descreve as atividades e transferências para diferentes cenários assíncronos de solicitação/resposta, com solicitações multi-threaded usando HTTP, TCP ou pipe nomeado.  
  
## <a name="asynchronous-requestreply-without-errors"></a>Solicitação/resposta assíncrona sem erros  

 Esta seção descreve as atividades e transferências para um cenário de solicitação/resposta assíncrona, com clientes multithread.  
  
 A atividade do chamador é encerrada quando `beginCall` retorna e `endCall` retorna. Se um retorno de chamada for chamado, o retorno de chamada retornará.  
  
 A atividade chamada termina quando `beginCall` retorna, `endCall` retorna ou quando o retorno de chamada retorna se foi chamado a partir dessa atividade.  
  
### <a name="asynchronous-client-without-callback"></a>Cliente assíncrono sem retorno de chamada  
  
#### <a name="propagation-is-enabled-on-both-sides-using-http"></a>A propagação está habilitada em ambos os lados, usando HTTP  

 ![Cliente assíncrono sem nenhum retorno de chamada, em que propagateActivity está definido como true em ambos os lados.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-no-callback.gif)
  
 Se `propagateActivity=true` , ProcessMessage indica a atividade processAction a ser transferida.  
  
 Para cenários baseados em HTTP, ReceiveBytes é invocado na primeira mensagem a ser enviada e existe durante o tempo de vida da solicitação.  
  
#### <a name="propagation-is-disabled-on-either-sides-using-http"></a>A propagação está desabilitada em qualquer um dos lados, usando HTTP  

 Se `propagateActivity=false` , em ambos os lados, ProcessMessage não indicar qual atividade processAction será transferida. Portanto, uma nova atividade processAction temporária com uma nova ID é invocada. Quando a resposta assíncrona é correspondida à solicitação no código de ServiceModel, a ID da atividade pode ser recuperada do contexto local. A atividade processAction real pode ser transferida para com essa ID.  
  
 ![Cliente assíncrono sem nenhum retorno de chamada, em que propagateActivity está definido como false em ambos os lados.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-disabled-either-side.gif)  

 Para cenários baseados em HTTP, ReceiveBytes é invocado na primeira mensagem a ser enviada e existe durante o tempo de vida da solicitação.  
  
 Uma atividade processar ação é criada em um cliente assíncrono quando `propagateActivity=false` no chamador ou receptor, e quando a mensagem de resposta não inclui um cabeçalho de ação.  
  
#### <a name="propagation-is-enabled-on-both-sides-using-tcp-or-named-pipe"></a>A propagação é habilitada em ambos os lados, usando TCP ou pipe nomeado  

 ![Cliente assíncrono sem nenhum retorno de chamada, em que propagateActivity está definido como true em ambos os lados e pipe nomeado/TCP.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-enabled-using-tcp.gif)  
  
 Para um cenário baseado em Named-Pipe ou TCP, ReceiveBytes é invocado quando o cliente é aberto e existe durante o tempo de vida da conexão.  
  
 Semelhante à primeira imagem, If `propagateActivity=true` , ProcessMessage indica a atividade processAction a ser transferida.  
  
#### <a name="propagation-is-disabled-on-either-sides-using-tcp-or-named-pipe"></a>A propagação está desabilitada em qualquer um dos lados, usando TCP ou pipe nomeado  

 Para um cenário baseado em Named-Pipe ou TCP, ReceiveBytes é invocado quando o cliente é aberto e existe durante o tempo de vida da conexão.  
  
 Semelhante à segunda imagem, se estiver `propagateActivity=false` em ambos os lados, ProcessMessage não indica qual atividade processAction transferir para. Portanto, uma nova atividade processAction temporária com uma nova ID é invocada. Quando a resposta assíncrona é correspondida à solicitação no código de ServiceModel, a ID da atividade pode ser recuperada do contexto local. A atividade processAction real pode ser transferida para com essa ID.  
  
 ![Cliente assíncrono sem nenhum retorno de chamada em que propagateActivity está definido como false em ambos os lados e pipe nomeado/TCP.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-scenario-propagation-disabled-using-tcp.gif)  

### <a name="asynchronous-client-with-callback"></a>Cliente assíncrono com retorno de chamada  

 Esse cenário adiciona as atividades G e A ', para o retorno de chamada e e `endCall` suas transferências para dentro/para fora.  
  
 Esta seção demonstra apenas o uso de HTTP com o `propagateActivity` = `true` . No entanto, as atividades e transferências adicionais também se aplicam aos outros casos (ou seja, `propagateActivity` = `false` usando TCP ou pipe nomeado).  
  
 O retorno de chamada cria uma nova atividade (G) quando o cliente chama o código do usuário para notificar que os resultados estão prontos. Em seguida, o código do usuário chama `endCall` o retorno de chamada (como mostrado na Figura 5) ou fora do retorno de chamada (Figura 6). Como não é conhecido qual atividade do usuário `endCall` está sendo chamada, essa atividade é rotulada `A’` . É possível que um ' possa ser idêntico ou diferente de um.  
  
 ![Mostra um cliente assíncrono com retorno de chamada, EndCall em chamada de retorno.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-callback-endcall-in-callback.gif)  

 ![Mostra um cliente assíncrono com retorno de chamada, EndCall externo.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-client-callback-endcall-outside-callback.gif)  

### <a name="asynchronous-server-with-callback"></a>Servidor assíncrono com retorno de chamada  

 ![Mostra um servidor assíncrono com retorno de chamada.](./media/asynchronous-scenarios-using-http-tcp-or-named-pipe/asynchronous-server-callback.gif)  

 A pilha de canais retorna de volta o cliente na mensagem de recebimento: os rastreamentos para esse processamento são emitidos na própria atividade ProcessRequest.  
  
## <a name="asynchronous-requestreply-with-errors"></a>Solicitação/resposta assíncrona com erros  

 Erros de mensagem de falha são recebidos durante `endCall` . Caso contrário, as atividades e transferências são semelhantes aos cenários anteriores.  
  
## <a name="asynchronous-one-way-with-or-without-errors"></a>One-Way assíncrona com ou sem erros  

 Nenhuma resposta ou falha é retornada ao cliente.
