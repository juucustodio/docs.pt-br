---
description: 'Saiba mais sobre: filtros de mensagens'
title: Filtros de mensagem
ms.date: 03/30/2017
helpviewer_keywords:
- routing [WCF], message filters
ms.assetid: cb33ba49-8b1f-4099-8acb-240404a46d9a
ms.openlocfilehash: 1b52b2b50dc94e79ba6960e834f601af18200f52
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99727047"
---
# <a name="message-filters"></a>Filtros de mensagem

Para implementar o roteamento baseado em conteúdo, o serviço de roteamento usa <xref:System.ServiceModel.Dispatcher.MessageFilter> implementações que inspecionam seções específicas de uma mensagem, como o endereço, o nome do ponto de extremidade ou uma instrução XPath específica. Se nenhum dos filtros de mensagem fornecidos com [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)] atender às suas necessidades, você poderá criar um filtro personalizado criando uma nova implementação da classe base <xref:System.ServiceModel.Dispatcher.MessageFilter> .  
  
 Ao configurar o serviço de roteamento, você deve definir elementos de filtro ( <xref:System.ServiceModel.Routing.Configuration.FilterElement> objetos) que descrevem o tipo de **MessageFilter** e quaisquer dados de suporte necessários para criar o filtro, como valores de cadeia de caracteres específicos para pesquisar dentro da mensagem. Observe que a criação dos elementos de filtro define apenas os filtros de mensagem individuais; para usar os filtros para avaliar e rotear mensagens, você também deve definir uma tabela de filtro ( <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryCollection> ).  
  
 Cada entrada na tabela de filtro referencia um elemento de filtro e especifica o ponto de extremidade do cliente para o qual uma mensagem será roteada se a mensagem corresponder ao filtro. As entradas de tabela de filtro também permitem que você especifique uma coleção de pontos de extremidade de backup ( <xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection> ), que define uma lista de pontos de extremidade para os quais a mensagem será transmitida no caso de uma falha de transmissão ao enviar para o ponto de extremidade primário. Esses pontos de extremidade serão tentados na ordem especificada até obter um sucesso.  
  
## <a name="message-filters"></a>Filtros de mensagem  

 Os filtros de mensagem usados pelo serviço de roteamento fornecem funcionalidade comum de seleção de mensagens, como avaliar o nome do ponto de extremidade para o qual uma mensagem foi enviada, a ação SOAP ou o endereço ou prefixo de endereço para o qual a mensagem foi enviada. Os filtros também podem ser Unidos com uma `AND` condição, de modo que as mensagens só serão roteadas para um ponto de extremidade se a mensagem corresponder a ambos os filtros. Você também pode criar filtros personalizados criando sua própria implementação do <xref:System.ServiceModel.Dispatcher.MessageFilter> .  
  
 A tabela a seguir lista o <xref:System.ServiceModel.Routing.Configuration.FilterType> usado pelo serviço de roteamento, a classe que implementa o filtro de mensagem específico e os <xref:System.ServiceModel.Routing.Configuration.FilterElement.FilterData%2A> parâmetros necessários.  
  
|Tipo de filtro|Descrição|Filtrar significado de dados|Filtro de exemplo|  
|------------------|-----------------|-------------------------|--------------------|  
|Ação|Usa a <xref:System.ServiceModel.Dispatcher.ActionMessageFilter> classe para corresponder as mensagens que contêm uma ação específica.|A ação a ser filtrada.|\<filter name="action1" filterType="Action" filterData="http://namespace/contract/operation" />|  
|EndpointAddress|Usa a <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter> classe, com <xref:System.ServiceModel.Dispatcher.EndpointAddressMessageFilter.IncludeHostNameInComparison%2A>  ==  `true` para corresponder mensagens que contêm um endereço específico.|O endereço a ser filtrado (no cabeçalho para).|\<filter name="address1" filterType="EndpointAddress" filterData="http://host/vdir/s.svc/b"  />|  
|EndpointAddressPrefix|Usa a <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter> classe, com <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter.IncludeHostNameInComparison%2A>  ==  `true` para corresponder mensagens que contêm um prefixo de endereço específico.|O endereço a ser filtrado com o uso de correspondência de prefixo mais longo.|\<filter name="prefix1" filterType="EndpointAddressPrefix" filterData="http://host/" />|  
|And|Usa a <xref:System.ServiceModel.Dispatcher.StrictAndMessageFilter> classe que sempre avalia as duas condições antes de retornar.|filterData não é usado; em vez disso, filter1 e filter2 têm os nomes dos filtros de mensagem correspondentes (também na tabela), que devem ser **e** Ed juntos.|\<filter name="and1" filterType="And" filter1="address1" filter2="action1" />|  
|Personalizado|Um tipo definido pelo usuário que estende a <xref:System.ServiceModel.Dispatcher.MessageFilter> classe e tem um construtor usando uma cadeia de caracteres.|O atributo CustomType é o nome do tipo totalmente qualificado da classe a ser criada; filterData é a cadeia de caracteres a ser passada para o construtor ao criar o filtro.|\<filter name="custom1" filterType="Custom" customType="CustomAssembly.CustomMsgFilter, CustomAssembly" filterData="Custom Data" />|  
|EndpointName|Usa a <xref:System.ServiceModel.Dispatcher.EndpointNameMessageFilter> classe para corresponder mensagens com base no nome do ponto de extremidade de serviço em que foram recebidas.|O nome do ponto de extremidade de serviço, por exemplo: "serviceEndpoint1".  Deve ser um dos pontos de extremidade expostos no serviço de roteamento.|\<filter name="stock1" filterType="Endpoint" filterData="SvcEndpoint" />|  
|MatchAll|Usa a <xref:System.ServiceModel.Dispatcher.MatchAllMessageFilter> classe. Esse filtro corresponde a todas as mensagens recebidas.|filterData não é usado. Esse filtro sempre corresponderá a todas as mensagens.|\<filter name="matchAll1" filterType="MatchAll" />|  
|XPath|Usa a <xref:System.ServiceModel.Dispatcher.XPathMessageFilter> classe para corresponder consultas XPath específicas dentro da mensagem.|A consulta XPath a ser usada ao corresponder mensagens.|\<filter name="XPath1" filterType="XPath" filterData="//ns:element" />|  
  
 O exemplo a seguir define as entradas de filtro que usam os filtros de mensagens XPath, EndpointName e PrefixEndpointAddress. Este exemplo também demonstra o uso de um filtro personalizado para as entradas RoundRobinFilter1 e RoundRobinFilter2.  
  
```xml  
<filters>  
     <filter name="XPathFilter" filterType="XPath"
             filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 1"/>  
     <filter name="EndpointNameFilter" filterType="EndpointName"
             filterData="calculatorEndpoint"/>  
     <filter name="PrefixAddressFilter" filterType="PrefixEndpointAddress"
             filterData="http://localhost/routingservice/router/rounding/"/>  
     <filter name="RoundRobinFilter1" filterType="Custom"
             customType="RoutingServiceFilters.RoundRobinMessageFilter,
             RoutingService" filterData="group1"/>  
     <filter name="RoundRobinFilter2" filterType="Custom"
             customType="RoutingServiceFilters.RoundRobinMessageFilter,
             RoutingService" filterData="group1"/>  
</filters>  
```  
  
> [!NOTE]
> Simplesmente definir um filtro não faz com que as mensagens sejam avaliadas em relação ao filtro. O filtro deve ser adicionado a uma tabela de filtro, que é então associada ao ponto de extremidade de serviço exposto pelo serviço de roteamento.  
  
### <a name="namespace-table"></a>Tabela de namespace  

 Ao usar um filtro XPath, os dados de filtro que contêm a consulta XPath podem se tornar muito grandes devido ao uso de namespaces. Para aliviar esse problema, o serviço de roteamento fornece a capacidade de definir seus próprios prefixos de namespace usando a tabela de namespace.  
  
 A tabela de namespace é uma coleção de <xref:System.ServiceModel.Routing.Configuration.NamespaceElement> objetos que define os prefixos de namespace para namespaces comuns que podem ser usados em um XPath. A seguir estão os namespaces padrão e os prefixos de namespace que estão contidos na tabela de namespace.  
  
|Prefixo|Namespace|  
|------------|---------------|  
|S11|`http://schemas.xmlsoap.org/soap/envelope`|  
|S12|`http://www.w3.org/2003/05/soap-envelope`|  
|wsaAugust2004|`http://schemas.xmlsoap.org/ws/2004/08/addressing`|  
|wsa10|`http://www.w3.org/2005/08/addressing`|  
|sm|`http://schemas.microsoft.com/serviceModel/2004/05/xpathfunctions`|  
|tempuri|`http://tempuri.org`|  
|ser|`http://schemas.microsoft.com/2003/10/Serialization`|  
  
 Quando você souber que usará um namespace específico em suas consultas XPath, poderá adicioná-lo à tabela de namespace junto com um prefixo de namespace exclusivo e usar o prefixo em qualquer consulta XPath em vez do namespace completo. O exemplo a seguir define um prefixo de "Custom" para o namespace `"http://my.custom.namespace"` , que é usado na consulta XPath contida em FilterData.  
  
```xml  
<namespaceTable>  
     <add prefix="custom" namespace="http://my.custom.namespace/"/>  
</namespaceTable>  
<filters>  
     <filter name="XPathFilter" filterType="XPath" filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 1"/>  
</filters>  
```  
  
## <a name="filter-tables"></a>Filtrar tabelas  

 Enquanto cada elemento Filter define uma comparação lógica que pode ser aplicada a uma mensagem, a tabela de filtros fornece a associação entre o elemento Filter e o ponto de extremidade do cliente de destino. Uma tabela de filtro é uma coleção nomeada de <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement> objetos que definem a associação entre um filtro, um ponto de extremidade de destino primário e uma lista de pontos de extremidades de backup alternativos. As entradas da tabela de filtro também permitem que você especifique uma prioridade opcional para cada condição de filtro. O exemplo a seguir define dois filtros e, em seguida, define uma tabela de filtro que associa cada filtro a um ponto de extremidade de destino.  
  
```xml  
<routing>  
     <filters>  
       <filter name="AddAction" filterType="Action" filterData="Add" />  
       <filter name="SubtractAction" filterType="Action" filterData="Subtract" />  
     </filters>  
     <filterTables>  
       <table name="routingTable1">  
         <filters>  
           <add filterName="AddAction" endpointName="Addition" />  
           <add filterName="SubtractAction" endpointName="Subtraction" />  
         </filters>  
       </table>  
     </filterTables>
</routing>  
```  
  
### <a name="filter-evaluation-priority"></a>Prioridade de avaliação do filtro  

 Por padrão, todas as entradas na tabela de filtro são avaliadas simultaneamente e a mensagem que está sendo avaliada é roteada para os pontos de extremidade associados a cada entrada de filtro correspondente. Se vários filtros forem avaliados para `true` e a mensagem for unidirecional ou duplex, a mensagem será multicast para os pontos de extremidade de todos os filtros de correspondência. As mensagens de solicitação-resposta não podem ser multicast porque apenas uma resposta pode ser retornada ao cliente.  
  
 A lógica de roteamento mais complexa pode ser implementada especificando-se níveis de prioridade para cada filtro; o serviço de roteamento avalia todos os filtros no nível de prioridade mais alto primeiro. Se uma mensagem corresponder a um filtro desse nível, não serão processados filtros de prioridade mais baixa. Por exemplo, uma mensagem unidirecional de entrada é avaliada pela primeira vez em todos os filtros com uma prioridade de 2. A mensagem não corresponde a nenhum filtro nesse nível de prioridade; portanto, a mensagem a seguir é comparada com filtros com uma prioridade de 1. Dois filtros de prioridade 1 correspondem à mensagem e, por ser uma mensagem unidirecional, ele é roteado para os pontos de extremidade de destino.  Como uma correspondência foi encontrada entre os filtros de prioridade 1, nenhum filtro de prioridade 0 é avaliado.  
  
> [!NOTE]
> Se nenhuma prioridade for especificada, a prioridade padrão 0 será usada.  
  
 O exemplo a seguir define uma tabela de filtro que especifica as prioridades de 2, 1 e 0 para os filtros referenciados na tabela.  
  
```xml  
<filterTables>  
     <filterTable name="filterTable1">  
          <add filterName="XPathFilter" endpointName="roundingCalcEndpoint"
               priority="2"/>  
          <add filterName="EndpointNameFilter" endpointName="regularCalcEndpoint"
               priority="1"/>  
          <add filterName="PrefixAddressFilter" endpointName="roundingCalcEndpoint"
               priority="1"/>  
          <add filterName="MatchAllMessageFilter" endpointName="defaultCalcEndpoint"
               priority="0"/>  
     </filterTable>  
</filterTables>  
```  
  
 No exemplo anterior, se uma mensagem corresponder a XPathFilter, ela será roteada para o roundingCalcEndpoint e nenhum outro filtro na tabela será avaliado porque todos os outros filtros são de prioridade mais baixa. No entanto, se a mensagem não corresponder ao XPathFilter, ela será avaliada em relação a todos os filtros da próxima prioridade mais baixa, EndpointNameFilter e PrefixAddressFilter.  
  
> [!NOTE]
> Quando possível, use filtros exclusivos em vez de especificar uma prioridade, pois a avaliação de prioridade pode resultar em degradação do desempenho.  
  
### <a name="backup-lists"></a>Listas de backup  

 Cada filtro na tabela de filtros pode, opcionalmente, especificar uma lista de backup, que é uma coleção nomeada de pontos de extremidade ( <xref:System.ServiceModel.Routing.Configuration.BackupEndpointCollection> ). Essa coleção contém uma lista ordenada de pontos de extremidade para os quais a mensagem será transmitida no caso de um <xref:System.ServiceModel.CommunicationException> ao enviar para o ponto de extremidade primário especificado em <xref:System.ServiceModel.Routing.Configuration.FilterTableEntryElement.EndpointName%2A> . O exemplo a seguir define uma lista de backup chamada "backupServiceEndpoints" que contém dois pontos de extremidade.  
  
```xml  
<filterTables>  
     <filterTable name="filterTable1">  
          <add filterName="MatchAllFilter1" endpointName="Destination" backupList="backupEndpointList"/>  
     </filterTable>  
</filterTables>  
<backupLists>  
     <backupList name="backupEndpointList">  
          <add endpointName="backupServiceQueue" />  
          <add endpointName="alternateServiceQueue" />  
     </backupList>  
</backupLists>  
```  
  
 No exemplo anterior, se um envio para o ponto de extremidade primário "destino" falhar, o serviço de roteamento tentará enviar para cada ponto de extremidade na sequência em que eles estão listados, primeiro enviando para backupServiceQueue e, subsequentemente, enviando para alternateServiceQueue se o envio para backupServiceQueue falhar. Se todos os pontos de extremidade de backup falharem, uma falha será retornada.
