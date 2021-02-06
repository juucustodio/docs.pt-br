---
description: 'Saiba mais sobre: entendendo alterações de estado'
title: Noções básicas de alterações de estado
ms.date: 03/30/2017
ms.assetid: a79ed2aa-e49a-47a8-845a-c9f436ec9987
ms.openlocfilehash: e537a7421ffa8ab924e4e9e4ab841343245534b2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644002"
---
# <a name="understanding-state-changes"></a>Noções básicas de alterações de estado

Este tópico discute os Estados e as transições que os canais têm, os tipos usados para estruturar os Estados de canal e como implementá-los.  
  
## <a name="state-machines-and-channels"></a>Máquinas e canais de estado  

 Os objetos que lidam com a comunicação, por exemplo, soquetes, geralmente apresentam uma máquina de estado cujas transições de estado se relacionam à alocação de recursos de rede, fazendo ou aceitando conexões, fechando conexões e encerrando a comunicação. A máquina de estado do canal fornece um modelo uniforme dos Estados de um objeto de comunicação que abstrai a implementação subjacente desse objeto. A <xref:System.ServiceModel.ICommunicationObject> interface fornece um conjunto de Estados, métodos de transição de estado e eventos de transição de estado. Todos os canais, fábricas de canal e ouvintes de canal implementam o computador de estado do canal.  
  
 Os eventos fechados, fechando, com falha, abertura e abertura sinalizam um observador externo após a ocorrência de uma transição de estado.  
  
 Os métodos anulam, fecham e abrem (e seus equivalentes assíncronos) causam transições de estado.  
  
 A propriedade State retorna o estado atual, conforme definido por <xref:System.ServiceModel.CommunicationState> :  
  
## <a name="icommunicationobject-communicationobject-and-states-and-state-transition"></a>ICommunicationObject, CommunicationObject e Estados e transição de estado  

 Um <xref:System.ServiceModel.ICommunicationObject> começa no estado criado em que suas várias propriedades podem ser configuradas. Uma vez no estado aberto, o objeto é utilizável para enviar e receber mensagens, mas suas propriedades são consideradas imutáveis. Uma vez no estado de fechamento, o objeto não pode mais processar novas solicitações de envio ou recebimento, mas as solicitações existentes têm a oportunidade de serem concluídas até que o tempo limite de fechamento seja atingido.  Se ocorrer um erro irrecuperável, o objeto passará para o estado com falha, no qual ele pode ser inspecionado para obter informações sobre o erro e, eventualmente, fechado. Quando estiver no estado closed, o objeto atingiu basicamente o final da máquina de estado. Depois que um objeto transita de um estado para o outro, ele não volta para um estado anterior.  
  
 O diagrama a seguir mostra os <xref:System.ServiceModel.ICommunicationObject> Estados e as transições de estado. As transições de estado podem ser causadas pela chamada de um dos três métodos: Abort, Open ou Close. Eles também podem ser causados pela chamada de outros métodos específicos de implementação. A transição para o estado com falha pode ocorrer como resultado de erros ao abrir ou depois de ter aberto o objeto de comunicação.  
  
 Cada <xref:System.ServiceModel.ICommunicationObject> começa no estado criado. Nesse estado, um aplicativo pode configurar o objeto definindo suas propriedades. Quando um objeto está em um estado diferente de criado, ele é considerado imutável.  
  
 ![Diagrama de Dataflow da transição de estado do canal.](./media/understanding-state-changes/channel-state-transitions.gif)  
Figura 1. A máquina de estado ICommunicationObject.  
  
 Windows Communication Foundation (WCF) fornece uma classe base abstrata chamada <xref:System.ServiceModel.Channels.CommunicationObject> que implementa <xref:System.ServiceModel.ICommunicationObject> e a máquina de estado do canal. O gráfico a seguir é um diagrama de estado modificado que é específico do <xref:System.ServiceModel.Channels.CommunicationObject> . Além do computador de <xref:System.ServiceModel.ICommunicationObject> estado, ele mostra o intervalo quando métodos adicionais <xref:System.ServiceModel.Channels.CommunicationObject> são invocados.  
  
 ![Diagrama de Dataflow das alterações de estado de implementação do CommunicationObject.](./media/understanding-state-changes/communicationobject-implementation-state-machine.gif)
Figura 2. A implementação de CommunicationObject do computador de estado ICommunicationObject, incluindo chamadas para eventos e métodos protegidos.  
  
### <a name="icommunicationobject-events"></a>Eventos de ICommunicationObject  

 <xref:System.ServiceModel.Channels.CommunicationObject> expõe os cinco eventos definidos pelo <xref:System.ServiceModel.ICommunicationObject> . Esses eventos são projetados para o código que usa o objeto de comunicação para ser notificado de transições de estado. Conforme mostrado na Figura 2 acima, cada evento é disparado uma vez após a transição do estado do objeto para o estado nomeado pelo evento. Todos os cinco eventos são do `EventHandler` tipo que é definido como:  
  
 `public delegate void EventHandler(object sender, EventArgs e);`  
  
 Na <xref:System.ServiceModel.Channels.CommunicationObject> implementação, o remetente é o <xref:System.ServiceModel.Channels.CommunicationObject> próprio ou o que foi passado como o remetente para o <xref:System.ServiceModel.Channels.CommunicationObject> Construtor (se a sobrecarga do Construtor foi usada). O parâmetro EventArgs, `e` , é sempre `EventArgs.Empty` .  
  
### <a name="derived-object-callbacks"></a>Retornos de chamada do objeto derivado  

 Além dos cinco eventos, o <xref:System.ServiceModel.Channels.CommunicationObject> declara oito métodos virtuais protegidos projetados para permitir que um objeto derivado seja chamado de volta antes e depois que as transições de estado ocorrerem.  
  
 Os <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A?displayProperty=nameWithType> <xref:System.ServiceModel.Channels.CommunicationObject.Close%2A?displayProperty=nameWithType> métodos e têm três retornos de chamada associados a cada um deles. Por exemplo, correspondente a <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A?displayProperty=nameWithType> há <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A?displayProperty=nameWithType> , <xref:System.ServiceModel.Channels.CommunicationObject.OnOpen%2A?displayProperty=nameWithType> , e <xref:System.ServiceModel.Channels.CommunicationObject.OnOpened%2A?displayProperty=nameWithType> . Associados aos <xref:System.ServiceModel.Channels.CommunicationObject.Close%2A?displayProperty=nameWithType> são os <xref:System.ServiceModel.Channels.CommunicationObject.OnClose%2A?displayProperty=nameWithType> <xref:System.ServiceModel.Channels.CommunicationObject.OnClosing%2A?displayProperty=nameWithType> métodos, e <xref:System.ServiceModel.Channels.CommunicationObject.OnClosed%2A?displayProperty=nameWithType> .  
  
 Da mesma forma, o <xref:System.ServiceModel.Channels.CommunicationObject.Abort%2A?displayProperty=nameWithType> método tem um correspondente <xref:System.ServiceModel.Channels.CommunicationObject.OnAbort%2A?displayProperty=nameWithType> .  
  
 Enquanto <xref:System.ServiceModel.Channels.CommunicationObject.OnOpen%2A?displayProperty=nameWithType> , <xref:System.ServiceModel.Channels.CommunicationObject.OnClose%2A?displayProperty=nameWithType> e <xref:System.ServiceModel.Channels.CommunicationObject.OnAbort%2A?displayProperty=nameWithType> não têm implementação padrão, os outros retornos de chamada têm uma implementação padrão que é necessária para a exatidão da máquina de estado. Se você substituir esses métodos, certifique-se de chamar a implementação base ou substituí-la corretamente.  
  
 <xref:System.ServiceModel.Channels.CommunicationObject.OnOpening%2A?displayProperty=nameWithType>, <xref:System.ServiceModel.Channels.CommunicationObject.OnClosing%2A?displayProperty=nameWithType> e <xref:System.ServiceModel.Channels.CommunicationObject.OnFaulted%2A?displayProperty=nameWithType> aciona os <xref:System.ServiceModel.Channels.CommunicationObject.Opening?displayProperty=nameWithType> eventos correspondentes <xref:System.ServiceModel.Channels.CommunicationObject.Closing?displayProperty=nameWithType> e <xref:System.ServiceModel.Channels.CommunicationObject.Faulted?displayProperty=nameWithType> . <xref:System.ServiceModel.Channels.CommunicationObject.OnOpened%2A?displayProperty=nameWithType> e <xref:System.ServiceModel.Channels.CommunicationObject.OnClosed%2A?displayProperty=nameWithType> defina o estado do objeto como aberto e fechado respectivamente e, em seguida, acione os <xref:System.ServiceModel.Channels.CommunicationObject.Opened?displayProperty=nameWithType> eventos e correspondentes <xref:System.ServiceModel.Channels.CommunicationObject.Closed?displayProperty=nameWithType> .  
  
### <a name="state-transition-methods"></a>Métodos de transição de estado  

 <xref:System.ServiceModel.Channels.CommunicationObject> fornece implementações de abortar, fechar e abrir. Ele também fornece um método Fault que causa uma transição de estado para o estado com falha. A Figura 2 mostra a <xref:System.ServiceModel.ICommunicationObject> máquina de estado com cada transição rotulada pelo método que a causa (as transições não rotuladas acontecem dentro da implementação do método que causou a transição do último rótulo).  
  
> [!NOTE]
> Todas as <xref:System.ServiceModel.Channels.CommunicationObject> implementações do estado de comunicação Obtém/define são sincronizadas por thread.  
  
 Construtor  
  
 <xref:System.ServiceModel.Channels.CommunicationObject> fornece três construtores, todos os quais deixam o objeto no estado criado. Os construtores são definidos como:  
  
 O primeiro construtor é um construtor sem parâmetros que delega para a sobrecarga do construtor que usa um objeto:  
  
 `protected CommunicationObject() : this(new object()) { … }`  
  
 O construtor que recebe um objeto usa esse parâmetro como o objeto a ser bloqueado ao sincronizar o acesso ao estado do objeto de comunicação:  
  
 `protected CommunicationObject(object mutex) { … }`  
  
 Por fim, um terceiro construtor usa um parâmetro adicional que é usado como o argumento de remetente quando os <xref:System.ServiceModel.ICommunicationObject> eventos são acionados.  
  
 `protected CommunicationObject(object mutex, object eventSender) { … }`  
  
 Os dois construtores anteriores definem o remetente como este.  
  
 Abrir método  
  
 Pré-condição: o estado é criado.  
  
 Pós-condição: o estado é aberto ou apresenta falha. Pode gerar uma exceção.  
  
 O método Open () tentará abrir o objeto de comunicação e definirá o estado como aberto. Se encontrar um erro, ele definirá o estado como falho.  
  
 O método primeiro verifica se o estado atual foi criado. Se o estado atual for abrindo ou aberto, ele lançará um <xref:System.InvalidOperationException> . Se o estado atual estiver fechando ou fechado, ele lançará um <xref:System.ServiceModel.CommunicationObjectAbortedException> se o objeto tiver sido encerrado e <xref:System.ObjectDisposedException> , de outra forma,. Se o estado atual tiver falhado, ele lançará um <xref:System.ServiceModel.CommunicationObjectFaultedException> .  
  
 Em seguida, ele define o estado como abrindo e chama OnOpening () (que gera o evento de abertura), OnOpen () e OnOpened () nessa ordem. OnOpened () define o estado como aberto e gera o evento Open. Se qualquer um desses gera uma exceção, Open () chama Fault () e permite que a exceção seja emergida. O diagrama a seguir mostra o processo aberto mais detalhadamente.  
  
 ![Diagrama de Dataflow das alterações de estado ICommunicationObject. Open.](./media/understanding-state-changes/ico-open-process-override-onopen.gif)  
Substitua o método OnOpen para implementar uma lógica aberta personalizada, como abrir um objeto de comunicação interno.  
  
 Método Close  
  
 Pré-condição: nenhuma.  
  
 Pós-condição: o estado é fechado. Pode gerar uma exceção.  
  
 O método Close () pode ser chamado em qualquer Estado. Ele tenta fechar o objeto normalmente. Se um erro for encontrado, ele encerrará o objeto. O método não fará nada se o estado atual estiver fechando ou fechado. Caso contrário, ele definirá o estado como fechando. Se o estado original foi criado, aberto ou falho, ele chama Abort () (consulte o diagrama a seguir). Se o estado original foi aberto, ele chama OnClosing () (que gera o evento de fechamento), fechamento () e oncloseed () nessa ordem. Se qualquer um deles lançar uma exceção, fechar () chamará Abort () e permitirá que a exceção seja emergida. Oncloseed () define o estado como Closed e gera o evento Closed. O diagrama a seguir mostra o processo de fechamento mais detalhadamente.  
  
 ![Diagrama de Dataflow das alterações de estado ICommunicationObject. Close.](./media/understanding-state-changes/ico-close-process-override-onclose.gif)  
Substitua o método fechamento para implementar uma lógica de fechamento personalizada, como fechar um objeto de comunicação interno. Toda a lógica de fechamento normal que pode ser bloqueada por um longo tempo (por exemplo, aguardando que o outro lado responda) deve ser implementada em fechamento () porque ela usa um parâmetro de tempo limite e não é chamada como parte de Abort ().  
  
 Anular  
  
 Pré-condição: nenhuma.  
Pós-condição: o estado é fechado. Pode gerar uma exceção.  
  
 O método Abort () não fará nada se o estado atual for fechado ou se o objeto tiver sido encerrado antes (por exemplo, possivelmente com Abort () em execução em outro thread). Caso contrário, ele define o estado para fechar e chama OnClosing () (que gera o evento de fechamento), OnAbort () e oncloseed () nessa ordem (não chama fechamento porque o objeto está sendo encerrado, não fechado). Oncloseed () define o estado como Closed e gera o evento Closed. Se qualquer uma delas lançar uma exceção, ela será relançada para o chamador da anulação. As implementações de onfechamento (), oncloseed () e OnAbort () não devem bloquear (por exemplo, na entrada/saída). O diagrama a seguir mostra o processo de anulação mais detalhadamente.  
  
 ![Diagrama de Dataflow das alterações de estado ICommunicationObject. Abort.](./media/understanding-state-changes/ico-abort-process-override-onabort.gif)  
Substitua o método OnAbort para implementar uma lógica de término personalizada, como encerrar um objeto de comunicação interno.  
  
 Falha  
  
 O método fault é específico <xref:System.ServiceModel.Channels.CommunicationObject> do e não faz parte da <xref:System.ServiceModel.ICommunicationObject> interface. Ele está incluído aqui para fins de integridade.  
  
 Pré-condição: nenhuma.  
  
 Pós-condição: estado com falha. Pode gerar uma exceção.  
  
 O método Fault () não fará nada se o estado atual tiver falhado ou fechado. Caso contrário, ele definirá o estado como falho e chamará OnFaulted (), que gera o evento com falha. Se onfaultd lançar uma exceção, ela será relançada.  
  
### <a name="throwifxxx-methods"></a>Métodos ThrowIfXxx  

 CommunicationObject tem três métodos protegidos que podem ser usados para gerar exceções se o objeto estiver em um estado específico.  
  
 <xref:System.ServiceModel.Channels.CommunicationObject.ThrowIfDisposed%2A> gera uma exceção se o estado estiver fechando, fechado ou com falha.  
  
 <xref:System.ServiceModel.Channels.CommunicationObject.ThrowIfDisposedOrImmutable%2A> gera uma exceção se o estado não for criado.  
  
 <xref:System.ServiceModel.Channels.CommunicationObject.ThrowIfDisposedOrNotOpen%2A> gera uma exceção se o estado não for aberto.  
  
 As exceções geradas dependem do estado. A tabela a seguir mostra os diferentes Estados e o tipo de exceção correspondente lançado chamando um ThrowIfXxx que é gerado nesse estado.  
  
|Estado|A anulação foi chamada?|Exceção|  
|-----------|----------------------------|---------------|  
|Criado|N/D|<xref:System.InvalidOperationException?displayProperty=nameWithType>|  
|Abertura|N/D|<xref:System.InvalidOperationException?displayProperty=nameWithType>|  
|Aberto|N/D|<xref:System.InvalidOperationException?displayProperty=nameWithType>|  
|Fechamento|Sim|<xref:System.ServiceModel.CommunicationObjectAbortedException?displayProperty=nameWithType>|  
|Fechamento|Não|<xref:System.ObjectDisposedException?displayProperty=nameWithType>|  
|Fechadas|Sim|<xref:System.ServiceModel.CommunicationObjectAbortedException?displayProperty=nameWithType> no caso de um objeto ser fechado por uma chamada anterior e explícita de Abort. Se você chamar fechar no objeto, um <xref:System.ObjectDisposedException?displayProperty=nameWithType> será lançado.|  
|Fechadas|Não|<xref:System.ObjectDisposedException?displayProperty=nameWithType>|  
|Com falha|N/D|<xref:System.ServiceModel.CommunicationObjectFaultedException?displayProperty=nameWithType>|  
  
### <a name="timeouts"></a>Tempos limite  

 Vários dos métodos que discutimos têm parâmetros de tempo limite. Esses são próximos, abertos (certas sobrecargas e versões assíncronas), fechamento e OnOpen. Esses métodos são projetados para permitir operações demoradas (por exemplo, bloqueio na entrada/saída enquanto fecham uma conexão normalmente) para que o parâmetro timeout indique quanto tempo essas operações podem levar antes de serem interrompidas. As implementações de qualquer um desses métodos devem usar o valor de tempo limite fornecido para garantir que ele retorne ao chamador dentro desse tempo limite. Implementações de outros métodos que não têm um tempo limite não são projetadas para operações demoradas e não devem ser bloqueadas na entrada/saída.  
  
 A exceção são as sobrecargas Open () e Close () que não têm um tempo limite. Eles usam um valor de tempo limite padrão fornecido pela classe derivada. <xref:System.ServiceModel.Channels.CommunicationObject> expõe duas propriedades abstratas protegidas nomeadas <xref:System.ServiceModel.Channels.CommunicationObject.DefaultCloseTimeout%2A> e <xref:System.ServiceModel.Channels.CommunicationObject.DefaultOpenTimeout%2A> definidas como:  
  
 `protected abstract TimeSpan DefaultCloseTimeout { get; }`  
  
 `protected abstract TimeSpan DefaultOpenTimeout { get; }`  
  
 Uma classe derivada implementa essas propriedades para fornecer o tempo limite padrão para as sobrecargas Open () e Close () que não usam um valor de tempo limite. Em seguida, as implementações Open () e Close () delegam para a sobrecarga que usa um tempo limite que passa o valor de tempo limite padrão, por exemplo:  
  
 `public void Open()`  
  
 `{`  
  
 `this.Open(this.DefaultOpenTimeout);`  
  
 `}`  
  
#### <a name="idefaultcommunicationtimeouts"></a>IDefaultCommunicationTimeouts  

 Esta interface tem quatro propriedades somente leitura para fornecer valores de tempo limite padrão para abrir, enviar, receber e fechar. Cada implementação é responsável por obter os valores padrão de qualquer maneira apropriada. Como uma conveniência e, por <xref:System.ServiceModel.Channels.ChannelFactoryBase> <xref:System.ServiceModel.Channels.ChannelListenerBase> padrão, esses valores são de 1 minuto a cada.
