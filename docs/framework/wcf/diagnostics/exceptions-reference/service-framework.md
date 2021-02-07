---
description: 'Saiba mais sobre: Service Framework'
title: Estrutura de serviço
ms.date: 03/30/2017
ms.assetid: 75f60b87-f80e-4377-ba7c-8e6becaa2b28
ms.openlocfilehash: aa53a6c0740c292c1f34920edabdb81f7c5a13ab
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99686130"
---
# <a name="service-framework"></a>Estrutura de serviço

Este tópico lista todas as exceções geradas pelos dados do Service Framework.  
  
## <a name="exception-list"></a>Lista de exceções  
  
|Código do recurso|Cadeia de caracteres de recurso|  
|-------------------|---------------------|  
|ABindingInstanceHasAlreadyBeenAssociatedTo1|Uma instância de associação já foi associada para escutar o identificador de recurso uniforme especificado. Se dois pontos de extremidade quiserem compartilhar o mesmo indicador de recurso ListenUniform, eles também deverão compartilhar a mesma instância de objeto de associação. Os dois pontos de extremidade conflitantes foram especificados em chamadas AddServiceEndpoint (), em um arquivo de configuração ou em uma combinação de AddServiceEndpoint () e configuração.|  
|AChannelServiceEndpointIsNull0|Um ponto de extremidade de canal ou de serviço é nulo.|  
|AChannelServiceEndpointSContractSNameIsNull0|Um nome de contrato de ponto de extremidade de canal/serviço é nulo ou está vazio.|  
|AChannelServiceEndpointSContractSNamespace0|Um namespace de contrato de ponto de extremidade de canal/serviço é nulo.|  
|BaseAddressCannotHaveFragment|Um endereço base não pode conter um fragmento de identificador de recurso uniforme.|  
|BaseAddressCannotHaveQuery|Um endereço base não pode conter uma cadeia de caracteres de consulta do identificador de recurso uniforme.|  
|BaseAddressCannotHaveUserInfo|Um endereço base não pode conter uma seção de informações de usuário do Uniform Resource Identifier.|  
|BaseAddressDuplicateScheme|Esta coleção já contém um endereço com o esquema especificado. Somente um endereço é permitido para cada esquema nesta coleção.|  
|BaseAddressMustBeAbsolute|Somente um Uniform Resource Identifier absoluto pode ser usado como um endereço base.|  
|BindingDoesnTSupportAnyChannelTypes1|A associação especificada não oferece suporte à criação de qualquer tipo de canal. Os elementos de associação em uma associação personalizada estão empilhados incorretamente ou na ordem errada. Um transporte é necessário na parte inferior da pilha. A ordem recomendada para elementos de associação é: TransactionFlow, ReliableSession, Security, CompositeDuplex, OneWay, StreamSecurity, MessageEncoding, Transport.|  
|BindingDoesnTSupportDuplexButContractRequires1|O contrato requer duplex. A associação especificada não oferece suporte a ela ou não está configurada corretamente para dar suporte a ela.|  
|BindingDoesnTSupportOneWayButContractRequires1|O contrato requer OneWay. A associação especificada não oferece suporte a ela ou não está configurada corretamente para dar suporte a ela.|  
|BindingDoesnTSupportRequestReplyButContract1|O contrato requer solicitação/resposta. A associação especificada não oferece suporte a ela ou não está configurada corretamente para dar suporte a ela.|  
|BindingDoesnTSupportSessionButContractRequires1|O contrato requer sessão.  A associação especificada não oferece suporte a ela ou não está configurada corretamente para dar suporte a ela.|  
|BindingDoesnTSupportTwoWayButContractRequires1|O contrato requer Two-Way (solicitação-resposta ou duplex). A associação especificada não oferece suporte a ela ou não está configurada corretamente para dar suporte a ela.|  
|BindingRequirementsAttributeDisallowsQueuedDelivery1|O DeliveryRequirementsAttribute não permite QueuedDelivery. A associação para o ponto de extremidade com o contrato especificado dá suporte a ele.|  
|BindingRequirementsAttributeRequiresQueuedDelivery1|O DeliveryRequirementsAttribute requer QueuedDelivery. A associação para o ponto de extremidade com o contrato especificado não oferece suporte a ele ou não está configurada corretamente para dar suporte a ele.|  
|channelDoesNotHaveADuplexSession0|O canal atual não dá suporte ao fechamento da sessão de saída. Este canal não implementa ISessionChannel \<IDuplexSession> .|  
|ClientRuntimeRequiresFormatter0|O ClientOperation especificado requer um formatador, pois SerializeRequest e DeserializeReply não são ambos falsos.|  
|CommunicationObjectAborted1|O objeto de comunicação especificado não pode ser usado para comunicação porque foi interrompido.|  
|CommunicationObjectAbortedStack2|O objeto de comunicação especificado não pode ser usado para comunicação porque foi interrompido: {1}|  
|CommunicationObjectBaseClassMethodNotCalled|O objeto de comunicação especificado substituiu a função virtual {1} , mas não chama a versão definida na classe base.|  
|ContractIsNotSelfConsistentItHasOneOrMore2|O contrato especificado tem uma ou mais operações istermination ou non-preiniciation. Ele não tem a Propriedade SessionMode definida como SessionMode. Required. Os atributos isiniciar e istermination só podem ser usados no contexto de uma sessão.|  
|CouldnTCreateChannelForChannelType2|O tipo de canal especificado foi solicitado, mas a associação especificada não oferece suporte a ele ou não está configurada corretamente para dar suporte a ele.|  
|DispatchRuntimeRequiresFormatter0|A DispatchOperation especificada requer um formatador, porque DeserializeRequest e SerializeReply não são false.|  
|EndMethodsCannotBeDecoratedWithOperationContractAttribute|O método End não pode ser usado com OperationContractAttribute ao usar o padrão de design IAsyncResult. Somente o método Begin correspondente pode ser usado com OperationContractAttribute. Esse atributo se aplica ao Begin-End par de métodos.|  
|EndpointListenerRequirementsCannotBeMetBy3|Os requisitos de ChannelDispatcher não podem ser atendidos pelo IChannelListener para a associação especificada porque o contrato requer suporte para um desses tipos de canal especificados. Mas a associação só dá suporte a esses tipos de canal especificados.|  
|EndpointsMustHaveAValidBinding0|Os pontos de extremidade devem ter uma Associação válida.|  
|InvalidOrUnrecognizedAction|A mensagem não pode ser processada porque a ação especificada é inválida ou não foi reconhecida.|  
|MultipleMebesInParameters|Mais de um MessageEncodingBindingElement foi encontrado em BindingParameters do BindingContext. CustomBinding não pode ter vários MessageEncodingBindingElements. Remova todos, exceto um desses elementos.|  
|MultipleStreamUpgradeProvidersInParameters|Mais de um IStreamUpgradeProviderElement foi encontrado em BindingParameters do BindingContext. CustomBinding não pode ter mais de um IStreamUpgradeProviderElements. Remova todos, exceto um desses elementos.|  
|NoChannelBuilderAvailable|A associação não pode ser usada para criar uma fábrica de canais ou um ouvinte de canal porque ele não tem um TransportBindingElement. Cada associação deve ter pelo menos um elemento de associação derivado de TransportBindingElement.|  
|NotAllBindingElementsBuilt|Alguns dos elementos de ligação nessa associação não foram usados durante a criação da fábrica de canais e do ouvinte de canal. Os elementos de associação não são ordenados corretamente. A ordem recomendada para elementos de associação é: TransactionFlow, ReliableSession, Security, CompositeDuplex, OneWay, StreamSecurity, MessageEncoding, Transport.  Observe que TransportBindingElement deve ser o último. Os elementos de associação especificados não foram compilados.|  
|RuntimeRequiresInvoker0|A operação de expedição requer um chamador.|  
|ServiceHasZeroAppEndpoints|O serviço especificado não tem pontos de extremidade de aplicativo (não infraestrutura). Isso pode ser porque nenhum arquivo de configuração foi encontrado para seu aplicativo ou porque nenhum elemento de serviço correspondente ao nome do serviço foi encontrado no arquivo de configuração ou porque nenhum ponto de extremidade foi definido no elemento de serviço.|  
|SFxActionMismatch|Não é possível criar uma mensagem tipada devido a uma incompatibilidade de ação. Esperando a ação especificada, mas foi encontrada outra|  
|SFxAnonymousTypeNotSupported|A parte especificada na mensagem especificada não pode ser exportada com RPC ou codificada porque seu tipo é anônimo.|  
|SFxBadMetadataLocationNoAppropriateBaseAddress|A URL fornecida para ServiceMetadataBehavior usando a propriedade ExternalMetadataLocation ou o atributo externalMetadataLocation na seção de metadados na seção de configuração era uma URL relativa e não há endereço base com o qual resolvê-la.|  
|SFxBadMetadataMustBePolicy|É necessário fornecer um XmlElement de política que tenha o namespace e o nome especificados. Este XmlElement tem o namespace e o nome especificados.|  
|SFxBodyObjectTypeCannotBeInherited|O tipo especificado não pode herdar de nenhuma classe diferente do objeto a ser usado como o objeto Body no estilo RPC.|  
|SFxBodyObjectTypeCannotBeInterface|O tipo especificado implementa a interface especificada, que não tem suporte para o objeto Body no estilo RPC.|  
|SFxCallbackBehaviorAttributeOnlyOnDuplex|CallbackBehaviorAttribute só pode ser executado como um comportamento em um ponto de extremidade com um contrato duplex. O contrato especificado não é duplex e não contém nenhuma operação de retorno de chamada.|  
|SFxCallbackRequestReplyInOrder1|A resposta não pode ser recebida desta operação até que a mensagem atual conclua o processamento. Se você quiser permitir o processamento de mensagens fora de ordem, especifique ConcurrencyMode de reentrante ou Multiple no especificado.|  
|SfxCallbackTypeCannotBeNull|Para usar o contrato especificado com a DuplexChannelFactory, o contrato deve especificar um contrato de retorno de chamada válido. Se seu contrato tiver um contrato de retorno de chamada, use ChannelFactory em vez de DuplexChannelFactory.|  
|SFxCannotGetMetadataFromLocation|O MetadataExchangeClient só pode obter metadados de HTTP e HTTPS MetadataLocations. Não é possível obter metadados do especificado.|  
|SFxCannotHttpGetMetadataFromAddress|O MetadataExchangeClient só pode obter metadados de endereços HTTP ou HTTPS ao usar MetadataExchangeClientmode HttpGet. Não é possível obter metadados do especificado.|  
|SFxCannotImportAsParameters_Bare|Gerando contrato de mensagem porque a operação especificada não é RPC nem documento encapsulado.|  
|SFxCannotImportAsParameters_DifferentWrapperName|Gerando contrato de mensagem porque o nome do wrapper da mensagem especificada não corresponde ao valor padrão.|  
|SFxCannotImportAsParameters_DifferentWrapperNs|Gerando contrato de mensagem porque o namespace do wrapper da mensagem especificada não corresponde ao valor padrão.|  
|SFxCannotImportAsParameters_ElementIsNotNillable|Gerando um contrato de mensagem porque o nome do elemento especificado do namespace especificado não está marcado como anulável.|  
|SFxCannotImportAsParameters_HeadersAreUnsupported|Gerando contrato de mensagem porque a mensagem especificada tem cabeçalhos.|  
|SFxCannotImportAsParameters_Message|Gerando um contrato de mensagem porque a operação especificada tem uma mensagem não tipada como argumento ou tipo de retorno.|  
|SFxCannotImportAsParameters_MessageHasProtectionLevel|Gerando contrato de mensagem porque a mensagem especificada requer proteção.|  
|SFxCannotImportAsParameters_NamespaceMismatch|Gerando contrato de mensagem porque o namespace da parte da mensagem especificada não corresponde ao valor padrão.|  
|SFxCannotRequireBothSessionAndDatagram3|O contrato especificado especifica SessionMode. não permitido e o contrato especificado especifica SessionMode. Required. Altere um dos valores de SessionMode ou especifique um endereço diferente, ou ListenURI, para cada ponto de extremidade.|  
|SFxCannotSetExtensionsByIndex|Esta coleção não oferece suporte à definição de extensões por índice. Use os métodos InsertItem ou RemoveItem.|  
|SFxChannelDispatcherDifferentHost0|O ChannelDispatcher não está atualmente anexado ao ServiceHost que foi fornecido.|  
|SFxChannelDispatcherMultipleHost0|O ChannelDispatcher não pode ser adicionado a mais de um ServiceHost.|  
|SFxChannelDispatcherNoHost0|Não é possível abrir o ChannelDispatcher porque ele não está anexado a um ServiceHost.|  
|SfxChannelFactoryDisposed|Esta ChannelFactory não pode ser aberta porque a ChannelFactory já foi descartada. Crie a ChannelFactory novamente antes de usá-la.|  
|SFxChannelFactoryNoBinding|Não é possível abrir a ChannelFactory porque nenhuma associação foi associada a seu ponto de extremidade. Especifique uma associação com o construtor ou a propriedade de ponto de extremidade.|  
|SFxChannelTerminated0|Uma operação marcada como istermination já foi invocada neste canal, fazendo com que a conexão do canal seja encerrada. Não é possível invocar mais operações nesse canal. Recrie o canal para continuar a comunicação.|  
|SFxCloseTimedOut1|A operação de fechamento de ServiceHost foi interrompida após o especificado. Isso pode ocorrer porque um cliente falhou ao fechar um canal de sessão no tempo necessário. O tempo permitido para esta operação pode ter sido parte de um tempo limite maior.|  
|SfxCloseTimedOutWaitingForDispatchToComplete|O tempo limite do processo de fechamento expirou enquanto aguardava a conclusão da expedição do serviço.|  
|SFxCodeGenIsNotAssignableFrom|Não é possível atribuir o especificado.|  
|SFxConfigChannelConfigurationNotFound|O elemento de ponto de extremidade com o nome e contrato especificados na seção de configuração do cliente ServiceModel não foi encontrado.|  
|SFxConflictingGlobalElement|O elemento de linguagem XML de nível superior com o nome especificado no namespace especificado não pode referenciar o tipo especificado. Ele já faz referência a um tipo diferente. Use um nome de operação diferente ou MessageBodyAttribute para especificar um nome diferente para as partes de mensagem ou mensagem.|  
|SFxContractHasZeroInitiatingOperations|Um contrato deve ter pelo menos uma operação de isiniciou = true.|  
|SFxContractHasZeroOperations|Um contrato deve ter pelo menos uma operação.|  
|SFxContractInheritanceRequiresInterfaces|A classe de serviço do tipo especificado define um ServiceContract e herda um ServiceContract do tipo especificado. A herança de contrato só pode ser usada entre tipos de interface. Se uma classe for marcada com ServiceContractAttribute, ela deverá ser o único tipo na hierarquia com ServiceContractAttribute.  Mova o ServiceContractAttribute no tipo especificado para uma interface separada que o tipo especificado implementa.|  
|SFxCreateDuplexChannel1|O contrato de retorno de chamada do contrato especificado não existe ou não define nenhuma operação. Se esse não for um contrato duplex, use ChannelFactory em vez de DuplexChannelFactory.|  
|SFxCreateDuplexChannelNoCallback|Esta sobrecarga de CreateChannel não pode ser chamada nesta instância do DuplexChannelFactory. A DuplexChannelFactory não foi inicializada com um InstanceContext. Chame a sobrecarga CreateChannel que usa um InstanceContext.|  
|SFxCreateDuplexChannelNoCallback1|Esta sobrecarga de CreateChannel não pode ser chamada nesta instância do DuplexChannelFactory. A DuplexChannelFactory foi inicializada com um tipo e nenhum InstanceContext válido foi fornecido. Chame a sobrecarga CreateChannel que usa um InstanceContext.|  
|SFxCreateDuplexChannelNoCallbackUserObject|Esta sobrecarga de CreateChannel não pode ser chamada nesta instância do DuplexChannelFactory. O InstanceContext fornecido para a DuplexChannelFactory não contém um UserObject válido.|  
|SFxCreateNonDuplexChannel1|ChannelFactory não dá suporte ao contrato especificado. ChannelFactory define um contrato de retorno de chamada com uma ou mais operações. Use a DuplexChannelFactory em vez de ChannelFactory.|  
|SFxCustomBindingNeedsTransport1|O CustomBinding no ServiceEndpoint com o contrato especificado não tem um TransportBindingElement. Cada associação deve ter pelo menos um elemento de associação derivado de TransportBindingElement.|  
|SFxCustomBindingWithoutTransport|O esquema não pode ser computado para esta associação personalizada porque não tem um TransportBindingElement. Cada associação deve ter pelo menos um elemento de associação derivado de TransportBindingElement.|  
|SFxDataContractSerializerDoesNotSupportBareArray|O DataContractSerializer não oferece suporte à coleção especificada no elemento especificado.|  
|SFxDictionaryIsEmpty|A operação não pode ser executada porque o dicionário está vazio.|  
|SFxDocEncodedNotSupported|Erro ao refletir o especificado. Não há suporte para Document-Encoded. Altere ' use ' para literal ou ' style ' para RPC.|  
|SFxDuplicateInitiatingActionAtSameVia|Esse serviço tem vários pontos de extremidade ouvindo no especificado. Os pontos de extremidade compartilham a mesma ação de inicialização especificada. Mensagens com esta ação seriam descartadas porque o Dispatcher não seria capaz de determinar o ponto de extremidade correto para manipular a mensagem.|  
|SFXEndpointBehaviorUsedOnWrongSide|O IEndpointBehavior especificado não pode ser usado no servidor. Esse comportamento só pode ser aplicado a clientes.|  
|SFxEndpointNoMatchingScheme|O endereço base que corresponde ao esquema especificado para o ponto de extremidade com a associação especificada não pode ser encontrado. Foram especificados esquemas de endereço base registrados.|  
|SFxErrorCreatingMtomReader|Ocorreu um erro ao criar um leitor para a mensagem do mecanismo de otimização de transmissão de mensagens.|  
|SFxErrorDeserializingFault|O servidor retornou uma falha inválida de protocolo de acesso a objeto simples. Consulte InnerException para obter mais detalhes.|  
|SFxErrorDeserializingHeader|Ocorreu um erro ao desserializar um dos cabeçalhos na mensagem especificada. Consulte InnerException para obter mais detalhes.|  
|SFxErrorReflectingOnMethod3|Ocorreu um erro ao carregar o atributo especificado no método especificado no tipo especificado.  Consulte InnerException para obter mais detalhes.|  
|SFxErrorReflectingOnParameter4|Ocorreu um erro ao carregar o atributo especificado no parâmetro especificado do método especificado no tipo especificado. Consulte InnerException para obter mais detalhes.|  
|SFxErrorReflectingOnType2|Ocorreu um erro ao carregar o atributo especificado no tipo especificado.  Consulte InnerException para obter mais detalhes.|  
|SFxErrorSerializingBody|Erro ao serializar o corpo da mensagem especificada. Consulte InnerException para obter mais detalhes.|  
|SFxErrorSerializingHeader|Ocorreu um erro ao serializar um dos cabeçalhos na mensagem especificada. Consulte InnerException para obter mais detalhes.|  
|SFxExpectedIMethodCallMessage|Erro Interno. A mensagem deve ser um IMethodCallMessage válido.|  
|SFxExportMustHaveType|A parte especificada na operação especificada não pode ser exportada porque não tem um tipo CLR válido.|  
|SFxHeaderNotUnderstood|A mensagem não foi processada. O cabeçalho especificado do namespace especificado não foi compreendido pelo destinatário desta mensagem. Esse erro normalmente indica que o remetente desta mensagem habilitou um protocolo de comunicação que o receptor não pode processar. Verifique se a configuração da associação do cliente é consistente com a associação do serviço.|  
|SFxHeadersAreNotSupportedInEncoded|A mensagem especificada não deve ter cabeçalhos a serem usados no estilo codificado de chamada de procedimento remoto.|  
|SFxInconsistentWsdlOperationStyleInMessageParts|Todas as partes da mensagem na operação especificada devem conter um tipo ou um elemento.|  
|SFxInconsistentWsdlOperationStyleInOperationMessages|O estilo especificado inferido das mensagens na operação especificada não corresponde ao estilo esperado especificado usando associações.|  
|SFxInvalidCallbackIAsyncResult|IAsyncResult não fornecido ou é do tipo incorreto.|  
|SFxInvalidMessageBody|O OperationFormatter encontrou um corpo de mensagem inválido. O tipo de nó ' element ' com o nome e o namespace especificados era esperado. O tipo de nó especificado com o nome e o namespace especificados foi encontrado.|  
|SFxInvalidMessageBodyEmptyMessage|O OperationFormatter não pode desserializar nenhuma informação da mensagem porque a mensagem está vazia.|  
|SFxInvalidMessageBodyErrorDeserializingParameter|Ocorreu um erro ao tentar desserializar o parâmetro especificado. Consulte InnerException para obter mais informações.|  
|SFxInvalidMessageBodyErrorSerializingParameter|Ocorreu um erro ao tentar serializar o parâmetro especificado. A mensagem InnerException foi especificada.  Consulte InnerException para obter mais detalhes.|  
|SFxInvalidMessageBodyUnexpectedNode|Encontrado o nó inesperado especificado, do namespace especificado durante a desserialização de parâmetros.|  
|SFxInvalidMessageContractSignature|A operação especificada tem um parâmetro ou um tipo de retorno marcado com MessageContractAttribute. Ao usar um contrato de mensagem para representar uma mensagem de solicitação, a operação deve ter um único parâmetro marcado com o MessageContractAttribute. Ao usar um contrato de mensagem para representar a mensagem de resposta, o valor de retorno da operação deve ser um tipo marcado com MessageContractAttribute. A operação não pode ter nenhum parâmetro ' out ' ou ' ref '.|  
|SFxInvalidReplyAction|A mensagem de resposta de saída para a operação tem a ação especificada, mas o contrato para essa operação especifica outra ReplyAction. A ação especificada na mensagem deve corresponder à ReplyAction no contrato ou o contrato de operação deve especificar ReplyAction = ' * '.|  
|SFxInvalidRequestAction|A mensagem de solicitação de saída para a operação tem a ação especificada, mas o contrato para essa operação especifica outra requestAction. A ação especificada na mensagem deve corresponder ao requestAction no contrato ou o contrato de operação deve especificar requestAction = ' * '.|  
|SFxInvalidStaticOverloadCalledForDuplexChannelFactory1|O método CreateChannel estático não pode ser usado com o contrato especificado porque esse contrato define um contrato de retorno de chamada. Use uma das sobrecargas de CreateChannel estáticos na DuplexChannelFactory \<TChannel> .|  
|SFxInvalidStreamInRequest|Para que a solicitação na operação especificada seja um fluxo, a operação deve ter um único parâmetro cujo tipo é Stream.|  
|SFxInvalidStreamInResponse|Para a resposta na operação especificada ser um fluxo, a operação deve ter um único parâmetro out ou um valor de retorno cujo tipo é Stream.|  
|SFxInvalidStreamInTypedMessage|Para usar fluxos com o modelo de programação de contrato de mensagem, o tipo especificado deve ter um único membro MessageBody cujo tipo é Stream.|  
|SFxInvalidUseOfPrimitiveOperationFormatter|O fornecido para PrimitiveOperationFormatter recebeu um parâmetro ou tipo de retorno para o qual ele não dá suporte.|  
|SFxMessageContractBaseTypeNotValid|O tipo especificado define um MessageContract e deriva de um tipo especificado que não define um MessageContract. Todos os objetos na hierarquia de herança especificada devem definir um MessageContract.|  
|SFxMethodNotSupported1|Não há suporte para o método especificado neste objeto. Isso pode acontecer se o método não estiver marcado com OperationContractAttribute ou se o tipo de interface não estiver marcado com ServiceContractAttribute.|  
|SFxMethodNotSupportedByType2|O tipo de implementação ServiceHost especificado não implementa o contrato de serviço especificado.|  
|SFxMethodNotSupportedOnCallback1|Não há suporte para o método de retorno de chamada especificado. Isso pode acontecer se o método não estiver marcado com OperationContractAttribute ou se seu tipo de interface não for o destino do ServiceContractAttribute CallbackContract.|  
|SFxMismatchedOperationParent|Uma DispatchOperation ou ClientOperation só pode ser adicionada a seu DispatchRuntime pai ou ClientRuntime, respectivamente.|  
|SFxNameCannotBeEmpty|A propriedade Name não pode ser uma cadeia de caracteres vazia.|  
|SfxNoTypeSpecifiedForParameter|Nenhum tipo CLR foi especificado para o parâmetro, o que impede que a operação seja gerada.|  
|SFxOperationBehaviorAttributeOnlyOnServiceClass|OperationBehaviorAttribute só pode ir para a classe de serviço. Ele não pode ser colocado na interface do ServiceContract. O método especificado no tipo especificado viola isso.|  
|SFxOperationContractOnNonServiceContract|O método especificado está marcado com OperationContractAttribute, mas o tipo especificado incluso não está marcado com ServiceContractAttribute. O OperationContractAttribute só pode ser usado em métodos em tipos ServiceContractAttribute ou em seus tipos CallbackContract.|  
|SFxParameterCountMismatch|Uma incompatibilidade entre o número de argumentos fornecidos e o número de argumentos esperados ocorreu. Especificamente, o argumento especificado tem o número especificado de elementos, enquanto o argumento esperado tem o número especificado de elementos.|  
|SFxPartNameMustBeUniqueInRpc|O nome da parte da mensagem especificada não é exclusivo em uma mensagem de chamada de procedimento remoto.|  
|SFxReplyActionMismatch3|Foi recebida uma mensagem de resposta para a operação especificada com a ação especificada. No entanto, o código do cliente requer a ação especificada.|  
|SFxRequestReplyNone|Foi recebida uma mensagem com um WS-Addressing cabeçalho ReplyTo ou FaultTo direcionado ao endereço "None". Esses valores não são válidos para operações de solicitação-resposta. Use uma operação unidirecional ou habilite ManualAddressing se você precisar oferecer suporte a valores de ReplyTo ou FaultTo de "None".|  
|SFxRequestTimedOut1|Esta operação de solicitação não recebeu uma resposta dentro do tempo configurado especificado. O tempo permitido pode ter sido parte de um tempo limite maior. Isso pode ocorrer porque o serviço ainda está processando a operação ou porque o serviço não pôde enviar uma mensagem de resposta.|  
|SFxRequestTimedOut2|A operação de solicitação enviada ao local especificado não recebeu uma resposta dentro do tempo configurado especificado. O tempo permitido pode ter sido parte de um tempo limite maior. Isso pode ocorrer porque o serviço ainda está processando a operação ou porque o serviço não pôde enviar uma mensagem de resposta.|  
|SFxSchemaDoesNotContainType|O esquema com o namespace de destino especificado não contém um tipo com o nome especificado.|  
|SfxServiceContractAttributeNotFound|O tipo de contrato especificado não é atribuído com ServiceContractAttribute. Para definir um contrato válido, o tipo especificado deve ser atribuído com ServiceContractAttribute. O tipo pode ser uma interface de contrato ou uma classe de serviço.|  
|SFxServiceContractGeneratorConfigRequired|Para gerar informações de configuração usando o método GenerateServiceEndpoint, a instância ServiceContractGenerator deve ser inicializada com um objeto de configuração válido.|  
|SFxServiceHostBaseCannotAddEndpointAfterOpen|Os pontos de extremidade não podem ser adicionados depois que o ServiceHost está em um dos seguintes Estados:<br /><br /> -Aberto<br />-Com falha<br />-Encerrado<br />-Fechado|  
|SFxServiceHostBaseCannotAddEndpointWithoutDescription|Os pontos de extremidade não podem ser adicionados antes que a propriedade Description seja inicializada.|  
|SFxServiceMetadataBehaviorNoHttpBaseAddress|A propriedade HttpGetEnabled de ServiceMetadataBehavior é definida como true e a propriedade HttpGetUrl é um endereço relativo, mas não há nenhum endereço base HTTP. Forneça um endereço base HTTP ou defina HttpGetUrl como um endereço absoluto.|  
|SFxServiceMetadataBehaviorNoHttpsBaseAddress|A propriedade HttpsGetEnabled de ServiceMetadataBehavior é definida como true e a propriedade HttpsGetUrl é um endereço relativo, mas não há nenhum endereço base HTTPS. Forneça um endereço base HTTPS ou defina HttpsGetUrl como um endereço absoluto.|  
|SFxServiceMetadataBehaviorUrlMustBeHttpOrRelative|A URL de comportamento deve ser um identificador de recurso uniforme relativo ou um identificador de recurso uniforme absoluto com o esquema especificado. A URL especificada é um identificador de recurso uniforme absoluto com o esquema especificado.|  
|SFxStreamRequestMessageClosed|A mensagem que contém este fluxo foi fechada. Os fluxos de solicitação não podem ser acessados depois que a operação de serviço retorna.|  
|SFxStreamResponseMessageClosed|A mensagem que contém este fluxo foi fechada.|  
|SFxTerminateRequestProcessingException|Uma extensão no pipeline de operação deve sair do processamento desta mensagem.|  
|SFxTerminatingOperationAlreadyCalled1|Este canal não pode enviar mais mensagens porque a operação istermination foi chamada.|  
|SFxThrottleLimitMustBeGreaterThanZero0|O limite de limitação deve ser maior que zero. Para desabilitar o limite de limitação, defina o valor como Int32. MaxValue.|  
|SFxTypedOrUntypedMessageCannotBeMixedWithVoidInRpc|Ao usar o estilo codificado por RPC, os tipos de contrato de mensagem ou o tipo System. ServiceModel. Channels. Message não poderão ser usados se a operação não tiver parâmetros ou tiver um valor de retorno void. Adicione um tipo de contrato de mensagem em branco como um parâmetro ou tipo de retorno à operação especificada.|  
|SFxUserCodeThrewException|A operação de usuário especificada gerou uma exceção sem tratamento no código do usuário. Se esse for um problema recorrente, ele poderá indicar um erro na implementação do método especificado.|  
|SfxUseTypedMessageForCustomAttributes|O parâmetro especificado não pode ser mapeado para o parâmetro de operação porque ele requer atributos adicionais.|  
|SFxVersionMismatchInOperationContextAndMessage2|Não é possível adicionar cabeçalhos de saída à mensagem porque a MessageVersion em OperationContext. Current não corresponde à versão de cabeçalho da mensagem que está sendo processada|  
|SFxWellKnownNonSingleton0|Para usar um dos construtores ServiceHost que usa uma instância de serviço, o InstanceContextmode do serviço deve ser definido como InstanceContextmode. single. Isso pode ser configurado usando o ServiceBehaviorAttribute. Caso contrário, use os construtores ServiceHost que usam um argumento de tipo.|  
|SFxWrapperTypeHasMultipleNamespaces|O tipo de wrapper para a mensagem especificada não pode ser projetado como um tipo de contrato de dados porque ele tem vários namespaces. Use o XmlSerializer.|  
|UriMustBeAbsolute|O URI deve ser absoluto.|
