---
description: 'Saiba mais sobre: validação de credencial e credencial personalizada'
title: Credencial personalizada e validação de credencial
ms.date: 03/30/2017
helpviewer_keywords:
- credentials [WCF], custom
- credentials [WCF]
- custom credentials [WCF]
- credential validation [WCF]
- credentials [WCF], validation
ms.assetid: da831bec-e281-4d44-b343-437b5eef688e
ms.openlocfilehash: f1ceb8cf46cca01ac31faeb9485cbeb6c8663d31
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735303"
---
# <a name="custom-credential-and-credential-validation"></a>Credencial personalizada e validação de credencial

A segurança no Windows Communication Foundation (WCF) é baseada na troca de credenciais entre serviços e clientes. A maioria dos cenários de segurança pode ser satisfeita usando tipos de credenciais comuns, como Windows (Kerberos), nome de usuário e senhas e certificados. No entanto, se um novo tipo de credencial for necessário, os tópicos nesta seção explicam como tratar e validar novos tipos.  
  
## <a name="in-this-section"></a>Nesta seção  

 [Como: criar um serviço que utiliza um validador de certificado personalizado](how-to-create-a-service-that-employs-a-custom-certificate-validator.md)  
 Explica como personalizar a validação do WCF herdando da <xref:System.IdentityModel.Selectors.X509CertificateValidator> classe.  
  
 [Passo a passo: criar credenciais de serviço e cliente personalizados](walkthrough-creating-custom-client-and-service-credentials.md)  
 Demonstra como estender as <xref:System.ServiceModel.Description.ClientCredentials> classes e <xref:System.ServiceModel.Description.ServiceCredentials> para acomodar novos tipos de credencial. Isso é primeiro em uma série de tópicos que permitem a criação de tipos de credenciais personalizados.  
  
 [Como: criar um provedor de token de segurança personalizado](how-to-create-a-custom-security-token-provider.md)  
 Explica como criar um provedor de token de segurança para lidar com novos tipos de credenciais e retornar novos tokens para a credencial. Este é o segundo tópico da série.  
  
 [Como: criar um autenticador de token de segurança personalizado](how-to-create-a-custom-security-token-authenticator.md)  
 Explica como criar um autenticador personalizado para autenticar um novo tipo de credencial. Este é o terceiro tópico da série.  
  
## <a name="reference"></a>Referência  

 <xref:System.ServiceModel.Security>  
  
 <xref:System.IdentityModel.Claims>  
  
 <xref:System.IdentityModel.Policy>  
  
 <xref:System.IdentityModel.Tokens>  
  
 <xref:System.IdentityModel.Selectors>  
  
 <xref:System.IdentityModel.Selectors.X509CertificateValidator>  
  
 <xref:System.ServiceModel.Description.ClientCredentials>  
  
 <xref:System.ServiceModel.Description.ServiceCredentials>  
  
## <a name="related-sections"></a>Seções relacionadas  

 [Autenticação](../feature-details/authentication-in-wcf.md)  
  
 [Federação e tokens emitidos](../feature-details/federation-and-issued-tokens.md)  
  
 [Autorização](../feature-details/authorization-in-wcf.md)  
  
## <a name="see-also"></a>Consulte também

- [Segurança](../feature-details/security.md)
