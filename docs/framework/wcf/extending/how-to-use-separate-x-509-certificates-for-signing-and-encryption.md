---
description: 'Saiba mais sobre: como usar certificados X. 509 separados para assinatura e criptografia'
title: 'Como: usar certificados X.509 separados para assinatura e criptografia'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- WCF, extensibility
- ClientCredentials class
- ClientCredentialsSecurityTokenManager class
ms.assetid: 0b06ce4e-7835-4d82-8baf-d525c71a0e49
ms.openlocfilehash: a1cb72265d9fa2742718b88bd574efe4cc9a4918
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99644236"
---
# <a name="how-to-use-separate-x509-certificates-for-signing-and-encryption"></a>Como: usar certificados X.509 separados para assinatura e criptografia

Este tópico mostra como configurar o Windows Communication Foundation (WCF) para usar certificados diferentes para assinatura e criptografia de mensagens no cliente e no serviço.

Para permitir que certificados separados sejam usados para assinatura e criptografia, um cliente personalizado ou credenciais de serviço (ou ambos) devem ser criadas porque o WCF não fornece uma API para definir vários certificados de cliente ou de serviço. Além disso, um Gerenciador de token de segurança deve ser fornecido para aproveitar as informações de vários certificados e para criar um provedor de token de segurança apropriado para o uso de chave e a direção da mensagem especificados.

O diagrama a seguir mostra as classes principais usadas, as classes das quais elas herdam (mostradas por uma seta apontando para cima) e os tipos de retorno de determinados métodos e propriedades.

- `MyClientCredentials` é uma implementação personalizada do <xref:System.ServiceModel.Description.ClientCredentials> .

  - Suas propriedades mostradas no diagrama todas as instâncias retornam de <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> .

  - Seu método <xref:System.ServiceModel.Description.ClientCredentials.CreateSecurityTokenManager%2A> retorna uma instância do `MyClientCredentialsSecurityTokenManager` .

- `MyClientCredentialsSecurityTokenManager` é uma implementação personalizada do <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> .

  - Seu método <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A> retorna uma instância do <xref:System.IdentityModel.Selectors.X509SecurityTokenProvider> .

![Gráfico mostrando como as credenciais do cliente são usadas](./media/e4971edd-a59f-4571-b36f-7e6b2f0d610f.gif "e4971edd-a59f-4571-b36f-7e6b2f0d610f")

Para obter mais informações sobre credenciais personalizadas, consulte [Walkthrough: criando credenciais personalizadas de cliente e serviço](walkthrough-creating-custom-client-and-service-credentials.md).

Além disso, você deve criar um verificador de identidade personalizado e vinculá-lo a um elemento de associação de segurança em uma associação personalizada. Você também deve usar as credenciais personalizadas em vez das credenciais padrão.

O diagrama a seguir mostra as classes envolvidas na associação personalizada e como o verificador de identidade personalizado está vinculado. Há vários elementos de ligação envolvidos, todos herdados de <xref:System.ServiceModel.Channels.BindingElement> . O <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> tem a <xref:System.ServiceModel.Channels.LocalClientSecuritySettings> propriedade, que retorna uma instância do <xref:System.ServiceModel.Security.IdentityVerifier> , da qual `MyIdentityVerifier` é personalizado.

![Gráfico mostrando um elemento de associação personalizado](./media/dddea4a2-0bb4-4921-9bf4-20d4d82c3da5.gif "dddea4a2-0bb4-4921-9bf4-20d4d82c3da5")

Para obter mais informações sobre como criar um verificador de identidade personalizado, consulte Como: [como criar um verificador de identidade de cliente personalizado](how-to-create-a-custom-client-identity-verifier.md).

### <a name="to-use-separate-certificates-for-signing-and-encryption"></a>Para usar certificados separados para assinatura e criptografia

1. Defina uma nova classe de credenciais de cliente que herda da <xref:System.ServiceModel.Description.ClientCredentials> classe. Implemente quatro novas propriedades para permitir a especificação de vários certificados: `ClientSigningCertificate` , `ClientEncryptingCertificate` , `ServiceSigningCertificate` e `ServiceEncryptingCertificate` . Além disso, substitua o <xref:System.ServiceModel.Description.ClientCredentials.CreateSecurityTokenManager%2A> método para retornar uma instância da <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> classe personalizada que é definida na próxima etapa.

     [!code-csharp[c_FourCerts#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#1)]
     [!code-vb[c_FourCerts#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#1)]

2. Defina um novo Gerenciador de token do Client Security que herda da <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager> classe. Substitua o <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A> método para criar um provedor de token de segurança apropriado. O `requirement` parâmetro (a <xref:System.IdentityModel.Selectors.SecurityTokenRequirement> ) fornece a direção da mensagem e o uso da chave.

     [!code-csharp[c_FourCerts#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#2)]
     [!code-vb[c_FourCerts#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#2)]

3. Defina uma nova classe de credenciais de serviço que herda da <xref:System.ServiceModel.Description.ServiceCredentials> classe. Implemente quatro novas propriedades para permitir a especificação de vários certificados: `ClientSigningCertificate` , `ClientEncryptingCertificate` , `ServiceSigningCertificate` e `ServiceEncryptingCertificate` . Além disso, substitua o <xref:System.ServiceModel.Description.ServiceCredentials.CreateSecurityTokenManager%2A> método para retornar uma instância da <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager> classe personalizada que é definida na próxima etapa.

     [!code-csharp[c_FourCerts#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#3)]
     [!code-vb[c_FourCerts#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#3)]

4. Defina um novo Gerenciador de token de segurança de serviço que herda da <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager> classe. Substitua o <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager.CreateSecurityTokenProvider%2A> método para criar um provedor de token de segurança apropriado, considerando a direção da mensagem passada e o uso da chave.

     [!code-csharp[c_FourCerts#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#4)]
     [!code-vb[c_FourCerts#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#4)]

### <a name="to-use-multiple-certificates-on-the-client"></a>Para usar vários certificados no cliente

1. Crie uma associação personalizada. O elemento de associação de segurança deve operar no modo duplex para permitir que diferentes provedores de token de segurança estejam presentes para solicitações e respostas. Uma maneira de fazer isso é usar um transporte compatível com duplex ou usar o <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement> , conforme mostrado no código a seguir. Vincule o personalizado <xref:System.ServiceModel.Security.IdentityVerifier> que é definido na próxima etapa para o elemento de associação de segurança. Substitua as credenciais de cliente padrão pelas credenciais de cliente personalizadas criadas anteriormente.

     [!code-csharp[c_FourCerts#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#5)]
     [!code-vb[c_FourCerts#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#5)]

2. Defina um personalizado <xref:System.ServiceModel.Security.IdentityVerifier> . O serviço tem várias identidades porque certificados diferentes são usados para criptografar a solicitação e para assinar a resposta.

    > [!NOTE]
    > No exemplo a seguir, o verificador de identidade personalizado fornecido não executa nenhuma verificação de identidade de ponto de extremidade para fins de demonstração. Essa não é uma prática recomendada para o código de produção.

     [!code-csharp[c_FourCerts#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#6)]
     [!code-vb[c_FourCerts#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#6)]

### <a name="to-use-multiple-certificates-on-the-service"></a>Para usar vários certificados no serviço

1. Crie uma associação personalizada. O elemento de associação de segurança deve operar em um modo duplex para permitir que diferentes provedores de token de segurança estejam presentes para solicitações e respostas. Assim como no cliente, use um transporte compatível com duplex ou use <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement> , conforme mostrado no código a seguir. Substitua as credenciais de serviço padrão pelas credenciais de serviço personalizadas criadas anteriormente.

     [!code-csharp[c_FourCerts#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_fourcerts/cs/source.cs#7)]
     [!code-vb[c_FourCerts#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_fourcerts/vb/source.vb#7)]

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Description.ClientCredentials>
- <xref:System.ServiceModel.Description.ServiceCredentials>
- <xref:System.ServiceModel.ClientCredentialsSecurityTokenManager>
- <xref:System.ServiceModel.Security.ServiceCredentialsSecurityTokenManager>
- <xref:System.ServiceModel.Security.IdentityVerifier>
- [Passo a passo: criar credenciais de serviço e cliente personalizados](walkthrough-creating-custom-client-and-service-credentials.md)
