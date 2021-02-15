---
description: 'Saiba mais sobre: práticas recomendadas para sessões confiáveis'
title: Práticas recomendadas para sessões confiáveis
ms.date: 03/30/2017
ms.assetid: b94f6e01-8070-40b6-aac7-a2cb7b4cb4f2
ms.openlocfilehash: 4b05dd914d2c5b8ec7941417b727bec1e5b43ba4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99643664"
---
# <a name="best-practices-for-reliable-sessions"></a>Práticas recomendadas para sessões confiáveis

Este tópico discute as práticas recomendadas para sessões confiáveis.

## <a name="setting-maxtransferwindowsize"></a>Configurando MaxTransferWindowSize

As sessões confiáveis no Windows Communication Foundation (WCF) usam uma janela de transferência para manter as mensagens no cliente e no serviço. A propriedade configurável <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> indica quantas mensagens a janela de transferência pode conter.

No remetente, isso indica quantas mensagens a janela de transferência pode conter ao aguardar confirmações; no receptor, ele indica quantas mensagens armazenar em buffer para o serviço.

Escolher o tamanho certo afeta a eficiência da rede e a capacidade ideal do serviço. As seções a seguir detalham o que considerar ao escolher um valor para essa propriedade e o impacto do valor.

O tamanho da janela de transferência padrão é oito mensagens.

### <a name="efficient-use-of-the-network"></a>Uso eficiente da rede

Nesse contexto, o termo *rede* corresponde a tudo usado como a base da comunicação entre um cliente (remetente) e um serviço (receptor). Isso inclui as conexões de transporte e qualquer intermediário ou ponte entre, incluindo roteadores SOAP ou proxies/firewalls HTTP.

O uso eficiente da rede garante que a capacidade da rede seja totalmente usada. A quantidade de dados que podem ser transferidos por segundo pela rede (taxa de *dados*) e o tempo necessário para transferir dados do remetente para o receptor (*latência*) impactam a eficácia com que a rede é utilizada.

No remetente, a propriedade <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> indica quantas mensagens sua janela de transferência pode conter ao aguardar confirmações. Se a latência de rede for alta e para garantir um remetente responsivo e uma utilização de rede eficaz, você deverá aumentar o tamanho da janela de transferência.

Por exemplo, mesmo que o remetente continue com a taxa de dados, a latência poderá ser alta se existirem vários intermediários entre o remetente e o destinatário ou os dados precisarem passar por uma rede ou um intermediário com perdas. Portanto, o remetente precisa aguardar as confirmações das mensagens em sua janela de transferência antes de aceitar novas mensagens para envio na conexão. Quanto menor o buffer com alta latência, menor a eficiência da utilização da rede. Por outro lado, um tamanho de janela de transferência muito alto pode afetar o serviço, pois o serviço pode precisar acompanhar a alta taxa de dados enviados pelo cliente.

### <a name="running-the-service-to-capacity"></a>Executando o serviço para a capacidade

Tanto quanto a rede for usada com eficiência, o ideal é que você também queira que o serviço seja executado com capacidade ideal. A propriedade tamanho da janela de transferência no receptor indica quantas mensagens o receptor pode armazenar em buffer. Esse buffer de mensagens ajuda não apenas o controle de fluxo de rede, mas também permite que o serviço seja executado com capacidade total. Por exemplo, se o buffer for uma mensagem e as mensagens chegarem mais rápido do que o serviço pode processá-las, a rede poderá remover mensagens e a capacidade poderá ser desperdiçada ou subutilizada.

O uso de um buffer aumenta a disponibilidade do serviço, pois ele recebe e armazena em buffers simultaneamente uma mensagem durante o processamento das mensagens recebidas anteriormente.

Recomendamos que você use o mesmo `MaxTransferWindowSize` no remetente e no destinatário.

### <a name="enabling-flow-control"></a>Habilitando o controle de fluxo

O *controle de fluxo* é um mecanismo que garante que o remetente e o destinatário mantenham o ritmo entre si, ou seja, as mensagens são consumidas e trabalhadas tão rapidamente quanto são produzidas. O tamanho da janela de transferência no cliente e no serviço garante que o remetente e o destinatário estejam dentro de uma janela razoável de sincronização.

É altamente recomendável que você defina a propriedade <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled%2A> como `true` quando estiver usando uma sessão confiável entre um cliente WCF e um serviço WCF.

## <a name="setting-maxpendingchannels"></a>Configurando MaxPendingChannels

Ao escrever um serviço que permite a comunicação de sessão confiável de diferentes clientes, é possível ter muitos clientes estabelecendo uma sessão confiável para o serviço ao mesmo tempo. A resposta do serviço nessas situações depende da `MaxPendingChannels` propriedade.

Quando o remetente cria um canal de sessão confiável para um receptor, um handshake entre eles estabelece uma sessão confiável. Depois que a sessão confiável é estabelecida, o canal é colocado em uma fila de canal pendente para a aceitação pelo serviço. A `MaxPendingChannels` propriedade indica quantos canais podem estar nesse estado.

É possível que o serviço esteja em um estado em que ele não aceite mais canais. Se a fila estiver cheia, uma tentativa de estabelecer uma sessão confiável será rejeitada e o cliente deverá tentar novamente.

Também é possível que os canais pendentes na fila permaneçam na fila por uma duração maior. Enquanto isso, um tempo limite de inatividade na sessão confiável pode ocorrer, fazendo com que o canal faça a transição para um estado com falha.

Ao escrever um serviço que atende a vários clientes simultaneamente, você deve definir um valor adequado às suas necessidades. Definir um valor muito alto para a `MaxPendingChannels` propriedade afeta seu conjunto de trabalho.

O valor padrão para o <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxPendingChannels%2A> é de quatro canais.

## <a name="reliable-sessions-and-hosting"></a>Hospedagem e sessões confiáveis

Quando a Web hospeda um serviço que usa sessões confiáveis, você deve manter as seguintes considerações importantes em mente:

- As sessões confiáveis são monitoradas e o estado é mantido no AppDomain. Isso significa que todas as mensagens que fazem parte de uma sessão confiável devem ser processadas no mesmo AppDomain. Web farms e ambientes Web em que o tamanho do farm ou do jardim é maior que um nó não pode garantir essa restrição.

- As sessões confiáveis que usam canais HTTP duplos (por exemplo, usando `WsDualHttpBinding` ) podem exigir mais do que o padrão de duas conexões http por cliente. Isso significa que uma sessão confiável duplex pode exigir até duas conexões, cada uma delas porque as mensagens simultâneas de aplicativo e protocolo podem ser transformadas cada uma delas em um determinado momento. Em determinadas condições, dependendo do padrão de troca de mensagens do serviço, isso significa que é possível fazer o deadlock de um serviço hospedado na Web usando HTTP duplo e sessões confiáveis. Para aumentar o número de conexões HTTP permitidas por cliente, adicione o seguinte ao arquivo de configuração relevante (por exemplo, *web.config* do serviço em questão):

  ```xml
  <configuration>
    <system.net>
      <connectionManagement>
        <add name="*" maxconnection="4" />
      </connectionManagement>
    </system.net>
  </configuration>
  ```

  O valor do `maxconnection` atributo é o número de conexões necessárias. O mínimo, nesse caso, deve ser de quatro conexões.
