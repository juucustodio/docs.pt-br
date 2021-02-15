---
description: 'Saiba mais sobre: exceções IdentityModel'
title: Exceções de IdentityModel
ms.date: 03/30/2017
ms.assetid: 4ef34497-8ff5-4621-b773-7731cc721231
ms.openlocfilehash: 902403d5809bd75a3b370e9b435dbefce2e97d3c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686421"
---
# <a name="identitymodel-exceptions"></a>Exceções de IdentityModel

Este tópico lista todas as exceções geradas por IdentityModel.  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres atual|  
|-------------------|--------------------|  
|ValueMustBeOf2Types|O valor desse argumento deve ser um desses dois tipos.|  
|SAMLSubjectNameIdentifierRequiresNameValue|O ' name ' especificado para um SamlNameIdentifier não pode ser nulo nem ter comprimento 0.|  
|TraceCodeIssuanceTokenProviderEndSecurityNegotiation|O IssuanceTokenProvider concluiu a negociação de segurança.|  
|TraceCodeSecurityNewServerSessionKeyIssued|Uma nova chave de sessão de segurança foi emitida pelo servidor.|  
|SAMLAttributeMissingNameAttributeOnRead|O ' name ' do SamlAttribute que está sendo lido está ausente ou tem comprimento 0.|  
|UnknownICryptoType|Não há suporte para a implementação de ICrypto.|  
|TraceCodeSecurityTokenProviderClosed|O provedor de token de segurança foi fechado.|  
|SAMLUnableToLoadAdvice|Falha ao carregar o \<saml:advice> elemento.|  
|SAMLAuthenticationStatementMissingAuthenticationMethodOnRead|O atributo ' AuthenticationMethod ' que está sendo lido para um SamlAuthenticationStatement está ausente ou tem comprimento 0.|  
|UnsupportedTransformAlgorithm|Algoritmo de transformação ou canonização sem suporte.|  
|SAMLAudienceRestrictionShouldHaveOneAudience|Um SamlAudienceRestrictionCondition deve conter pelo menos um público (URI).|  
|SAMLEvidenceShouldHaveOneAssertion|SamlEvidence deve referenciar pelo menos um SamlAssertion por ID ou referência.|  
|SAMLAudienceRestrictionInvalidAudienceValueOnRead|O SamlAudienceRestrictionCondition que está sendo lido está faltando um valor no elemento ' Audience '.|  
|X509ChainBuildFail|Falha na criação da cadeia de certificados X. 509 específica. O certificado que foi usado tem uma cadeia de confiança que não pode ser verificada. Substitua o certificado ou altere o certificateValidationMode.|  
|XDCannotFindValueInDictionaryString|A ID do valor específico não foi encontrada na cadeia de caracteres do dicionário.|  
|TraceCodeImportSecurityChannelBindingEntry|Iniciando ImportChannelBinding de segurança.|  
|PrivateKeyExchangeNotSupported|A chave privada não oferece suporte à KeySpec do Exchange.|  
|TokenProviderUnableToGetToken|O provedor de token específico não pôde fornecer um token de segurança.|  
|SAMLEntityCannotBeNullOrEmpty|A entidade SamlAssertion específica não pode ser nula ou vazia.|  
|SAMLAssertionRequireOneStatement|Um SamlAssertion requer pelo menos uma instrução. Certifique-se de ter adicionado pelo menos um SamlStatement à SamlAssertion que você está criando.|  
|AESInvalidInputBlockSize|O tamanho de entrada deve ser um múltiplo de bytes específicos.|  
|AESCryptAcquireContextFailed|Falha ao adquirir o contexto do CSP.|  
|SAMLAssertionRequireOneStatementOnRead|O SamlAssertion que está sendo lido não continha nenhum SamlStatement. Um SamlAssertion deve conter pelo menos um SamlStatement.|  
|TraceCodeSecuritySessionClosedFaultReceived|A sessão do Client Security recebeu uma falha de sessão fechada do servidor.|  
|TraceCodeIssuanceTokenProviderRedirectApplied|O IssuanceTokenProvider aplicou um cabeçalho de redirecionamento.|  
|TraceCodeSecuritySessionClosedFaultSendFailure|Ocorreu uma falha ao enviar uma falha de sessão de segurança fechada ao cliente.|  
|ValueMustBeZero|O valor desse argumento deve ser 0.|  
|SAMLUnableToResolveSignatureKey|Não é possível resolver o SecurityKeyIdentifier encontrado na assinatura de SamlAssertion. A assinatura de SamlAssertion não pode ser validada para o emissor específico.|  
|X509IsNotInTrustedStore|O certificado X. 509 específico não está no repositório de pessoas confiáveis.|  
|SAMLElementNotRecognized|Não há suporte para o elemento específico.|  
|SAMLAuthorizationDecisionStatementMissingResourceAttributeOnRead|O atributo ' Resource ' para o SamlAuthorizationDecisionStatement que está sendo lido está ausente ou tem comprimento 0.|  
|SamlTokenMissingSignature|O SamlAssertion não está assinado. Os SamlAssertions podem ser assinados Configurando o SigningCredentials.|  
|ExpectedElementMissing|O elemento esperado com o namespace específico está ausente.|  
|NoKeyIdentifierClauseFound|Nenhuma cláusula do tipo específico foi encontrada no SecurityKeyIdentifier.|  
|MissingPrivateKey|A chave privada não está presente no certificado X. 509.|  
|UnexpectedEOFFromReader|EOF inesperado do leitor de XML.|  
|UnsupportedKeyDerivationAlgorithm|Não há suporte para o algoritmo de derivação de chave específico.|  
|TokenDoesNotSupportKeyIdentifierClauseCreation|O token específico não oferece suporte à criação de cláusula de identificador de chave específica.|  
|LastMessageNumberExceeded|Foi detectada uma violação do protocolo de número de sequência.|  
|SymmetricKeyLengthTooShort|O comprimento da chave simétrica especificada é muito curto.|  
|SAMLAuthorityBindingMissingAuthorityKindOnRead|O SamlAuthorityBinding que está sendo lido foi encontrado para conter um ' AuthorityKind ' que estava faltando ou tem comprimento 0.  Isso não é permitido.|  
|XmlTokenBufferIsEmpty|XmlTokenBuffer está vazio.|  
|InvalidXmlQualifiedName|Um nome qualificado de XML era esperado, mas um nome inválido foi encontrado.|  
|SAMLAuthorityKindMissingName|O XmlQualifiedName que representa o ' AuthorityKind ' em SamlAuthorityBinding não pode ser nulo nem ter comprimento 0.|  
|AESCryptEncryptFailed|Falha ao criptografar os dados específicos.|  
|AuthorizationContextCreated|O contexto de autorização com a ID específica é criado.|  
|SamlSerializerUnableToReadSecurityKeyIdentifier|O SamlSerializer não contém um SecurityTokenSerializer capaz de ler o SecurityKeyIdentifier. Se você estiver usando um SecurityKeyIdentifier personalizado, deverá fornecer um SecurityTokenSerializer personalizado.|  
|TraceCodeIssuanceTokenProviderServiceTokenCacheFull|IssuanceTokenProvider reduziu o cache de token de serviço.|  
|TraceCodeSecurityTokenProviderOpened|O provedor de token de segurança foi aberto.|  
|PublicKeyNotRSA|A chave pública não é uma chave RSA.|  
|InvalidReaderState|O estado específico é inválido para o leitor de entrada fornecido.|  
|UnableToResolveReferenceUriForSignature|Não é possível resolver o URI específico na assinatura para computar o resumo.|  
|EmptyBase64Attribute|Um valor vazio foi encontrado para o nome e o namespace do atributo Base64 obrigatório.|  
|SAMLSubjectRequiresConfirmationMethodWhenConfirmationDataOrKeyInfoIsSpecified|O SubjectConfirmation SAML requer um método de confirmação quando os dados de confirmação ou KeyInfo são especificados.|  
|SAMLAudienceRestrictionShouldHaveOneAudienceOnRead|O SamlAudienceRestrictionCondition que está sendo lido deve conter pelo menos um valor ' Audience '. Nenhum foi encontrado.|  
|TokenProviderUnableToRenewToken|O provedor de token específico não pôde renovar o token de segurança.|  
|AESIVLengthNotSupported|Não há suporte para o bits IV específico. Há suporte apenas para 128 bits IV.|  
|SAMLAuthorityBindingMissingAuthorityKind|Um SamlAuthorityBinding deve conter um ' AuthorityKind ' que não seja nulo.|  
|TraceCodeSecuritySessionDemuxFailure|A mensagem de entrada não faz parte de uma sessão de segurança existente.|  
|TokenRenewalNotSupported|O provedor de token específico não oferece suporte à renovação de token.|  
|AtLeastOneReferenceRequired|Pelo menos uma referência é necessária em uma assinatura.|  
|SAMLSignatureAlreadyRead|A assinatura já está lida na Asserção SAML.|  
|AlgorithmAndPrivateKeyMisMatch|O algoritmo especificado e a chave privada não correspondem.|  
|EmptyTransformChainNotSupported|Não há suporte para a cadeia de transformação vazia.|  
|SspiWrapperEncryptDecryptAssert1|SSPIWrapper:: EncryptDecryptHelper&#124; ' offset ' está fora do intervalo.|  
|SspiWrapperEncryptDecryptAssert2|SSPIWrapper:: EncryptDecryptHelper&#124; ' size ' está fora do intervalo. SecurityTokenManagerCannotCreateAuthenticatorForRequirement = o Gerenciador de token de segurança não pode criar um autenticador de token para o requisito específico.|  
|UnableToCreateKeyedHashAlgorithm|Não é possível criar um KeyedHashAlgorithm a partir do valor específico para o algoritmo de assinatura específico.|  
|SAMLUnableToLoadAssertion|\<saml:assertion>Falha ao carregar o elemento.|  
|X509FindValueMismatchMulti|O X509FindType específico requer que o tipo do argumento FindValue seja um dos 2 valores. O argumento FindValue é de outro tipo.|  
|TraceCodeSecurityIdentityDeterminationSuccess|A identidade foi determinada para um EndpointAddress.|  
|UndefinedUseOfPrefixAtElement|O prefixo específico que é usado no elemento não tem nenhum namespace definido.|  
|TraceCodeSecuritySessionResponderOperationFailure|Falha na operação de sessão de segurança no servidor.|  
|CannotFindCert|Não é possível localizar o certificado X. 509 usando os critérios de pesquisa específicos: StoreName, StoreLocation, findType, Localizevalue.|  
|X509InvalidUsageTime|O tempo de uso do certificado X. 509 específico é inválido. O tempo de uso não se situa entre a hora necessária de não antes e não após a hora.|  
|TraceCodeSecurityIdentityDeterminationFailure|A identidade não pode ser determinada para um EndpointAddress.|  
|AsyncObjectAlreadyEnded|O método End já foi chamado neste objeto de resultado assíncrono.|  
|ExternalDictionaryDoesNotContainAllRequiredStrings|O dicionário externo não contém definições para todas as cadeias de caracteres necessárias. A cadeia de caracteres específica não está disponível no dicionário remoto.|  
|TraceCodeSecuritySessionKeyRenewalFaultReceived|A sessão do Client Security recebeu uma falha de renovação de chave do servidor.|  
|SAMLActionNameRequired|A cadeia de caracteres que representa a SamlAction não pode ser nula nem ter comprimento 0.|  
|SignatureVerificationFailed|Falha na verificação da assinatura.|  
|TraceCodeSecurityContextTokenCacheFull|O cache SecurityContextSecurityToken está cheio.|  
|SAMLAssertionMissingMajorVersionAttributeOnRead|O MajorVersion para o SamlAssertion que está sendo lido está ausente ou tem comprimento 0.|  
|SamlAttributeClaimRightShouldBePossessProperty|Esse construtor SamlAttribute requer que o direito da declaração tenha o valor System. IdentityModel. Declarations. Rights. temproperty.|  
|AuthorizationPolicyEvaluated|A política com a ID específica é avaliada.|  
|SAMLUnableToLoadCondtions<!-- the misspelling here is deliberate. -->|\<saml:conditions>Falha ao carregar o elemento.|  
|AESKeyLengthNotSupported|Não há suporte para a chave bits específica. Há suporte apenas para a chave de bits 128, 192 e 256.|  
|UserNameCannotBeEmpty|O nome de usuário não pode ficar vazio.|  
|AlgorithmAndPublicKeyMisMatch|O algoritmo especificado e a chave pública não correspondem.|  
|SAMLUnableToLoadCondtion<!-- the misspelling here is deliberate. -->|\<saml:conditions>Falha ao carregar o elemento.|  
|SamlAssertionMissingSigningCredentials|SigningCredentials não foram definidos no SamlAssertion. Os SamlAssertions devem ser assinados, defina um SigningCredentials válido no SamlAssertion para continuar.|  
|SspiPayloadNotEncrypted|Os dados binários não foram criptografados com o contexto de segurança SSPI.|  
|SAMLAuthorizationDecisionShouldHaveOneActionOnRead|O SamlAuthorizationDecisionStatement que está sendo lido não contém SamlAction.|  
|TraceCodeSecurityBindingSecureOutgoingMessageFailure|O protocolo de segurança não pode proteger a mensagem de saída.|  
|UndefinedUseOfPrefixAtAttribute|O prefixo específico usado no atributo específico não tem nenhum namespace definido.|  
|NoInputIsSetForCanonicalization|Nenhuma entrada está definida para gravar a saída canônica.|  
|TraceCodeSecurityPendingServerSessionAdded|Uma sessão de segurança pendente é adicionada ao servidor.|  
|AsyncCallbackexception|Um AsyncCallback gerou uma exceção.|  
|PrivateKeyNotRSA|A chave privada não é uma chave RSA.|  
|TraceCodeSecurityClientSessionKeyRenewed|A sessão do Client Security renovou a chave de sessão.|  
|SAMLAuthorizationDecisionStatementMissingDecisionAttributeOnRead|A ' decisão ' para o SamlAuthorizationDecisionStatement que está sendo lido está ausente ou tem comprimento 0.|  
|SAMLAttributeNameAttributeRequired|O ' name ' especificado para um SamlAttribute não pode ser nulo nem ter comprimento 0.|  
|SamlSerializerRequiresExternalSerializers|O SamlSerializer requer um SecurityTokenSerializer para serializar o SecurityKeyIdentifier presente no token.|  
|UnableToResolveKeyReference|O resolvedor de token não pode resolver a referência de chave de segurança específica.|  
|UnsupportedKeyWrapAlgorithm|Não há suporte para o algoritmo de encapsulamento de chave específico.|  
|SAMLAssertionMissingIssuerAttributeOnRead|O ' emissor ' do SamlAssertion que está sendo lido está ausente ou tem comprimento 0.|  
|TraceCodeIssuanceTokenProviderUsingCachedToken|O IssuanceTokenProvider usou o token de serviço em cache.|  
|AESCryptGetKeyParamFailed|Falha ao obter o parâmetro de chave específico.|  
|InvalidNamespaceForEmptyPrefix|O namespace é inválido para o prefixo vazio.|  
|AESCipherModeNotSupported|Não há suporte para o modo de codificação específico. Somente o CBC tem suporte.|  
|ArgumentCannotBeEmptyString|O argumento deve ser uma cadeia de caracteres não vazia.|  
|SAMLAssertionMissingMinorVersionAttributeOnRead|O MinorVersion para o SamlAssertion que está sendo lido está ausente ou tem comprimento 0.|  
|SpecifiedStringNotAvailableInDictionary|A cadeia de caracteres especificada não é uma entrada no dicionário atual.|  
|KerberosApReqInvalidOrOutOfMemory|O AP-REQ é inválido ou o sistema não tem memória suficiente.|  
|FailLogonUser|Falha no LogonUser para o usuário especificado. Verifique se o usuário tem uma conta do Windows válida.|  
|ValueMustBeNonNegative|O valor desse argumento deve ser não negativo.|  
|X509ValidationFail|A validação do certificado X. 509 especificada falhou.|  
|TraceCodeSecuritySessionRequestorOperationSuccess|A operação de sessão de segurança foi concluída com êxito no cliente.|  
|SAMLActionNameRequiredOnRead|A cadeia de caracteres lida para a SamlAction está ausente ou tem comprimento 0.|  
|KerberosMultilegsNotSupported|A identidade é especificada como UPN. A autenticação de um serviço em execução em uma conta de usuário requer múltiplos segmentos Kerberos, que não têm suporte.|  
|SAMLAssertionIdRequired|A ' AssertionId ' para um SamlAssertion não pode ser nula ou vazia.|  
|InvalidOperationForWriterState|A operação especificada é inválida no estado de XmlWriter especificado.|  
|CannotValidateSecurityTokenType|O autenticador de token de segurança especificado não pode validar um token do tipo especificado.|  
|X509FindValueMismatch|O X509FindType especificado requer que o tipo do argumento FindValue seja o valor especificado. O argumento FindValue é de outro tipo.|  
|TraceCodeSecurityClientSessionCloseSent|Uma mensagem de fechamento foi enviada pela sessão do Client Security.|  
|SuiteDoesNotAcceptAlgorithm|O algoritmo especificado não é aceito para a operação especificada pelo conjunto de algoritmos especificado|  
|TraceCodeSecuritySessionRequestorOperationFailure|Falha na operação de sessão do Client Security.|  
|SAMLUnableToLoadStatement|Falha ao carregar um SamlStatement.|  
|InnerReaderMustBeAtElement|O leitor interno deve estar no elemento.|  
|UnableToCreateTokenReference|Não é possível criar uma referência de token de segurança.|  
|TraceCodeSecurityBindingIncomingMessageVerified|O protocolo de segurança verificou a mensagem de entrada.|  
|Objectisreadonly|O objeto é somente leitura.|  
|TraceCodeSecurityClientSessionPreviousKeyDiscarded|A sessão do Client Security descartou a chave de sessão anterior.|  
|SAMLTokenTimeInvalid|O SamlToken não é um tempo válido. A hora atual está fora do tempo efetivo e de expiração do token.|  
|TraceCodeSecurityIdentityVerificationSuccess|Verificação de identidade bem-sucedida.|  
|SigningTokenHasNoKeys|O token de assinatura especificado não tem chaves.|  
|TraceCodeSecurityIdentityVerificationFailure|Falha na verificação de identidade.|  
|AESCryptImportKeyFailed|Falha ao importar o material da chave.|  
|FailInitializeSecurityContext|InitializeSecurityContent falhou. Verifique se o nome da entidade de serviço está correto.|  
|TraceCodeStreamSecurityUpgradeAccepted|A atualização de segurança do fluxo foi aceita com êxito.|  
|SAMLAuthorityBindingRequiresLocation|O atributo ' location ' especificado em SamlAuthorityBinding não pode ser nulo nem ter comprimento 0.|  
|PublicKeyNotDSA|A chave pública não é uma chave DSA.|  
|ImpersonationLevelNotSupported|Os modos de autenticação usando Kerberos não dão suporte ao nível de representação especificado. Especifique uma identificação válida ou um nível de representação.|  
|RequiredTargetNotSigned|O elemento com a ID especificada deve ser assinado, mas não foi.|  
|SAMLAuthenticationStatementMissingAuthenticationInstanceOnRead|O atributo ' AuthenticationInstant ' que está sendo lido para um SamlAuthenticationStatement está ausente ou tem comprimento 0.|  
|SAMLEvidenceShouldHaveOneAssertionOnRead|O SamlEvidence que está sendo lido não continha uma referência a ou um SamlAssertion inserido.|  
|LengthOfArrayToConvertMustGreaterThanZero|O comprimento da matriz a ser convertida em um inteiro deve ser maior que 0.|  
|InvalidAsyncResult|AsyncResult inválido.|  
|TraceCodeIssuanceTokenProviderRemovedCachedToken|O IssuanceTokenProvider removeu o token de serviço expirado.|  
|IncorrectUserNameFormat|O nome de usuário está em um formato inválido. O formato de nome de usuário deve estar no formato "nome de usuário" ou "domínio \\ \username".|  
|TraceCodeExportSecurityChannelBindingEntry|Iniciando ExportChannelBinding de segurança.|  
|UnsupportedInputTypeForTransform|O tipo de entrada especificado não tem suporte para a transformação.|  
|CannotFindDocumentRoot|Não é possível localizar a raiz do documento.|  
|XmlBufferQuotaExceeded|O tamanho necessário para armazenar em buffer o conteúdo XML excedeu a cota de buffer.|  
|TraceCodeSecuritySessionClosedResponseSendFailure|Ocorreu uma falha ao enviar uma resposta de fechamento de sessão de segurança para o cliente.|  
|UnableToResolveReferenceInSamlSignature|Não é possível resolver a referência especificada na assinatura SAML com AssertionId.|  
|SAMLSubjectRequiresNameIdentifierOrConfirmationMethod|Um SamlSubject requer que um ' NameIdentifier ' ou ' ConfirmationMethod ' seja especificado. Ambos estavam ausentes.|  
|SAMLAttributeMissingNamespaceAttributeOnRead|O ' namespace ' para o SamlAttribute que está sendo lido está ausente ou tem comprimento 0.|  
|SAMLSubjectConfirmationClauseMissingConfirmationMethodOnRead|Um ' ConfirmationMethod ' não pode ser encontrado no SamlSubjectConfirmation que está sendo lido.|  
|SecurityTokenRequirementHasInvalidTypeForProperty|O requisito de token tem um tipo inesperado para a propriedade especificada. O tipo de propriedade esperado é de outro valor.|  
|TraceCodeNegotiationTokenProviderAttached|NegotiationTokenProvider foi anexado.|  
|TraceCodeSpnegoClientNegotiationCompleted|SpnegoTokenProvider concluiu a negociação SSPI.|  
|SAMLUnableToLoadUnknownElement|O SamlSerializer selecionado não pode desserializar esse elemento. Registre um SamlSerializer personalizado para desserializar elementos personalizados.|  
|CreateSequenceRefused|A solicitação de criação de sequência foi recusada pelo destino RM.|  
|TraceCodeSecuritySessionRedirectApplied|A sessão do Client Security foi redirecionada.|  
|SecurityTokenRequirementDoesNotContainProperty|O requisito de token não contém a propriedade especificada.|  
|SAMLAttributeValueCannotBeNull|Um dos attributeValues encontrados no SamlAttribute foi considerado um valor nulo. Verifique se as listas não são nulas ao criar o SamlAttribute.|  
|ValueMustBeGreaterThanZero|O valor deste argumento deve ser maior que 0.|  
|TraceCodeNegotiationAuthenticatorAttached|NegotiationTokenAuthenticator foi anexado.|  
|ValueMustBePositive||  
|SAMLAuthorizationDecisionShouldHaveOneAction|Um SamlAuthorizationDecisionStatement deve ter pelo menos um SamlAction.|  
|TraceCodeSecurityTokenAuthenticatorClosed|O autenticador de token de segurança foi fechado.|  
|TraceCodeSecurityAuditWrittenSuccess|O log de auditoria de segurança foi gravado com êxito.|  
|PrivateKeyNotDSA|A chave privada não é uma chave DSA.|  
|MessageNumberRollover|O número de sequência máximo para esta sequência foi excedido.|  
|AESPaddingModeNotSupported|Não há suporte para o modo de preenchimento especificado. Somente PKCS7 e ISO10126 têm suporte.|  
|SAMLSubjectRequiresNameIdentifierOrConfirmationMethodOnRead|Os elementos ' NameIdentifier ' e ' ConfirmationMethod ' necessários não foram encontrados para o SamlSubject que está sendo lido.|  
|TraceCodeSecurityAuditWrittenFailure|Ocorreu uma falha ao gravar no log de auditoria de segurança.|  
|UnsupportedCryptoAlgorithm|Não há suporte para o algoritmo de criptografia especificado neste contexto.|  
|SigningTokenHasNoKeysSupportingTheAlgorithmSuite|O token de assinatura não tem nenhuma chave que ofereça suporte ao conjunto de algoritmos especificado.|  
|SAMLNameIdentifierMissingIdentifierValueOnRead|A cadeia de caracteres ' identifier ' para o SamlNameIdentifier que está sendo lido está ausente.|  
|SAMLSubjectStatementRequiresSubject|A instrução SAML Subject requer que uma entidade SAML seja especificada.|  
|TraceCodeSslClientCertMissing|O cliente SSL remoto não pôde fornecer um certificado necessário.|  
|SAMLTokenVersionNotSupported|A versão principal especificada e a versão secundária não têm suporte.|  
|TraceCodeConfigurationIsReadOnly|A configuração é somente leitura.|  
|TraceCodeSecuritySessionRenewFaultSendFailure|Ocorreu uma falha ao enviar uma falha de renovação na chave de sessão de segurança para o cliente.|  
|TraceCodeSecurityInactiveSessionFaulted|Uma sessão de segurança inativa falhou pelo servidor.|  
|SAMLUnableToLoadAttribute|Falha ao carregar SamlAttribute.|  
|Psha1KeyLengthInvalid|O comprimento de chave PSHA1 especificado é inválido.|  
|KeyIdentifierCannotCreateKey|Este SecurityKeyIdentifier não tem nenhuma cláusula que possa criar uma chave.|  
|X509IsInUntrustedStore|O certificado X. 509 especificado está em um repositório de certificados não confiável.|  
|UnexpectedXmlChildNode|O nó filho XML especificado do tipo especificado é inesperado para o elemento especificado.|  
|TokenDoesNotMeetKeySizeRequirements|Os requisitos de tamanho de chave para o conjunto de algoritmos especificado não são atendidos pelo token especificado.|  
|TraceCodeSecuritySessionRequestorStartOperation|Uma operação de sessão de segurança foi iniciada no cliente.|  
|InvalidHexString|Formato de cadeia de caracteres hexadecimal inválido.|  
|SamlAttributeClaimResourceShouldBeAString|Esse construtor SamlAttribute requer que o recurso da declaração seja do tipo ' String '.|  
|SamlSigningTokenNotFound|O SamlAssertion é assinado, mas o token que assinou o SamlAssertion não pode ser encontrado. Verifique se SecurityTokenResolver contém o token que assinou o SamlAssertion.|  
|TraceCodeSecuritySpnToSidMappingFailure|Não foi possível mapear o servicePrincipalName para um SecurityIdentifier.|  
|UnableToCreateSignatureFormatterFromAsymmetricCrypto|Não é possível criar um formatador de assinatura para o algoritmo especificado a partir da criptografia assimétrica especificada.|  
|TraceCodeSecurityServerSessionClosedFaultSent|A sessão de segurança do servidor enviou uma falha de sessão fechada ao cliente.|  
|UnableToFindPrefix|Não é possível localizar o prefixo para o prefixo usado visivelmente especificado no elemento especificado.|  
|TraceCodeSecurityTokenAuthenticatorOpened|O autenticador de token de segurança foi aberto.|  
|RequiredAttributeMissing|O atributo especificado é necessário no elemento especificado.|  
|LocalIdCannotBeEmpty|A localId não pode estar vazia. Especifique um ' LocalId ' válido.|  
|ValueMustBeInRange|O valor desse argumento deve estar dentro do intervalo especificado.|  
|TraceCodeIssuanceTokenProviderBeginSecurityNegotiation|IssuanceTokenProvider iniciou uma nova negociação de segurança.|  
|InvalidNtMapping|O certificado X. 509 especificado não pode ser mapeado para uma conta do Windows. O nome alternativo da entidade UPN é necessário.|  
|AESCryptSetKeyParamFailed|Falha ao definir o parâmetro de chave especificado.|  
|TraceCodeSecuritySessionClosedResponseReceived|A sessão do Client Security recebeu uma resposta fechada do servidor.|  
|UnableToCreateSignatureDeformatterFromAsymmetricCrypto|Não é possível criar um desformatador de assinatura para o algoritmo especificado a partir da criptografia assimétrica especificada.|  
|TraceCodeIdentityModelAsyncCallbackThrewException|Um retorno de chamada assíncrono gerou uma exceção.|  
|LengthMustBeGreaterThanZero|O comprimento deste argumento deve ser maior que 0.|  
|FoundMultipleCerts|Foram encontrados vários certificados X. 509 usando os critérios de pesquisa especificados: StoreName, StoreLocation, findType e findValue. Forneça um valor de localização mais específico.|  
|AtLeastOneTransformRequired|O elemento transformações deve conter pelo menos uma transformação.|  
|SAMLTokenNotSerialized|O SamlAssertion não pôde ser serializado para XML. Consulte a exceção interna para obter detalhes.|  
|TraceCodeSecurityBindingOutgoingMessageSecured|O protocolo de segurança protegeu a mensagem de saída.|  
|KeyIdentifierClauseDoesNotSupportKeyCreation|Este SecurityKeyIdentifierClause não dá suporte à criação de chave.|  
|UnableToResolveTokenReference|O resolvedor de token não pode resolver a referência de token especificada.|  
|UnsupportedEncryptionAlgorithm|Não há suporte para o algoritmo de criptografia especificado.|  
|SamlSerializerUnableToWriteSecurityKeyIdentifier|O SamlSerializer não contém um SecurityTokenSerializer capaz de serializar o SecurityKeyIdentifier determinado. Se você estiver usando um SecurityKeyIdentifier personalizado, deverá fornecer um SecurityTokenSerializer personalizado.|  
|SAMLAttributeShouldHaveOneValue|Nenhum valor de atributo encontrado. Um atributo SamlAttribute deve ter pelo menos um valor de atributo.|  
|TraceCodeSecurityBindingVerifyIncomingMessageFailure|O protocolo de segurança não pode verificar a mensagem de entrada.|  
|SamlSigningTokenMissing|O SamlAssertion passado para o SamlSecurityTokenAuthenticator não contém um token de assinatura.|  
|NoPrivateKeyAvailable|Nenhuma chave privada está disponível.|  
|ValueMustBeOne|O valor desse argumento deve ser 1.|  
|TraceCodeSecurityPendingServerSessionRemoved|Uma sessão de segurança pendente foi tornada ativa pelo servidor.|  
|TraceCodeImportSecurityChannelBindingExit|ImportChannelBinding de segurança concluídos.|  
|X509CertStoreLocationNotValid|O StoreLocation deve ser LocalMachine ou CurrentUser.|  
|SettingdMayBeModifiedOnlyWhenTheWriterIsInStartState|As configurações do gravador podem ser modificadas somente quando o gravador está no estado de início.|  
|ArgumentInvalidCertificate|O certificado é inválido.|  
|DigestVerificationFailedForReference|Falha na verificação de resumo para a referência especificada.|  
|SAMLAuthorityBindingRequiresBinding|O atributo ' Binding ' especificado em SamlAuthorityBinding não pode ser nulo nem ter comprimento 0.|  
|AESInsufficientOutputBuffer|O buffer de saída deve ser maior que os bytes especificados.|  
|SAMLAuthorityBindingMissingBindingOnRead|O atributo ' Binding ' para o SamlAuthorityBinding que está sendo lido está ausente ou tem comprimento 0.|  
|SAMLAuthorityBindingInvalidAuthorityKind|O SamlAuthorityBinding que está sendo lido tem um AuthorityKind inválido. O formato de AuthorityKind deve ser um QName.|  
|ProvidedNetworkCredentialsForKerberosHasInvalidUserName|O NetworkCredentials fornecido para o token Kerberos não tem um nome de usuário válido.|  
|SSPIPackageNotSupported|Não há suporte para o pacote SSPI especificado.|  
|TokenCancellationNotSupported|O provedor de token especificado não dá suporte ao cancelamento de token.|  
|UnboundPrefixInQName|Um prefixo não associado é usado no nome qualificado especificado.|  
|SAMLAuthorizationDecisionResourceRequired|O ' Resource ' especificado para SamlAuthorizationDecisionStatement não pode ser nulo nem ter comprimento 0.|  
|TraceCodeSecurityNegotiationProcessingFailure|Falha no processamento da negociação de segurança do serviço.|  
|SAMLAssertionIssuerRequired|O ' emissor ' especificado para um SamlAssertion não pode ser nulo ou vazio.|  
|UnableToCreateHashAlgorithmFromAsymmetricCrypto|Não é possível criar um HashAlgorithm para o algoritmo especificado a partir da criptografia assimétrica especificada.|  
|SamlUnableToExtractSubjectKey|O SecurityKeyIdentifier que foi encontrado no SamlSubject não pode ser resolvido para um SecurityToken. O SecurityTokenResolver deve conter um SecurityToken para o qual o SecurityKeyIdentifier resolve.|  
|ChildNodeTypeMissing|O elemento XML especificado não tem um filho do tipo especificado.|  
|TraceCodeSecurityPendingServerSessionClosed|A sessão de segurança pendente foi fechada pelo servidor.|  
|TraceCodeSecuritySessionCloseResponseSent|A sessão de segurança do servidor enviou uma resposta de fechamento ao cliente.|  
|TraceCodeSecurityIdentityHostNameNormalizationFailure|A porção HostName de um endereço de ponto de extremidade não pode ser normalizada.|  
|FailAcceptSecurityContext|O AcceptSecurityContext falhou.|  
|EmptyXmlElementError|O elemento especificado não pode estar vazio.|  
|PrefixNotDefinedForNamespace|Um prefixo para o namespace especificado não está definido neste contexto e não pode ser declarado.|  
|SAMLAuthorizationDecisionHasMoreThanOneEvidence|O SamlAuthorizationDecisionStatement que está sendo lido foi encontrado para conter mais de uma evidência. Isso não é permitido.|  
|SamlTokenAuthenticatorCanOnlyProcessSamlTokens|O SamlSecurityTokenAuthenticator só pode processar SamlSecurityTokens. O SecurityTokentype especificado foi recebido.|  
|SAMLAttributeStatementMissingAttributeOnRead|O SamlAttributeStatement que está sendo lido não contém nenhum elemento ' SamlAttribute '. Isso não é permitido.|  
|CouldNotFindNamespaceForPrefix|Não é possível pesquisar o namespace para o prefixo especificado.|  
|TraceCodeExportSecurityChannelBindingExit|ExportChannelBinding de segurança concluídos.|  
|AESCryptDecryptFailed|Falha ao descriptografar os dados especificados.|  
|SAMLAttributeNamespaceAttributeRequired|O ' namespace ' especificado para um SamlAttribute não pode ser nulo nem ter comprimento 0.|  
|TraceCodeSpnegoServiceNegotiationCompleted|SpnegoTokenAuthenticator concluiu a negociação SSPI.|  
|TraceCodeSecurityServerSessionRenewalFaultSent|A sessão de segurança do servidor enviou uma falha de renovação de chave ao cliente.|  
|AlgorithmMismatchForTransform|Ocorreu uma incompatibilidade no algoritmo para a transformação.|  
|UserNameAuthenticationFailed|Falha na autenticação de um nome de usuário/senha usando o mecanismo especificado. O usuário não está autenticado.|  
|SamlInvalidSigningToken|O SamlAssertion foi assinado com um token que não foi validado de acordo com o protocolo. Se você estiver usando certificados X. 509, examine sua semântica de validação.|  
|TraceCodeSecurityServerSessionKeyUpdated|A chave de sessão de segurança foi atualizada pelo servidor.|  
|TraceCodeSecurityServerSessionCloseReceived|A sessão de segurança do servidor recebeu uma mensagem de fechamento do cliente.|  
|SAMLAuthenticationStatementMissingSubject|O SamlSubjectStatement necessário está ausente no SamlAuthenticationStatement.|  
|UnexpectedEndOfFile|Fim de arquivo inesperado.|  
|UnsupportedAlgorithmForCryptoOperation|O algoritmo especificado não tem suporte para a operação especificada.|  
|XmlLangAttributeMissing|O atributo XML: lang necessário está ausente.|  
|TraceCodeSecurityImpersonationSuccess|Representação de segurança bem-sucedida no servidor.|  
|SAMLAuthorityBindingMissingLocationOnRead|O atributo ' location ' para o SamlAuthorityBinding que está sendo lido está ausente ou tem comprimento 0.|  
|SAMLAttributeStatementMissingSubjectOnRead|O elemento ' SamlSubject ' para o SamlAttributeStatement está ausente.|  
|SAMLAuthorizationDecisionStatementMissingSubjectOnRead|O elemento ' SamlSubject ' para SamlAuthorizationDecisionStatement que está sendo lido está ausente.|  
|SAMLBadSchema|Ao ler um SamlAssertion, esse elemento especificado não está em conformidade com o esquema.|  
|SAMLAssertionIDIsInvalid|A ' AssertionId ' especificada para um SamlAssertion deve começar com uma letra ou ' _ '.|  
|TraceCodeSecurityActiveServerSessionRemoved|Uma sessão de segurança ativa foi removida pelo servidor.|  
|UnableToCreateKeyedHashAlgorithmFromSymmetricCrypto|Não é possível criar um keyedHashAlgorithm para o algoritmo especificado a partir da criptografia simétrica especificada.|  
|SAMLAuthenticationStatementMissingAuthenticationMethod|O ' AuthenticationMethod ' especificado para um SamlAuthenticationStatement não pode ser nulo nem ter comprimento 0.|  
|TraceCodeSecurityImpersonationFailure|Falha na representação de segurança no servidor.|  
|Padrão|(Padrão)|  
|UnsupportedNodeTypeInReader|Não há suporte para o tipo de nó especificado com o nome especificado.|
