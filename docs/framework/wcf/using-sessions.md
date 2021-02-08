---
description: 'Saiba mais sobre: usando sessões'
title: Utilizando sessões
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- sessions [WCF]
ms.assetid: 864ba12f-3331-4359-a359-6d6d387f1035
ms.openlocfilehash: bd5fc82af9b613566885bcf27e659edc4ba0e579
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99778159"
---
# <a name="using-sessions"></a>Utilizando sessões

Em aplicativos Windows Communication Foundation (WCF), uma *sessão* correlaciona um grupo de mensagens em uma conversa. As sessões do WCF são diferentes do objeto de sessão disponível em aplicativos ASP.NET, dão suporte a comportamentos diferentes e são controladas de maneiras diferentes. Este tópico descreve os recursos que as sessões habilitam em aplicativos WCF e como usá-las.  
  
## <a name="sessions-in-windows-communication-foundation-applications"></a>Sessões em aplicativos Windows Communication Foundation  

 Quando um contrato de serviço especifica que ele requer uma sessão, esse contrato está especificando que todas as chamadas (ou seja, as trocas de mensagens subjacentes que dão suporte às chamadas) devem fazer parte da mesma conversa. Se um contrato especifica que ele permite sessões, mas não requer uma, os clientes podem se conectar e estabelecer uma sessão ou não estabelecer uma sessão. Se a sessão terminar e uma mensagem for enviada por meio do mesmo canal, uma exceção será lançada.  
  
 As sessões do WCF têm os seguintes recursos conceituais principais:  
  
- Elas são explicitamente iniciadas e terminadas pelo aplicativo de chamada (o cliente WCF).  
  
- As mensagens entregues durante uma sessão são processadas na ordem em que são recebidas.  
  
- As sessões correlacionam um grupo de mensagens em uma conversa. Diferentes tipos de correlação são possíveis. Por exemplo, um canal baseado em sessão pode correlacionar mensagens com base em uma conexão de rede compartilhada enquanto outro canal baseado em sessão pode correlacionar mensagens com base em uma marca compartilhada no corpo da mensagem. Os recursos que podem ser derivados da sessão dependem da natureza da correlação.  
  
- Não há nenhum repositório de dados geral associado a uma sessão WCF.  
  
 Se você estiver familiarizado com a <xref:System.Web.SessionState.HttpSessionState?displayProperty=nameWithType> classe em aplicativos ASP.net e a funcionalidade que ele fornece, você poderá observar as seguintes diferenças entre esse tipo de sessão e sessões do WCF:  
  
- As sessões ASP.NET são sempre iniciadas pelo servidor.  
  
- As sessões ASP.NET são implicitamente desordenadas.  
  
- As sessões ASP.NET fornecem um mecanismo de armazenamento de dados geral entre solicitações.  
  
 Este tópico descreve:  
  
- O comportamento de execução padrão ao usar associações baseadas em sessão na camada do modelo de serviço.  
  
- Os tipos de recursos fornecidos pelas associações baseadas em sessão do WCF, fornecidas pelo sistema.  
  
- Como criar um contrato que declara um requisito de sessão.  
  
- Como entender e controlar a criação e o encerramento da sessão e a relação da sessão com a instância do serviço.  
  
## <a name="default-execution-behavior-using-sessions"></a>Comportamento de execução padrão usando sessões  

 Uma associação que tenta iniciar uma sessão é chamada de associação *baseada em sessão* . Os contratos de serviço especificam que eles exigem, permitem ou recusam associações baseadas em sessão definindo a <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType> Propriedade na interface do contrato de serviço (ou classe) como um dos <xref:System.ServiceModel.SessionMode?displayProperty=nameWithType> valores de enumeração. Por padrão, o valor dessa propriedade é <xref:System.ServiceModel.SessionMode.Allowed> , o que significa que, se um cliente usar uma associação baseada em sessão com uma implementação de serviço WCF, o serviço estabelecerá e usará a sessão fornecida.  
  
 Quando um serviço WCF aceita uma sessão de cliente, os seguintes recursos são habilitados por padrão:  
  
1. Todas as chamadas entre um objeto de cliente WCF são manipuladas pela mesma instância de serviço.  
  
2. Associações baseadas em sessão diferentes fornecem recursos adicionais.  
  
## <a name="system-provided-session-types"></a>Tipos de sessão de System-Provided  

 Uma associação baseada em sessão dá suporte à associação padrão de uma instância de serviço com uma sessão específica. No entanto, associações baseadas em sessão diferentes dão suporte a diferentes recursos, além de habilitar o controle de instanciação baseado em sessão descrito anteriormente.  
  
 O WCF fornece os seguintes tipos de comportamento de aplicativo baseado em sessão:  
  
- O <xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=nameWithType> oferece suporte a sessões baseadas em segurança, nas quais ambas as extremidades da comunicação têm acordado uma conversa segura específica. Para obter mais informações, consulte [Securing Services](securing-services.md). Por exemplo, a <xref:System.ServiceModel.WSHttpBinding?displayProperty=nameWithType> associação, que contém suporte para sessões de segurança e sessões confiáveis, por padrão usa apenas uma sessão segura que criptografa e assina digitalmente as mensagens.  
  
- A <xref:System.ServiceModel.NetTcpBinding?displayProperty=nameWithType> Associação dá suporte a sessões baseadas em TCP/IP para garantir que todas as mensagens sejam correlacionadas pela conexão no nível do soquete.  
  
- O <xref:System.ServiceModel.Channels.ReliableSessionBindingElement?displayProperty=nameWithType> elemento, que implementa a especificação de WS-ReliableMessaging, fornece suporte para sessões confiáveis nas quais as mensagens podem ser configuradas para serem entregues em ordem e exatamente uma vez, garantindo que as mensagens sejam recebidas mesmo quando as mensagens viajam por vários nós durante a conversa. Para obter mais informações, consulte [sessões confiáveis](./feature-details/reliable-sessions.md).  
  
- A <xref:System.ServiceModel.NetMsmqBinding?displayProperty=nameWithType> associação fornece sessões de datagrama MSMQ. Para obter mais informações, consulte [filas no WCF](./feature-details/queues-in-wcf.md).  
  
 Definir a <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> propriedade não especifica o tipo de sessão que o contrato requer, apenas que ele requer um.  
  
## <a name="creating-a-contract-that-requires-a-session"></a>Criando um contrato que requer uma sessão  

 A criação de um contrato que requer uma sessão declara que o grupo de operações que o contrato de serviço declara deve ser executado dentro da mesma sessão e que as mensagens devem ser entregues em ordem. Para declarar o nível de suporte de sessão que um contrato de serviço requer, defina a <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=nameWithType> Propriedade na sua interface de contrato de serviço ou classe como o valor da <xref:System.ServiceModel.SessionMode?displayProperty=nameWithType> enumeração para especificar se o contrato:  
  
- Requer uma sessão.  
  
- Permite que um cliente estabeleça uma sessão.  
  
- Proíbe uma sessão.  
  
 <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A>No entanto, definir a propriedade não especifica o tipo de comportamento baseado em sessão que o contrato requer. Ele instrui o WCF a confirmar em tempo de execução que a associação configurada (que cria o canal de comunicação) para o serviço faz, não pode estabelecer uma sessão ao implementar um serviço. Novamente, a associação pode atender a esse requisito com qualquer tipo de comportamento baseado em sessão que ele escolhe — segurança, transporte, confiável ou alguma combinação. O comportamento exato depende do <xref:System.ServiceModel.SessionMode?displayProperty=nameWithType> valor selecionado. Se a associação configurada do serviço não estiver de acordo com o valor de <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A> , uma exceção será lançada. Associações e os canais que eles criam que dão suporte a sessões são considerados baseados em sessão.  
  
 O contrato de serviço a seguir especifica que todas as operações no `ICalculatorSession` devem ser trocadas em uma sessão. Nenhuma das operações retorna um valor para o chamador, exceto o `Equals` método. No entanto, o `Equals` método não usa parâmetros e, portanto, pode retornar apenas um valor diferente de zero dentro de uma sessão na qual os dados já foram passados para as outras operações. Este contrato requer uma sessão para funcionar corretamente. Sem uma sessão associada a um cliente específico, a instância de serviço não tem como saber quais dados anteriores esse cliente enviou.  
  
 [!code-csharp[S_Service_Session#1](../../../samples/snippets/csharp/VS_Snippets_CFX/s_service_session/cs/service.cs#1)]
 [!code-vb[S_Service_Session#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_service_session/vb/service.vb#1)]  
  
 Se um serviço permitir uma sessão, uma sessão será estabelecida e usada se o cliente iniciar uma; caso contrário, nenhuma sessão será estabelecida.  
  
## <a name="sessions-and-service-instances"></a>Sessões e instâncias de serviço  

 Se você usar o comportamento de instanciação padrão no WCF, todas as chamadas entre um objeto de cliente WCF serão manipuladas pela mesma instância de serviço. Portanto, no nível do aplicativo, você pode considerar uma sessão como habilitar o comportamento do aplicativo semelhante ao comportamento de chamada local. Por exemplo, quando você cria um objeto local:  
  
- Um construtor é chamado.  
  
- Todas as chamadas subsequentes feitas à referência de objeto do cliente WCF são processadas pela mesma instância de objeto.  
  
- Um destruidor é chamado quando a referência do objeto é destruída.  
  
 As sessões permitem um comportamento semelhante entre clientes e serviços, contanto que o comportamento da instância de serviço padrão seja usado. Se um contrato de serviço exigir ou oferecer suporte a sessões, uma ou mais operações de contrato poderão ser marcadas como iniciando ou encerrando uma sessão definindo as <xref:System.ServiceModel.OperationContractAttribute.IsInitiating%2A> <xref:System.ServiceModel.OperationContractAttribute.IsTerminating%2A> Propriedades e.  
  
 *As operações de inicialização* são aquelas que devem ser chamadas como a primeira operação de uma nova sessão. Iniciar operações não pode ser chamado somente após pelo menos uma operação iniciando foi chamada. Portanto, você pode criar um tipo de construtor de sessão para seu serviço declarando operações de inicialização criadas para obter entrada de clientes apropriados para o início da instância do serviço. (No entanto, o estado é associado à sessão, e não ao objeto de serviço.)  
  
 *As operações de encerramento*, por outro lado, são aquelas que devem ser chamadas como a última mensagem em uma sessão existente. Em casos padrão, WCF recicla o objeto de serviço e seu contexto após a sessão com que o serviço foi associado é fechada. Você pode, portanto, criar um tipo de destruidor declarando operações de encerramento projetadas para executar uma função apropriada ao final da instância do serviço.  
  
> [!NOTE]
> Embora o comportamento padrão tenha uma aparência para construtores e destruidores locais, é apenas uma semelhança. Qualquer operação de serviço WCF pode ser uma operação de inicialização ou encerramento, ou ambas ao mesmo tempo. Além disso, no caso padrão, as operações de inicialização podem ser chamadas de qualquer número de vezes em qualquer ordem; nenhuma sessão adicional é criada depois que ela é estabelecida e associada a uma instância, a menos que você controle explicitamente o tempo de vida da instância do serviço (manipulando o <xref:System.ServiceModel.InstanceContext?displayProperty=nameWithType> objeto). Por fim, o estado é associado à sessão e não ao objeto de serviço.  
  
 Por exemplo, o `ICalculatorSession` contrato usado no exemplo anterior requer que o objeto cliente do WCF primeiro chame a `Clear` operação antes de qualquer outra operação e que a sessão com esse objeto cliente WCF seja encerrada quando chamar a `Equals` operação. O exemplo de código a seguir mostra um contrato que impõe esses requisitos. `Clear` deve ser chamado primeiro para iniciar uma sessão e essa sessão termina quando `Equals` é chamado.  
  
 [!code-csharp[SCA.IsInitiatingIsTerminating#1](../../../samples/snippets/csharp/VS_Snippets_CFX/sca.isinitiatingisterminating/cs/service.cs#1)]
 [!code-vb[SCA.IsInitiatingIsTerminating#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.isinitiatingisterminating/vb/service.vb#1)]  
  
 Os serviços não iniciam sessões com clientes. Em aplicativos cliente WCF, existe uma relação direta entre o tempo de vida do canal baseado em sessão e o tempo de vida da própria sessão. Dessa forma, os clientes criam novas sessões criando novos canais baseados em sessão e subdividindo sessões existentes fechando os canais baseados em sessão normalmente. Um cliente inicia uma sessão com um ponto de extremidade de serviço chamando um dos seguintes:  
  
- <xref:System.ServiceModel.ICommunicationObject.Open%2A?displayProperty=nameWithType> no canal retornado por uma chamada para <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType> .  
  
- <xref:System.ServiceModel.ClientBase%601.Open%2A?displayProperty=nameWithType> no objeto cliente do WCF gerado pela [ferramenta do utilitário de metadados ServiceModel (Svcutil.exe)](servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
- Uma operação de inicialização em qualquer tipo de objeto de cliente WCF (por padrão, todas as operações são iniciadas). Quando a primeira operação é chamada, o objeto cliente do WCF abre o canal automaticamente e inicia uma sessão.  
  
 Normalmente, um cliente encerra uma sessão com um ponto de extremidade de serviço chamando um dos seguintes:  
  
- <xref:System.ServiceModel.ICommunicationObject.Close%2A?displayProperty=nameWithType> no canal retornado por uma chamada para <xref:System.ServiceModel.ChannelFactory%601.CreateChannel%2A?displayProperty=nameWithType> .  
  
- <xref:System.ServiceModel.ClientBase%601.Close%2A?displayProperty=nameWithType> no objeto cliente do WCF gerado por Svcutil.exe.  
  
- Uma operação de encerramento em qualquer tipo de objeto de cliente do WCF (por padrão, nenhuma operação está sendo encerrada; o contrato deve especificar explicitamente uma Operation de encerramento). Quando a primeira operação é chamada, o objeto cliente do WCF abre o canal automaticamente e inicia uma sessão.  
  
 Para obter exemplos, consulte [como criar um serviço que requer sessões](./feature-details/how-to-create-a-service-that-requires-sessions.md) , bem como o [comportamento do serviço padrão](./samples/default-service-behavior.md) e amostras de [instanciação](./samples/instancing.md) .  
  
 Para obter mais informações sobre clientes e sessões, consulte [acessando serviços usando um cliente WCF](./feature-details/accessing-services-using-a-client.md).  
  
## <a name="sessions-interact-with-instancecontext-settings"></a>Sessões interagem com configurações de InstanceContext  

 Há uma interação entre a <xref:System.ServiceModel.SessionMode> enumeração em um contrato e a <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=nameWithType> propriedade, que controla a associação entre canais e objetos de serviço específicos. Para obter mais informações, consulte [sessões, instanciação e simultaneidade](./feature-details/sessions-instancing-and-concurrency.md).  
  
### <a name="sharing-instancecontext-objects"></a>Compartilhando objetos InstanceContext  

 Você também pode controlar qual canal baseado em sessão ou chamada está associado a qual <xref:System.ServiceModel.InstanceContext> objeto executando essa associação por conta própria.
  
## <a name="sessions-and-streaming"></a>Sessões e streaming  

 Quando você tem uma grande quantidade de dados a serem transferidos, o modo de transferência de streaming no WCF é uma alternativa viável para o comportamento padrão de armazenamento em buffer e processamento de mensagens na memória em sua totalidade. Você pode obter um comportamento inesperado durante o streaming de chamadas com uma associação baseada em sessão. Todas as chamadas de streaming são feitas por um único canal (o canal de datagrama) que não oferece suporte a sessões mesmo que a associação que está sendo usada esteja configurada para usar sessões. Se vários clientes fizerem chamadas de streaming para o mesmo objeto de serviço em uma associação baseada em sessão, e o modo de simultaneidade do objeto de serviço for definido como único e seu modo de contexto de instância for definido como `PerSession` , todas as chamadas deverão passar pelo canal do datagrama e, portanto, apenas uma chamada será processada de cada vez. Um ou mais clientes podem atingir o tempo limite. Você pode contornar esse problema Configurando o objeto de serviço `InstanceContextMode` para `PerCall` ou a simultaneidade com vários.  
  
> [!NOTE]
> MaxConcurrentSessions não têm nenhum efeito nesse caso porque há apenas uma "sessão" disponível.  
  
## <a name="see-also"></a>Confira também

- <xref:System.ServiceModel.OperationContractAttribute.IsInitiating%2A>
- <xref:System.ServiceModel.OperationContractAttribute.IsTerminating%2A>
