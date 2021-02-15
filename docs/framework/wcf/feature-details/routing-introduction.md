---
description: 'Saiba mais sobre: introdução ao roteamento'
title: Introdução ao roteamento
ms.date: 03/30/2017
ms.assetid: bf6ceb38-6622-433b-9ee7-f79bc93497a1
ms.openlocfilehash: 86f5b5dcc0bea067ac3dcfc8a87331da42c642aa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99779888"
---
# <a name="routing-introduction"></a>Introdução ao roteamento

O serviço de roteamento fornece um intermediário SOAP conectável genérico que é capaz de rotear mensagens com base no conteúdo da mensagem. Com o serviço de roteamento, você pode criar uma lógica de roteamento complexa que permite implementar cenários como agregação de serviço, controle de versão de serviço, roteamento prioritário e roteamento multicast. O serviço de roteamento também fornece tratamento de erros que permite configurar listas de pontos de extremidade de backup, para as quais as mensagens são enviadas se ocorrer uma falha ao enviar para o ponto de extremidade de destino primário.

Este tópico destina-se a novos para o serviço de roteamento e aborda a configuração básica e a hospedagem do serviço de roteamento.

## <a name="configuration"></a>Configuração

O serviço de roteamento é implementado como um serviço WCF que expõe um ou mais pontos de extremidade de serviço que recebem mensagens de aplicativos cliente e roteiam as mensagens para um ou mais pontos de extremidade de destino. O serviço fornece um <xref:System.ServiceModel.Routing.RoutingBehavior> , que é aplicado aos pontos de extremidade de serviço expostos pelo serviço. Esse comportamento é usado para configurar vários aspectos de como o serviço opera. Para facilitar a configuração ao usar um arquivo de configuração, os parâmetros são especificados no **RoutingBehavior**. Em cenários baseados em código, esses parâmetros seriam especificados como parte de um <xref:System.ServiceModel.Routing.RoutingConfiguration> objeto, que pode ser passado para um **RoutingBehavior**.

Ao iniciar, esse comportamento adiciona o <xref:System.ServiceModel.Routing.SoapProcessingBehavior> , que é usado para executar o processamento SOAP de mensagens para os pontos de extremidade do cliente. Isso permite que o serviço de roteamento transmita mensagens para pontos de extremidade que exigem uma **MessageVersion** diferente do ponto de extremidade em que a mensagem foi recebida. O **RoutingBehavior** também registra uma extensão de serviço, <xref:System.ServiceModel.Routing.RoutingExtension> que fornece um ponto de acessibilidade para modificar a configuração do serviço de roteamento em tempo de execução.

A classe **RoutingConfiguration** fornece um meio consistente de configurar e atualizar a configuração do serviço de roteamento.  Ele contém parâmetros que atuam como as configurações para o serviço de roteamento e são usados para configurar o **RoutingBehavior** quando o serviço é iniciado, ou é passado para o **RoutingExtension** para modificar a configuração de roteamento em tempo de execução.

A lógica de roteamento usada para executar o roteamento baseado em conteúdo de mensagens é definida por meio do agrupamento de vários <xref:System.ServiceModel.Dispatcher.MessageFilter> objetos juntos em filtrar tabelas ( <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> objetos). As mensagens de entrada são avaliadas em relação aos filtros de mensagem contidos na tabela de filtro e para cada **MessageFilter** que corresponde à mensagem, encaminhada para um ponto de extremidade de destino. A tabela de filtros que deve ser usada para rotear mensagens é especificada usando o **RoutingBehavior** na configuração ou por meio de código usando o objeto **RoutingConfiguration** .

### <a name="defining-endpoints"></a>Definindo pontos de extremidade

Embora possa parecer que você deve iniciar sua configuração definindo a lógica de roteamento que você usará, sua primeira etapa deve ser, na verdade, determinar a forma dos pontos de extremidade para os quais você irá rotear mensagens. O serviço de roteamento usa contratos que definem a forma dos canais usados para receber e enviar mensagens e, portanto, a forma do canal de entrada deve corresponder à do canal de saída.  Por exemplo, se você estiver Roteando para pontos de extremidade que usam a forma de canal de solicitação-resposta, deverá usar um contrato compatível nos pontos de extremidade de entrada, como o <xref:System.ServiceModel.Routing.IRequestReplyRouter> .

Isso significa que se os pontos de extremidade de destino usam contratos com vários padrões de comunicação (como a combinação de operações unidirecional e bidirecional), não é possível criar um ponto de extremidade de serviço único que possa receber e rotear mensagens para todos eles. Você deve determinar quais pontos de extremidade têm formas compatíveis e definir um ou mais pontos de extremidade de serviço que serão usados para receber mensagens a serem roteadas para os pontos de extremidade de destino.

> [!NOTE]
> Ao trabalhar com contratos que especificam vários padrões de comunicação (como uma combinação de operações unidirecionais e bidirecionais), uma solução alternativa é usar um contrato duplex no serviço de roteamento, como o <xref:System.ServiceModel.Routing.IDuplexSessionRouter> . No entanto, isso significa que a associação deve ser capaz de comunicação duplex, o que pode não ser possível para todos os cenários. Em cenários em que isso não é possível, considerar a comunicação em vários pontos de extremidade ou modificar o aplicativo pode ser necessário.

Para obter mais informações sobre contratos de roteamento, consulte [encaminhar contratos](routing-contracts.md).

Depois que o ponto de extremidade de serviço é definido, você pode usar o **RoutingBehavior** para associar um **RoutingConfiguration** específico ao ponto de extremidade. Ao configurar o serviço de roteamento usando um arquivo de configuração, o **RoutingBehavior** é usado para especificar a tabela de filtro que contém a lógica de roteamento usada para processar as mensagens recebidas nesse ponto de extremidade. Se você estiver configurando o serviço de roteamento programaticamente, poderá especificar a tabela de filtros usando o **RoutingConfiguration**.

O exemplo a seguir define os pontos de extremidade do serviço e do cliente que são usados pelo serviço de roteamento de forma programática e usando um arquivo de configuração.

```xml
<services>
  <!--ROUTING SERVICE -->
  <service behaviorConfiguration="routingData"
            name="System.ServiceModel.Routing.RoutingService">
    <host>
      <baseAddresses>
        <add baseAddress="http://localhost:8000/routingservice/router"/>
      </baseAddresses>
    </host>
    <!-- Define the service endpoints that are receive messages -->
    <endpoint address=""
              binding="wsHttpBinding"
              name="reqReplyEndpoint"
              contract="System.ServiceModel.Routing.IRequestReplyRouter" />
  </service>
</services>
<behaviors>
  <serviceBehaviors>
    <behavior name="routingData">
      <serviceMetadata httpGetEnabled="True"/>
      <!-- Add the RoutingBehavior and specify the Routing Table to use -->
      <routing filterTableName="routingTable1" />
    </behavior>
  </serviceBehaviors>
</behaviors>
<client>
<!-- Define the client endpoint(s) to route messages to -->
  <endpoint name="CalculatorService"
            address="http://localhost:8000/servicemodelsamples/service"
            binding="wsHttpBinding" contract="*" />
</client>
```

```csharp
//set up some communication defaults
string clientAddress = "http://localhost:8000/servicemodelsamples/service";
string routerAddress = "http://localhost:8000/routingservice/router";
Binding routerBinding = new WSHttpBinding();
Binding clientBinding = new WSHttpBinding();
//add the endpoint the router uses to receive messages
serviceHost.AddServiceEndpoint(
     typeof(IRequestReplyRouter),
     routerBinding,
     routerAddress);
//create the client endpoint the router routes messages to
ContractDescription contract = ContractDescription.GetContract(
     typeof(IRequestReplyRouter));
ServiceEndpoint client = new ServiceEndpoint(
     contract,
     clientBinding,
     new EndpointAddress(clientAddress));
//create a new routing configuration object
RoutingConfiguration rc = new RoutingConfiguration();
….
rc.FilterTable.Add(new MatchAllMessageFilter(), endpointList);
//attach the behavior to the service host
serviceHost.Description.Behaviors.Add(
     new RoutingBehavior(rc));
```

Este exemplo configura o serviço de roteamento para expor um único ponto de extremidade com um endereço de `http://localhost:8000/routingservice/router` , que é usado para receber mensagens a serem roteadas. Como as mensagens são roteadas para pontos de extremidade de solicitação-resposta, o ponto de extremidade de serviço usa o <xref:System.ServiceModel.Routing.IRequestReplyRouter> contrato. Essa configuração também define um único ponto de extremidade de cliente `http://localhost:8000/servicemodelsample/service` para o qual as mensagens são roteadas. A tabela de filtros (não mostrada) denominada "routingTable1" contém a lógica de roteamento usada para rotear mensagens e está associada ao ponto de extremidade de serviço usando o **RoutingBehavior** (para um arquivo de configuração) ou **RoutingConfiguration** (para configuração programática).

### <a name="routing-logic"></a>Lógica de roteamento

Para definir a lógica de roteamento usada para rotear mensagens, você deve determinar quais dados contidos nas mensagens de entrada podem ser tratados com exclusividade. Por exemplo, se todos os pontos de extremidade de destino que você está Roteando para compartilhar as mesmas ações SOAP, o valor da ação contida na mensagem não é um bom indicador de qual ponto de extremidade específico a mensagem deve ser roteada. Se você precisar rotear mensagens exclusivamente para um ponto de extremidade específico, filtre os dados que identificam exclusivamente o ponto de extremidade de destino para o qual a mensagem é roteada.

O serviço de roteamento fornece várias implementações **MessageFilter** que inspecionam valores específicos dentro da mensagem, como o endereço, a ação, o nome do ponto de extremidade ou até mesmo uma consulta XPath. Se nenhuma dessas implementações atender às suas necessidades, você poderá criar uma implementação de **MessageFilter** personalizada. Para obter mais informações sobre filtros de mensagens e uma comparação das implementações usadas pelo serviço de roteamento, consulte [filtros de mensagens](message-filters.md) e [escolhendo um filtro](choosing-a-filter.md).

Vários filtros de mensagens são organizados em conjunto em tabelas de filtro, que associam cada **MessageFilter** a um ponto de extremidade de destino. Opcionalmente, a tabela de filtros também pode ser usada para especificar uma lista de pontos de extremidade de backup para os quais o serviço de roteamento tentará enviar a mensagem no caso de uma falha de transmissão.

Por padrão, todos os filtros de mensagem em uma tabela de filtro são avaliados simultaneamente; no entanto, você pode especificar um <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement.Priority%2A> que faz com que os filtros de mensagem sejam avaliados em uma ordem específica. Todas as entradas com a prioridade mais alta são avaliadas primeiro, e os filtros de mensagens de prioridades inferiores não serão avaliados se uma correspondência for encontrada em um nível de prioridade mais alto. Para obter mais informações sobre as tabelas de filtro, consulte [filtros de mensagem](message-filters.md).

Os exemplos a seguir usam o <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> , que é avaliado como `true` para todas as mensagens. Esse **MessageFilter** é adicionado à tabela de filtro "routingTable1", que associa o **MessageFilter** ao ponto de extremidade do cliente chamado "CalculatorService". O **RoutingBehavior** então especifica que essa tabela deve ser usada para rotear mensagens processadas pelo ponto de extremidade de serviço.

```xml
<behaviors>
  <serviceBehaviors>
    <behavior name="routingData">
      <serviceMetadata httpGetEnabled="True"/>
      <!-- Add the RoutingBehavior and specify the Routing Table to use -->
      <routing filterTableName="routingTable1" />
    </behavior>
  </serviceBehaviors>
</behaviors>
<!--ROUTING SECTION -->
<routing>
  <filters>
    <filter name="MatchAllFilter1" filterType="MatchAll" />
  </filters>
  <filterTables>
    <table name="routingTable1">
      <filters>
        <add filterName="MatchAllFilter1" endpointName="CalculatorService" />
      </filters>
    </table>
  </filterTables>
</routing>
```

```csharp
//create a new routing configuration object
RoutingConfiguration rc = new RoutingConfiguration();
//create the endpoint list that contains the endpoints to route to
//in this case we have only one
List<ServiceEndpoint> endpointList = new List<ServiceEndpoint>();
endpointList.Add(client);
//add a MatchAll filter to the Router's filter table
//map it to the endpoint list defined earlier
//when a message matches this filter, it is sent to the endpoint contained in the list
rc.FilterTable.Add(new MatchAllMessageFilter(), endpointList);
```

> [!NOTE]
> Por padrão, o serviço de roteamento avalia apenas os cabeçalhos da mensagem. Para permitir que os filtros acessem o corpo da mensagem, você deve definir <xref:System.ServiceModel.Routing.RoutingConfiguration.RouteOnHeadersOnly%2A> como `false` .

**Multicast**

Embora muitas configurações de serviço de roteamento usem lógica de filtro exclusivo que roteia mensagens para apenas um ponto de extremidade específico, talvez seja necessário rotear uma determinada mensagem para vários pontos de extremidades de destino. Para multicast de uma mensagem para vários destinos, as seguintes condições devem ser verdadeiras:

- A forma de canal não deve ser solicitação-resposta (embora possa ser unidirecional ou duplex) porque apenas uma resposta pode ser recebida pelo aplicativo cliente em resposta à solicitação.

- Vários filtros devem retornar `true` ao avaliar a mensagem.

Se essas condições forem atendidas, a mensagem será roteada para todos os pontos de extremidade de todos os filtros que forem avaliados como `true` . O exemplo a seguir define uma configuração de roteamento que resulta em mensagens sendo roteadas para ambos os pontos de extremidade se o endereço do ponto final na mensagem for `http://localhost:8000/routingservice/router/rounding` .

```xml
<!--ROUTING SECTION -->
<routing>
  <filters>
    <filter name="MatchAllFilter1" filterType="MatchAll" />
    <filter name="RoundingFilter1" filterType="EndpointAddress"
            filterData="http://localhost:8000/routingservice/router/rounding" />
  </filters>
  <filterTables>
    <table name="routingTable1">
      <filters>
        <add filterName="MatchAllFilter1" endpointName="CalculatorService" />
        <add filterName="RoundingFilter1" endpointName="RoundingCalcService" />
      </filters>
    </table>
  </filterTables>
</routing>
```

```csharp
rc.FilterTable.Add(new MatchAllMessageFilter(), calculatorEndpointList);
rc.FilterTable.Add(new EndpointAddressMessageFilter(new EndpointAddress(
    "http://localhost:8000/routingservice/router/rounding")),
    roundingCalcEndpointList);
```

### <a name="soap-processing"></a>Processamento de SOAP

Para dar suporte ao roteamento de mensagens entre protocolos diferentes, o **RoutingBehavior** , por padrão, adiciona o <xref:System.ServiceModel.Routing.SoapProcessingBehavior> ao (s) ponto de extremidade de cliente para o qual as mensagens são roteadas. Esse comportamento cria automaticamente uma nova **MessageVersion** antes de rotear a mensagem para o ponto de extremidade, bem como criar uma **MessageVersion** compatível para qualquer documento de resposta antes de retorná-la para o aplicativo cliente solicitante.

As etapas tomadas para criar uma nova **MessageVersion** para a mensagem de saída são as seguintes:

**Processamento de solicitações**

- Obtenha a **MessageVersion** da Associação/canal de saída.

- Obtenha o leitor de corpo da mensagem original.

- Crie uma nova mensagem com a mesma ação, leitor de corpo e uma nova **MessageVersion**.

- Se <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> ! = **Addressing. None**, copie os cabeçalhos para, de, FaultTo e RelatesTo para a nova mensagem.

- Copie todas as propriedades de mensagem para a nova mensagem.

- Armazene a mensagem de solicitação original a ser usada ao processar a resposta.

- Retornar a nova mensagem de solicitação.

**Processamento de resposta**

- Obter a **MessageVersion** da mensagem de solicitação original.

- Obtenha o leitor de corpo da mensagem de resposta recebida.

- Crie uma nova mensagem de resposta com a mesma ação, leitor de corpo e **MessageVersion** da mensagem de solicitação original.

- Se <xref:System.ServiceModel.Channels.MessageVersion.Addressing%2A> ! = **Addressing. None**, copie os cabeçalhos para, de, FaultTo e RelatesTo para a nova mensagem.

- Copie as propriedades da mensagem para a nova mensagem.

- Retornar a nova mensagem de resposta.

Por padrão, o **SoapProcessingBehavior** é automaticamente adicionado aos pontos de extremidade do cliente pelo <xref:System.ServiceModel.Routing.RoutingBehavior> quando o serviço é iniciado; no entanto, você pode controlar se o processamento SOAP é adicionado a todos os pontos de extremidade do cliente usando a <xref:System.ServiceModel.Routing.RoutingConfiguration.SoapProcessingEnabled%2A> propriedade. Você também pode adicionar o comportamento diretamente a um ponto de extremidade específico e habilitar ou desabilitar esse comportamento no nível do ponto de extremidade, se um controle mais granular do processamento de SOAP for necessário.

> [!NOTE]
> Se o processamento de SOAP estiver desabilitado para um ponto de extremidade que exija uma MessageVersion diferente daquela da mensagem de solicitação original, você deverá fornecer um mecanismo personalizado para executar quaisquer modificações de SOAP necessárias antes de enviar a mensagem para o ponto de extremidade de destino.

Nos exemplos a seguir, a propriedade **soapProcessingEnabled** é usada para impedir que o **SoapProcessingBehavior** seja adicionado automaticamente a todos os pontos de extremidade do cliente.

```xml
<behaviors>
  <!--default routing service behavior definition-->
  <serviceBehaviors>
    <behavior name="routingConfiguration">
      <routing filterTableName="filterTable1" soapProcessingEnabled="false"/>
    </behavior>
  </serviceBehaviors>
</behaviors>
```

```csharp
//create the default RoutingConfiguration
RoutingConfiguration rc = new RoutingConfiguration();
rc.SoapProcessingEnabled = false;
```

### <a name="dynamic-configuration"></a>Configuração dinâmica

Quando você adiciona pontos de extremidade de cliente adicionais ou precisa modificar os filtros que são usados para rotear mensagens, você deve ter uma maneira de atualizar a configuração dinamicamente em tempo de execução para impedir a interrupção do serviço para os pontos de extremidade que estão recebendo mensagens no momento por meio do serviço de roteamento. Modificar um arquivo de configuração ou o código do aplicativo host nem sempre é suficiente, porque o método requer a reciclagem do aplicativo, o que levaria à perda potencial de todas as mensagens atualmente em trânsito e o potencial de tempo de inatividade enquanto aguardava a reinicialização do serviço.

Você só pode modificar o **RoutingConfiguration** de forma programática. Embora seja possível configurar inicialmente o serviço usando um arquivo de configuração, você só pode modificar a configuração em tempo de execução, construindo um novo **RoutingConfiguration** e passando-o como um parâmetro para o <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> método exposto pela <xref:System.ServiceModel.Routing.RoutingExtension> extensão de serviço. Todas as mensagens atualmente em trânsito continuam sendo roteadas usando a configuração anterior, enquanto as mensagens recebidas após a chamada para **ApplyConfiguration** usam a nova configuração. O exemplo a seguir demonstra como criar uma instância do serviço de roteamento e, em seguida, modificar a configuração posteriormente.

```csharp
RoutingConfiguration routingConfig = new RoutingConfiguration();
routingConfig.RouteOnHeadersOnly = true;
routingConfig.FilterTable.Add(new MatchAllMessageFilter(), endpointList);
RoutingBehavior routing = new RoutingBehavior(routingConfig);
routerHost.Description.Behaviors.Add(routing);
routerHost.Open();
// Construct a new RoutingConfiguration
RoutingConfiguration rc2 = new RoutingConfiguration();
ServiceEndpoint clientEndpoint = new ServiceEndpoint();
ServiceEndpoint clientEndpoint2 = new ServiceEndpoint();
// Add filters to the FilterTable in the new configuration
rc2.FilterTable.add(new MatchAllMessageFilter(),
       new List<ServiceEndpoint>() { clientEndpoint });
rc2.FilterTable.add(new MatchAllMessageFilter(),
       new List<ServiceEndpoint>() { clientEndpoint2 });
rc2.RouteOnHeadersOnly = false;
// Apply the new configuration to the Routing Service hosted in
routerHost.routerHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc2);
```

> [!NOTE]
> Ao atualizar o serviço de roteamento dessa maneira, só é possível passar por uma nova configuração. Não é possível modificar apenas os elementos Select da configuração atual ou acrescentar novas entradas à configuração atual; Você deve criar e passar uma nova configuração que substitua a existente.

> [!NOTE]
> Todas as sessões abertas usando a configuração anterior continuarão usando a configuração anterior. A nova configuração é usada somente por novas sessões.

## <a name="error-handling"></a>Tratamento de erros

Se algum <xref:System.ServiceModel.CommunicationException> for encontrado durante a tentativa de enviar uma mensagem, ocorrerá o tratamento de erros. Essas exceções normalmente indicam que um problema foi encontrado durante a tentativa de comunicação com o ponto de extremidade do cliente definido, como um <xref:System.ServiceModel.EndpointNotFoundException> , <xref:System.ServiceModel.ServerTooBusyException> ou <xref:System.ServiceModel.CommunicationObjectFaultedException> . O código de tratamento de erro também detectará e tentará repetir o envio quando <xref:System.TimeoutException> ocorrer, que é outra exceção comum que não é derivada de **CommunicationException**.

Quando uma das exceções anteriores ocorre, o serviço de roteamento faz failover para uma lista de pontos de extremidade de backup. Se todos os pontos de extremidade de backup falharem com uma falha de comunicação, ou se um EndPoint retornar uma exceção que indica uma falha no serviço de destino, o serviço de roteamento retornará uma falha ao aplicativo cliente.

> [!NOTE]
> A funcionalidade de tratamento de erros captura e manipula as exceções que ocorrem ao tentar enviar uma mensagem e ao tentar fechar um canal. O código de tratamento de erros não se destina a detectar ou tratar exceções criadas pelos pontos de extremidade do aplicativo com os quais ele está se comunicando; um <xref:System.ServiceModel.FaultException> gerado por um serviço aparece no serviço de roteamento como um **FaultMessage** e é transmitido de volta para o cliente.
>
> Se ocorrer um erro quando o serviço de roteamento tentar retransmitir uma mensagem, você poderá obter um <xref:System.ServiceModel.FaultException> no lado do cliente, em vez de um <xref:System.ServiceModel.EndpointNotFoundException> que normalmente obteria na ausência do serviço de roteamento. Um serviço de roteamento pode, portanto, mascarar exceções e não fornecer transparência total, a menos que você examine exceções aninhadas.

### <a name="tracing-exceptions"></a>Exceções de rastreamento

Ao enviar uma mensagem para um ponto de extremidade em uma lista falhar, o serviço de roteamento rastreará os dados de exceção resultantes e anexará os detalhes da exceção como uma propriedade de mensagem chamada **Exceptions**. Isso preserva os dados de exceção e permite que um usuário acesse o acesso programático por meio de um inspetor de mensagem.  Os dados de exceção são armazenados por mensagem em um dicionário que mapeia o nome do ponto de extremidade para os detalhes da exceção encontrados ao tentar enviar uma mensagem a ele.

### <a name="backup-endpoints"></a>Pontos de extremidade de backup

Cada entrada de filtro na tabela de filtros pode, opcionalmente, especificar uma lista de pontos de extremidade de backup, que são usados no caso de uma falha de transmissão ao enviar para o ponto final primário. Se essa falha ocorrer, o serviço de roteamento tentará transmitir a mensagem para a primeira entrada na lista de pontos de extremidade de backup. Se essa tentativa de envio também encontrar uma falha de transmissão, o próximo ponto de extremidade na lista de backup será tentado. O serviço de roteamento continua enviando a mensagem para cada ponto de extremidade na lista até que a mensagem seja recebida com êxito, todos os pontos de extremidade retornam uma falha de transmissão ou uma falha de não transmissão é retornada por um ponto de extremidades.

Os exemplos a seguir configuram o serviço de roteamento para usar uma lista de backup.

```xml
<routing>
  <filters>
    <!-- Create a MatchAll filter that catches all messages -->
    <filter name="MatchAllFilter1" filterType="MatchAll" />
  </filters>
  <filterTables>
    <!-- Set up the Routing Service's Message Filter Table -->
    <filterTable name="filterTable1">
        <!-- Add an entry that maps the MatchAllMessageFilter to the dead destination -->
        <!-- If that endpoint is down, tell the Routing Service to try the endpoints -->
        <!-- Listed in the backupEndpointList -->
        <add filterName="MatchAllFilter1" endpointName="deadDestination" backupList="backupEndpointList"/>
    </filterTable>
  </filterTables>
  <!-- Create the backup endpoint list -->
  <backupLists>
    <!-- Add an endpoint list that contains the backup destinations -->
    <backupList name="backupEndpointList">
      <add endpointName="realDestination" />
      <add endpointName="backupDestination" />
    </backupList>
  </backupLists>
</routing>
```

```csharp
//create the endpoint list that contains the service endpoints we want to route to
List<ServiceEndpoint> backupList = new List<ServiceEndpoint>();
//add the endpoints in the order that the Routing Service should contact them
//first add the endpoint that we know is down
//clearly, normally you wouldn't know that this endpoint was down by default
backupList.Add(fakeDestination);
//then add the real Destination endpoint
//the Routing Service attempts to send to this endpoint only if it
//encounters a TimeOutException or CommunicationException when sending
//to the previous endpoint in the list.
backupList.Add(realDestination);
//add the backupDestination endpoint
//the Routing Service attempts to send to this endpoint only if it
//encounters a TimeOutException or CommunicationsException when sending
//to the previous endpoints in the list
backupList.Add(backupDestination);
//create the default RoutingConfiguration option
RoutingConfiguration rc = new RoutingConfiguration();
//add a MatchAll filter to the Routing Configuration's filter table
//map it to the list of endpoints defined above
//when a message matches this filter, it is sent to the endpoints in the list in order
//if an endpoint is down or does not respond (which the first endpoint won't
//since the client does not exist), the Routing Service automatically moves the message
//to the next endpoint in the list and try again.
rc.FilterTable.Add(new MatchAllMessageFilter(), backupList);
```

### <a name="supported-error-patterns"></a>Padrões de erro com suporte

A tabela a seguir descreve os padrões que são compatíveis com o uso de listas de pontos de extremidade de backup, juntamente com observações que descrevem os detalhes da manipulação de erros para padrões específicos.

|Padrão|Sessão|Transação|Contexto de recebimento|Lista de backup com suporte|Observações|
|-------------|-------------|-----------------|---------------------|---------------------------|-----------|
|Unidirecional||||Sim|Tenta reenviar a mensagem em um ponto de extremidade de backup. Se essa mensagem estiver sendo multicast, somente a mensagem no canal com falha será movida para seu destino de backup.|
|Unidirecional||✔️||Não|Uma exceção é lançada e a transação é revertida.|
|Unidirecional|||✔️|Sim|Tenta reenviar a mensagem em um ponto de extremidade de backup. Depois que a mensagem for recebida com êxito, preencha todos os contextos de recebimento. Se a mensagem não for recebida com êxito por nenhum ponto de extremidade, não conclua o contexto de recebimento.<br /><br /> Quando essa mensagem estiver sendo multicast, o contexto de recebimento só será concluído se a mensagem for recebida com êxito por pelo menos um ponto de extremidade (primário ou backup). Se nenhum dos pontos de extremidade em nenhum dos caminhos de multicast receber a mensagem com êxito, não conclua o contexto de recebimento.|
|Unidirecional||✔️|✔️|Sim|Anule a transação anterior, crie uma nova transação e reenvie todas as mensagens. Mensagens que encontraram um erro são transmitidas para um destino de backup.<br /><br /> Após a criação de uma transação na qual todas as transmissões forem bem sucedidos, conclua os contextos de recebimento e confirme a transação.|
|Unidirecional|✔️|||Sim|Tenta reenviar a mensagem em um ponto de extremidade de backup. Em um cenário de multicast, somente as mensagens em uma sessão que encontraram um erro ou em uma sessão cujo fechamento de sessão falhou são reenviadas para os destinos de backup.|
|Unidirecional|✔️|✔️||Não|Uma exceção é lançada e a transação é revertida.|
|Unidirecional|✔️||✔️|Sim|Tenta reenviar a mensagem em um ponto de extremidade de backup. Depois que todos os envios de mensagem forem concluídos sem erros, a sessão indicará que não há mais mensagens e o serviço de roteamento fechará com êxito todos os canais de sessão de saída, todos os contextos de recebimento serão concluídos e o canal de sessão de entrada será fechado.|
|Unidirecional|✔️|✔️|✔️|Sim|Anule a transação atual e crie uma nova. Reenvie todas as mensagens anteriores na sessão. Depois que uma transação tiver sido criada na qual todas as mensagens foram enviadas com êxito e a sessão não indicar mais mensagens, todos os canais de sessão de saída serão fechados, os contextos de recebimento serão todos concluídos com a transação, o canal de sessão de entrada será fechado e a transação será confirmada.<br /><br /> Quando as sessões estão sendo multicast, as mensagens sem erros são reenviadas para o mesmo destino que antes e as mensagens que encontraram um erro são enviadas para os destinos de backup.|
|Two-Way||||Sim|Enviar para um destino de backup.  Depois que um canal retorna uma mensagem de resposta, retorne a resposta para o cliente original.|
|Two-Way|✔️|||Sim|Envie todas as mensagens no canal para um destino de backup.  Depois que um canal retorna uma mensagem de resposta, retorne a resposta para o cliente original.|
|Two-Way||✔️||Não|Uma exceção é lançada e a transação é revertida.|
|Two-Way|✔️|✔️||Não|Uma exceção é lançada e a transação é revertida.|
|Duplex||||Não|Não há suporte para comunicação duplex de não sessão no momento.|
|Duplex|✔️|||Sim|Enviar para um destino de backup.|

## <a name="hosting"></a>Hospedagem

Como o serviço de roteamento é implementado como um serviço WCF, ele deve ser hospedado internamente dentro de um aplicativo ou hospedado pelo IIS ou WAS. É recomendável que o serviço de roteamento seja hospedado no IIS, WAS ou em um aplicativo de serviço do Windows para aproveitar os recursos de início automático e gerenciamento de ciclo de vida disponíveis nesses ambientes de hospedagem.

O exemplo a seguir demonstra como hospedar o serviço de roteamento em um aplicativo.

```csharp
using (ServiceHost serviceHost =
                new ServiceHost(typeof(RoutingService)))
```

Para hospedar o serviço de roteamento no IIS ou WAS, você deve criar um arquivo de serviço (. svc) ou usar a ativação baseada em configuração do serviço. Ao usar um arquivo de serviço, você deve especificar o <xref:System.ServiceModel.Routing.RoutingService> usando o parâmetro Service. O exemplo a seguir contém um arquivo de serviço de exemplo que pode ser usado para hospedar o serviço de roteamento com o IIS ou o WAS.

```aspx-csharp
<%@ ServiceHost Language="C#" Debug="true" Service="System.ServiceModel.Routing.RoutingService,
     System.ServiceModel.Routing, version=4.0.0.0, Culture=neutral,
     PublicKeyToken=31bf3856ad364e35" %>
```

## <a name="routing-service-and-impersonation"></a>Serviço de roteamento e representação

O serviço de roteamento do WCF pode ser usado com a representação para enviar e receber mensagens. Todas as restrições comuns do Windows de representação se aplicam. Se você precisasse ter necessário configurar permissões de serviço ou de conta para usar a representação ao escrever seu próprio serviço, precisará executar as mesmas etapas para usar a representação com o serviço de roteamento. Para obter mais informações, consulte [delegação e representação](delegation-and-impersonation-with-wcf.md).

A representação com o serviço de roteamento requer o uso da representação ASP.NET no modo de compatibilidade ASP.NET ou o uso de credenciais do Windows que foram configuradas para permitir a representação. Para obter mais informações sobre o modo de compatibilidade ASP.NET, consulte [Serviços WCF e ASP.net](wcf-services-and-aspnet.md).

> [!WARNING]
> O serviço de roteamento do WCF não oferece suporte à representação com a autenticação básica.

Para usar a representação ASP.NET com o serviço de roteamento, habilite o modo de compatibilidade ASP.NET no ambiente de Hospedagem de serviço. O serviço de roteamento já foi marcado como permitir o modo de compatibilidade ASP.NET e a representação será habilitada automaticamente. A representação é o único uso com suporte da integração do ASP.NET com o serviço de roteamento.

Para usar a representação de credencial do Windows com o serviço de roteamento, você precisa configurar as credenciais e o serviço. O objeto de credenciais do cliente ( <xref:System.ServiceModel.Security.WindowsClientCredential> , acessado a partir do <xref:System.ServiceModel.ChannelFactory> ) define uma <xref:System.ServiceModel.Security.WindowsClientCredential.AllowedImpersonationLevel%2A> propriedade que deve ser definida para permitir a representação. Por fim, no serviço, você precisa configurar o <xref:System.ServiceModel.Description.ServiceAuthorizationBehavior> comportamento para definir `ImpersonateCallerForAllOperations` como `true` . O serviço de roteamento usa esse sinalizador para decidir se os clientes devem ser criados para encaminhar mensagens com representação habilitada.

## <a name="see-also"></a>Consulte também

- [Filtros de mensagem](message-filters.md)
- [Contratos de roteamento](routing-contracts.md)
- [Escolhendo um filtro](choosing-a-filter.md)
