---
description: 'Saiba mais sobre: como criar um provedor de token de segurança personalizado'
title: 'Como: criar um provedor de token de segurança personalizado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- security [WCF], providing credentials
ms.assetid: db8cb478-aa43-478b-bf97-c6489ad7c7fd
ms.openlocfilehash: 4e0970ff01be74d0eb9f4ae8968bd100a0dafe00
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735030"
---
# <a name="how-to-create-a-custom-security-token-provider"></a>Como: criar um provedor de token de segurança personalizado

Este tópico mostra como criar novos tipos de token com um provedor de token de segurança personalizado e como integrar o provedor com um Gerenciador de token de segurança personalizado.  
  
> [!NOTE]
> Crie um provedor de token personalizado se os tokens fornecidos pelo sistema encontrados no <xref:System.IdentityModel.Tokens> namespace não corresponderem aos seus requisitos.  
  
 O provedor de token de segurança cria uma representação de token de segurança com base nas informações nas credenciais do cliente ou do serviço. Para usar o provedor de token de segurança personalizado na segurança do Windows Communication Foundation (WCF), você deve criar credenciais personalizadas e implementações do Gerenciador de token de segurança.  
  
 Para obter mais informações sobre as credenciais personalizadas e o Gerenciador de token de segurança, consulte o [passo a passos: criando credenciais personalizadas de cliente e serviço](walkthrough-creating-custom-client-and-service-credentials.md).  
  
### <a name="to-create-a-custom-security-token-provider"></a>Para criar um provedor de token de segurança personalizado  
  
1. Defina uma nova classe derivada da <xref:System.IdentityModel.Selectors.SecurityTokenProvider> classe.  
  
2. Implementar o método de <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> . O método é responsável por criar e retornar uma instância do token de segurança. O exemplo a seguir cria uma classe chamada `MySecurityTokenProvider` e substitui o <xref:System.IdentityModel.Selectors.SecurityTokenProvider.GetTokenCore%28System.TimeSpan%29> método para retornar uma instância da <xref:System.IdentityModel.Tokens.X509SecurityToken> classe. O construtor de classe requer uma instância da <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> classe.  
  
     [!code-csharp[c_CustomTokenProvider#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#1)]
     [!code-vb[c_CustomTokenProvider#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#1)]  
  
### <a name="to-integrate-a-custom-security-token-provider-with-a-custom-security-token-manager"></a>Para integrar um provedor de token de segurança personalizado com um Gerenciador de token de segurança personalizado  
  
1. Defina uma nova classe derivada da <xref:System.IdentityModel.Selectors.SecurityTokenManager> classe. (O exemplo a seguir deriva da <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> classe, que deriva da <xref:System.IdentityModel.Selectors.SecurityTokenManager> classe.)  
  
2. Substitua o <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> método se ainda não estiver substituído.  
  
     O <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenProvider%28System.IdentityModel.Selectors.SecurityTokenRequirement%29> método é responsável por retornar uma instância da <xref:System.IdentityModel.Selectors.SecurityTokenProvider> classe apropriada ao <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> parâmetro passado para o método pela estrutura de segurança do WCF. Modifique o método para retornar a implementação do provedor de token de segurança personalizado (criado no procedimento anterior) quando o método for chamado com um parâmetro de token de segurança apropriado. Para obter mais informações sobre o Gerenciador de token de segurança, consulte o [passo a passos: criando credenciais personalizadas de cliente e serviço](walkthrough-creating-custom-client-and-service-credentials.md).  
  
3. Adicione uma lógica personalizada ao método para permitir que ele retorne seu provedor de token de segurança personalizado com base no <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> parâmetro. O exemplo a seguir retorna o provedor de token de segurança personalizado se os requisitos de token forem atendidos. Os requisitos incluem um token de segurança X. 509 e a direção da mensagem (que o token é usado para saída da mensagem). Para todos os outros casos, o código chama a classe base para manter o comportamento fornecido pelo sistema para outros requisitos de token de segurança.  
  
 [!code-csharp[c_CustomTokenProvider#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#2)]
 [!code-vb[c_CustomTokenProvider#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#2)]  
  
## <a name="example"></a>Exemplo  

 O seguinte mostra uma <xref:System.IdentityModel.Selectors.SecurityTokenProvider> implementação completa junto com uma <xref:System.IdentityModel.Selectors.SecurityTokenManager> implementação correspondente.  
  
 [!code-csharp[c_CustomTokenProvider#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenprovider/cs/source.cs#0)]
 [!code-vb[c_CustomTokenProvider#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenprovider/vb/source.vb#0)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.IdentityModel.Selectors.SecurityTokenProvider>
- <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>
- <xref:System.IdentityModel.Selectors.SecurityTokenManager>
- <xref:System.IdentityModel.Tokens.X509SecurityToken>
- [Passo a passo: criar credenciais de serviço e cliente personalizados](walkthrough-creating-custom-client-and-service-credentials.md)
- [Como: criar um autenticador de token de segurança personalizado](how-to-create-a-custom-security-token-authenticator.md)
