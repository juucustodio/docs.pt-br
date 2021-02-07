---
description: 'Saiba mais sobre: protocolos de mensagens'
title: Protocolos de mensagens
ms.date: 03/30/2017
ms.assetid: 5b20bca7-87b3-4c8f-811b-f215b5987104
ms.openlocfilehash: f4dd15d41266d3e5492b584f9f8e31f456a70ef7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99733964"
---
# <a name="messaging-protocols"></a>Protocolos de mensagens

A pilha de canais do Windows Communication Foundation (WCF) emprega canais de codificação e transporte para transformar a representação de mensagem interna em seu formato de conexão e enviá-la usando um transporte específico. O transporte mais comum usado para a interoperabilidade de serviços Web é HTTP, e as codificações mais comuns usadas pelos serviços Web são SOAP 1,1 baseado em XML, SOAP 1,2 e MTOM (mecanismo de otimização de transmissão de mensagens).

Este tópico aborda os detalhes de implementação do WCF para os seguintes protocolos empregados pelo <xref:System.ServiceModel.Channels.HttpTransportBindingElement> .

Especificação/documento:

- [HTTP 1.1](https://www.ietf.org/rfc/rfc2616.txt)
- [Associação HTTP SOAP 1,1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508), seção 7
- [Associação HTTP SOAP 1,2](https://www.w3.org/TR/soap12-part2) Seção 7

Este tópico aborda os detalhes de implementação do WCF para os seguintes protocolos que <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> e <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> empregam.

Especificação/documento:

- [XML](https://www.w3.org/TR/REC-xml)
- [SOAP 1,1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/)
- [Núcleo SOAP 1,2](https://www.w3.org/TR/soap12-part1/)
- [WS-Addressing 2004/08](https://www.w3.org/Submission/2004/SUBM-ws-addressing-20040810/)
- [Endereçamento de serviços da Web do W3C 1,0-Core](https://www.w3.org/TR/2006/REC-ws-addr-core-20060509)
- [Endereçamento de serviços Web W3C 1,0-Associação SOAP](https://www.w3.org/TR/2006/REC-ws-addr-soap-20060509)
- [Endereçamento de serviços Web W3C 1,0-Associação de WSDL](https://www.w3.org/TR/2006/CR-ws-addr-wsdl-20060529/)
- [Endereçamento de serviços Web W3C 1,0-metadados](https://www.w3.org/TR/ws-addr-metadata/)
- [Associação WSDL SOAP 1.1](https://www.w3.org/TR/wsdl/)
- [Associação WSDL de SOAP 1.2](https://www.w3.org/Submission/wsdl11soap12/)

Este tópico aborda os detalhes de implementação do WCF para os seguintes protocolos que o <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> emprega.

Especificação/documento:

- [XOP](https://www.w3.org/TR/xop10/)
- [Associação de MTOM + SOAP 1,2](https://www.w3.org/TR/soap12-mtom/)
- [Associação de SOAP 1,1 de MTOM](https://www.w3.org/Submission/soap11mtom10/)
- [Asserção de WS-Policy de MTOM](https://www.w3.org/Submission/2006/SUBM-WS-MTOMPolicy-20061101/)

Os namespaces XML e os prefixos associados a seguir são usados em todo este tópico:

| Prefixo | Uniform Resource Identifier de namespace (URI) |
|------------|---------------------------------------------------|
| S11 | `http://schemas.xmlsoap.org/soap/envelope` |
| S12 |`http://www.w3.org/2003/05/soap-envelope` |
| WSA |`http://www.w3.org/2004/08/addressing` |
| wsam |`http://www.w3.org/2007/05/addressing/metadata` |
| wsap |`http://schemas.xmlsoap.org/ws/2004/09/policy/addressing` |
| wsa10 |`http://www.w3.org/2005/08/addressing` |
| wsaw10 |`http://www.w3.org/2006/05/addressing/wsdl` |
| XOP |`http://www.w3.org/2004/08/xop/include` |
| xmime |`http://www.w3.org/2004/06/xmlmime`<br /><br /> `http://www.w3.org/2005/05/xmlmime` |
| DP |`http://schemas.microsoft.com/net/2006/06/duplex` |

## <a name="soap-11-and-soap-12"></a>SOAP 1,1 e SOAP 1,2

### <a name="envelope-and-processing-model"></a>Modelo de envelope e processamento

O WCF implementa o processamento de envelope SOAP 1,1 seguindo o perfil básico 1,1 (BP11) e o perfil básico 1,0 (SSBP10). O processamento de envelope SOAP 1,2 é implementado após SOAP12-part1.

Esta seção explica algumas opções de implementação feitas pelo WCF em relação a BP11 e SOAP12-part1.

#### <a name="mandatory-header-processing"></a>Processamento de cabeçalho obrigatório

O WCF segue as regras para o processamento de cabeçalhos marcados como `mustUnderstand` descrito nas especificações soap 1,1 e soap 1,2, com as seguintes variações.

Uma mensagem que entra na pilha de canais do WCF é processada por canais individuais configurados por elementos de associação associados, por exemplo, codificação de mensagem de texto, segurança, mensagens confiáveis e transações. Cada canal reconhece cabeçalhos do namespace associado e os marca como entendi. Quando uma mensagem entra no Dispatcher, o formatador de operação lê os cabeçalhos esperados pelo contrato de mensagem/operação correspondente e os marca como entendi. Em seguida, o Dispatcher verifica se os cabeçalhos restantes não são compreendidos, mas marcados como `mustUnderstand` e gera uma exceção. As mensagens que contêm `mustUnderstand` cabeçalhos que são direcionados ao destinatário não são processadas pelo código do aplicativo de destinatário.

Esse processamento em camadas permite a separação entre camadas de infraestrutura e camadas de aplicativo do nó SOAP:

- B1111: cabeçalhos que não são compreendidos são detectados depois que a mensagem é processada pela pilha de canais da infraestrutura do WCF, mas antes de ser processada pelo aplicativo

     O `mustUnderstand` valor do cabeçalho difere entre soap 1,1 e soap 1,2. O perfil básico 1,1 requer que o `mustUnderstand` valor seja 0 ou 1 para mensagens SOAP 1,1. O SOAP 1,2 permite 0, 1, `false` e `true` como valores, mas recomenda emitir uma representação canônica de `xs:boolean` valores ( `false` , `true` ).

- B1112: o WCF emite `mustUnderstand` os valores 0 e 1 para as versões soap 1,1 e soap 1,2 do envelope SOAP. O WCF aceita todo o espaço de valor de `xs:boolean` para o `mustUnderstand` cabeçalho (0, 1, `false` , `true` )

#### <a name="soap-faults"></a>Falhas de SOAP

Veja a seguir uma lista de implementações de falhas SOAP específicas do WCF.

- B2121: o WCF retorna os seguintes códigos de falha SOAP 1,1: `s11:mustUnderstand` , `s11:Client` e `s11:Server` .

- B2122: o WCF retorna os seguintes códigos de falha SOAP 1,2: `s12:MustUnderstand` , `s12:Sender` e `s12:Receiver` .

### <a name="http-binding"></a>Associação HTTP

#### <a name="soap-11-http-binding"></a>Associação HTTP SOAP 1,1

O WCF implementa a associação HTTP SOAP 1.1 seguindo a seção de especificação Basic Profile 1,1 3,4 com os seguintes esclarecimentos:

- B2211: o serviço WCF não implementa o redirecionamento de solicitações HTTP POST.

- B2212: os clientes WCF dão suporte a cookies HTTP de acordo com o 3.4.8.

#### <a name="soap-12-http-binding"></a>Associação HTTP SOAP 1,2

O WCF implementa a associação HTTP SOAP 1,2, conforme descrito na especificação SOAP 1,2-parte 2 (SOAP12Part2) com os seguintes esclarecimentos.

O SOAP 1,2 introduziu um parâmetro de ação opcional para o `application/soap+xml` tipo de mídia. Esse parâmetro é útil para otimizar a expedição de mensagens sem a necessidade de que o corpo da mensagem SOAP seja analisado quando WS-Addressing não é usado.

- R2221: o `application/soap+xml` parâmetro Action, quando presente em uma solicitação SOAP 1,2, deve corresponder ao `soapAction` atributo no `wsoap12:operation` elemento dentro da Associação WSDL correspondente.

- R2222: o `application/soap+xml` parâmetro Action, quando presente em uma mensagem SOAP 1,2, deve corresponder `wsa:Action` quando WS-Addressing 2004/08 ou WS-Addressing 1,0 forem usados.

Quando WS-Addressing está desabilitado e uma solicitação de entrada não contém um parâmetro de ação, a mensagem `Action` é considerada não especificada.

## <a name="ws-addressing"></a>WS-Addressing

O WCF implementa 3 versões do WS-Addressing:

- WS-Addressing 2004/08

- W3C Web Services Addressing 1,0 Core (ADDR10-CORE) e ligação SOAP (ADDR10-SOAP)

- WS-Addressing 1,0-metadados

### <a name="endpoint-references"></a>Referências de ponto de extremidade

Todas as versões do WS-Addressing que o WCF implementa usam referências de ponto de extremidade para descrever pontos de extremidades.

#### <a name="endpoint-references-and-ws-addressing-versions"></a>Referências de ponto de extremidade e versões de WS-Addressing

O WCF implementa vários protocolos de infraestrutura que usam WS-Addressing e, em particular `EndpointReference` , o elemento e a `W3C.WsAddressing.EndpointReferenceType` classe (por exemplo, WS-RELIABLEMESSAGING, WS-SECURECONVERSATION e WS-Trust). O WCF dá suporte ao uso de qualquer uma das versões do WS-Addressing com outros protocolos de infraestrutura. Os pontos de extremidade do WCF dão suporte a uma versão do WS-Addressing por ponto final.

Para R3111, o namespace para o `EndpointReference` elemento ou tipo usado em mensagens trocadas com um ponto de extremidade WCF deve corresponder à versão do WS-Addressing implementada por esse ponto de extremidade.

Por exemplo, se um ponto de extremidade WCF implementa WS-ReliableMessaging, o `AcksTo` cabeçalho retornado por tal ponto de extremidade dentro `CreateSequenceResponse` usa a versão de WS-Addressing que o `EncodingBinding` elemento especifica para esse ponto de extremidade.

#### <a name="endpoint-references-and-metadata"></a>Referências de ponto de extremidade e metadados

Vários cenários exigem a comunicação de metadados ou uma referência a metadados para um determinado ponto de extremidade.

B3121: o WCF emprega mecanismos descritos na especificação de WS-MetadataExchange (MEX) 6 para incluir metadados para referências de ponto de extremidade por valor ou por referência.

Considere um cenário em que um serviço WCF requer autenticação usando um token SAML (Security Asserts Markup Language) emitido pelo emissor do token em `http://sts.fabrikam123.com` . O ponto de extremidade do WCF descreve esse requisito de autenticação usando `sp:IssuedToken` a asserção com uma asserção aninhada `sp:Issuer` apontando para o emissor do token. Os aplicativos cliente que acessam a `sp:Issuer` declaração precisam saber como se comunicar com o ponto de extremidade do emissor do token. O cliente precisa saber os metadados sobre o emissor do token. Usando as extensões de metadados de referência do ponto de extremidade definidas em MEX, o WCF fornece uma referência aos metadados do emissor do token.

```xml
<sp:IssuedToken>
  <sp:Issuer>
    <wsa10:Address>
      http://sts.fabrikam123.com
    </wsa10:Address>
    <wsa10:Metadata>
      <mex:Metadata>
        <mex:MetadataSection>
          <mex:MetadataReference>
            <wsa10:Address>
              http://sts.fabrikam123.com/mex
            </wsa10:Address>
          </mex:MetadataReference>
        </mex:MetadataSection>
      </mex:Metadata>
    </wsa10:Metadata>
  </sp:Issuer>
</sp:IssuedToken>
```

### <a name="message-addressing-headers"></a>Cabeçalhos de endereçamento de mensagens

#### <a name="message-headers"></a>Cabeçalhos da mensagem

Para as versões WS-Addressing, o WCF usa os seguintes cabeçalhos de mensagem, conforme prescrito pelas especificações `wsa:To` , `wsa:ReplyTo` ,, `wsa:Action` `wsa:MessageID` e `wsa:RelatesTo` .

B3211: para todas as versões de WS-Addressing, o WCF honra, mas não é produzido prontamente, WS-Addressing cabeçalhos de mensagens `wsa:FaultTo` e `wsa:From` .

Os aplicativos que interagem com aplicativos WCF podem adicionar esses cabeçalhos de mensagens e o WCF os processará de forma adequada.

#### <a name="reference-parameters-and-properties"></a>Parâmetros e propriedades de referência

O WCF implementa o processamento de parâmetros de referência de ponto de extremidade e propriedades de referência de acordo com as respectivas especificações.

B3221: quando configurado para usar o WS-Addressing 2004/08, os pontos de extremidade do WCF não diferenciam as propriedades de referência de processamento e os parâmetros de referência.

### <a name="message-exchange-patterns"></a>Padrões de troca de mensagens

A sequência de mensagens envolvidas na invocação de operação do serviço Web é chamada de *padrão de troca de mensagens*. O WCF dá suporte a padrões unidirecionais, de solicitação-resposta e de troca de mensagens duplex. Esta seção esclarece WS-Addressing requisitos de processamento de mensagens dependendo do padrão de troca de mensagens que está sendo usado.

Ao longo desta seção, o solicitante envia a primeira mensagem e o respondente recebe a primeira mensagem.

#### <a name="one-way-message"></a>One-Way mensagem

Quando um ponto de extremidade WCF é configurado para dar suporte a mensagens com um determinado `Action` para seguir um padrão unidirecional, o ponto de extremidade do WCF segue os seguintes comportamentos e requisitos. A menos que especificado de outra forma, os comportamentos e as regras se aplicam a ambas as versões do WS-Addressing com suporte no WCF:

- R3311: o solicitante deve incluir `wsa:To` `wsa:Action` cabeçalhos, e para todos os parâmetros de referência especificados pela referência do ponto de extremidade. Quando WS-Addressing 2004/08 é usado e [Propriedades de referência] são especificadas pela referência do ponto de extremidade, os cabeçalhos correspondentes também devem ser adicionados à mensagem.

- B3312: o solicitante pode incluir `MessageID` `ReplyTo` cabeçalhos, e `FaultTo` . A infraestrutura do receptor irá ignorá-las e elas serão passadas para o aplicativo.

- R3313: quando HTTP é usado e nenhuma mensagem está sendo enviada no trecho de resposta HTTP, o respondente deve enviar uma resposta HTTP com um corpo vazio e um código de status HTTP 202.

     Quando o transporte HTTP está em uso e o contrato de operação declara uma mensagem unidirecional, a resposta HTTP ainda pode ser usada para enviar mensagens de infraestrutura — por exemplo, mensagens confiáveis podem enviar uma `SequenceAcknowledgement` mensagem em uma resposta http.

- B3314: o respondente do WCF não envia uma mensagem de falha em resposta a uma mensagem unidirecional.

#### <a name="request-reply"></a>Solicitação-resposta

Quando um ponto de extremidade do WCF é configurado para uma mensagem com um determinado `Action` para seguir o padrão de solicitação-resposta, o ponto de extremidade do WCF segue os comportamentos e os requisitos abaixo. A menos que especificado caso contrário, os comportamentos e as regras se aplicam a ambas as versões do WS-Addressing com suporte no WCF:

- R3321: o solicitante deve incluir nos cabeçalhos Request `wsa:To` , `wsa:Action` , `wsa:MessageID` e para todos os parâmetros de referência ou propriedades de referência (ou ambos) especificados pela referência do ponto de extremidade.

- R3322: quando WS-Addressing 2004/08 é usado, `ReplyTo` também deve ser incluído na solicitação.

- R3323: quando WS-Addressing 1,0 é usado e `ReplyTo` não está presente na solicitação, uma referência de ponto de extremidade padrão com a propriedade [address] igual a `http://www.w3.org/2005/08/addressing/anonymous` é usada.

- R3324: o solicitante deve incluir `wsa:To` `wsa:Action` cabeçalhos, e `wsa:RelatesTo` na mensagem de resposta, bem como cabeçalhos para todos os parâmetros de referência ou propriedades de referência (ou ambos) especificados pela `ReplyTo` referência do ponto de extremidade na solicitação.

### <a name="web-services-addressing-faults"></a>Falhas de endereçamento de serviços Web

R3411: o WCF produz as seguintes falhas definidas por WS-Addressing 2004/08.

| Código | Causa |
|----------|-----------|
| `wsa:DestinationUnreachable` | A mensagem recebida com um `ReplyTo` que é diferente do endereço de resposta estabelecido para este canal; não há nenhum ponto de extremidade ouvindo no endereço especificado no cabeçalho to. |
| `wsa:ActionNotSupported` | os canais de infraestrutura ou o Dispatcher associado ao ponto de extremidade não reconhece a ação especificada no `Action` cabeçalho. |

R3412: o WCF produz as seguintes falhas definidas por WS-Addressing 1,0.

| Código | Causa |
|----------|-----------|
| `wsa10:InvalidAddressingHeader` | Duplicar `wsa:To` , `wsa:ReplyTo` , `wsa:From` ou `wsa:MessageID` . Duplicar `wsa:RelatesTo` com o mesmo `RelationshipType` . |
| `wsa10:MessageAddressingHeaderRequired` | O cabeçalho de endereçamento necessário está ausente. |
| `wsa10:DestinationUnreachable` | A mensagem recebida com um `ReplyTo` que é diferente do endereço de resposta estabelecido para esse canal. Não há nenhum ponto de extremidade ouvindo no endereço especificado no cabeçalho to. |
| `wsa10:ActionNotSupported` | Uma ação especificada no `Action` cabeçalho não é reconhecida pelos canais de infraestrutura ou pelo Dispatcher associado ao ponto de extremidade. |
| `wsa10:EndpointUnavailable` | O canal do RM envia essa falha de volta, indicando que o ponto de extremidade não processará a sequência com base no exame dos `CreateSequence` cabeçalhos de endereçamento da mensagem. |

O código nas tabelas anteriores é mapeado para `FaultCode` em soap 1,1 e `SubCode` (com código = remetente) em SOAP 1,2.

### <a name="wsdl-11-binding-and-ws-policy-assertions"></a>Associação de WSDL 1,1 e declarações de WS-Policy

#### <a name="indicating-use-of-ws-addressing"></a>Indicando o uso de WS-Addressing

O WCF usa declarações de política para indicar o suporte de ponto de extremidade para uma versão de WS-Addressing específica.

A declaração de política a seguir tem o assunto da política de ponto de extremidade [WS-PA] e indica que as mensagens enviadas e recebidas do ponto de extremidade devem usar WS-Addressing 2004/08.

```xml
<wsap:UsingAddressing />
```

Esta declaração de política aumenta a especificação WS-Addressing 2004/08.

A declaração de política a seguir indica que as mensagens enviadas/recebidas devem usar WS-Addressing 1,0.

```xml
<wsam:Addressing/>
```

A declaração de política a seguir tem um assunto de política de ponto de extremidade [WS-PA] e indica que as mensagens enviadas e recebidas do ponto de extremidade devem usar WS-Addressing 2004/08.

```xml
<wsaw10:UsingAddressing />
```

O `wsaw10:UsingAddressing` elemento é emprestado de [WS-Addressing-WSDL] e é usado no contexto de WS-Policy em conformidade com essa especificação, seção 3.1.2.

O uso de endereçamento não altera a semântica de associações HTTP de WSDL 1,1, SOAP 1,1 e SOAP 1,2. Por exemplo, se uma resposta for esperada para uma solicitação que é enviada para um ponto de extremidade que usa o endereçamento e a associação HTTP SOAP 1. x WSDL, a resposta deve ser enviada usando a resposta HTTP.

Para respostas enviadas pela resposta http, a declaração WS-AM é:

```xml
<wsam:AnonymousResponses/>
```

A declaração de política completa pode ser parecida com esta:

```xml
<wsam:Addressing>
    <wsp:Policy>
        <wsam:AnonymousResponses />
    </wsp:Policy>
</wsam:Addressing>
```

No entanto, há padrões de troca de mensagens que se beneficiam da existência de duas conexões HTTP de converso independentes estabelecidas entre o solicitante e o respondente, por exemplo, mensagens unidirecionais não solicitadas enviadas pelo respondente.

O WCF oferece um recurso pelo qual dois canais de transporte subjacentes podem formar um canal duplex composto, em que um canal é usado para mensagens de entrada e o outro é usado para mensagens de saída. No caso do transporte HTTP, o Composite duplex fornece duas conexões HTTP de contrapartida. O solicitante usa uma conexão para enviar mensagens ao Respondente e o respondente usa o outro para enviar mensagens de volta para o solicitante.

Para respostas enviadas por solicitações HTTP separadas, a declaração WS-am é

```xml
<wsam:NonAnonymousResponses/>
```

A declaração de política completa pode ser parecida com esta:

```xml
<wsam:Addressing>
    <wsp:Policy>
        <wsam:NonAnonymousResponses />
    </wsp:Policy>
</wsam:Addressing>
```

O uso da declaração a seguir que tem o assunto da política de ponto de extremidade [WS-PA] em pontos de extremidades que usam associações HTTP SOAP 1. x de WSDL 1,1 requer duas conexões HTTP de discagem separadas a serem usadas para mensagens que fluem do solicitante para Respondente e Respondente ao solicitante, respectivamente.

```xml
<cdp:CompositeDuplex/>
```

A instrução anterior leva aos seguintes requisitos no `wsa:ReplyTo` cabeçalho para mensagens de solicitação:

- R3514: as mensagens de solicitação enviadas a um ponto de extremidade devem ter um `ReplyTo` cabeçalho com a propriedade diferente de `[address]` `http://www.w3.org/2005/08/addressing/anonymous` se o ponto de extremidade usa uma associação HTTP SOAP 1. x WSDL 1,1 e tem uma alternativa de política com uma `wsap10:UsingAddressing` asserção ou associada `wsap:UsingAddressing` com `cdp:CompositeDuplex` anexada.

- R3515: as mensagens de solicitação enviadas a um ponto de extremidade devem ter um `ReplyTo` cabeçalho com a `[address]` propriedade igual a `http://www.w3.org/2005/08/addressing/anonymous` , ou não ter um `ReplyTo` cabeçalho, se o ponto de extremidade usar uma associação HTTP SOAP 1. x WSDL 1,1 e tiver uma alternativa de política com `wsap10:UsingAddressing` asserção e nenhuma `cdp:CompositeDuplex` declaração anexada.

- R3516: as mensagens de solicitação enviadas a um ponto de extremidade devem ter um `ReplyTo` cabeçalho com uma `[address]` propriedade igual a `http://www.w3.org/2005/08/addressing/anonymous` se o ponto de extremidade usa uma associação HTTP SOAP 1. x WSDL 1,1 e tem uma alternativa de política com `wsap:UsingAddressing` asserção e nenhuma `cdp:CompositeDuplex` declaração anexada.

A especificação WSDL do WS-Addressing tenta descrever associações de protocolo semelhantes introduzindo um elemento `<wsaw:Anonymous/>` com três valores textuais (obrigatório, opcional e proibido) para indicar os requisitos no `wsa:ReplyTo` cabeçalho (seção 3,2). Infelizmente, essa definição de elemento não é particularmente utilizável como uma declaração no contexto de WS-Policy, pois requer extensões específicas de domínio para dar suporte à interseção de alternativas usando um elemento como uma asserção. Essa definição de elemento também indica o valor do `ReplyTo` cabeçalho em oposição ao comportamento do ponto de extremidade na conexão, o que o torna específico ao transporte http.

#### <a name="action-definition"></a>Definição de ação

WS-Addressing 2004/08 define um `wsa:Action` atributo para os `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` elementos. WS-Addressing Associação de WSDL 1,0 (WS-ADDR10-WSDL) define um atributo semelhante, `wsaw10:Action` .

A única diferença entre os dois é a semântica padrão de padrão de ação descrita na seção 3.3.2 do WS-ADDR e da seção 4.4.4 de WS-ADDR10-WSDL, respectivamente.

É razoável ter dois pontos de extremidade que compartilham o mesmo `portType` (ou contrato, na terminologia do WCF), mas usando versões diferentes do WS-Addressing. Mas, Considerando que a ação é definida pelo `portType` e não deve ser alterada nos pontos de extremidade que implementam o `portType` , torna-se impossível dar suporte a ambos os padrões de ação padrão.

Para resolver esse secou, o WCF dá suporte a uma única versão do `Action` atributo.

B3521: o WCF usa o `wsaw10:Action` atributo em `wsdl:portType/wsdl:operation/[wsdl:input | wsdl:output | wsdl:fault]` elementos, conforme definido em WS-ADDR10-WSDL para determinar o `Action` URI das mensagens correspondentes, independentemente da versão de WS-Addressing usada pelo ponto de extremidade.

#### <a name="use-endpoint-reference-inside-wsdl-port"></a>Usar referência de ponto de extremidade dentro da porta WSDL

A seção 4,1 do WS-ADDR10-WSDL estende o `wsdl:port` elemento para incluir o `<wsa10:EndpointReference…/>` elemento filho para descrever o ponto de extremidade em WS-Addressing termos. O WCF expande esse utilitário no WS-Addressing 2004/08, permitindo que ele `<wsa:EndpointReference…/>` apareça como um elemento filho de `wsdl:port` .

- R3531: se um ponto de extremidade tiver uma alternativa de política anexada com uma `<wsaw10:UsingAddressing/>` declaração de política, o `wsdl:port` elemento correspondente poderá conter um elemento filho `<wsa10:EndpointReference …/>` .

- R3532: se um `wsdl:port` contiver um elemento filho `<wsa10:EndpointReference …/>` , o `wsa10:EndpointReference/wsa10:Address` valor do elemento filho deverá corresponder ao valor do `@address` atributo do `wsdl:port` / `wsdl:location` elemento irmão.

- R3533: se um ponto de extremidade tiver uma alternativa de política anexada com `<wsap:UsingAddressing/>` a declaração de política, o `wsdl:port` elemento correspondente poderá conter um elemento filho `<wsa:EndpointReference …/>` .

- R3534: se um `wsdl:port` contiver um elemento filho `<wsa:EndpointReference …/>` , o `wsa:EndpointReference/wsa:Address` valor do elemento filho deverá corresponder ao valor do `@address` atributo do `wsdl:port` / `wsdl:location` elemento irmão.

### <a name="composition-with-ws-security"></a>Composição com WS-Security

De acordo com as seções de consideração de segurança em WS-ADDR e WS-ADDR10, é recomendável que todos os cabeçalhos de mensagens de endereçamento sejam assinados junto com o corpo da mensagem para associá-los.

Quando WS-Security é usado para proteção de integridade de mensagem, os cabeçalhos de mensagem WS-Addressing, bem como os cabeçalhos resultantes de parâmetros de referência ou Propriedades (ou ambos) devem ser assinados com o corpo da mensagem.

### <a name="examples"></a>Exemplos

#### <a name="one-way-message"></a>One-Way mensagem

Nesse cenário, o remetente envia uma mensagem unidirecional para o destinatário. SOAP 1,2, HTTP 1,1 e W3C WS-Addressing 1,0 são usados.

A estrutura da mensagem de solicitação: os cabeçalhos de mensagem incluem `wsa10:To` `wsa10:Action` elementos e. O corpo da mensagem inclui um `<app:Ping>` elemento específico do namespace do aplicativo.

Cabeçalhos HTTP: o destino em POST corresponde ao URI no `wsa10:To` elemento.

O cabeçalho Content-Type tem o valor de `application/soap+xml` conforme exigido pelo SOAP 1,2. Parâmetros `charset` e `action` são incluídos. O `action` parâmetro do cabeçalho Content-Type corresponde ao valor do cabeçalho da `wsa10:Action` mensagem.

```http
POST http://fabrikam123.com/Service HTTP/1.1
Content-Type: application/soap+xml; charset=utf-8;  
              action="http://fabrikam123.com/Service/OneWay"
Host: 131.107.72.15
Content-Length: 1501
Expect: 100-continue
Proxy-Connection: Keep-Alive
<s12:Envelope>
  <s12:Header>
    <wsa10:To s12:mustUnderstand="1">
        http://fabrikam123.com/Service
    </wsa10:To>
    <wsa10:Action s12:mustUnderstand="1">
        http://fabrikam123.com/Service/OneWay
    </wsa10:Action>
  </s12:Header>
  <s12:Body>
    <Ping xmlns="http://fabrikam123.com/Service/">
      <Text>Hello World</Text>
    </Ping>
  </s12:Body>
</s12:Envelope>
```

O receptor responde com uma resposta HTTP vazia e o status 202. Um exemplo da resposta HTTP:

```http
HTTP/1.1 202 Accepted
Date: Fri, 15 Jul 2005 08:56:07 GMT
Server: Microsoft-IIS/6.0
MicrosoftOfficeWebServer: 5.0_Pub
X-Powered-By: ASP.NET
X-AspNet-Version: 2.0.50215
Cache-Control: private
Content-Length: 0
```

## <a name="soap-message-transmission-optimization-mechanism"></a>Mecanismo de otimização de transmissão de mensagens SOAP

Esta seção descreve os detalhes de implementação do WCF para HTTP SOAP MTOM. A tecnologia MTOM é um mecanismo de codificação de mensagens SOAP da mesma classe que a codificação de texto/XML tradicional ou a codificação binária do WCF. O MTOM inclui o seguinte:

- Um mecanismo de codificação e empacotamento XML descrito por [XOP] que otimiza itens de informações XML contendo dados binários codificados na base64 em partes binárias separadas.

- Um encapsulamento MIME do pacote XOP que serializa o XML infoset e cada parte binária do pacote XOP em uma parte MIME separada.

- Uma codificação de XOP MIME aplicada ao envelope SOAP 1. x.

- Uma associação de transporte HTTP.

É possível usar o MTOM com transportes não HTTP com o WCF. No entanto, neste tópico, vamos nos concentrar no HTTP.

O formato MTOM aproveita um grande conjunto de especificações que abrangem o próprio MTOM, XOP e MIME. A modularidade desse conjunto de especificação torna um pouco difícil reconstruir os requisitos exatos no formato e na semântica de processamento. Esta seção descreve os requisitos de formato e processamento para a associação HTTP MTOM.

### <a name="mtom-message-encoding"></a>Codificação de mensagem MTOM

#### <a name="generating-mtom-messages"></a>Gerando mensagens MTOM

A seção [XOP] 3,1 descreve o processo de codificação de XML com itens de informações de elemento que contêm valores de Base64 em um pacote XOP definido de forma abstrata.

A seguinte sequência de etapas descreve o processo de codificação específico de MTOM:

1. Verifique se o envelope SOAP a ser codificado não contém nenhum item de informações de elemento com um `[namespace name]` de `http://www.w3.org/2004/08/xop/include` e um `[local name]` de `Include` .

2. Crie um pacote MIME vazio.

3. Identifique dentro do XML infoset original os itens de informações de elemento a serem otimizados. Para os itens a serem otimizados, os caracteres que compõem o `[children]` do item de informações do elemento devem estar na forma canônica de `xs:base64Binary` (consulte XSD-2, 3.2.16 base64Binary) e não devem conter nenhum caractere de espaço em branco anterior, embutido ou seguir o conteúdo que não seja de espaço em branco.

4. Crie um envelope de XOP SOAP que seja uma cópia do envelope SOAP original, mas com os filhos de cada item de informações de elemento identificado na etapa anterior substituída por um `xop:Include` item de informações de elemento construído da seguinte maneira:

    1. Transforme os caracteres substituídos em dados binários processando-os como dados codificados em base64.

    2. Gere um valor de cabeçalho Content-ID exclusivo que atenda aos requisitos R3133 e R3134.

    3. Gere um cabeçalho MIME de codificação de transferência de conteúdo com o valor binário.

    4. Se o item de informações do elemento que está sendo otimizado (o [pai] do item de informações do elemento recentemente inserido `xop:Include` ) tiver um `xmime:contentType` item de informações de atributo, gere um cabeçalho MIME de tipo de conteúdo com o valor do `xmime:contentType` atributo.

    5. Gere uma nova parte Binary binária com conteúdo formado por dados binários decodificados a partir dos caracteres substituídos processados como Base64, cabeçalho Content-ID de 4B, Content-Transfer-Encoding Header de 4C, cabeçalho Content-Type, se gerado na etapa 4D.

    6. Adicione um `href` atributo ao `xop:Include` elemento com o valor CID: URI derivado do valor de cabeçalho Content-ID gerado na etapa 4B. Remova o "" caracteres de circunscrição \<" and "> , a URL-escape a cadeia de caracteres restante e adicione o prefixo `cid:` . O seguinte conjunto mínimo de caracteres deve ser ignorado por RFC1738 e RFC2396. Outros caracteres podem ter escape.

        ```
        Hexadecimal 00-1F , 7F, 20, "<" | ">" | "#" | "%" | <">
        "{" | "}" | "|" | "\" | "^" | "[" | "]" | "`" | "~" | "^"
        ```

5. Crie uma parte raiz MIME com o envelope XOP SOAP da etapa 4.

6. Grave os cabeçalhos HTTP, incluindo o cabeçalho Content-Type HTTP.

7. Grave o pacote MIME.

#### <a name="processing-mtom-messages"></a>Processando mensagens MTOM

O processamento de uma mensagem MTOM é o inverso exato do processo descrito na seção "gerando mensagens MTOM" anteriores:

1. Verifique se a parte MIME raiz tem o tipo de conteúdo `application/xop+xml` .

2. Construa um envelope SOAP analisando a parte MIME raiz do pacote como um documento XML. A codificação de caracteres é determinada pelo `charset` parâmetro do tipo de conteúdo da parte MIME raiz.

3. Para cada item de informações de elemento no envelope SOAP construído, que tem, como o único membro de sua propriedade [Children], um `xop:Include` item de informações do elemento:

    1. Remova o `cid:` prefixo e desescape todas as sequências de escape URI (RFC 2396) no valor do `@href` atributo do `xop:Include` elemento. Coloque a cadeia de caracteres de resultado em " \<", "> ".

    2. Localize a parte MIME com o valor de cabeçalho Content-ID que corresponde à cadeia de caracteres derivada na etapa 3a.

    3. Substitua o `xop:Include` item de informações do elemento que aparece na `children` propriedade de cada item com os itens de informações de caractere que representam a codificação canônica Base64 (consulte XSD-2, 3.2.16 base64Binary) do corpo da entidade da parte MIME identificada na etapa 3B (substitua efetivamente o `xop:Include` item de informações do elemento pelos dados reconstruídos da parte do pacote).

#### <a name="http-content-type-header"></a>Cabeçalho de tipo de conteúdo HTTP

Veja a seguir uma lista de esclarecimentos do WCF para o formato do cabeçalho de tipo de conteúdo HTTP de uma mensagem codificada por MTOM SOAP 1. x derivada dos requisitos declarados na própria especificação MTOM e são derivados de MTOM e RFC 2387.

- R4131: um cabeçalho de tipo de conteúdo HTTP deve ter o valor de várias partes/relacionadas (não diferencia maiúsculas de minúsculas) e seus parâmetros. Os nomes de parâmetro não diferenciam maiúsculas de minúsculas. A ordem dos parâmetros não é significativa.

- O formulário completo de Backus-Naur (BNF) do cabeçalho Content-Type para mensagens MIME está listado na RFC 2045, seção 5,1.

- R4132: um cabeçalho de tipo de conteúdo HTTP deve ter um parâmetro de tipo com o valor `application/xop+xml` entre aspas duplas.

Embora a necessidade de usar aspas duplas não seja explícita no RFC 2387, o texto observa que todos os parâmetros de tipo de mídia com diversas partes/relacionadas provavelmente contenham caracteres reservados como " \@ " ou "/" e, portanto, precisam de aspas duplas.

- R4133: um cabeçalho de tipo de conteúdo HTTP deve ter um parâmetro de inicialização com o valor do cabeçalho Content-ID da parte MIME que contém o envelope SOAP 1. x, entre aspas duplas. Se o parâmetro Start for omitido, a primeira parte MIME deverá conter o envelope SOAP 1. x.

- R4134: um cabeçalho de tipo de conteúdo HTTP para uma mensagem codificada de MTOM SOAP 1,1 deve incluir o parâmetro Start-info com o valor de text/xml, entre aspas duplas.

- R4135: um cabeçalho de tipo de conteúdo HTTP para uma mensagem codificada em MTOM SOAP 1,2 deve incluir o parâmetro Start-info com o valor de `application/soap+xml` , entre aspas duplas.

- R4136: cabeçalho Content-Type de HTTP para uma mensagem codificada em MTOM SOAP 1. x deve ter o parâmetro de limite com o valor (entre aspas duplas) que corresponde ao limite MIME BNF definido no RFC 2046, seção 5.1.1

    ```
    boundary := 0*69<bchars> bcharsnospace
    bchars := bcharsnospace / " "
    bcharsnospace :=    DIGIT / ALPHA / "'" / "(" / ")" / "+"
                        / "_" / "," / "-" / "." / "/" / ":" / "=" / "?"
    ```

     Exemplos:

     CORRIGI

    ```http
    Content-Type: multipart/related; type="application/xop+xml";start=" <part0@tempuri.org>";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1";start-info="text/xml"
    ```

     CORRIGI

    ```http
    Content-Type: Multipart/Related; type="application/xop+xml";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"
    ```

     INCORRETO

    ```http
    Content-Type: Multipart/Related; type=application/xop+xml;start=" <part0@tempuri.org>";start-info="text/xml";boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"
    ```

#### <a name="infoset-mime-part"></a>Parte MIME do infoset

O envelope SOAP 1. x é encapsulado como uma parte raiz do pacote de MIME XOP e geralmente é chamado de `infoset` parte.

- R4141: o envelope SOAP 1. x deve ser encapsulado como uma parte raiz do pacote do XOP MIME, chamado de `infoset` parte e referenciado do tipo de conteúdo http.

- R4142: a `Infoset` parte SOAP deve incluir os seguintes cabeçalhos MIME: `Content-ID` , `Content-Transfer-Encoding` , e `Content-Type` .

O formato do cabeçalho Content-ID é definido pela RFC 2045 como

```
"Content-ID" ":" msg-id
```

onde `msg-id` é definido no rfc 2822 (que substitui a rfc 822, referenciada na rfc 2045) como:

```
msg-id    =       [CFWS] "<" id-left "@" id-right ">" [CFWS]
```

e é efetivamente um endereço de email entre " \<" and  "> ". O `[CFWS]` prefixo e o sufixo foram adicionados ao RFC 2822 para transportar comentários e não devem ser usados para preservar a interoperabilidade.

R4143: o valor do cabeçalho Content-ID para a parte MIME infoset deve seguir a `msg-id` produção do RFC 2822 com as `[CFWS]` partes de prefixo e sufixo omitidas.

Várias implementações de MIME requisitos relaxados para o valor incluído em " \<" and "> " para serem um endereço de email e usados `absoluteURI` entre " \<" , "> ", além do endereço de email. Esta versão do WCF usa valores do cabeçalho MIME Content-ID do formulário:

```
Content-ID: <http://tempuri.org/0>
```

R4144: os processadores MTOM devem aceitar valores de cabeçalho Content-ID que correspondam aos seguintes relaxados `msg-id` .

```
msg-id-relaxed =     [CFWS] "<" (absoluteURI | mail-address) ">" [CFWS]
mail-address   =     id-left "@" id-right
```

MIME (RFC 2045) fornece o cabeçalho Content-Transfer-Encoding para comunicar a codificação do conteúdo da parte MIME. O padrão definido para a codificação de transferência de conteúdo é de 7 bits, o que não é adequado para a maioria das mensagens SOAP, portanto, o cabeçalho de codificação de transferência de conteúdo é necessário para uma interoperabilidade maior:

- R4145: a parte do infoset SOAP deve conter o cabeçalho Content-Transfer-Encoding.

- R4146: se a codificação de caracteres de envelope SOAP for UTF-8, o valor do cabeçalho Content-Transfer-Encoding deverá ser de 8 bits.

- R4147: se a codificação de caracteres de envelope SOAP for UTF-16, o valor do cabeçalho Content-Transfer-Encoding deverá ser binário.

- De acordo com [XOP] seção 5,

- R4148: a parte do infoset SOAP 1.1 deve conter o cabeçalho Content-Type com o tipo de mídia Application/XOP + XML e os parâmetros Type = "text/xml" e charset

    ```http
    Content-Type: application/xop+xml;
                  charset=utf-8;type="text/xml"
    ```

- R4149: a parte do infoset SOAP 1,2 deve conter o cabeçalho Content-Type com tipo `application/xop+xml` de mídia e parâmetros Type = " `application/soap+xml` " e `charset` .

    ```http
    Content-Type: application/xop+xml;
                  charset=utf-8;type="application/soap+xml"
    ```

     Embora XOP defina o `charset` parâmetro para `application/xop+xml` ser opcional, ele é necessário para interoperabilidade semelhante ao requisito 1,1 de BP no `charset` parâmetro para o `text/xml` tipo de mídia.

- R41410: os `type` `charset` parâmetros e devem estar presentes no cabeçalho Content-Type da parte SOAP 1. x infoset.

#### <a name="wcf-endpoint-support-for-mtom"></a>Suporte de ponto de extremidade WCF para MTOM

A finalidade do MTOM é codificar uma mensagem SOAP para otimizar os dados codificados em base64. Veja a seguir uma lista de restrições:

- R4151: qualquer item de informações de elemento que contenha dados codificados em base64 pode ser otimizado.

- B4152: o WCF otimiza itens de informações de elemento que contêm dados codificados na Base64 e excede 1024 bytes de comprimento.

Um ponto de extremidade WCF configurado para usar o MTOM sempre enviará mensagens codificadas em MTOM. Mesmo que nenhuma peça atenda aos critérios necessários, a mensagem ainda é codificada por MTOM (serializada como um pacote MIME com uma única parte MIME que contém o envelope SOAP).

### <a name="ws-policy-assertion-for-mtom"></a>Declaração de WS-Policy para MTOM

O WCF usa a seguinte declaração de política para indicar o uso de MTOM pelo ponto de extremidade:

```xml
<wsoma:OptimizedMimeSerialization />
```

- R4211: a declaração de política anterior tem um assunto de política de ponto de extremidade e especifica que todas as mensagens enviadas e recebidas do ponto de extremidade devem ser otimizadas usando MTOM.

- B4212: quando configurado para usar a otimização de MTOM, um ponto de extremidade WCF adiciona uma declaração de política de MTOM à política anexada ao correspondente `wsdl:binding` .

### <a name="composition-with-ws-security"></a>Composição com WS-Security

MTOM é um mecanismo de codificação semelhante a `text/xml` e XML binário do WCF. O MTOM oferece composição natural com WS-Security e outros protocolos WS-*: uma mensagem protegida usando WS-Security pode ser otimizada usando MTOM.

### <a name="examples"></a>Exemplos

#### <a name="wcf-soap-11-message-encoded-using-mtom"></a>Mensagem do WCF SOAP 1,1 codificada usando MTOM

```http
POST http://131.107.72.15/Mtom/svc/service.svc/Soap11MtomUTF8 HTTP/1.1
SOAPAction: "http://xmlsoap.org/echoBinaryAsString"
Content-Type: multipart/related;type="application/xop+xml";
              start="<http://tempuri.org/0>";start-info="text/xml";
       boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1"
Host: 131.107.72.15
Content-Length: 1501
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1
Content-ID: <http://tempuri.org/0>
Content-Transfer-Encoding: 8bit
Content-Type: application/xop+xml;charset=utf-8;type="text/xml"
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/">
  <s:Body>
    <EchoBinaryAsString xmlns="http://xmlsoap.org/Ping">
      <array>
        <xop:Include
         href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206521093670"
         xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
      </array>
    </EchoBinaryAsString>
  </s:Body>
</s:Envelope>
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1
Content-ID: <http://tempuri.org/1/632618206521093670>
Content-Transfer-Encoding: binary
Content-Type: application/octet-stream
…Binary Content..
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=1
```

#### <a name="wcf-secure-soap-12-message-encoded-using-mtom"></a>Mensagem SMB Secure SOAP 1,2 codificada usando MTOM

Neste exemplo, uma mensagem é codificada usando MTOM e SOAP 1,2 que é protegido usando o WS-Security. As partes binárias identificadas para codificação são o conteúdo do `BinarySecurityToken` , `CipherValue` do `EncryptedData` correspondente à assinatura criptografada e ao corpo criptografado. Observe que o `CipherValue` de `EncryptedKey` não foi identificado para otimização pelo WCF, pois seu comprimento é menor que 1024 bytes.

```http
POST http://131.107.72.15/Mtom/service.svc/Soap12MtomSecureSignEncrypt HTTP/1.1
Content-Type: multipart/related; type="application/xop+xml";
              start="<http://tempuri.org/0>";
            boundary="uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3";
              start-info="application/soap+xml";
              action="http://xmlsoap.org/echoBinaryAsString"
Host: 131.107.72.15
Content-Length: 1941
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3
Content-ID: <http://tempuri.org/0>
Content-Transfer-Encoding: 8bit
Content-Type: application/xop+xml;charset=utf-8;type="application/soap+xml"
<s:Envelope xmlns:s="http://schemas.xmlsoap.org/soap/envelope/" xmlns:u="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
  <s:Header>
    <o:Security s:mustUnderstand="1" xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
      <u:Timestamp u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-5">
        <u:Created>2005-09-09T06:57:32.488Z</u:Created>
        <u:Expires>2005-09-09T07:02:32.488Z</u:Expires>
      </u:Timestamp>
      <o:BinarySecurityToken u:Id="uuid-4d4ee765-5717-4d53-9ac9-99bddc07df6c-2" ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509v3" EncodingType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0#Base64Binary">
        <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F1%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
      </o:BinarySecurityToken>
      <e:EncryptedKey Id="_1" xmlns:e="http://www.w3.org/2001/04/xmlenc#">
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#rsa-oaep-mgf1p"/>
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
          <o:SecurityTokenReference>
            <o:KeyIdentifier ValueType="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0#X509SubjectKeyIdentifier">Xeg55vRyK3ZhAEhEf+YT0z986L0=</o:KeyIdentifier>
          </o:SecurityTokenReference>
        </KeyInfo>
        <e:CipherData>          <e:CipherValue>oQfpxwT8/SAGyZQzKE2b4yO6dXuQj7pwJ+5CGL3Rf7C06bQ5ttMoQ9GLJcQYkXTzin+WwHEgs5bj5ml9HKTW9QAU5JJ6lksdymmQvWP5ZtGPBVchO4sofEGoCKmBiZL/DYS/cnbzgnc/3a6NYnc10y2fWGaGLiqa00zijAw7o0Y=</e:CipherValue>
        </e:CipherData>
      </e:EncryptedKey>
      <c:DerivedKeyToken u:Id="_2" xmlns:c="http://schemas.xmlsoap.org/ws/2005/02/sc">
        <o:SecurityTokenReference>
          <o:Reference URI="#_1"/>
        </o:SecurityTokenReference>
        <c:Nonce>OrEPRX7fISIS4sXYWPMv3g==</c:Nonce>
      </c:DerivedKeyToken>
      <e:ReferenceList xmlns:e="http://www.w3.org/2001/04/xmlenc#">
        <e:DataReference URI="#_3"/>
        <e:DataReference URI="#_4"/>
      </e:ReferenceList>
      <e:EncryptedData Id="_4" Type="http://www.w3.org/2001/04/xmlenc#Element" xmlns:e="http://www.w3.org/2001/04/xmlenc#">
        <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>
        <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
          <o:SecurityTokenReference>
            <o:Reference URI="#_2"/>
          </o:SecurityTokenReference>
        </KeyInfo>
        <e:CipherData>
          <e:CipherValue>
            <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F2%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
          </e:CipherValue>
        </e:CipherData>
      </e:EncryptedData>
    </o:Security>
  </s:Header>
  <s:Body u:Id="_0">
    <e:EncryptedData Id="_3" Type="http://www.w3.org/2001/04/xmlenc#Content" xmlns:e="http://www.w3.org/2001/04/xmlenc#">
      <e:EncryptionMethod Algorithm="http://www.w3.org/2001/04/xmlenc#aes256-cbc"/>
      <KeyInfo xmlns="http://www.w3.org/2000/09/xmldsig#">
        <o:SecurityTokenReference xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
          <o:Reference URI="#_2"/>
        </o:SecurityTokenReference>
      </KeyInfo>
      <e:CipherData>
        <e:CipherValue>
          <xop:Include href="cid:http%3A%2F%2Ftempuri.org%2F3%2F632618206525089430" xmlns:xop="http://www.w3.org/2004/08/xop/include"/>
        </e:CipherValue>
      </e:CipherData>
    </e:EncryptedData>
  </s:Body>
</s:Envelope>
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3
Content-ID: <http://tempuri.org/1/632618206525089430>
Content-Transfer-Encoding: binary
Content-Type: application/octet-stream
...Binary content of BinarySecurityToken - X509 Certificate...
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3
Content-ID: <http://tempuri.org/2/632618206525089430>
Content-Transfer-Encoding: binary
Content-Type: application/octet-stream
...Binary serialization of the encrypted primary signature...
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3
Content-ID: <http://tempuri.org/3/632618206525089430>
Content-Transfer-Encoding: binary
Content-Type: application/octet-stream
...Binary serialization of the encrypted Body...
--uuid:0ca0e16e-feb1-426c-97d8-c4508ada5e82+id=3--
```
