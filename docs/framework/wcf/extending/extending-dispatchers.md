---
description: 'Saiba mais sobre: estendendo expatchers'
title: Estendendo distribuidores
ms.date: 03/30/2017
helpviewer_keywords:
- dispatcher extensions [WCF]
ms.assetid: d0ad15ac-fa12-4f27-80e8-7ac2271e5985
ms.openlocfilehash: 22be85c57439a88746e3e87625472d02ab412c1d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99735277"
---
# <a name="extending-dispatchers"></a>Estendendo distribuidores

Os despachantes são responsáveis por extrair mensagens de entrada dos canais subjacentes, traduzi-las em invocações de método no código do aplicativo e enviar os resultados de volta para o chamador. As extensões do Dispatcher permitem que você modifique esse processamento.  Você pode implementar os inspetores de mensagem ou de parâmetro que inspecionam ou modificam o conteúdo de mensagens ou parâmetros.  Você pode alterar a maneira como as mensagens são roteadas para operações ou fornecer outras funcionalidades.

Este tópico descreve como usar as <xref:System.ServiceModel.Dispatcher.DispatchRuntime> classes e <xref:System.ServiceModel.Dispatcher.DispatchOperation> em um aplicativo de serviço Windows Communication Foundation (WCF) para modificar o comportamento de execução padrão de um Dispatcher ou para interceptar ou modificar mensagens, parâmetros ou valores de retorno antes ou depois de enviá-los ou recuperá-los da camada de canal. Para obter mais informações sobre o processamento de mensagens de tempo de execução de cliente equivalente, consulte [estendendo clientes](extending-clients.md). Para entender a função que os <xref:System.ServiceModel.IExtensibleObject%601> tipos desempenham no acesso ao estado compartilhado entre vários objetos de personalização de tempo de execução, consulte [objetos extensíveis](extensible-objects.md).

## <a name="dispatchers"></a>Dispatchers

A camada modelo de serviço executa a conversão entre o modelo de programação do desenvolvedor e a troca de mensagens subjacente, normalmente chamada de camada de canal. No WCF, os despachantes de canal e ponto de extremidade ( <xref:System.ServiceModel.Dispatcher.ChannelDispatcher> e <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> , respectivamente) são os componentes de serviço responsáveis por aceitar novos canais, receber mensagens, despacho de operação e invocação e processamento de resposta. Os objetos Dispatcher são objetos receptores, mas as implementações de contrato de retorno de chamada em serviços duplex também expõem seus objetos Dispatcher para inspeção, modificação ou extensão.

O Dispatcher do canal (e Companion <xref:System.ServiceModel.Channels.IChannelListener> ) efetua pull de mensagens do canal em questão e passa as mensagens para seus respectivos distribuidores de ponto de extremidade. Cada Dispatcher de ponto de extremidade tem um <xref:System.ServiceModel.Dispatcher.DispatchRuntime> que roteia mensagens para o apropriado <xref:System.ServiceModel.Dispatcher.DispatchOperation> , que é responsável por chamar o método que implementa a operação. Várias classes de extensão opcionais e obrigatórias são invocadas ao longo do caminho. Este tópico explica como essas partes se encaixam e como você pode modificar as propriedades e conectar seu próprio código para estender a funcionalidade base.

As propriedades do Dispatcher e os objetos de personalização modificados são inseridos usando objetos de comportamento de serviço, ponto de extremidade, contrato ou operação. Este tópico não descreve como usar comportamentos. Para obter mais informações sobre os tipos usados para inserir modificações do Dispatcher, consulte [Configurando e estendendo o tempo de execução com comportamentos](configuring-and-extending-the-runtime-with-behaviors.md).

O gráfico a seguir fornece uma exibição de alto nível dos itens arquitetônicos em um serviço.

![A arquitetura de tempo de execução de despacho](./media/wcfc-dispatchruntimearchc.gif "wcfc_DispatchRuntimeArchc")

### <a name="channel-dispatchers"></a>Distribuidores de canal

Um <xref:System.ServiceModel.Dispatcher.ChannelDispatcher> objeto é criado para associar um <xref:System.ServiceModel.Channels.IChannelListener> em um URI específico (chamado de URI de escuta) com uma instância de um serviço. Cada <xref:System.ServiceModel.ServiceHost> objeto pode ter muitos <xref:System.ServiceModel.Dispatcher.ChannelDispatcher> objetos, cada um associado a apenas um ouvinte e um URI de escuta. Quando uma mensagem chega, o <xref:System.ServiceModel.Dispatcher.ChannelDispatcher> consulta cada um dos <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> objetos associados se o ponto de extremidade pode aceitar a mensagem e passa a mensagem para aquela que pode.

Todas as propriedades que controlam o tempo de vida e o comportamento de uma sessão de canal estão disponíveis para inspeção ou modificação no <xref:System.ServiceModel.Dispatcher.ChannelDispatcher> objeto. Isso inclui inicializadores de canal personalizados, o ouvinte de canal, o host, o associado <xref:System.ServiceModel.InstanceContext> e assim por diante.

### <a name="endpoint-dispatchers"></a>Despachantes de ponto de extremidade

O <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> objeto é responsável por processar mensagens de um <xref:System.ServiceModel.Dispatcher.ChannelDispatcher> quando o endereço de destino de uma mensagem corresponde a <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> e a ação da mensagem corresponde à <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> propriedade. Se dois <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> objetos puderem aceitar uma mensagem, o <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.FilterPriority%2A> valor da propriedade determinará o ponto de extremidade de prioridade mais alta.

Use o <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> para adquirir os dois pontos principais de extensão do modelo de serviço – as <xref:System.ServiceModel.Dispatcher.DispatchRuntime> <xref:System.ServiceModel.Dispatcher.DispatchOperation> classes e – que você pode usar para personalizar o processamento do Dispatcher. A <xref:System.ServiceModel.Dispatcher.DispatchRuntime> classe permite que os usuários interceptem e estendam o Dispatcher no escopo do contrato (ou seja, para todas as mensagens em um contrato). A <xref:System.ServiceModel.Dispatcher.DispatchOperation> classe permite que os usuários interceptem e estendam o Dispatcher em um escopo de operação (ou seja, para todas as mensagens em uma operação).

## <a name="scenarios"></a>Cenários

Há vários motivos para estender o Dispatcher:

- Validação de mensagem personalizada. Os usuários podem impor que uma mensagem seja válida para um determinado esquema. Isso pode ser feito com a implementação das interfaces do interceptador de mensagens. Para obter um exemplo, consulte [inspetores de mensagem](../samples/message-inspectors.md).

- Log de mensagens personalizado. Os usuários podem inspecionar e registrar um conjunto de mensagens de aplicativo que fluem por meio de um ponto de extremidade. Isso também pode ser feito com as interfaces do interceptador de mensagens.

- Transformações de mensagens personalizadas. Os usuários podem aplicar determinadas transformações à mensagem no tempo de execução (por exemplo, para controle de versão). Isso pode ser feito, novamente, com as interfaces do interceptador de mensagens.

- Modelo de dados personalizado. Os usuários podem ter um modelo de serialização de dados diferente daqueles com suporte por padrão no WCF (a saber,,, <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> e mensagens brutas). Isso pode ser feito implementando as interfaces de formatador de mensagem. Para obter um exemplo, consulte [formatador de operação e seletor de operação](../samples/operation-formatter-and-operation-selector.md).

- Validação de parâmetro personalizado. Os usuários podem impor que os parâmetros digitados sejam válidos (em oposição a XML). Isso pode ser feito usando as interfaces do Inspetor de parâmetro.

- Expedição da operação personalizada. Os usuários podem implementar a expedição em algo diferente de Action – por exemplo, no elemento body ou em uma propriedade de mensagem personalizada. Isso pode ser feito usando a <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> interface. Para obter um exemplo, consulte [formatador de operação e seletor de operação](../samples/operation-formatter-and-operation-selector.md).

- Pool de objetos. Os usuários podem agrupar instâncias em vez de alocar uma nova para cada chamada. Isso pode ser implementado usando as interfaces do provedor de instância. Para obter um exemplo, consulte [pooling](../samples/pooling.md).

- Concessão de instância. Os usuários podem implementar um padrão de concessão para o tempo de vida da instância, semelhante ao do .NET Framework comunicação remota. Isso pode ser feito usando as interfaces de tempo de vida do contexto de instância.

- Tratamento de erro personalizado. Os usuários podem controlar como os erros locais são processados e como as falhas são comunicadas de volta para os clientes. Isso pode ser implementado usando as <xref:System.ServiceModel.Dispatcher.IErrorHandler> interfaces do.

- Comportamentos de autorização personalizados. Os usuários podem implementar o controle de acesso personalizado estendendo as partes de tempo de execução do contrato ou da operação e adicionando verificações de segurança com base nos tokens presentes na mensagem. Isso pode ser feito usando as interfaces interceptador de mensagem ou interceptador de parâmetro. Para obter exemplos, consulte [extensibilidade de segurança](../samples/security-extensibility.md).

  > [!CAUTION]
  > Como alterar as propriedades de segurança tem o potencial de comprometer a segurança dos aplicativos WCF, é altamente recomendável que você realize modificações relacionadas à segurança com cuidado e teste exaustivamente antes da implantação.

- Validadores de tempo de execução WCF personalizados. Você pode instalar validadores personalizados que examinam serviços, contratos e associações para impor políticas de nível empresarial em relação a aplicativos WCF. (Por exemplo, consulte [como bloquear pontos de extremidade na empresa](how-to-lock-down-endpoints-in-the-enterprise.md).)

### <a name="using-the-dispatchruntime-class"></a>Usando a classe DispatchRuntime

Use a <xref:System.ServiceModel.Dispatcher.DispatchRuntime> classe para modificar o comportamento padrão de um serviço ou ponto de extremidade individual, ou para inserir objetos que implementam modificações personalizadas em um ou ambos os processos de serviço (ou processos de cliente no caso de um cliente duplex):

- A transformação de mensagens de entrada em objetos e a liberação desses objetos como invocações de método em um objeto de serviço.

- A transformação de objetos recebidos da resposta a uma invocação de operação de serviço em mensagens de saída.

O <xref:System.ServiceModel.Dispatcher.DispatchRuntime> permite interceptar e estender o canal ou Dispatcher de ponto de extremidade para todas as mensagens em um determinado contrato, mesmo quando uma mensagem não é reconhecida. Quando uma mensagem chega que não corresponde a nenhum declarado no contrato, ela é expedida para a operação retornada pela <xref:System.ServiceModel.Dispatcher.DispatchRuntime.UnhandledDispatchOperation%2A> propriedade. Para interceptar ou estender todas as mensagens para uma operação específica, consulte a <xref:System.ServiceModel.Dispatcher.DispatchOperation> classe.

Há quatro áreas principais da extensibilidade do Dispatcher expostas pela <xref:System.ServiceModel.Dispatcher.DispatchRuntime> classe:

1. Os componentes do canal usam as propriedades do <xref:System.ServiceModel.Dispatcher.DispatchRuntime> e do dispatcher do canal associado retornado pela <xref:System.ServiceModel.Dispatcher.DispatchRuntime.ChannelDispatcher%2A> propriedade para personalizar como o Dispatcher do canal aceita e fecha os canais. Essa categoria inclui as <xref:System.ServiceModel.Dispatcher.ChannelDispatcher.ChannelInitializers%2A> <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InputSessionShutdownHandlers%2A> Propriedades e.

2. Os componentes de mensagem são personalizados para cada mensagem processada. Essa categoria inclui as <xref:System.ServiceModel.Dispatcher.DispatchRuntime.MessageInspectors%2A> <xref:System.ServiceModel.Dispatcher.DispatchRuntime.OperationSelector%2A> Propriedades,, e <xref:System.ServiceModel.Dispatcher.DispatchRuntime.Operations%2A> <xref:System.ServiceModel.Dispatcher.ChannelDispatcher.ErrorHandlers%2A> .

3. Os componentes de instância personalizam a criação, o tempo de vida e a alienação de instâncias do tipo de serviço. Para obter mais informações sobre tempos de vida de objeto de serviço, consulte a <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> propriedade. Essa categoria inclui as <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextInitializers%2A> Propriedades e <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> .

4. Os componentes relacionados à segurança podem usar as seguintes propriedades:

    - <xref:System.ServiceModel.Dispatcher.DispatchRuntime.SecurityAuditLogLocation%2A> indica onde os eventos de auditoria são gravados.

    - <xref:System.ServiceModel.Dispatcher.DispatchRuntime.ImpersonateCallerForAllOperations%2A> controla se o serviço tenta representar usando as credenciais fornecidas pela mensagem de entrada.

    - <xref:System.ServiceModel.Dispatcher.DispatchRuntime.MessageAuthenticationAuditLevel%2A> controla se os eventos de autenticação de mensagem bem-sucedidos são gravados no log de eventos especificado por <xref:System.ServiceModel.Dispatcher.DispatchRuntime.SecurityAuditLogLocation%2A> .

    - <xref:System.ServiceModel.Dispatcher.DispatchRuntime.PrincipalPermissionMode%2A> controla como a <xref:System.Threading.Thread.CurrentPrincipal%2A> propriedade é definida.

    - <xref:System.ServiceModel.Dispatcher.DispatchRuntime.ServiceAuthorizationAuditLevel%2A> Especifica como a auditoria de eventos de autorização é executada.

    - <xref:System.ServiceModel.Dispatcher.DispatchRuntime.SuppressAuditFailure%2A> Especifica se é para suprimir exceções não críticas que ocorrem durante o processo de log.

Normalmente, os objetos de extensão personalizados são atribuídos a uma <xref:System.ServiceModel.Dispatcher.DispatchRuntime> propriedade ou inseridos em uma coleção por um comportamento de serviço (um objeto que implementa <xref:System.ServiceModel.Description.IServiceBehavior> ), um comportamento de contrato (um objeto que implementa <xref:System.ServiceModel.Description.IContractBehavior> ) ou um comportamento de ponto de extremidade (um objeto que implementa <xref:System.ServiceModel.Description.IEndpointBehavior> ). Em seguida, o objeto de comportamento de instalação é adicionado à coleção apropriada de comportamentos de forma programática ou implementando um <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> objeto personalizado para permitir que o comportamento seja inserido usando um arquivo de configuração de aplicativo.

Clientes duplex (clientes que implementam um contrato de retorno de chamada especificado por um serviço duplex) também têm um <xref:System.ServiceModel.Dispatcher.DispatchRuntime> objeto que pode ser acessado usando a <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A> propriedade.

### <a name="using-the-dispatchoperation-class"></a>Usando a classe DispatchOperation

A <xref:System.ServiceModel.Dispatcher.DispatchOperation> classe é o local para modificações de tempo de execução e o ponto de inserção para extensões personalizadas que têm o escopo para apenas uma operação de serviço. (Para modificar o comportamento de tempo de execução de serviço para todas as mensagens em um contrato, use a <xref:System.ServiceModel.Dispatcher.DispatchRuntime> classe.)

Instalar <xref:System.ServiceModel.Dispatcher.DispatchOperation> modificações usando um objeto de comportamento de serviço personalizado.

Use a <xref:System.ServiceModel.Dispatcher.DispatchRuntime.Operations%2A> propriedade para localizar o <xref:System.ServiceModel.Dispatcher.DispatchOperation> objeto que representa uma operação de serviço específica.

As propriedades a seguir controlam a execução do tempo de execução no nível da operação:

- As <xref:System.ServiceModel.Dispatcher.DispatchOperation.Action%2A> <xref:System.ServiceModel.Dispatcher.DispatchOperation.ReplyAction%2A> Propriedades,, <xref:System.ServiceModel.Dispatcher.DispatchOperation.FaultContractInfos%2A> ,, <xref:System.ServiceModel.Dispatcher.DispatchOperation.IsOneWay%2A> <xref:System.ServiceModel.Dispatcher.DispatchOperation.IsTerminating%2A> e <xref:System.ServiceModel.Dispatcher.DispatchOperation.Name%2A> obtêm os respectivos valores para a operação.

- O <xref:System.ServiceModel.Dispatcher.DispatchOperation.TransactionAutoComplete%2A> e <xref:System.ServiceModel.Dispatcher.DispatchOperation.TransactionRequired%2A> especificam o comportamento da transação.

- As <xref:System.ServiceModel.Dispatcher.DispatchOperation.ReleaseInstanceBeforeCall%2A> <xref:System.ServiceModel.Dispatcher.DispatchOperation.ReleaseInstanceAfterCall%2A> Propriedades e controlam o tempo de vida do objeto de serviço definido pelo usuário em relação ao <xref:System.ServiceModel.InstanceContext> .

- As <xref:System.ServiceModel.Dispatcher.DispatchOperation.DeserializeRequest%2A> <xref:System.ServiceModel.Dispatcher.DispatchOperation.SerializeReply%2A> Propriedades,, e <xref:System.ServiceModel.Dispatcher.DispatchOperation.Formatter%2A> permitem o controle explícito sobre a conversão de mensagens para objetos e objetos em mensagens.

- A <xref:System.ServiceModel.Dispatcher.DispatchOperation.Impersonation%2A> propriedade especifica o nível de representação da operação.

- A <xref:System.ServiceModel.Dispatcher.DispatchOperation.CallContextInitializers%2A> Propriedade insere extensões de contexto de chamada personalizadas para a operação.

- A <xref:System.ServiceModel.Dispatcher.DispatchOperation.AutoDisposeParameters%2A> propriedade controla quando objetos de parâmetro são destruídos.

- A <xref:System.ServiceModel.Dispatcher.DispatchOperation.Invoker%2A> propriedade para inserir um objeto chamador personalizado.

- A <xref:System.ServiceModel.Dispatcher.DispatchOperation.ParameterInspectors%2A> propriedade permite que você insira um inspetor de parâmetro personalizado que você pode usar para inspecionar ou modificar parâmetros e retornar valores.

## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Dispatcher.DispatchRuntime>
- <xref:System.ServiceModel.Dispatcher.DispatchOperation>
- [Como: inspecionar e modificar mensagens do serviço](how-to-inspect-and-modify-messages-on-the-service.md)
- [Como: inspecionar ou modificar parâmetros](how-to-inspect-or-modify-parameters.md)
- [Como: bloquear pontos de extremidade na empresa](how-to-lock-down-endpoints-in-the-enterprise.md)
