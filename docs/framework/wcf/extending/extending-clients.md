---
description: 'Saiba mais sobre: estendendo clientes'
title: Estendendo clientes
ms.date: 03/30/2017
helpviewer_keywords:
- proxy extensions [WCF]
ms.assetid: 1328c61c-06e5-455f-9ebd-ceefb59d3867
ms.openlocfilehash: 259136b3d8c35c47edbab1badf55139eb315d2f5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99685745"
---
# <a name="extending-clients"></a>Estendendo clientes

Em um aplicativo de chamada, a camada de modelo de serviço é responsável pela conversão de invocações de método no código do aplicativo em mensagens de saída, enviando-as por push para os canais subjacentes, convertendo os resultados em valores de retorno e parâmetros de saída no código do aplicativo e retornando os resultados de volta para o chamador. As extensões de modelo de serviço modificam ou implementam o comportamento de execução ou de comunicação e os recursos que envolvem funcionalidade de cliente ou Dispatcher, comportamentos personalizados, interceptação de mensagem e de parâmetro e outras funcionalidades de extensibilidade.  
  
 Este tópico descreve como usar as <xref:System.ServiceModel.Dispatcher.ClientRuntime> classes e <xref:System.ServiceModel.Dispatcher.ClientOperation> em um aplicativo cliente Windows Communication Foundation (WCF) para modificar o comportamento de execução padrão de um cliente WCF ou interceptar ou modificar mensagens, parâmetros ou valores de retorno antes ou depois de enviá-los ou recuperá-los da camada de canal. Para obter mais informações sobre como estender o tempo de execução do serviço, consulte [estendendo expatchers](extending-dispatchers.md). Para obter mais informações sobre os comportamentos que modificam e inserem objetos de personalização no tempo de execução do cliente, consulte [Configurando e estendendo o tempo de execução com comportamentos](configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="clients"></a>Clientes  

 Em um cliente, um objeto de cliente do WCF ou canal de cliente converte invocações de método em mensagens de saída e mensagens de entrada para resultados de operação que são retornados para o aplicativo de chamada. (Para obter mais informações sobre tipos de cliente, consulte [arquitetura de cliente WCF](../feature-details/client-architecture.md).)  
  
 Os tipos de cliente do WCF têm tipos de tempo de execução que lidam com esse ponto de extremidade e funcionalidade de nível de operação. Quando um aplicativo chama uma operação, o <xref:System.ServiceModel.Dispatcher.ClientOperation> converte os objetos de saída em uma mensagem, os interceptadores de processos, confirma que a chamada de saída está em conformidade com o contrato de destino e distribui a mensagem de saída para o <xref:System.ServiceModel.Dispatcher.ClientRuntime> , que é responsável por criar e gerenciar canais de saída (e canais de entrada no caso de serviços duplex), lidando com o processamento de mensagens de saída extra (como modificação de cabeçalho), processar interceptadores de mensagens em ambas as direções e rotear chamadas duplex de entrada para o <xref:System.ServiceModel.Dispatcher.DispatchRuntime> objeto O <xref:System.ServiceModel.Dispatcher.ClientOperation> e o <xref:System.ServiceModel.Dispatcher.ClientRuntime> fornecem serviços semelhantes quando mensagens (incluindo falhas) são retornadas ao cliente.  
  
 Essas duas classes de tempo de execução são a extensão principal para personalizar o processamento de canais e objetos de cliente WCF. A <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe permite que os usuários interceptem e estendam a execução do cliente em todas as mensagens no contrato. A <xref:System.ServiceModel.Dispatcher.ClientOperation> classe permite aos usuários interceptar e estender a execução do cliente para todas as mensagens em uma determinada operação.  
  
 A modificação das propriedades ou a inserção de personalizações é feita usando os comportamentos de contrato, ponto de extremidade e operação. Para obter mais informações sobre como usar esses tipos de comportamentos para executar personalizações de tempo de execução do cliente, consulte [Configurando e estendendo o tempo de execução com comportamentos](configuring-and-extending-the-runtime-with-behaviors.md).  
  
## <a name="scenarios"></a>Cenários  

 Há vários motivos para estender o sistema cliente, incluindo:  
  
- Validação de mensagem personalizada. Um usuário pode querer impor que uma mensagem seja válida para um determinado esquema. Isso pode ser feito implementando a <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> interface e atribuindo a implementação à <xref:System.ServiceModel.Dispatcher.DispatchRuntime.MessageInspectors%2A> propriedade. Para obter exemplos, consulte [como: inspecionar ou modificar mensagens no cliente](how-to-inspect-or-modify-messages-on-the-client.md) e [como inspecionar ou modificar mensagens no cliente](how-to-inspect-or-modify-messages-on-the-client.md).  
  
- Log de mensagens personalizado. Um usuário pode querer inspecionar e registrar um conjunto de mensagens de aplicativo que fluem por meio de um ponto de extremidade. Isso também pode ser feito com as interfaces do interceptador de mensagens.  
  
- Transformações de mensagens personalizadas. Em vez de modificar o código do aplicativo, o usuário pode querer aplicar determinadas transformações à mensagem no tempo de execução (por exemplo, para controle de versão). Isso pode ser feito, novamente, com as interfaces do interceptador de mensagens.  
  
- Modelo de dados personalizado. Um usuário pode querer ter um modelo de dados ou de serialização diferente daqueles com suporte por padrão no WCF (a saber,, <xref:System.Runtime.Serialization.DataContractSerializer?displayProperty=nameWithType> <xref:System.Xml.Serialization.XmlSerializer?displayProperty=nameWithType> e <xref:System.ServiceModel.Channels.Message?displayProperty=nameWithType> objetos). Isso pode ser feito com a implementação das interfaces de formatadores de mensagem. Para obter mais informações, consulte <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=nameWithType> e a <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A?displayProperty=nameWithType> propriedade.  
  
- Validação de parâmetro personalizado. Um usuário pode querer impor que os parâmetros digitados sejam válidos (em oposição a XML). Isso pode ser feito usando as interfaces do Inspetor de parâmetro. Para obter um exemplo, consulte [How to: inspecionar ou modificar parâmetros](how-to-inspect-or-modify-parameters.md) ou [validação do cliente](../samples/client-validation.md).  
  
### <a name="using-the-clientruntime-class"></a>Usando a classe ClientRuntime  

 A <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe é um ponto de extensibilidade ao qual você pode adicionar objetos de extensão que interceptam mensagens e estendem o comportamento do cliente. Os objetos de interceptação podem processar todas as mensagens em um contrato específico, processar somente mensagens para operações específicas, executar a inicialização de canal personalizado e implementar outro comportamento de aplicativo cliente personalizado.  
  
- A <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A> propriedade retorna o objeto de tempo de execução de expedição para clientes de retorno de chamada iniciados pelo serviço.  
  
- A <xref:System.ServiceModel.Dispatcher.ClientRuntime.OperationSelector%2A> propriedade aceita um objeto seletor de operação personalizado.  
  
- A <xref:System.ServiceModel.Dispatcher.ClientRuntime.ChannelInitializers%2A> propriedade permite a adição de um inicializador de canal que pode inspecionar ou modificar o canal do cliente.  
  
- A <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> propriedade Obtém uma coleção de <xref:System.ServiceModel.Dispatcher.ClientOperation> objetos para os quais você pode adicionar interceptadores de mensagens personalizados que fornecem funcionalidade específica para as mensagens dessa operação.  
  
- A <xref:System.ServiceModel.Dispatcher.ClientRuntime.ManualAddressing%2A> propriedade permite que um aplicativo desative alguns cabeçalhos de endereçamento automáticos para controlar diretamente o endereçamento.  
  
- A <xref:System.ServiceModel.Dispatcher.ClientRuntime.Via%2A> propriedade define o valor do destino da mensagem no nível de transporte para dar suporte a intermediários e outros cenários.  
  
- A <xref:System.ServiceModel.Dispatcher.ClientRuntime.MessageInspectors%2A> propriedade Obtém uma coleção de <xref:System.ServiceModel.Dispatcher.IClientMessageInspector> objetos para os quais você pode adicionar interceptadores de mensagens personalizados para todas as mensagens viajando por meio de um cliente WCF.  
  
 Além disso, há várias outras propriedades que recuperam as informações de contrato:  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractName%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractNamespace%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.ContractClientType%2A>  
  
 Se o cliente WCF for um cliente do WCF duplex, as propriedades a seguir também recuperarão as informações de retorno de chamada do cliente WCF:  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackClientType%2A>  
  
- <xref:System.ServiceModel.Dispatcher.ClientRuntime.CallbackDispatchRuntime%2A>  
  
 Para estender a execução do cliente WCF em todo um cliente WCF, examine as propriedades disponíveis na <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe para ver se a modificação de uma propriedade ou a implementação de uma interface e a adição dela a uma propriedade cria a funcionalidade que você está procurando. Depois de escolher uma extensão específica para compilar, insira sua extensão na <xref:System.ServiceModel.Dispatcher.ClientRuntime> propriedade apropriada implementando um comportamento de cliente que fornece acesso à <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe quando invocada.  
  
 Você pode inserir objetos de extensão personalizados em uma coleção usando um comportamento de operação (um objeto que implementa <xref:System.ServiceModel.Description.IOperationBehavior> ), um comportamento de contrato (um objeto que implementa <xref:System.ServiceModel.Description.IContractBehavior> ) ou um comportamento de ponto de extremidade (um objeto que implementa <xref:System.ServiceModel.Description.IEndpointBehavior> ). O objeto de comportamento de instalação é adicionado à coleção apropriada de comportamentos de forma programática, declarativamente (Implementando um atributo personalizado) ou implementando um <xref:System.ServiceModel.Configuration.BehaviorExtensionElement> objeto personalizado para permitir que o comportamento seja inserido usando um arquivo de configuração de aplicativo. Para obter detalhes, consulte [Configurando e estendendo o tempo de execução com comportamentos](configuring-and-extending-the-runtime-with-behaviors.md).  
  
 Para obter exemplos que demonstram a interceptação em um cliente WCF, consulte [como inspecionar ou modificar mensagens no cliente](how-to-inspect-or-modify-messages-on-the-client.md).  
  
### <a name="using-the-clientoperation-class"></a>Usando a classe ClientOperation  

 A <xref:System.ServiceModel.Dispatcher.ClientOperation> classe é o local para as modificações de tempo de execução do cliente e o ponto de inserção para extensões personalizadas com escopo para apenas uma operação de serviço. (Para modificar o comportamento de tempo de execução do cliente para todas as mensagens em um contrato, use a <xref:System.ServiceModel.Dispatcher.ClientRuntime> classe.)  
  
 Use a <xref:System.ServiceModel.Dispatcher.ClientRuntime.Operations%2A> propriedade para localizar o <xref:System.ServiceModel.Dispatcher.ClientOperation> objeto que representa uma operação de serviço específica. As propriedades a seguir permitem que você insira objetos personalizados no sistema cliente WCF:  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> propriedade para inserir uma <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> implementação personalizada para uma operação ou modificar o formatador atual.  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.ParameterInspectors%2A> propriedade para inserir uma <xref:System.ServiceModel.Dispatcher.IParameterInspector> implementação personalizada ou para modificar a atual.  
  
 As propriedades a seguir permitem que você modifique o sistema em interação com o formatador e inspetores de parâmetro personalizados:  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.SerializeRequest%2A> propriedade para controlar a serialização de uma mensagem de saída.  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.DeserializeReply%2A> propriedade para controlar a desserialização de uma mensagem de entrada.  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.Action%2A> propriedade para controlar a ação de WS-Addressing da mensagem de solicitação.  
  
- Use o <xref:System.ServiceModel.Dispatcher.ClientOperation.BeginMethod%2A> e <xref:System.ServiceModel.Dispatcher.ClientOperation.EndMethod%2A> para especificar quais métodos de cliente WCF estão associados a uma operação assíncrona.  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.FaultContractInfos%2A> propriedade para obter uma coleção que contém os tipos que podem aparecer em falhas de SOAP como o tipo de detalhe.  
  
- Use as <xref:System.ServiceModel.Dispatcher.ClientOperation.IsInitiating%2A> <xref:System.ServiceModel.Dispatcher.ClientOperation.IsTerminating%2A> Propriedades e para controlar se uma sessão é iniciada ou interrompida, respectivamente, quando a operação é chamada.  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.IsOneWay%2A> propriedade para controlar se a operação é uma operação unidirecional.  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.Parent%2A> propriedade para obter o <xref:System.ServiceModel.Dispatcher.ClientRuntime> objeto recipiente.  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.Name%2A> propriedade para obter o nome da operação.  
  
- Use a <xref:System.ServiceModel.Dispatcher.ClientOperation.SyncMethod%2A> propriedade para controlar qual método é mapeado para a operação.  
  
 Para estender a execução do cliente do WCF em apenas uma operação de serviço, examine as propriedades disponíveis na <xref:System.ServiceModel.Dispatcher.ClientOperation> classe para ver se a modificação de uma propriedade ou a implementação de uma interface e como adicioná-la a uma propriedade cria a funcionalidade que você está procurando. Depois de escolher uma extensão específica para compilar, insira sua extensão na <xref:System.ServiceModel.Dispatcher.ClientOperation> propriedade apropriada implementando um comportamento de cliente que fornece acesso à <xref:System.ServiceModel.Dispatcher.ClientOperation> classe quando invocada. Dentro desse comportamento, você pode modificar a <xref:System.ServiceModel.Dispatcher.ClientRuntime> propriedade de acordo com seus requisitos.  
  
 Normalmente, a implementação de um comportamento de operação (um objeto que implementa a <xref:System.ServiceModel.Description.IOperationBehavior> interface) é suficiente, mas você também pode usar comportamentos de ponto de extremidade e comportamentos de contrato para realizar a mesma localização, localizando o <xref:System.ServiceModel.Description.OperationDescription> para uma operação específica e anexando o comportamento lá. Para obter detalhes, consulte [Configurando e estendendo o tempo de execução com comportamentos](configuring-and-extending-the-runtime-with-behaviors.md).  
  
 Para usar o comportamento personalizado da configuração, instale seu comportamento usando um manipulador de seção de configuração de comportamento personalizado. Você também pode instalar seu comportamento criando um atributo personalizado.  
  
 Para obter exemplos que demonstram a interceptação em um cliente WCF, consulte [How to: inspecionar ou modificar parâmetros](how-to-inspect-or-modify-parameters.md).  
  
## <a name="see-also"></a>Consulte também

- <xref:System.ServiceModel.Dispatcher.ClientRuntime>
- <xref:System.ServiceModel.Dispatcher.ClientOperation>
- [Como: inspecionar ou modificar mensagens no cliente](how-to-inspect-or-modify-messages-on-the-client.md)
- [Como: inspecionar ou modificar parâmetros](how-to-inspect-or-modify-parameters.md)
