---
description: 'Saiba mais sobre: exceções de segurança'
title: Exceções de segurança
ms.date: 03/30/2017
ms.assetid: 76d5e5cd-e4f4-404f-9a5a-ec3522494ad8
ms.openlocfilehash: efa3b7e132f3f3fdc8f2cb5b7dc09614ce584fdb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686226"
---
# <a name="security-exceptions"></a>Exceções de segurança

Este tópico lista todas as exceções de segurança.

## <a name="exception-list"></a>Lista de exceções

|Código do recurso|Cadeia de caracteres de recurso|
|-------------------|---------------------|
|AnonymousLogonsAreNotAllowed|O serviço não permite que você faça logon anonimamente.|
|AtLeastOneContractOperationRequestRequiresProtectionLevelNotSupportedByBinding|A mensagem de solicitação deve ser protegida. Isso é exigido por uma operação do contrato especificado. A proteção deve ser fornecida pela associação especificada.|
|AtLeastOneContractOperationResponseRequiresProtectionLevelNotSupportedByBinding|A mensagem de resposta deve ser protegida. Isso é exigido por uma operação do contrato especificado. A proteção deve ser fornecida pela associação especificada.|
|AtMostOnePrimarySignatureInReceiveSecurityHeader|Somente uma assinatura principal é permitida em um cabeçalho de segurança.|
|BadContextTokenFaultReason|O token de contexto de segurança expirou ou não é válido. A mensagem não foi processada.|
|BadEncryptionState|O EncryptedData ou EncryptedKey está em um estado inválido para esta operação.|
|BasicHttpMessageSecurityRequiresCertificate|A associação BasicHttp exige que BasicHttpBinding. Security. Message. ClientCredentialtype seja equivalente ao tipo de credencial BasicHttpMessageCredentialType. Certificate para mensagens seguras. Selecione transporte ou segurança TransportWithMessageCredential para credenciais de nome de usuário.|
|BasicTokenCannotBeWrittenWithoutEncryption|O token básico não pode ser gravado sem criptografia.|
|BindingDoesNotSupportProtectionForRst|A associação especificada para o contrato especificado está configurada com SecureConversation, mas o modo de autenticação não é capaz de fornecer a integridade e a confidencialidade com base em solicitação/resposta necessárias para a negociação.|
|BindingDoesNotSupportWindowsIdenityForImpersonation|A operação de contrato especificada requer a identidade do Windows para representação automática. Uma identidade do Windows que representa o chamador não é fornecida pela associação especificada para o contrato especificado.|
|CachedNegotiationStateQuotaReached|O serviço não pode armazenar em cache o estado de negociação, pois a capacidade especificada foi atingida. Tente novamente a solicitação.|
|CacheQuotaReached|Não é possível adicionar o item. O tamanho máximo do cache é especificado.|
|CannotDetermineSPNBasedOnAddress|O cliente não pode determinar o nome da entidade de serviço com base na identidade no endereço de destino especificado para a finalidade de SspiNegotiation/Kerberos. A identidade do endereço de destino deve ser uma identidade de UPN (como acmedomain \\ \alice) ou a identidade do SPN (como host/bobs-Machine).|
|CannotFindCert|Não é possível localizar o certificado X. 509 usando os critérios de pesquisa especificados: StoreName, StoreLocation, findType, Localizevalue.|
|CannotFindCertForTarget|Não é possível localizar o certificado X. 509 usando os critérios de pesquisa especificados: StoreName, StoreLocation, findType, Localizevalue para o destino especificado.|
|CannotFindCorrelationStateForApplyingSecurity|Não é possível encontrar o estado de correlação para aplicar a segurança a responder no respondente.|
|CannotFindNegotiationState|Não é possível localizar o estado de negociação para o contexto especificado.|
|CannotFindSecuritySession|Não é possível localizar a sessão de segurança com a ID especificada.|
|CannotImportProtectionLevelForContract|A política para importar um processo não pode importar uma associação para o contrato especificado. Os requisitos de proteção para a associação não são compatíveis com uma associação já importada para o contrato. Você deve reconfigurar a associação.|
|CannotImportSupportingTokensForOperationWithoutRequestAction|Falha na importação da política de segurança. A política de segurança contém requisitos de token de suporte no escopo da operação. A descrição do contrato não especifica a ação da mensagem de solicitação associada a esta operação.|
|CannotIssueRstTokenType|Não é possível emitir o token ou o tipo especificado.|
|CannotObtainIssuedTokenKeySize|Não é possível determinar o tamanho da chave do token emitido.|
|CannotPerformImpersonationOnUsernameToken|Não é possível representar a representação usando o token do cliente. A associação especificada para o contrato especificado usa o token de segurança de nome de usuário para autenticação de cliente com um provedor de associação registrado. Use um tipo diferente de token de segurança para o cliente.|
|CannotPerformS4UImpersonationOnPlatform|A associação especificada para o contrato especificado dá suporte à representação somente no Windows Server 2003 e na versão mais recente do Windows. Use a autenticação do SspiNegotiated e uma associação com a conversa segura com o cancelamento habilitado.|
|CannotReadKeyIdentifier|Não é possível ler o identificador Keydo elemento especificado com o namespace especificado.|
|CannotReadToken|Não é possível ler o token do elemento especificado com o namespace especificado para BinarySecretSecurityToken, com um ValueType especificado. Se for esperado que esse elemento seja válido, verifique se a segurança está configurada para consumir tokens com o nome, namespace e tipo de valor especificados.|
|CertificateUnsupportedForHttpTransportCredentialOnly|Não há suporte para autenticação de cliente baseada em certificado no modo de segurança TransportCredentialOnly. Selecione o modo de segurança de transporte.|
|ClaimTypeCannotBeEmpty|O ClaimType não pode ser uma cadeia de caracteres vazia.|
|ClientCertificateNotProvided|O certificado para o cliente não foi fornecido. O certificado pode ser definido em ClientCredentials ou ServiceCredentials.|
|ClientCredentialTypeMustBeSpecifiedForMixedMode|ClientCredentialtype. None não é válido para o modo de segurança TransportWithMessageCredential. Especifique um tipo de credencial ou use um modo de segurança diferente.|
|ConfigurationSchemaInsuffientForSecurityBindingElementInstance|O esquema de configuração é insuficiente para descrever a configuração não padrão do seguinte elemento de associação de segurança:|
|DerivedKeyTokenGenerationAndLengthTooHigh|A geração e o comprimento especificados da chave derivada resultam em um deslocamento de derivação de chave maior que o deslocamento máximo permitido.|
|DnsIdentityCheckFailedForIncomingMessage|A verificação de identidade falhou para a mensagem de entrada. A identidade esperada do DNS (sistema de nomes de domínio) do ponto de extremidade remoto foi especificada. O ponto de extremidade remoto forneceu a declaração de DNS (sistema de nomes de domínio) especificada. Se esse for um ponto de extremidade remoto legítimo, você poderá corrigir o problema especificando a identidade do sistema de nome de domínio como a propriedade Identity de EndpointAddress ao criar o proxy de canal.|
|DnsIdentityCheckFailedForOutgoingMessage|A verificação de identidade falhou para a mensagem que estava saindo. O ponto de extremidade remoto deve ter a identidade do sistema de nome de domínio especificada. O ponto de extremidade remoto forneceu a declaração de DNS (sistema de nomes de domínio). Se esse for um ponto de extremidade remoto legítimo, você poderá corrigir o problema especificando explicitamente a identidade DNS como a propriedade Identity de EndpointAddress ao criar o proxy de canal.|
|DuplicateIdInMessageToBeVerified|A ID especificada ocorreu duas vezes na mensagem que é fornecida para verificação.|
|EmptyBase64Attribute|Um valor vazio foi encontrado para o nome e o namespace do atributo base 64 obrigatório.|
|ExportOfBindingWithAsymmetricAndTransportSecurityNotSupported|Falha na exportação da política de segurança. A associação contém um AsymmetricSecurityBindingElement e um elemento de associação de transporte seguro. Não há suporte para a exportação de política para tal associação.|
|ExportOfBindingWithSymmetricAndTransportSecurityNotSupported|Falha na exportação da política de segurança. A associação contém um SymmetricSecurityBindingElement e um elemento de associação de transporte seguro. Não há suporte para a exportação de política para tal associação.|
|ExportOfBindingWithTransportSecurityBindingElementAndNoTransportSecurityNotSupported|Falha na exportação da política de segurança. A associação contém um TransportSecurityBindingElement, mas nenhum elemento de associação de transporte que implementa ITransportTokenAssertionProvider. Não há suporte para a exportação de política para tal associação. Verifique se o elemento de associação de transporte na associação implementa a interface ITransportTokenAssertionProvider.|
|FoundMultipleCerts|Foram encontrados vários certificados X. 509 usando os critérios de pesquisa especificados: StoreName, StoreLocation, findType e findValue. Forneça um valor de localização mais específico.|
|FoundMultipleCertsForTarget|Foram encontrados vários certificados X. 509 usando os critérios de pesquisa especificados: StoreName, StoreLocation, findType, Localizevalue para o destino especificado. Forneça um valor de localização mais específico.|
|HeaderDecryptionNotSupportedInWsSecurityJan2004|SecurityVersion. WSSecurityJan2004 não dá suporte à descriptografia de cabeçalho. Use SecurityVersion. WsSecurityXXX2005 e superior ou use a segurança de transporte para criptografar a mensagem completa.|
|IdentityCheckFailedForIncomingMessage|A verificação de identidade falhou para a mensagem de entrada. A identidade esperada é especificada para o ponto de extremidade de destino.|
|IdentityCheckFailedForOutgoingMessage|A verificação de identidade falhou para a mensagem de saída. A identidade esperada é especificada para o ponto de extremidade de destino.|
|IncorrectSpnOrUpnSpecified|Falha na autenticação da interface de provedor de suporte de segurança (SSPI). O servidor pode não estar sendo executado em uma conta com a identidade especificada. Se o servidor estiver sendo executado em uma conta de serviço (serviço de rede, por exemplo), especifique o servicePrincipalName da conta como a identidade no EndpointAddress para o servidor. Se o servidor estiver sendo executado em uma conta de usuário, especifique o UserPrincipalName da conta como a identidade no EndpointAddress para o servidor.|
|InvalidAttributeInSignedHeader|O cabeçalho assinado especificado contém o atributo especificado. O atributo esperado foi especificado.|
|InvalidCloseResponseAction|Uma resposta de fechamento de sessão de segurança foi recebida com a ação inválida especificada.|
|InvalidQName|O QName é inválido.|
|InvalidRenewResponseAction|Uma resposta de renovação de sessão de segurança foi recebida com a ação inválida especificada.|
|InvalidSspiNegotiation|Falha na negociação da interface do provedor de suporte de segurança.|
|IssuerBindingNotPresentInTokenRequirement|O Gerenciador de token de segurança requer que o elemento de associação de segurança de Bootstrap seja especificado no requisito de token que descreve a conversa segura. O requisito de token é especificado da seguinte maneira.|
|KeyLengthMustBeMultipleOfEight|O comprimento de chave especificado não é um múltiplo de 8 para chaves simétricas.|
|LsaAuthorityNotContacted|Erro interno de SSL (consulte o código de status do Win32 para obter detalhes). Verifique o certificado do servidor para determinar se ele é capaz de trocar de chave.|
|MaximumPolicyRedirectionsExceeded|O limite de busca de política recursiva foi atingido. Verifique para determinar se há um loop na cadeia de serviços de Federação.|
|MessagePartSpecificationMustBeImmutable|A especificação de parte da mensagem deve se tornar constante antes de ser definida.|
|MissingCustomCertificateValidator|X509CertificateValidationMode. Custom requer CustomCertificateValidator. Especifique a propriedade CustomCertificateValidator.|
|MissingCustomUserNamePasswordValidator|UserNamePasswordValidationMode. Custom requer CustomUserNamePasswordValidator. Especifique a propriedade CustomUserNamePasswordValidator.|
|MissingMembershipProvider|UserNamePasswordValidationMode. MembershipProvider requer MembershipProvider. Especifique a Propriedade MembershipProvider.|
|NoBinaryNegoToSend|Nenhuma negociação binária foi enviada para a outra entidade.|
|NoEncryptionPartsSpecified|Nenhuma parte de mensagem de criptografia foi especificada para mensagens com a ação especificada.|
|NoKeyInfoInEncryptedItemToFindDecryptingToken|O valor de KeyInfo não foi encontrado no item criptografado para localizar o token de descriptografia.|
|NonceLengthTooShort|O nonce especificado é muito curto. O comprimento mínimo necessário de nonce é de 4 bytes.|
|NoOutgoingEndpointAddressAvailableForDoingIdentityCheck|Nenhum EndpointAddress de saída está disponível para verificar a identidade em uma mensagem a ser enviada.|
|NoOutgoingEndpointAddressAvailableForDoingIdentityCheckOnReply|Não há EndpointAddress de saída disponível para verificar a identidade em uma resposta recebida.|
|NoPartsOfMessageMatchedPartsToSign|Nenhuma assinatura foi criada porque nenhuma parte da mensagem correspondeu à especificação de parte da mensagem fornecida.|
|NoPrincipalSpecifiedInAuthorizationContext|Nenhuma entidade de segurança personalizada foi especificada no contexto de autorização.|
|NoSignatureAvailableInSecurityHeaderToDoReplayDetection|Nenhuma assinatura está disponível no cabeçalho de segurança para fornecer o nonce para detecção de reprodução.|
|NoSignaturePartsSpecified|Nenhuma parte de mensagem de assinatura foi especificada para mensagens com a ação especificada.|
|NoSigningTokenAvailableToDoIncomingIdentityCheck|Nenhum token de assinatura está disponível para fazer uma verificação de identidade de entrada.|
|NoTimestampAvailableInSecurityHeaderToDoReplayDetection|Nenhum carimbo de data/hora está disponível no cabeçalho de segurança para fazer a detecção de repetição.|
|NoTransportTokenAssertionProvided|Falha no especialista da política de segurança. A declaração de token de transporte fornecida do tipo especificado não criou uma asserção de token de transporte para incluir a declaração de política de segurança SP: TransportBinding.|
|OnlyOneOfEncryptedKeyOrSymmetricBindingCanBeSelected|O protocolo de segurança simétrica pode ser configurado com um provedor de token simétrico e um autenticador de token simétrico ou um provedor de token assimétrico. Ele não pode ser configurado com ambos.|
|OperationCannotBeDoneOnReceiverSideSecurityHeaders|Esta operação não pode ser feita nos cabeçalhos de segurança do receptor.|
|OperationDoesNotAllowImpersonation|A operação de serviço especificada que pertence ao contrato com o nome especificado e o namespace não permite a representação.|
|PolicyRequiresConfidentialityWithoutIntegrity|A política de segurança de mensagem para a ação especificada requer confidencialidade sem integridade. Não há suporte para confidencialidade sem integridade.|
|PrimarySignatureIsRequiredToBeEncrypted|A assinatura principal deve ser criptografada.|
|PropertySettingErrorOnProtocolFactory|A propriedade necessária no alocador de protocolo de segurança especificado não está definida ou tem um valor inválido.|
|ProtocolFactoryCouldNotCreateProtocol|A fábrica de protocolos não pode criar um protocolo.|
|PublicKeyNotRSA|A chave pública não é uma chave RSA.|
|RequiredMessagePartNotEncrypted|A parte da mensagem necessária especificada não foi criptografada.|
|RequiredMessagePartNotEncryptedNs|A parte da mensagem necessária especificada não foi criptografada.|
|RequiredMessagePartNotSigned|A parte da mensagem necessária especificada não foi assinada.|
|RequiredMessagePartNotSignedNs|A parte da mensagem necessária especificada não foi assinada.|
|RequiredSecurityHeaderElementNotSigned|O elemento de cabeçalho de segurança especificado com a ID especificada deve ser assinado.|
|RequiredSecurityTokenNotEncrypted|O ' token de segurança ' especificado com o modo de anexo especificado deve ser criptografado.|
|RequiredSecurityTokenNotSigned|O token de segurança especificado com o modo de anexo especificado deve ser assinado.|
|RequiredSignatureMissing|A assinatura deve estar no cabeçalho de segurança.|
|RequireNonCookieMode|A associação especificada com o namespace especificado está configurada para emitir tokens de contexto de segurança de cookie. O COM+ Integration Services não oferece suporte a tokens de contexto de segurança de cookie.|
|RevertingPrivilegeFailed|Falha na operação de reversão com a exceção especificada.|
|RSTRAuthenticatorIncorrect|O CombinedHash de RequestSecurityTokenResponse está incorreto.|
|SecureConversationCancelNotAllowedFaultReason|Um cancelamento de conversa segura não é permitido pela associação.|
|SecureConversationDriverVersionDoesNotSupportSession|A versão configurada de SecureConversation não oferece suporte a sessões. Use WSSecureConversationFeb2005 ou superior.|
|SecureConversationRequiredByReliableSession|Não é possível estabelecer uma sessão confiável sem conversa segura. Habilite a conversa segura.|
|SecurityAuditFailToLoadDll|Falha ao carregar a biblioteca de vínculo dinâmico (DLL) especificada.|
|SecurityAuditNotSupportedOnChannelFactory|Não há suporte para SecurityAuditBehavior na fábrica de canais.|
|SecurityAuditPlatformNotSupported|Não há suporte para a gravação de mensagens de auditoria no log de segurança na plataforma atual. Você deve gravar mensagens de auditoria no log do aplicativo.|
|SecurityBindingElementCannotBeExpressedInConfig|Uma política de segurança foi importada para o ponto de extremidade. A política de segurança contém requisitos que não podem ser representados em uma configuração de Windows Communication Foundation. Procure um comentário sobre os parâmetros SecurityBindingElement que são necessários no arquivo de configuração que foi gerado. Crie o elemento de ligação correto com o código. A configuração de associação que está no arquivo de configuração não é segura.|
|SecurityBindingSupportsOneWayOnly|A Securitybinding para a associação especificada para o contrato especificado só dá suporte à operação OneWay.|
|SecurityContextDoesNotAllowImpersonation|Não é possível iniciar a representação porque o SecurityContext para a função UltimateReceiver da mensagem de solicitação com a ação especificada não está mapeada para uma identidade do Windows.|
|SecurityListenerClosing|O ouvinte não está aceitando novas conversas seguras porque está fechando.|
|SecurityListenerClosingFaultReason|O servidor não está aceitando novas conversas seguras no momento porque está fechando. Tente novamente mais tarde.|
|SecurityProtocolFactoryShouldBeSetBeforeThisOperation|A fábrica de protocolo de segurança deve ser definida antes que esta operação seja executada.|
|SecuritySessionAbortedFaultReason|A sessão de segurança foi encerrada. Isso pode ser porque nenhuma mensagem foi recebida na sessão por muito tempo.|
|SecuritySessionKeyIsStale|A chave de sessão deve ser renovada para que possa proteger as mensagens do aplicativo.|
|SecuritySessionLimitReached|Não é possível criar uma sessão de segurança. Tente novamente mais tarde.|
|SecuritySessionNotPending|Nenhuma sessão de segurança com a ID especificada está pendente.|
|SecurityTokenParametersHasIncompatibleInclusionMode|A associação especificada está configurada com um parâmetro de token de segurança que tem o modo de inclusão de token de segurança incompatível especificado. Especifique um modo de inclusão de token de segurança alternativo.|
|SecurityVersionDoesNotSupportEncryptedKeyBinding|A associação especificada para o contrato especificado foi configurada com uma versão de segurança incompatível que não oferece suporte a referências não anexadas a EncryptedKeys. Use o valor especificado ou superior como a versão de segurança para a associação.|
|SecurityVersionDoesNotSupportSignatureConfirmation|O SecurityVersion especificado não oferece suporte à confirmação de assinatura. Use um SecurityVersion posterior.|
|SecurityVersionDoesNotSupportThumbprintX509KeyIdentifierClause|A associação especificada para o contrato especificado está configurada com uma versão de segurança que não oferece suporte a referências externas a tokens X. 509 usando o valor de impressão digital do certificado. Use o valor especificado ou superior como a versão de segurança para a associação.|
|SenderSideSupportingTokensMustSpecifySecurityTokenParameters|Os parâmetros de token de segurança devem ser especificados com tokens de suporte para cada mensagem.|
|ServerCertificateNotProvided|O destinatário não forneceu seu certificado. Esse certificado é exigido pelo protocolo TLS. Ambas as partes devem ter acesso aos seus certificados.|
|SignatureConfirmationNotSupported|O SecurityVersion configurado não oferece suporte à confirmação de assinatura. Use WSSecurityXXX2005 ou superior.|
|SignatureConfirmationRequiresRequestReply|A fábrica de protocolos deve dar suporte à segurança de solicitação/resposta para oferecer confirmação de assinatura.|
|SignatureNotExpected|Uma assinatura não é esperada para esta mensagem.|
|SigningTokenHasNoKeys|O token de assinatura especificado não tem chaves. O token de segurança é usado em um contexto que exige que ele execute operações criptográficas, mas o token não contém chaves criptográficas. O tipo de token não oferece suporte a operações criptográficas ou a instância de token específica não contém chaves criptográficas. Verifique sua configuração para garantir que os tipos de token desabilitados criptograficamente (por exemplo, UserNameSecurityToken) não sejam especificados em um contexto que exija operações criptográficas (por exemplo, um token de suporte de endosso).|
|SpnegoImpersonationLevelCannotBeSetToNone|A interface do provedor de suporte de segurança não oferece suporte ao nível de representação ' none '. Especifique o nível de identificação, representação ou delegação.|
|SslClientCertMustHavePrivateKey|O certificado especificado deve ter uma chave privada. O processo deve ter direitos de acesso para a chave privada.|
|SslServerCertMustDoKeyExchange|O certificado especificado deve ter uma chave privada capaz de troca de chaves. O processo deve ter direitos de acesso para a chave privada.|
|StandardsManagerCannotWriteObject|O serializador de token não pode serializar o objeto especificado.  Se esse for um tipo personalizado, você deverá fornecer um serializador personalizado.|
|TimeStampHasCreationAheadOfExpiry|O carimbo de data/hora de segurança é inválido porque sua hora de criação é maior ou igual à sua hora de expiração.|
|TimeStampHasCreationTimeInFuture|O carimbo de data/hora de segurança é inválido porque sua hora de criação está no futuro. A hora atual é especificada e a distorção de relógio permitida é especificada.|
|TimeStampHasExpiryTimeInPast|O carimbo de data/hora de segurança está obsoleto porque seu tempo de expiração está no passado. A hora atual é especificada e a distorção de relógio permitida é especificada.|
|TimeStampWasCreatedTooLongAgo|O carimbo de data/hora de segurança está obsoleto porque seu tempo de criação está muito distante no passado. Hora atual, tempo de vida máximo de carimbo de data/hora e distorção de relógio permitido são especificados.|
|TokenProviderCannotGetTokensForTarget|O provedor de token não pode obter tokens para o destino especificado.|
|TooManyIssuedSecurityTokenParameters|Um trecho da cadeia de segurança federada contém vários IssuedSecurityTokenParameters. O sistema InfoCard só dá suporte a um IssuedSecurityTokenParameters para cada segmento.|
|TransportDoesNotProtectMessage|A associação especificada para o contrato especificado é configurada com um modo de autenticação que requer a integridade e a confidencialidade do nível de transporte. No entanto, o transporte não pode fornecer integridade e confidencialidade.|
|TrustApr2004DoesNotSupportCertainIssuedTokens|WSTrustApr2004 não dá suporte à emissão de certificados X. 509 ou EncryptedKeys. Use WsTrustFeb2005 ou superior.|
|TrustDriverVersionDoesNotSupportSession|A versão de confiança configurada não oferece suporte a sessões. Use WSTrustFeb2005 ou superior.|
|UnableToCreateICryptoFromTokenForSignatureVerification|Não é possível criar uma interface ICrypto a partir do token especificado para verificação de assinatura.|
|UnableToCreateSymmetricAlgorithmFromToken|Não é possível criar o algoritmo simétrico especificado a partir do token.|
|UnableToDeriveKeyFromKeyInfoClause|A cláusula KeyInfo especificada foi resolvida para o token especificado, que não contém uma chave simétrica que pode ser usada para derivação.|
|UnableToFindTokenAuthenticator|Não é possível encontrar um autenticador de token para o tipo de token especificado. Tokens desse tipo não podem ser aceitos de acordo com as configurações de segurança atuais.|
|UnableToLoadCertificateIdentity|Não é possível carregar a identidade do certificado X. 509 especificada na configuração.|
|UnexpectedEmptyElementExpectingClaim|O elemento especificado do namespace especificado está vazio e não especifica uma declaração de identidade válida.|
|UnknownEncodingInBinarySecurityToken|Codificação não reconhecida ao ler o token de segurança binário.|
|UnsecuredMessageFaultReceived|Uma falha não segura ou protegida incorretamente foi recebida da outra entidade. Consulte a FaultException interna para obter o código de falha e detalhes.|
|UnsupportedPasswordType|O token de nome de usuário especificado tem um tipo de senha sem suporte.|
|UnsupportedSecureConversationBootstrapProtectionRequirements|Não é possível importar a política de segurança. Não há suporte para os requisitos de proteção para a associação de inicialização de conversa segura. Os requisitos de proteção para a inicialização de conversa segura devem exigir que a solicitação e a resposta sejam assinadas e criptografadas.|
|UnsupportedSecurityPolicyAssertion|Uma declaração de política de segurança sem suporte foi detectada durante a importação da política de segurança especificada.|
