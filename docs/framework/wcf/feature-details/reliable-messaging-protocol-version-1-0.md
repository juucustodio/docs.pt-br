---
description: 'Saiba mais sobre: protocolo de mensagens confiáveis versão 1,0'
title: Protocolo de mensagens confiável versão 1.0
ms.date: 03/30/2017
ms.assetid: a5509a5c-de24-4bc2-9a48-19138055dcce
ms.openlocfilehash: dbd0184fd6ea9f92c96639d71088ac61bec20f3e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99793591"
---
# <a name="reliable-messaging-protocol-version-10"></a>Protocolo de mensagens confiável versão 1.0

Este tópico aborda os detalhes de implementação do Windows Communication Foundation (WCF) para o protocolo WS-Reliable de mensagens de fevereiro de 2005 (versão 1,0) necessário para interoperação usando o transporte HTTP. O WCF segue as WS-Reliable especificação de mensagens com as restrições e esclarecimentos explicados neste tópico. Observe que o protocolo WS-ReliableMessaging versão 1,0 é implementado a partir do WinFX.

O protocolo WS-Reliable sistema de mensagens de fevereiro de 2005 é implementado no WCF pelo <xref:System.ServiceModel.Channels.ReliableSessionBindingElement> .

Para sua conveniência, o tópico usa as seguintes funções:

- Iniciador: o cliente que inicia WS-Reliable a criação da sequência de mensagens

- Respondente: o serviço que recebe as solicitações do iniciador

Este documento usa os prefixos e namespaces na tabela a seguir.

|Prefixo|Namespace|
|------------|---------------|
|WSRM|`http://schemas.xmlsoap.org/ws/2005/02/rm`|
|netrm|`http://schemas.microsoft.com/ws/2006/05/rm`|
|s|`http://www.w3.org/2003/05/soap-envelope`|
|WSA|`http://schemas.xmlsoap.org/ws/2005/08/addressing`|
|wsse|`http://docs.oasis-open.org/wss/2004/01/oasis-200401-wssecurity-secext-1.0.xsd`|

## <a name="messaging"></a>Mensagens

### <a name="sequence-establishment-messages"></a>Mensagens de estabelecimento de sequência

O WCF implementa `CreateSequence` e `CreateSequenceResponse` mensagens para estabelecer uma sequência de mensagens confiável. As seguintes restrições se aplicam:

- B1101: o iniciador do WCF não gera o elemento Expires opcional na `CreateSequence` mensagem ou, nos casos em que a `CreateSequence` mensagem contém um `Offer` elemento, o `Expires` elemento opcional no `Offer` elemento.

- B1102: ao acessar a `CreateSequence` mensagem, o WCF `Responder` envia e recebe os dois `Expires` elementos, se existirem, mas não usa seus valores.

WS-Reliable mensagens introduz o `Offer` mecanismo para estabelecer as duas sequências correlacionadas que formam uma sessão.

- R1103: se `CreateSequence` contiver um `Offer` elemento, o respondente de mensagens confiáveis deverá aceitar a sequência e responder com `CreateSequenceResponse` que contenha um `wsrm:Accept` elemento, formando duas sequências de converso correlacionadas ou rejeitar a `CreateSequence` solicitação.

- R1104: `SequenceAcknowledgement` e as mensagens de aplicativo que fluem na sequência de converso devem ser enviadas para a `ReplyTo` referência do ponto de extremidade do `CreateSequence` .

- R1105: `AcksTo` e `ReplyTo` referências de ponto de extremidade no `CreateSequence` devem ter valores de endereço que correspondam ao octeto.

  O respondente do WCF verifica se a parte do URI de `AcksTo` e `ReplyTo` EPRS são idênticas antes de criar uma sequência.

- R1106: `AcksTo` e `ReplyTo` referências de ponto de extremidade no `CreateSequence` devem ter o mesmo conjunto de parâmetros de referência.

  O WCF não se aplica, mas pressupõe que [parâmetros de referência] de `AcksTo` e `ReplyTo` em `CreateSequence` são idênticos e usa [parâmetros de referência] de `ReplyTo` referência de ponto de extremidade para confirmações e mensagens de sequência de inverso.

- R1107: quando duas sequências de conversos são estabelecidas usando o `Offer` mecanismo, `SequenceAcknowledgement` e as mensagens de aplicativo que fluem em sequências de contraversais devem ser enviadas à `ReplyTo` referência do ponto de extremidade do `CreateSequence` .

- R1108: quando duas sequências de converso são estabelecidas usando o mecanismo de oferta, a `[address]` Propriedade do `wsrm:AcksTo` elemento filho de referência do ponto de extremidade do `wsrm:Accept` elemento de `CreateSequenceResponse` deve corresponder ao URI de destino do `CreateSequence` .

- R1109: quando duas seqüências de converso são estabelecidas usando o `Offer` mecanismo, as mensagens enviadas pelo iniciador e confirmações para mensagens pelo Respondente devem ser enviadas para a mesma referência de ponto de extremidade.

  O WCF usa WS-Reliable mensagens para estabelecer sessões confiáveis entre o iniciador e o respondente. A implementação de mensagens WS-Reliable do WCF fornece uma sessão confiável para os padrões unidirecional, resposta de solicitação e mensagens duplex completos. O mecanismo de mensagens WS-Reliable `Offer` no `CreateSequence` / `CreateSequenceResponse` permite que você estabeleça duas sequências de contraverse correlacionadas e fornece um protocolo de sessão que é adequado para todos os pontos de extremidade da mensagem. Como o WCF fornece uma garantia de segurança para tal sessão, incluindo proteção de ponta a ponta para integridade da sessão, é prático garantir que as mensagens pretendidas para a mesma parte cheguem ao mesmo destino. Isso também permite transportado de confirmações de sequência em mensagens de aplicativo. Portanto, as restrições R1104, R1105 e R1108 se aplicam ao WCF.

Um exemplo de uma `CreateSequence` mensagem.

```xml
<s:Envelope>
  <s:Header>
    <a:Action s:mustUnderstand="1">
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequence
    </a:Action>
    <a:ReplyTo>
      <a:Address>
         http://Business456.com/clientA
      </a:Address>
    </a:ReplyTo>
    <a:MessageID>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </a:MessageID>
    <a:To s:mustUnderstand="1">
      http://Business456.com/clientA
    </a:To>
  </s:Header>
  <s:Body>
    <wsrm:CreateSequence>
      <wsrm:AcksTo>
       <wsa:Address>
         http://Business456.com/clientA
       </wsa:Address>
     </wsrm:AcksTo>
     <wsrm:Offer>
      <wsrm:Identifier>
        urn:uuid:0afb8d36-bf26-4776-b8cf-8c91fddb5496
      </wsrm:Identifier>
     </wsrm:Offer>
   </wsrm:CreateSequence>
  </s:Body>
</s:Envelope>
```

 Um exemplo de uma `CreateSequenceResponse` mensagem.

```xml
<s:Envelope>
  <s:Header>
    <a:Action s:mustUnderstand="1">
      http://schemas.xmlsoap.org/ws/2005/02/rm/CreateSequenceResponse
    </a:Action>
    <a:RelatesTo>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </a:RelatesTo>
    <a:To s:mustUnderstand="1">
      http://Business456.com/clientA
    </a:To>
  </s:Header>
  <s:Body>
   <wsrm:CreateSequenceResponse>
    <Identifier>
     urn:uuid:eea0a36c-b38a-43e8-8c76-2fabe2d76386
    </Identifier>
    <Accept>
    <AcksTo>
      <a:Address>
        http://BusinessABC.com/serviceA
      </a:Address>
    </AcksTo>
    </Accept>
   </wsrm:CreateSequenceResponse>
  </s:Body>
</s:Envelope>
```

### <a name="sequence"></a>Sequência

Veja a seguir uma lista de restrições que se aplicam a sequências:

- B1201: o WCF gera e acessa números de sequência que não `xs:long` são maiores do que o valor inclusivo máximo, 9223372036854775807.

- B1202: o WCF sempre gera uma última mensagem apto para vazia com o URI de ação de `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage` .

- B1203: o WCF recebe e entrega uma mensagem com um cabeçalho de sequência que contém um `LastMessage` elemento, desde que o URI de ação não seja `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage` .

Um exemplo de um cabeçalho de sequência.

```xml
<wsrm:Sequence>
  <wsrm:Identifier>
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
  </wsrm:Identifier>
  <wsrm:MessageNumber>
    10
  </wsrm:MessageNumber>
  <wsrm:LastMessage/>
 </wsrm:Sequence>
```

### <a name="ackrequested-header"></a>Cabeçalho AckRequested

O WCF usa o `AckRequested` cabeçalho como um mecanismo Keep-Alive. O WCF não gera o `MessageNumber` elemento opcional. Após receber uma mensagem com um `AckRequested` cabeçalho que contém o `MessageNumber` elemento, o WCF ignora o `MessageNumber` valor do elemento, conforme mostrado no exemplo a seguir.

```xml
<wsrm:AckRequested>
  <wsrm:Identifier>
    urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
  </wsrm:Identifier>
</wsrm:AckRequested>
```

### <a name="sequenceacknowledgement-header"></a>Cabeçalho SequenceAcknowledgement

O WCF usa o mecanismo de transportado para confirmações de sequência fornecidas em WS-Reliable mensagens.

- R1401: quando duas sequências de conversos são estabelecidas usando o `Offer` mecanismo, o `SequenceAcknowledgement` cabeçalho pode ser incluído em qualquer mensagem de aplicativo transmitida para o destinatário pretendido.

- B1402: quando o WCF deve gerar uma confirmação antes de receber qualquer mensagem de sequência (por exemplo, para satisfazer uma `AckRequested` mensagem), o WCF gera um `SequenceAcknowledgement` cabeçalho que contém o intervalo de 0-0, conforme mostrado no exemplo a seguir.

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>
      urn:uuid:addabbbf-60cb-44d3-8c5b-9e0841629a36
    </wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="0" Lower="0"/>
  </wsrm:SequenceAcknowledgement>
  ```

- B1403: o WCF não gera `SequenceAcknowledgement` cabeçalhos que contêm um `Nack` elemento, mas dá suporte a `Nack` elementos.

### <a name="ws-reliablemessaging-faults"></a>Falhas de WS-ReliableMessaging

Veja a seguir uma lista de restrições que se aplicam à implementação do WCF de WS-Reliable falhas de mensagens:

- B1501: o WCF não gera `MessageNumberRollover` falhas.

- B1502: o ponto de extremidade do WCF pode gerar `CreateSequenceRefused` falhas conforme descrito na especificação.

- B1503: quando o ponto de extremidade de serviço atinge seu limite de conexão e não pode processar novas conexões, o WCF gera um `CreateSequenceRefused` subcódigo de falha adicional, `netrm:ConnectionLimitReached` , conforme mostrado no exemplo a seguir.

  ```xml
  <s:Envelope>
    <s:Header>
      <wsa:Action>
        http://schemas.xmlsoap.org/ws/2005/08/addressing/fault
      </wsa:Action>
    </s:Header>
    <s:Body>
      <s:Fault>
        <s:Code>
          <s:Value>
            s:Receiver
          </s:Value>
          <s:Subcode>
            <s:Value>
              wsrm:CreateSequenceRefused
            </s:Value>
            <s:Subcode>
              <s:Value>
                netrm:ConnectionLimitReached
              </s:Value>
            </s:Subcode>
          </s:Subcode>
        </s:Code>
        <s:Reason>
          <s:Text xml:lang="en">
            [Reason]
          </s:Text>
        </s:Reason>
      </s:Fault>
    </s:Body>
  </s:Envelope>
  ```

### <a name="ws-addressing-faults"></a>Falhas de WS-Addressing

Como WS-Reliable sistema de mensagens usa o WS-Addressing, o WCF WS-Reliable a implementação de mensagens pode gerar WS-Addressing falhas. Esta seção aborda as WS-Addressing falhas que o WCF gera explicitamente na camada de mensagens de WS-Reliable:

- B1601: o WCF gera o cabeçalho de endereçamento de mensagens de falha necessário quando uma das seguintes opções é verdadeira:

  - Um `Sequence` cabeçalho e um cabeçalho estão ausentes em uma mensagem `Action` .

  - `CreateSequence`Falta um cabeçalho em uma mensagem `MessageId` .

  - `CreateSequence`Falta um cabeçalho em uma mensagem `ReplyTo` .

- B1602: o WCF gera a ação de falha sem suporte em resposta a uma mensagem que não tem um `Sequence` cabeçalho e tem um `Action` cabeçalho que não é reconhecido na especificação de WS-Reliable mensagens.

- B1603: o WCF gera o ponto de extremidade de falha indisponível para indicar que o ponto de extremidade não processa a sequência com base no exame dos `CreateSequence` cabeçalhos de endereçamento da mensagem.

## <a name="protocol-composition"></a>Composição de protocolo

### <a name="composition-with-ws-addressing"></a>Composição com WS-Addressing

O WCF dá suporte a duas versões do WS-Addressing: WS-Addressing 2004/08 [WS-ADDR] e às recomendações do W3C WS-Addressing 1,0 [WS-ADDR-CORE] e [WS-ADDR-SOAP].

Embora a especificação do WS-Reliable Messaging mencione apenas WS-Addressing 2004/08, ela não restringe a versão do WS-Addressing a ser usada. Veja a seguir uma lista de restrições que se aplicam ao WCF:

- R2101: os WS-Addressing 2004/08 e WS-Addressing 1,0 podem ser usados com WS-Reliable mensagens.

- R2102: uma única versão de WS-Addressing deve ser usada em uma determinada sequência de mensagens WS-Reliable ou um par de sequências de inverso correlacionadas usando o `wsrm:Offer` mecanismo.

### <a name="composition-with-soap"></a>Composição com SOAP

O WCF dá suporte ao uso de SOAP 1,1 e SOAP 1,2 com WS-Reliable Messaging.

### <a name="composition-with-ws-security-and-ws-secureconversation"></a>Composição com WS-Security e WS-SecureConversation

O WCF fornece proteção para WS-Reliable sequências de mensagens usando transporte seguro (HTTPS), composição com WS-Security e composição com WS-Secure conversa. Veja a seguir uma lista de restrições que se aplicam ao WCF:

- R2301: para proteger a integridade de uma sequência de WS-Reliable de mensagens, além da integridade e confidencialidade de mensagens individuais, o WCF requer que WS-Secure conversa deva ser usada.

- R2302: AWS-a sessão de conversa segura deve ser estabelecida antes de estabelecer WS-Reliable sequência (s) de mensagens.

- R2303: se o tempo de vida da sequência de mensagens WS-Reliable exceder o tempo de vida da sessão de conversa WS-Secure, o `SecurityContextToken` estabelecido usando WS-Secure conversa deve ser renovado usando a associação de renovação de conversa WS-Secure correspondente.

- B2304: a sequência de mensagens do WS-Reliable ou um par de sequências correlacionadas correlatas sempre está associado a uma única sessão de WS-SecureConversation.

  A origem do WCF gera o `wsse:SecurityTokenReference` elemento na seção extensibilidade do elemento da `CreateSequence` mensagem.

- R2305: quando composto com WS-Secure conversa, uma `CreateSequence` mensagem deve conter o `wsse:SecurityTokenReference` elemento.

## <a name="ws-reliable-messaging-ws-policy-assertion"></a>Asserção de WS-Policy de mensagens WS-Reliable

O WCF usa WS-Reliable mensagem WS-Policy asserção `wsrm:RMAssertion` para descrever os recursos de pontos de extremidade. Veja a seguir uma lista de restrições que se aplicam ao WCF:

- B3001: o WCF anexa `wsrm:RMAssertion` WS-Policy asserção a `wsdl:binding` elementos. O WCF dá suporte tanto a anexos `wsdl:binding` quanto a `wsdl:port` elementos.

- B3002: o WCF dá suporte às seguintes propriedades opcionais de WS-Reliable declaração de mensagens e fornece controle sobre elas no WCF `ReliableMessagingBindingElement` :

  - `wsrm:InactivityTimeout`

  - `wsrm:AcknowledgementInterval`

  A seguir, é mostrado um exemplo.

  ```xml
  <wsrm:RMAssertion>
    <wsrm:InactivityTimeout Milliseconds="600000" />
    <wsrm:AcknowledgementInterval Milliseconds="200" />
  </wsrm:RMAssertion>
  ```

## <a name="flow-control-ws-reliable-messaging-extension"></a>Controle de fluxo WS-Reliable extensão de mensagens

O WCF usa WS-Reliable extensibilidade de mensagens para fornecer controle mais rígido adicional opcional sobre o fluxo de mensagens de sequência.

O controle de fluxo é habilitado definindo a <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled?displayProperty=nameWithType> propriedade como `true` . Veja a seguir uma lista de restrições que se aplicam ao WCF:

- B4001: quando o controle de fluxo de mensagens confiável está habilitado, o WCF gera um `netrm:BufferRemaining` elemento na extensibilidade do elemento do `SequenceAcknowledgement` cabeçalho.

- B4002: quando o controle de fluxo de mensagens confiável está habilitado, o WCF não exige `netrm:BufferRemaining` que um elemento esteja presente no `SequenceAcknowledgement` cabeçalho, conforme mostrado no exemplo a seguir.

  ```xml
  <wsrm:SequenceAcknowledgement>
    <wsrm:Identifier>
      http://fabrikam123.com/abc
    </wsrm:Identifier>
    <wsrm:AcknowledgementRange Upper="1" Lower="1"/>
    <netrm:BufferRemaining>
      8
    </netrm:BufferRemaining>
  </wsrm:SequenceAcknowledgement>
  ```

- B4003: o WCF usa `netrm:BufferRemaining` para indicar quantas novas mensagens o destino do sistema de mensagens confiável pode armazenar em buffer.

- B4004: o serviço de mensagens confiáveis do WCF limita o número de mensagens transmitidas quando o aplicativo de destino do sistema de mensagens confiável não pode receber mensagens rapidamente. O destino de mensagens confiáveis armazena em buffer mensagens e o valor do elemento cai para 0.

- B4005: o WCF gera `netrm:BufferRemaining` valores inteiros entre 0 e 4096, inclusive, e lê os valores inteiros entre 0 e o `xs:int` `maxInclusive` valor 214748364, inclusive.

## <a name="message-exchange-patterns"></a>Padrões de troca de mensagens

Esta seção descreve o comportamento do WCF quando WS-Reliable mensagens é usada para diferentes padrões de troca de mensagens. Para cada padrão de troca de mensagens, os seguintes dois cenários de implantações são considerados:

- Iniciador não endereçável: iniciador está protegido por firewall; O respondente pode entregar mensagens ao iniciador somente em respostas HTTP.

- Iniciador endereçável: o iniciador e o respondente podem ser enviados solicitações HTTP; em outras palavras, duas conexões HTTP de converso podem ser estabelecidas.

### <a name="one-way-non-addressable-initiator"></a>Iniciador unidirecional e não endereçável

#### <a name="binding"></a>Associação

O WCF fornece um padrão de troca de mensagens unidirecional usando uma sequência em um canal HTTP. O WCF usa as solicitações HTTP para transmitir todas as mensagens do RMS para o RMD e a resposta HTTP para transmitir todas as mensagens do RMD para o RMS.

#### <a name="createsequence-exchange"></a>Exchange CreateSequence

O iniciador do WCF gera uma `CreateSequence` mensagem sem oferta. O respondente do WCF garante que o `CreateSequence` não tem nenhuma oferta antes de criar uma sequência. O respondente do WCF responde à `CreateSequence` solicitação com uma `CreateSequenceResponse` mensagem.

#### <a name="sequenceacknowledgement"></a>SequenceAcknowledgement

O iniciador do WCF processa confirmações na resposta de todas as mensagens, exceto nas `CreateSequence` mensagens de mensagem e de falha. O respondente do WCF sempre gera uma confirmação autônoma na resposta para sequência e `AckRequested` mensagens.

#### <a name="terminatesequence-message"></a>Mensagem TerminateSequence

O WCF trata `TerminateSequence` como uma operação unidirecional, ou seja, a resposta http tem um corpo vazio e um código de status HTTP 202.

### <a name="one-way-addressable-initiator"></a>Iniciador endereçável unidirecional

#### <a name="binding"></a>Associação

O WCF fornece um padrão de troca de mensagens unidirecional usando uma sequência em um canal http de entrada e de saída. O WCF usa as solicitações HTTP para transmitir todas as mensagens. Todas as respostas HTTP têm um corpo vazio e um código de status HTTP 202.

#### <a name="createsequence-exchange"></a>Exchange CreateSequence

O iniciador do WCF gera uma `CreateSequence` mensagem sem oferta. O respondente do WCF garante que o `CreateSequence` não tem nenhuma oferta antes de criar uma sequência. O respondente do WCF transmite a `CreateSequenceResponse` mensagem em uma solicitação HTTP endereçada com a `ReplyTo` referência do ponto de extremidade.

### <a name="duplex-addressable-initiator"></a>Iniciador duplex, endereçável

#### <a name="binding"></a>Associação

O WCF fornece um padrão de troca de mensagens bidirecional totalmente assíncrona usando duas sequências em um canal HTTP de entrada e de saída. O WCF usa as solicitações HTTP para transmitir todas as mensagens. Todas as respostas HTTP têm um corpo vazio e um código de status HTTP 202.

#### <a name="createsequence-exchange"></a>Exchange CreateSequence

O iniciador do WCF gera uma `CreateSequence` mensagem com uma oferta. O respondente do WCF garante que o `CreateSequence` tem uma oferta antes de criar uma sequência. O WCF envia o `CreateSequenceResponse` na solicitação HTTP endereçada à `CreateSequence` `ReplyTo` referência do ponto de extremidade da.

#### <a name="sequence-lifetime"></a>Tempo de vida da sequência

O WCF trata as duas sequências como uma sessão totalmente duplex.

Ao gerar uma falha que apresenta uma sequência, o WCF espera que o ponto de extremidade remoto tenha uma falha nas duas sequências. Após a leitura de uma falha que falha em uma sequência, o WCF falha em ambas as sequências.

O WCF pode fechar sua sequência de saída e continuar a processar mensagens em sua sequência de entrada. Por outro lado, o WCF pode processar o fechamento da sequência de entrada e continuar a enviar mensagens em sua sequência de saída.

### <a name="request-reply-non-addressable-initiator"></a>Iniciador de solicitação-resposta, não endereçável

#### <a name="binding"></a>Associação

O WCF fornece um padrão de troca de mensagens unidirecional e de solicitação-resposta usando duas sequências em um canal HTTP. O WCF usa as solicitações HTTP para transmitir as mensagens da sequência de solicitação e usa as respostas HTTP para transmitir as mensagens da sequência de resposta.

#### <a name="createsequence-exchange"></a>Exchange CreateSequence

O iniciador do WCF gera uma `CreateSequence` mensagem com uma oferta. O respondente do WCF garante que o `CreateSequence` tem uma oferta antes de criar uma sequência. O respondente do WCF responde à `CreateSequence` solicitação com uma `CreateSequenceResponse` mensagem.

#### <a name="one-way-message"></a>Mensagem unidirecional

Para concluir com êxito um protocolo de troca de mensagens unidirecional, o iniciador do WCF transmite uma mensagem de sequência de solicitação na solicitação HTTP e recebe uma `SequenceAcknowledgement` mensagem autônoma na resposta http. O `SequenceAcknowledgement` deve reconhecer a mensagem transmitida.

O respondente do WCF pode responder à solicitação com uma confirmação, uma falha ou uma resposta com um corpo vazio e um código de status HTTP 202.

#### <a name="two-way-messages"></a>Mensagens de duas vias

Para concluir com êxito um protocolo de troca de mensagens de duas vias, o iniciador do WCF transmite uma mensagem de sequência de solicitação na solicitação HTTP e recebe uma mensagem de sequência de resposta na resposta HTTP. A resposta deve receber uma `SequenceAcknowledgement` confirmação da mensagem de sequência de solicitação transmitida.

O respondente do WCF pode responder à solicitação com uma resposta do aplicativo, uma falha ou uma resposta com um corpo vazio e um código de status HTTP 202.

Devido à presença de mensagens unidirecionais e do tempo das respostas do aplicativo, o número de sequência da mensagem da sequência de solicitação e o número de sequência da mensagem de resposta não têm nenhuma correlação.

#### <a name="retrying-replies"></a>Repetindo respostas

O WCF conta com correlação de solicitação-resposta HTTP para correlação de protocolo de troca de mensagens bidirecional. Por isso, o iniciador do WCF não interrompe a repetição de uma mensagem de sequência de solicitação quando a mensagem da sequência de solicitação é confirmada, mas sim quando a resposta HTTP recebe uma confirmação, mensagem do usuário ou falha. O respondente do WCF tenta respostas novamente no segmento de solicitação HTTP da solicitação à qual a resposta está correlacionada.

#### <a name="lastmessage-exchange"></a>LastMessage Exchange

O iniciador do WCF gera e transmite uma última mensagem apto para vazia no segmento de solicitação HTTP. O WCF requer uma resposta, mas ignora a mensagem de resposta real. O respondente do WCF responde à última mensagem Empty-apto para da sequência de solicitação com a última mensagem Empty-apto para da sequência de resposta.

Se o respondente do WCF receber uma última mensagem na qual o URI de ação não é `http://schemas.xmlsoap.org/ws/2005/02/rm/LastMessage` , o WCF responderá com uma última mensagem. No caso de um protocolo de troca de mensagens bidirecional, a última mensagem carrega a mensagem do aplicativo; no caso de um protocolo de troca de mensagens unidirecional, a última mensagem está vazia.

O respondente do WCF não exige uma confirmação para a última mensagem Empty-apto para da sequência de resposta.

#### <a name="terminatesequence-exchange"></a>Troca de TerminateSequence

Quando todas as solicitações receberam uma resposta válida, o iniciador do WCF gera e transmite a mensagem da sequência de solicitação `TerminateSequence` no segmento de solicitação HTTP. O WCF requer uma resposta, mas ignora a mensagem de resposta real. O respondente do WCF responde à mensagem da sequência de solicitação `TerminateSequence` com a mensagem da sequência de resposta `TerminateSequence` .

Em uma sequência de desligamento normal, ambas `TerminateSequence` as mensagens carregam um intervalo completo `SequenceAcknowledgement` .

### <a name="requestreply-addressable-initiator"></a>Solicitação/resposta, iniciador endereçável

#### <a name="binding"></a>Associação

O WCF fornece um padrão de troca de mensagens de solicitação-resposta usando duas sequências em um canal HTTP de entrada e de saída. O WCF usa as solicitações HTTP para transmitir todas as mensagens. Todas as respostas HTTP têm um corpo vazio e um código de status HTTP 202.

#### <a name="createsequence-exchange"></a>Exchange CreateSequence

O iniciador do WCF gera uma `CreateSequence` mensagem com uma oferta. O respondente do WCF garante que o `CreateSequence` tem uma oferta antes de criar uma sequência. O WCF envia o `CreateSequenceResponse` na solicitação HTTP endereçada à `CreateSequence` `ReplyTo` referência do ponto de extremidade da.

#### <a name="requestreply-correlation"></a>Correlação de solicitação/resposta

O iniciador do WCF garante que todas as mensagens de solicitação de aplicativo tenham um `MessageId` e uma `ReplyTo` referência de ponto de extremidade. O iniciador do WCF aplica a `CreateSequence` referência de ponto de extremidade da mensagem `ReplyTo` em cada mensagem de solicitação de aplicativo. O respondente do WCF requer que as mensagens de solicitação de entrada tenham um `MessageId` e um `ReplyTo` . O respondente do WCF garante que o URI da referência do ponto de extremidade do `CreateSequence` e de todas as mensagens de solicitação do aplicativo sejam idênticos.
