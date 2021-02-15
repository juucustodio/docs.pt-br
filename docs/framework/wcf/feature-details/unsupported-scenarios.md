---
description: 'Saiba mais sobre: cenários sem suporte'
title: Cenários sem suporte
ms.date: 03/30/2017
ms.assetid: 72027d0f-146d-40c5-9d72-e94392c8bb40
ms.openlocfilehash: 7547a1acc060a6611a4750e512501cd314bed702
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99726748"
---
# <a name="unsupported-scenarios"></a>Cenários sem suporte

Por vários motivos, Windows Communication Foundation (WCF) não oferece suporte a alguns cenários de segurança específicos. Por exemplo, o Windows XP Home Edition não implementa os protocolos de autenticação SSPI ou Kerberos e, portanto, o WCF não dá suporte à execução de um serviço com a autenticação do Windows nessa plataforma. Há suporte para outros mecanismos de autenticação, como nome de usuário/senha e autenticação integrada de HTTP/HTTPS ao executar o WCF no Windows XP Home Edition.

## <a name="impersonation-scenarios"></a>Cenários de representação

### <a name="impersonated-identity-might-not-flow-when-clients-make-asynchronous-calls"></a>A identidade representada pode não fluir quando os clientes fizerem chamadas assíncronas

 Quando um cliente WCF faz chamadas assíncronas para um serviço WCF usando a autenticação do Windows em representação, a autenticação pode ocorrer com a identidade do processo do cliente em vez da identidade representada.

### <a name="windows-xp-and-secure-context-token-cookie-enabled"></a>Windows XP e cookie de token de contexto seguro habilitado

O WCF não oferece suporte à representação e um <xref:System.InvalidOperationException> é gerado quando existem as seguintes condições:

- O sistema operacional é o Windows XP.

- O modo de autenticação resulta em uma identidade do Windows.

- A propriedade <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> do <xref:System.ServiceModel.OperationBehaviorAttribute> é definida como <xref:System.ServiceModel.ImpersonationOption.Required>.

- Um identificador de contexto de segurança (SCT) baseado em estado é criado (por padrão, a criação é desabilitada).

 O SCT baseado em estado só pode ser criado usando uma associação personalizada. Para obter mais informações, consulte [como: criar um token de contexto de segurança para uma sessão segura](how-to-create-a-security-context-token-for-a-secure-session.md).) No código, o token é habilitado pela criação de um elemento de associação de segurança ( <xref:System.ServiceModel.Channels.SymmetricSecurityBindingElement> ou <xref:System.ServiceModel.Channels.AsymmetricSecurityBindingElement> ) usando o <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSspiNegotiationBindingElement%28System.Boolean%29?displayProperty=nameWithType> <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateSecureConversationBindingElement%28System.ServiceModel.Channels.SecurityBindingElement%2CSystem.Boolean%29?displayProperty=nameWithType> método ou e definindo o `requireCancellation` parâmetro como `false` . O parâmetro refere-se ao cache do SCT. Definir o valor como `false` habilita o recurso SCT baseado em estado.

 Como alternativa, em configuração, o token é habilitado criando um <`customBinding`>, depois adicionando um <`security` elemento> e definindo o `authenticationMode` atributo como SecureConversation e o `requireSecurityContextCancellation` atributo como `true` .

> [!NOTE]
> Os requisitos anteriores são específicos. Por exemplo, o <xref:System.ServiceModel.Channels.SecurityBindingElement.CreateKerberosBindingElement%2A> cria um elemento de associação que resulta em uma identidade do Windows, mas não estabelece um SCT. Portanto, você pode usá-lo com a `Required` opção no Windows XP.

### <a name="possible-aspnet-conflict"></a>Possível conflito de ASP.NET

O WCF e o ASP.NET podem habilitar ou desabilitar a representação. Quando o ASP.NET hospeda um aplicativo WCF, pode haver um conflito entre as definições de configuração do WCF e do ASP.NET. Em caso de conflito, a configuração do WCF tem precedência, a menos que a <xref:System.ServiceModel.OperationBehaviorAttribute.Impersonation%2A> propriedade seja definida como <xref:System.ServiceModel.ImpersonationOption.NotAllowed> ; nesse caso, a configuração de representação ASP.net tem precedência.

### <a name="assembly-loads-may-fail-under-impersonation"></a>Cargas de assembly podem falhar em representação

Se o contexto representado não tiver direitos de acesso para carregar um assembly e se for a primeira vez que o Common Language Runtime (CLR) está tentando carregar o assembly para esse AppDomain, o <xref:System.AppDomain> armazenará em cache a falha. As tentativas subsequentes de carregar esse assembly (ou assemblies) falham, mesmo após a reversão da representação, e mesmo se o contexto revertido tiver direitos de acesso para carregar o assembly. Isso ocorre porque o CLR não tenta novamente a carga depois que o contexto do usuário é alterado. Você deve reiniciar o domínio do aplicativo para se recuperar da falha.

> [!NOTE]
> O valor padrão para a <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> propriedade da <xref:System.ServiceModel.Security.WindowsClientCredential> classe é <xref:System.Security.Principal.TokenImpersonationLevel.Identification> . Na maioria dos casos, um contexto de representação no nível de identificação não tem direitos para carregar nenhum assembly adicional. Esse é o valor padrão, portanto, essa é uma condição muito comum a ser observada. A representação de nível de identificação também ocorre quando o processo de representação não tem o `SeImpersonate` privilégio. Para obter mais informações, consulte [delegação e representação](delegation-and-impersonation-with-wcf.md).

### <a name="delegation-requires-credential-negotiation"></a>A delegação requer negociação de credencial

Para usar o protocolo de autenticação Kerberos com a delegação, você deve implementar o protocolo Kerberos com a negociação de credencial (às vezes chamada de Kerberos de várias etapas ou vários lados). Se você implementar a autenticação Kerberos sem negociação de credencial (às vezes chamada de Kerberos de uma foto ou de um único segmento), uma exceção será lançada. Para obter mais informações sobre como implementar a negociação de credenciais, consulte [Depurando erros de autenticação do Windows](debugging-windows-authentication-errors.md).

## <a name="cryptography"></a>Criptografia

### <a name="sha-256-supported-only-for-symmetric-key-usages"></a>SHA-256 com suporte apenas para usos de chave simétrica

O WCF dá suporte a uma variedade de algoritmos de criação de Resumo de assinatura e criptografia que você pode especificar usando o conjunto de algoritmos nas associações fornecidas pelo sistema. Para maior segurança, o WCF dá suporte a algoritmos de SHA (algoritmo de hash seguro) 2, especificamente SHA-256, para criar hashes de Resumo de assinatura. Esta versão oferece suporte a SHA-256 somente para usos de chave simétrica, como chaves Kerberos, e onde um certificado X. 509 não é usado para assinar a mensagem. O WCF não oferece suporte a assinaturas RSA (usadas em certificados X. 509) usando o hash SHA-256 devido à falta de suporte atual para RSA-SHA256 no WinFX.

### <a name="fips-compliant-sha-256-hashes-not-supported"></a>Não há suporte para hashes SHA-256 em conformidade com FIPS

O WCF não dá suporte a hashes em conformidade com o SHA-256, portanto, os conjuntos de algoritmos que usam SHA-256 não têm suporte do WCF em sistemas em que o uso de algoritmos compatíveis com FIPS é necessário.

### <a name="fips-compliant-algorithms-may-fail-if-registry-is-edited"></a>Algoritmos em conformidade com FIPS podem falhar se o registro for editado

Você pode habilitar e desabilitar algoritmos em conformidade com FIPS (Federal Information Processing Standards) usando o snap-in do MMC (console de gerenciamento Microsoft) de configurações de segurança local. Você também pode acessar a configuração no registro. No entanto, observe que o WCF não dá suporte ao uso do registro para redefinir a configuração. Se o valor for definido como algo diferente de 1 ou 0, poderão ocorrer resultados inconsistentes entre o CLR e o sistema operacional.

### <a name="fips-compliant-aes-encryption-limitation"></a>Limitação de criptografia AES em conformidade com FIPS

A criptografia AES em conformidade com FIPS não funciona em retornos de chamada duplex na representação do nível de identificação.

### <a name="cngksp-certificates"></a>Certificados CNG/KSP

*CRYPTOGRAPHY API: CNG (próxima geração)* é a substituição de longo prazo para o CryptoAPI. Essa API está disponível em código não gerenciado no Windows Vista, no Windows Server 2008 e em versões posteriores do Windows.

 .NET Framework 4.6.1 e versões anteriores não dão suporte a esses certificados porque usam o CryptoAPI herdado para manipular certificados CNG/KSP. O uso desses certificados com .NET Framework 4.6.1 e versões anteriores causará uma exceção.

 Há duas maneiras possíveis de saber se um certificado usa KSP:

- Faça um `p/invoke` de `CertGetCertificateContextProperty` e inspecione `dwProvType` no retornado `CertGetCertificateContextProperty` .

- Use o  `certutil` comando da linha de comando para consultar certificados. Para obter mais informações, consulte [tarefas de certutil para solucionar problemas de certificados](/previous-versions/orphan-topics/ws.10/cc772619(v=ws.10)).

## <a name="message-security-fails-if-using-aspnet-impersonation-and-aspnet-compatibility-is-required"></a>A segurança da mensagem falhará se estiver usando a representação de ASP.NET e a compatibilidade do ASP.NET for necessária

O WCF não oferece suporte à seguinte combinação de configurações porque pode impedir que a autenticação do cliente ocorra:

- A representação ASP.NET está habilitada. Isso é feito no arquivo de Web.config definindo o `impersonate` atributo do elemento de> de <`identity` como `true` .

- O modo de compatibilidade ASP.NET é habilitado definindo o `aspNetCompatibilityEnabled` atributo de [\<serviceHostingEnvironment>](../../configure-apps/file-schema/wcf/servicehostingenvironment.md) para `true` .

- A segurança do modo de mensagem é usada.

A solução alternativa é desativar o modo de compatibilidade ASP.NET. Ou, se o modo de compatibilidade ASP.NET for necessário, desabilite o recurso de representação ASP.NET e use a representação fornecida pelo WCF. Para obter mais informações, consulte [delegação e representação](delegation-and-impersonation-with-wcf.md).

## <a name="ipv6-literal-address-failure"></a>Falha de endereço literal IPv6

As solicitações de segurança falham quando o cliente e o serviço estão no mesmo computador e os endereços IPv6 literais são usados para o serviço.

 Os endereços IPv6 literais funcionam se o serviço e o cliente estiverem em computadores diferentes.

## <a name="wsdl-retrieval-failures-with-federated-trust"></a>Falhas de recuperação de WSDL com confiança federada

O WCF requer exatamente um documento WSDL para cada nó na cadeia de confiança federada. Tenha cuidado para não configurar um loop ao especificar pontos de extremidade. Uma maneira na qual os loops podem surgir é usar um download WSDL de cadeias de confiança federada com dois ou mais links no mesmo documento WSDL. Um cenário comum que pode produzir esse problema é um serviço federado em que o servidor de token de segurança e o serviço estão contidos no mesmo ServiceHost.

 Um exemplo dessa situação é um serviço com os três seguintes endereços de ponto de extremidade:

- `http://localhost/CalculatorService/service` (o serviço)

- `http://localhost/CalculatorService/issue_ticket` (o STS)

- `http://localhost/CalculatorService/mex` (o ponto de extremidade de metadados)

 Isso gera uma exceção.

 Você pode fazer com que esse cenário funcione colocando o `issue_ticket` ponto de extremidade em outro lugar.

## <a name="wsdl-import-attributes-can-be-lost"></a>Atributos de importação de WSDL podem ser perdidos

O WCF perde o controle dos atributos em um `<wst:Claims>` elemento em um `RST` modelo ao fazer uma importação de WSDL. Isso acontece durante uma importação de WSDL, se você especificar `<Claims>` diretamente em `WSFederationHttpBinding.Security.Message.TokenRequestParameters` ou `IssuedSecurityTokenRequestParameters.AdditionalRequestParameters` em vez de usar as coleções de tipo de declaração diretamente.  Como a importação perde os atributos, a associação não Arredonda a viagem corretamente por meio do WSDL e, portanto, está incorreta no lado do cliente.

 A correção é modificar a associação diretamente no cliente depois de fazer a importação.

## <a name="see-also"></a>Consulte também

- [Considerações sobre segurança](security-considerations-in-wcf.md)
- [Divulgação de Informações Confidenciais](information-disclosure.md)
- [Elevação de Privilégio](elevation-of-privilege.md)
- [Negação de Serviço](denial-of-service.md)
- [Adulteração](tampering.md)
- [Ataques por repetição](replay-attacks.md)
