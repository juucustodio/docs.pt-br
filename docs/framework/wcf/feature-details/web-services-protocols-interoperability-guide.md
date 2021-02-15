---
description: 'Saiba mais sobre o: guia de interoperabilidade de protocolos de serviços Web'
title: Guia de interoperabilidade de protocolos de serviços Web
ms.date: 03/30/2017
ms.assetid: f2981678-ebdb-433d-899b-467f7df95fb2
ms.openlocfilehash: cab744818d3a52c6f6cd0d95195d9112ac9babf6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99752542"
---
# <a name="web-services-protocols-interoperability-guide"></a>Guia de interoperabilidade de protocolos de serviços Web

O Windows Communication Foundation (WCF) implementa vários protocolos de serviços da Web. Muitos desses protocolos incluem uma série de opções e pontos de extensibilidade deixados para o critério do implementador. Este artigo fornece uma lista de protocolos de serviços da Web que o WCF implementa. Outros artigos nesta seção fornecem detalhes de implementação para cada protocolo com suporte.

## <a name="web-services-protocols-implemented-by-wcf"></a>Protocolos de serviços Web implementados pelo WCF

O WCF fornece suporte para protocolos de infraestrutura de serviços Web (WS) por meio de canais e protocolos de aplicativo de serviços Web por meio do recurso de contratos. A interoperabilidade para protocolos de aplicativo é realizada por meio da 1,0 linguagem XSD e da linguagem de descrição de serviços da Web (WSDL) 1,1.

A interoperabilidade dos protocolos de infraestrutura é fornecida pelas especificações WS-*. Os canais do WCF oferecem suporte a vários protocolos WS- \* Infrastructure. Os canais do WCF são configurados usando elementos de associação. As tabelas a seguir contêm a lista completa dos protocolos WS- \* Infrastructure implementados por vários elementos de associação do WCF.

<xref:System.ServiceModel.Channels.HttpTransportBindingElement> oferece suporte às especificações na tabela a seguir.

|Especificação/documento|Link|
|-----------------------------|----------|
|HTTP 1.1|[RFC 2616](https://www.rfc-editor.org/rfc/rfc2616.txt)|
|Associação HTTP SOAP 1,1|[Protocolo SOAP (Simple Object Access Protocol) 1,1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/), seção 7|
|Associação HTTP SOAP 1,2|[SOAP versão 1,2 parte 2: Adjuncts (segunda edição)](https://www.w3.org/TR/soap12-part2/), seção 7|

<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> e <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> dão suporte às especificações na tabela a seguir.

|Especificação/documento|Link|
|-----------------------------|----------|
|XML|[Linguagem XML (XML) 1,0 (quarta edição)](https://www.w3.org/TR/REC-xml/)|
|SOAP 1,1|[Protocolo SOAP (Simple Object Access Protocol) 1,1](https://www.w3.org/TR/2000/NOTE-SOAP-20000508/)|
|Núcleo SOAP 1,2|[SOAP versão 1,2 parte 1: estrutura de mensagens (segunda edição)](https://www.w3.org/TR/2007/REC-soap12-part1-20070427/)|
|WS-Addressing 2004/08|[Endereçamento de serviços da Web (WS-Addressing)](https://www.w3.org/Submission/2004/SUBM-ws-addressing-20040810/)|
|Endereçamento de serviços da Web do W3C 1,0-Core|[Endereçamento de serviços da Web 1,0-Core](https://www.w3.org/TR/2006/REC-ws-addr-core-20060509/)|
|Endereçamento de serviços Web W3C 1,0-Associação SOAP|[Endereçamento de serviços Web 1,0-Associação SOAP](https://www.w3.org/TR/2006/REC-ws-addr-soap-20060509/)|
|Endereçamento de serviços Web W3C 1,0-Associação WSDL *|[Endereçamento de serviços Web 1,0-Associação de WSDL](https://www.w3.org/TR/2006/CR-ws-addr-wsdl-20060529/)|
|Metadados de endereçamento do W3C Web Services 1,0|[Endereçamento de serviços Web 1,0-metadados](https://www.w3.org/TR/ws-addr-metadata/)|
|Associação WSDL SOAP 1.1|[WSDL (Web Services Description Language) 1,1](https://www.w3.org/TR/wsdl/)|
|Associação WSDL de SOAP 1.2|[Extensão de associação de WSDL 1,1 para SOAP 1,2](https://www.w3.org/Submission/wsdl11soap12/)|

<xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement> oferece suporte às especificações na tabela a seguir.

|Especificação/documento|Link|
|-----------------------------|----------|
|XOP|[Empacotamento XML-binário otimizado](https://www.w3.org/TR/xop10/)|
|Associação de MTOM + SOAP 1.2|[Mecanismo de otimização de transmissão de mensagens SOAP](https://www.w3.org/TR/soap12-mtom/)|
|Associação de SOAP 1,1 de MTOM|[Ligação SOAP 1,1 para MTOM 1,0](https://www.w3.org/Submission/soap11mtom10/)|
|WS-PolicyAssertions MTOM|[Declaração de política de serialização MTOM (WS-MTOMPolicy)](https://www.w3.org/Submission/WS-MTOMPolicy/)|

<xref:System.ServiceModel.Channels.SecurityBindingElement> oferece suporte às especificações na tabela a seguir.

|Especificação/documento|Link|
|-----------------------------|----------|
|WSS: segurança de mensagem SOAP 1,0|[Especificação Web Services Security: segurança de mensagem SOAP 1,0](https://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-soap-message-security-1.0.pdf)|
|WSS: nome do perfil do token 1,0|[Especificação Web Services Security perfil do UsernameToken 1,0](https://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-username-token-profile-1.0.pdf)<br /><br /> Require Password/@Type = PasswordText (padrão)|
|WSS: X. 509 o perfil de token 1,0|[Especificação Web Services Security perfil de token de certificado X. 509](https://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-x509-token-profile-1.0.pdf)|
|WSS: perfil de token 1,1 SAML 1,0|[Especificação Web Services Security: perfil de token SAML](https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.0.pdf)|
|WSS: segurança de mensagem SOAP 1,1|[Especificação Web Services Security: segurança de mensagem SOAP 1,1](https://www.oasis-open.org/committees/download.php/16790/wss-v1.1-spec-os-SOAPMessageSecurity.pdf)|
|Perfil de token de nome de usuário do WSS 1,1|[Especificação Web Services Security perfil do UsernameToken 1,1](https://www.oasis-open.org/committees/download.php/16782/wss-v1.1-spec-os-UsernameTokenProfile.pdf)<br /><br /> Não implementar derivação de chave baseada em senha;<br /><br /> Require Password/@Type = PasswordText (padrão)|
|WSS: perfil de token X509 1,1|[Especificação Web Services Security perfil do token de certificado X. 509 1,1](https://www.oasis-open.org/committees/download.php/16785/wss-v1.1-spec-os-x509TokenProfile.pdf)|
|WSS: perfil de token Kerberos 1,1|[Especificação Web Services Security perfil de token Kerberos 1,1](https://www.oasis-open.org/committees/download.php/16788/wss-v1.1-spec-os-KerberosTokenProfile.pdf)|
|WSS: perfil de token 1,1 SAML 1,1|[Especificação Web Services Security perfil de token SAML 1,1](https://www.oasis-open.org/committees/download.php/16768/wss-v1.1-spec-os-SAMLTokenProfile.pdf)|
|WS-Secure conversa|[Linguagem de conversa segura de serviços Web](http://specs.xmlsoap.org/ws/2005/02/sc/ws-secureconversation.pdf)|
|WS-Trust 1,4|[Linguagem de confiança dos serviços Web](https://docs.oasis-open.org/ws-sx/ws-trust/200802)|
|WS-SecurityPolicy 2005/07|[Linguagem de conversa segura de serviços Web](http://specs.xmlsoap.org/ws/2005/02/sc/ws-secureconversation.pdf)<br /><br /> Conforme alterado por errata enviada para o comitê técnico WS-SX OASIS.<br /><br /> [mensagem WS-SX](https://lists.oasis-open.org/archives/ws-sx/200512/msg00017.html)|
|WS-ReliableMessaging 1,1|[Protocolo de mensagem confiável versão 1.1](reliable-messaging-protocol-version-1-1.md)|

<xref:System.ServiceModel.Channels.TransactionFlowBindingElement> oferece suporte às especificações na tabela a seguir.

|Especificação/documento|Link|
|-----------------------------|----------|
|WS-Coordination|[Coordenação de serviços Web](/previous-versions/ms951231(v=msdn.10))|
|WS-AtomicTransaction|[Transação atômica de serviços Web](http://specs.xmlsoap.org/ws/2004/10/wsat/wsat.pdf)|

As <xref:System.ServiceModel.Description.MetadataExporter> classes,, <xref:System.ServiceModel.Description.MetadataImporter> <xref:System.ServiceModel.Description.WsdlExporter> , <xref:System.ServiceModel.Description.WsdlImporter> e <xref:System.ServiceModel.Description.MetadataResolver> fornecem suporte para as seguintes especificações de metadados:

- [Esquema XML parte 1: estruturas segunda edição](https://www.w3.org/TR/xmlschema-1/)

- [Esquema XML parte 2: tipos de dados segunda edição](https://www.w3.org/TR/xmlschema-2/)

- [WSDL 1,1](https://www.w3.org/TR/wsdl/)

- [WS-Policy 1,2](https://www.w3.org/Submission/2006/SUBM-WS-Policy-20060425/)

- [WS-Policy 1,5](https://www.w3.org/TR/ws-policy/)

- [WS-PolicyAttachment 1,2](https://www.w3.org/Submission/2006/SUBM-WS-PolicyAttachment-20060425/)

- [WS-MetadataExchange 1,1](http://specs.xmlsoap.org/ws/2004/09/mex/WS-MetadataExchange.pdf)

- [WS-Transfer get para recuperação de metadados](https://www.w3.org/Submission/2006/SUBM-WS-Transfer-20060315/)

Além disso, os seguintes perfis de interoperabilidade são implementados no WCF:

- [Basic Profile 1.1](http://www.ws-i.org/Profiles/BasicProfile-1.1-2004-08-24.html)

- [Vinculação SOAP simples 1,0](http://www.ws-i.org/Profiles/SimpleSoapBindingProfile-1.0-2004-08-24.html)

- [Rascunho de trabalho do perfil de segurança básico 1,0](http://www.ws-i.org/Profiles/BasicSecurityProfile-1.0-2006-03-29.html)

## <a name="see-also"></a>Consulte também

- [Associações de interoperabilidade fornecidas pelo sistema oferece suporte para protocolos de serviços Web](web-services-protocols-supported-by-system-provided-interoperability-bindings.md)
- [Protocolos de mensagens](messaging-protocols.md)
- [Referência de esquema de contrato de dados](data-contract-schema-reference.md)
- [WSDL e política](wsdl-and-policy.md)
- [Protocolos de segurança](security-protocols.md)
- [Protocolo de mensagens confiável versão 1.0](reliable-messaging-protocol-version-1-0.md)
- [Protocolo de mensagem confiável versão 1.1](reliable-messaging-protocol-version-1-1.md)
- [Protocolos de transação](transaction-protocols.md)
- [Protocolo de intercâmbio de contexto](context-exchange-protocol.md)
