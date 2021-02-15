---
description: 'Saiba mais sobre: como alterar o provedor criptográfico para uma chave privada do certificado X. 509'
title: 'Como: alterar o provedor de criptografia de uma chave privada de certificado X.509'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- cryptographic provider [WCF], changing
- cryptographic provider [WCF]
ms.assetid: b4254406-272e-4774-bd61-27e39bbb6c12
ms.openlocfilehash: e68f4ffb5626a2c332853bd97eb513516401a185
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99756702"
---
# <a name="how-to-change-the-cryptographic-provider-for-an-x509-certificates-private-key"></a>Como: alterar o provedor de criptografia de uma chave privada de certificado X.509

Este tópico mostra como alterar o provedor criptográfico usado para fornecer uma chave privada do certificado X. 509 e como integrar o provedor à estrutura de segurança do Windows Communication Foundation (WCF). Para obter mais informações sobre como usar certificados, consulte [trabalhando com certificados](../feature-details/working-with-certificates.md).  
  
 A estrutura de segurança do WCF fornece uma maneira de introduzir novos tipos de token de segurança, conforme descrito em [como criar um token personalizado](how-to-create-a-custom-token.md). Também é possível usar um token personalizado para substituir os tipos de token existentes fornecidos pelo sistema.  
  
 Neste tópico, o token de segurança X. 509 fornecido pelo sistema é substituído por um token X. 509 personalizado que fornece uma implementação diferente para a chave privada do certificado. Isso é útil em cenários em que a chave privada real é fornecida por um provedor criptográfico diferente do provedor de criptografia padrão do Windows. Um exemplo de um provedor criptográfico alternativo é um módulo de segurança de hardware que executa todas as operações criptográficas relacionadas à chave privada e não armazena as chaves privadas na memória, melhorando assim a segurança do sistema.  
  
 O exemplo a seguir é apenas para fins de demonstração. Ele não substitui o provedor criptográfico padrão do Windows, mas mostra onde esse provedor poderia ser integrado.  
  
## <a name="procedures"></a>Procedimentos  

 Cada token de segurança que tem uma chave de segurança ou chaves associadas deve implementar a <xref:System.IdentityModel.Tokens.SecurityToken.SecurityKeys%2A> propriedade, que retorna uma coleção de chaves da instância de token de segurança. Se o token for um token de segurança X. 509, a coleção conterá uma única instância da <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey> classe que representa as chaves pública e privada associadas ao certificado. Para substituir o provedor criptográfico padrão usado para fornecer as chaves do certificado, crie uma nova implementação dessa classe.  
  
#### <a name="to-create-a-custom-x509-asymmetric-key"></a>Para criar uma chave assimétrica X. 509 personalizada  
  
1. Defina uma nova classe derivada da <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey> classe.  
  
2. Substitua a <xref:System.IdentityModel.Tokens.SecurityKey.KeySize%2A> propriedade somente leitura. Essa propriedade retorna o tamanho real da chave do par de chaves pública/privada do certificado.  
  
3. Substitua o método <xref:System.IdentityModel.Tokens.SecurityKey.DecryptKey%2A>. Esse método é chamado pela estrutura de segurança do WCF para descriptografar uma chave simétrica com a chave privada do certificado. (A chave foi criptografada anteriormente com a chave pública do certificado.)  
  
4. Substitua o método <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetAsymmetricAlgorithm%2A>. Esse método é chamado pela estrutura de segurança do WCF para obter uma instância da <xref:System.Security.Cryptography.AsymmetricAlgorithm> classe que representa o provedor criptográfico para a chave pública ou privada do certificado, dependendo dos parâmetros passados para o método.  
  
5. Opcional. Substitua o método <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetHashAlgorithmForSignature%2A>. Substitua esse método se uma implementação diferente da <xref:System.Security.Cryptography.HashAlgorithm> classe for necessária.  
  
6. Substitua o método <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey.GetSignatureFormatter%2A>. Esse método retorna uma instância da <xref:System.Security.Cryptography.AsymmetricSignatureFormatter> classe associada à chave privada do certificado.  
  
7. Substitua o método <xref:System.IdentityModel.Tokens.SecurityKey.IsSupportedAlgorithm%2A>. Esse método é usado para indicar se há suporte para um algoritmo criptográfico específico pela implementação da chave de segurança.  
  
     [!code-csharp[c_CustomX509Token#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#1)]
     [!code-vb[c_CustomX509Token#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#1)]  
  
 O procedimento a seguir mostra como integrar a implementação personalizada da chave de segurança assimétrica X. 509 criada no procedimento anterior com a estrutura de segurança do WCF para substituir o token de segurança X. 509 fornecido pelo sistema.  
  
#### <a name="to-replace-the-system-provided-x509-security-token-with-a-custom-x509-asymmetric-security-key-token"></a>Para substituir o token de segurança X. 509 fornecido pelo sistema por um token de chave de segurança assimétrica X. 509 personalizado  
  
1. Crie um token de segurança X. 509 personalizado que retorna a chave de segurança assimétrica personalizada X. 509 em vez da chave de segurança fornecida pelo sistema, conforme mostrado no exemplo a seguir. Para obter mais informações sobre tokens de segurança personalizados, consulte [como: criar um token personalizado](how-to-create-a-custom-token.md).  
  
     [!code-csharp[c_CustomX509Token#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#2)]
     [!code-vb[c_CustomX509Token#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#2)]  
  
2. Crie um provedor de token de segurança personalizado que retorne um token de segurança X. 509 personalizado, conforme mostrado no exemplo. Para obter mais informações sobre provedores de token de segurança personalizados, consulte [como criar um provedor de token de segurança personalizado](how-to-create-a-custom-security-token-provider.md).  
  
     [!code-csharp[c_CustomX509Token#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#3)]
     [!code-vb[c_CustomX509Token#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#3)]  
  
3. Se a chave de segurança personalizada precisar ser usada no lado do iniciador, crie um Gerenciador de tokens de segurança do cliente personalizado e classes de credenciais de cliente personalizadas, conforme mostrado no exemplo a seguir. Para obter mais informações sobre credenciais de cliente personalizadas e gerenciadores de tokens de segurança do cliente, consulte [passo a passos: criando credenciais personalizadas de cliente e serviço](walkthrough-creating-custom-client-and-service-credentials.md).  
  
     [!code-csharp[c_CustomX509Token#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#4)]
     [!code-vb[c_CustomX509Token#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#4)]  
  
     [!code-csharp[c_CustomX509Token#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#6)]
     [!code-vb[c_CustomX509Token#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#6)]  
  
4. Se a chave de segurança personalizada precisar ser usada no lado do destinatário, crie um Gerenciador de token de segurança de serviço personalizado e as credenciais de serviço personalizadas, conforme mostrado no exemplo a seguir. Para obter mais informações sobre credenciais de serviço personalizadas e gerenciadores de token de segurança de serviço, consulte [passo a passos: criando credenciais personalizadas de cliente e serviço](walkthrough-creating-custom-client-and-service-credentials.md).  
  
     [!code-csharp[c_CustomX509Token#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#5)]
     [!code-vb[c_CustomX509Token#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#5)]  
  
     [!code-csharp[c_CustomX509Token#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_customx509token/cs/source.cs#7)]
     [!code-vb[c_CustomX509Token#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_customx509token/vb/source.vb#7)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.IdentityModel.Tokens.X509AsymmetricSecurityKey>
- <xref:System.IdentityModel.Tokens.AsymmetricSecurityKey>
- <xref:System.IdentityModel.Tokens.SecurityKey>
- <xref:System.Security.Cryptography.AsymmetricAlgorithm>
- <xref:System.Security.Cryptography.HashAlgorithm>
- <xref:System.Security.Cryptography.AsymmetricSignatureFormatter>
- [Passo a passo: criar credenciais de serviço e cliente personalizados](walkthrough-creating-custom-client-and-service-credentials.md)
- [Como: criar um autenticador de token de segurança personalizado](how-to-create-a-custom-security-token-authenticator.md)
- [Como: criar um provedor de token de segurança personalizado](how-to-create-a-custom-security-token-provider.md)
- [Como: criar um token personalizado](how-to-create-a-custom-token.md)
