---
description: 'Saiba mais sobre: Federação e tokens emitidos'
title: Federação e tokens emitidos
ms.date: 03/30/2017
helpviewer_keywords:
- WCF, federation
- issued tokens [WCF]
- federation [WCF], issued tokens
ms.assetid: 4c31ee7d-a820-4067-8b84-a83049021bb6
ms.openlocfilehash: 209a3f158e2ffc00c3fd09053374340c430cc823
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780239"
---
# <a name="federation-and-issued-tokens"></a>Federação e tokens emitidos

Com o Windows Communication Foundation (WCF), você pode criar clientes que se comunicam de forma segura com os serviços que implementam as especificações de WS-Federation e WS-Trust. As especificações usam XML, SOAP e WSDL (Web Services Description Language) para fornecer mecanismos que habilitam a autenticação e a autorização entre territórios de confiança diferentes.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Federação](federation.md)  
 Fornece uma visão geral da Federação.  
  
 [Federação e confiabilidade](federation-and-trust.md)  
 Lista os problemas de design a serem considerados ao criar serviços ou clientes federados.  
  
 [Como: criar um cliente federado](how-to-create-a-federated-client.md)  
 Descreve as noções básicas de criação de um cliente federado com o WCF.  
  
 [Como: configurar credenciais em um serviço de federação](how-to-configure-credentials-on-a-federation-service.md)  
 Descreve as etapas de criação de um serviço federado.  
  
 [Como: criar uma WSFederationHttpBinding](how-to-create-a-wsfederationhttpbinding.md)  
 Descreve como configurar clientes e serviços que usam o `WSFederationHttpBinding` .  
  
 [Como: criar um serviço de token de segurança](how-to-create-a-security-token-service.md)  
 Descreve as etapas de criação de um serviço de token de segurança.  
  
 [Declarações e tokens de SAML (Security Assertions Markup Language)](saml-tokens-and-claims.md)  
 Descreve os tokens SAML (Security Asserties Markup Language), que são extensíveis e permitem que você crie tipos de declaração avançados.  
  
 [Como: configurar um emissor local](how-to-configure-a-local-issuer.md)  
 Descreve como criar um emissor local de tokens de segurança.  
  
 [Como: desabilitar sessões seguras em uma WSFederationHttpBinding](how-to-disable-secure-sessions-on-a-wsfederationhttpbinding.md)  
 Descreve como desabilitar sessões seguras em um `WSFederationHttpBinding` . A desabilitação de sessões seguras é necessária ao criar um Web farm que requer uma sessão para cada cliente.  
  
## <a name="reference"></a>Referência  

 <xref:System.IdentityModel.Claims>  
  
 <xref:System.ServiceModel.ServiceAuthorizationManager>  
  
 <xref:System.IdentityModel.Tokens.SamlSecurityToken>  
  
 <xref:System.ServiceModel.Security.IssuedTokenClientCredential>  
  
 <xref:System.ServiceModel.Security.IssuedTokenServiceCredential>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenParameters>  
  
 <xref:System.ServiceModel.Security.Tokens.IssuedSecurityTokenProvider>  
  
 <xref:System.ServiceModel.WSFederationHttpBinding>  
  
## <a name="see-also"></a>Consulte também

- [Autorização](authorization-in-wcf.md)
- [Tokens personalizados](../extending/custom-tokens.md)
- [Modelo de segurança para o Windows Server app Fabric](/previous-versions/appfabric/ee677202(v=azure.10))
