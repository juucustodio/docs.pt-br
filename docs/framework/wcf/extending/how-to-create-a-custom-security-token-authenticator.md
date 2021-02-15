---
description: 'Saiba mais sobre: como criar um autenticador de token de segurança personalizado'
title: 'Como: criar um autenticador de token de segurança personalizado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, authentication
ms.assetid: 10e245f7-d31e-42e7-82a2-d5780325d372
ms.openlocfilehash: dd1dbd413638ab8693ec5ac3454d9fac9b26565b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99780746"
---
# <a name="how-to-create-a-custom-security-token-authenticator"></a>Como: criar um autenticador de token de segurança personalizado

Este tópico mostra como criar um autenticador de token de segurança personalizado e como integrá-lo a um Gerenciador de token de segurança personalizado. Um autenticador de token de segurança valida o conteúdo de um token de segurança fornecido com uma mensagem de entrada. Se a validação for realizada com sucesso, o autenticador retornará uma coleção de <xref:System.IdentityModel.Policy.IAuthorizationPolicy> instâncias que, quando avaliada, retornará um conjunto de declarações.  
  
 Para usar um autenticador de token de segurança personalizado no Windows Communication Foundation (WCF), você deve primeiro criar credenciais personalizadas e implementações do Gerenciador de token de segurança. Para obter mais informações sobre como criar credenciais personalizadas e um Gerenciador de token de segurança, consulte [passo a passos: criando credenciais personalizadas de cliente e serviço](walkthrough-creating-custom-client-and-service-credentials.md).
  
## <a name="procedures"></a>Procedimentos  
  
#### <a name="to-create-a-custom-security-token-authenticator"></a>Para criar um autenticador de token de segurança personalizado  
  
1. Defina uma nova classe derivada da <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator> classe.  
  
2. Substitua o método <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.CanValidateTokenCore%2A>. O método retorna `true` ou `false` dependendo se o autenticador personalizado pode validar o tipo de token de entrada ou não.  
  
3. Substitua o método <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.ValidateTokenCore%2A>. Esse método precisa validar o conteúdo do token adequadamente. Se o token passar na etapa de validação, ele retornará uma coleção de <xref:System.IdentityModel.Policy.IAuthorizationPolicy> instâncias. O exemplo a seguir usa uma implementação de política de autorização personalizada que será criada no próximo procedimento.  
  
     [!code-csharp[C_CustomTokenAuthenticator#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#1)]
     [!code-vb[C_CustomTokenAuthenticator#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#1)]  
  
 O código anterior retorna uma coleção de políticas de autorização no <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator.CanValidateToken%28System.IdentityModel.Tokens.SecurityToken%29> método. O WCF não fornece uma implementação pública dessa interface. O procedimento a seguir mostra como fazer isso para seus próprios requisitos.  
  
#### <a name="to-create-a-custom-authorization-policy"></a>Para criar uma política de autorização personalizada  
  
1. Defina uma nova classe que implementa a <xref:System.IdentityModel.Policy.IAuthorizationPolicy> interface.  
  
2. Implemente a <xref:System.IdentityModel.Policy.IAuthorizationComponent.Id%2A> propriedade somente leitura. Uma maneira de implementar essa propriedade é gerar um GUID (identificador global exclusivo) no construtor da classe e retorná-la sempre que o valor dessa propriedade for solicitado.  
  
3. Implemente a <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Issuer%2A> propriedade somente leitura. Essa propriedade precisa retornar um emissor dos conjuntos de declarações que são obtidos do token. Esse emissor deve corresponder ao emissor do token ou a uma autoridade responsável pela validação do conteúdo do token. O exemplo a seguir usa a declaração de emissor que passou para essa classe do autenticador de token de segurança personalizado criado no procedimento anterior. O autenticador de token de segurança personalizado usa o conjunto de declarações fornecido pelo sistema (retornado pela <xref:System.IdentityModel.Claims.ClaimSet.System%2A> Propriedade) para representar o emissor do token de nome de usuário.  
  
4. Implementar o método de <xref:System.IdentityModel.Policy.IAuthorizationPolicy.Evaluate%2A> . Esse método popula uma instância da <xref:System.IdentityModel.Policy.EvaluationContext> classe (passada como um argumento) com declarações baseadas no conteúdo do token de segurança de entrada. O método retorna `true` quando é feito com a avaliação. Em casos em que a implementação depende da presença de outras políticas de autorização que fornecem informações adicionais para o contexto de avaliação, esse método pode retornar `false` se as informações necessárias ainda não estiverem presentes no contexto de avaliação. Nesse caso, o WCF chamará o método novamente depois de avaliar todas as outras políticas de autorização geradas para a mensagem de entrada se pelo menos uma dessas políticas de autorização modificar o contexto de avaliação.  
  
     [!code-csharp[c_CustomTokenAuthenticator#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#3)]
     [!code-vb[c_CustomTokenAuthenticator#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#3)]  

 [Walkthrough: criando credenciais de cliente e de serviço personalizadas](walkthrough-creating-custom-client-and-service-credentials.md) descreve como criar credenciais personalizadas e um Gerenciador de token de segurança personalizado. Para usar o autenticador de token de segurança personalizado criado aqui, uma implementação do Gerenciador de token de segurança é modificada para retornar o autenticador personalizado do <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%2A> método. O método retorna um autenticador quando um requisito de token de segurança apropriado é passado.  
  
#### <a name="to-integrate-a-custom-security-token-authenticator-with-a-custom-security-token-manager"></a>Para integrar um autenticador de token de segurança personalizado com um Gerenciador de token de segurança personalizado  
  
1. Substitua o <xref:System.IdentityModel.Selectors.SecurityTokenManager.CreateSecurityTokenAuthenticator%2A> método em sua implementação personalizada do Gerenciador de token de segurança.  
  
2. Adicione lógica ao método para permitir que ele retorne seu autenticador de token de segurança personalizado com base no <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> parâmetro. O exemplo a seguir retorna um autenticador de token de segurança personalizado se o tipo de token de requisitos de token for um nome de usuário (representado pela <xref:System.IdentityModel.Tokens.SecurityTokenTypes.UserName%2A> Propriedade) e a direção da mensagem para a qual o autenticador de token de segurança está sendo solicitado é entrada (representada pelo <xref:System.ServiceModel.Description.MessageDirection.Input> campo).  
  
     [!code-csharp[c_CustomTokenAuthenticator#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customtokenauthenticator/cs/source.cs#2)]
     [!code-vb[c_CustomTokenAuthenticator#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customtokenauthenticator/vb/source.vb#2)]  

## <a name="see-also"></a>Consulte também

- <xref:System.IdentityModel.Selectors.SecurityTokenAuthenticator>
- <xref:System.IdentityModel.Selectors.SecurityTokenRequirement>
- <xref:System.IdentityModel.Selectors.SecurityTokenManager>
- <xref:System.IdentityModel.Tokens.UserNameSecurityToken>
- [Passo a passo: criar credenciais de serviço e cliente personalizados](walkthrough-creating-custom-client-and-service-credentials.md)
- [Como: criar um provedor de token de segurança personalizado](how-to-create-a-custom-security-token-provider.md)
