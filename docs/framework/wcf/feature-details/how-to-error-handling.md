---
description: 'Saiba mais sobre: como: tratamento de erros'
title: 'Como: Tratamento de erros'
ms.date: 03/30/2017
ms.assetid: de566e39-9358-44ff-8244-780f6b799966
ms.openlocfilehash: 1d385070e4cc0d55bc3327114baf4e4ff543171f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99704648"
---
# <a name="how-to-error-handling"></a>Como: Tratamento de erros

Este tópico descreve as etapas básicas necessárias para criar uma configuração de roteamento que usa o tratamento de erros. Neste exemplo, as mensagens são roteadas para um ponto de extremidade de destino. Se uma mensagem não puder ser entregue devido a uma falha relacionada à rede ou à comunicação ( <xref:System.ServiceModel.CommunicationException> ), a mensagem será reenviada para um ponto de extremidade alternativo.

> [!NOTE]
> Para simular uma falha de rede, o ponto de extremidade de destino usado neste exemplo contém um endereço incorreto. As mensagens roteadas para esse ponto de extremidade falham, pois nenhum serviço está escutando no endereço especificado.

> [!NOTE]
> Embora o exemplo contido neste tópico não discuta explicitamente as configurações de tempo limite, você deve levar isso em consideração ao usar o tratamento de erros. Quando forem encontrados erros, haverá um atraso adicional encontrado antes que o cliente receba uma resposta. Isso ocorre porque o erro é recebido no serviço de roteamento, que tenta enviar a mensagem para um ponto de extremidade de backup. Se os valores de tempo limite associados aos pontos de extremidade de destino primário e de backup forem grandes, o cliente poderá experimentar um longo atraso enquanto a mensagem falha em vários pontos de extremidade na lista de backup antes de ser enviada com êxito.
>
> Como o serviço de roteamento pode encontrar um atraso máximo igual à soma do valor de tempo limite para todos os pontos de extremidade associados a um filtro, recomendamos que você aumente o tempo limite esperado no cliente de acordo.

### <a name="implement-error-handling"></a>Implementar tratamento de erros

1. Crie a configuração básica do serviço de roteamento especificando o ponto de extremidade de serviço exposto pelo serviço. O exemplo a seguir define um único ponto de extremidade de serviço, que é usado para receber mensagens. Ele também define os pontos de extremidade do cliente que são usados para enviar mensagens; deadDestination e realDestination. O ponto de extremidade deadDestination contém um endereço que não faz referência a um serviço em execução e é usado para simular uma falha de rede ao enviar mensagens para esse ponto de extremidade.

    ```xml
    <services>
      <service behaviorConfiguration="routingConfiguration"
               name="System.ServiceModel.Routing.RoutingService">
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost/routingservice/" />
          </baseAddresses>
        </host>
        <!-- Create the Routing Service endpoint -->
        <endpoint address="router"
                  binding="basicHttpBinding"
                  name="RoutingServiceEndpoint"
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />
      </service>
    </services>

    <!-- Create the destination endpoints that we want to send to -->
    <client>
      <!-- Create a dummy endpoint that we know will be down -->
      <endpoint name="deadDestination"
                address="net.tcp://localhost:9090/servicemodelsamples/fakeDestination"
                binding="netTcpBinding"
                contract="*" />

      <!-- Now create the real service endpoint -->
      <endpoint name="realDestination"
                address="net.tcp://localhost:8080/servicemodelsamples/service"
                binding="netTcpBinding"
                contract="*" />
    </client>
    ```

2. Defina os filtros usados para rotear mensagens para os pontos de extremidade de destino.  Para este exemplo, um filtro filtro matchall é usado para corresponder a todas as mensagens recebidas pelo serviço de roteamento.

    ```xml
    <filters>
      <!-- Create a MatchAll filter which will catch all messages -->
      <filter name="MatchAllFilter1" filterType="MatchAll" />
    </filters>
    ```

3. Defina a lista de pontos de extremidade de backup, que contém os pontos de extremidades para os quais uma mensagem é enviada no caso de uma falha de comunicação ou rede ao enviar para o ponto de extremidade de destino primário. O exemplo a seguir define uma lista de backup que contém um ponto de extremidade; no entanto, vários pontos de extremidade podem ser especificados em uma lista de backup.

     Se a lista de backup contiver vários pontos de extremidade, quando ocorrer uma falha de rede ou de comunicação, o serviço de roteamento tentará enviar a mensagem para o primeiro ponto de extremidade na lista. Se ocorrer uma falha de rede ou comunicação ao enviar para esse ponto de extremidade, o serviço de roteamento tentará enviar a mensagem para o próximo ponto de extremidade contido na lista. O serviço continua enviando a mensagem para cada ponto de extremidade na lista de pontos de extremidade de backup até que a mensagem seja enviada com êxito, todos os pontos de extremidade de backup retornam uma rede ou um erro relacionado à comunicação, ou a mensagem é enviada e o ponto final retorna um erro não relacionado à rede e não à comunicação.

    ```xml
    <backupLists>
      <backupList name="backupEndpointList">
          <add endpointName="realDestination" />
      </backupList>
    </backupLists>
    ```

4. Defina a tabela de filtros, que associa o filtro ao ponto de extremidade deadDestination e à lista de pontos de extremidade de backup.  O serviço de roteamento primeiro tenta enviar a mensagem para o ponto de extremidade de destino associado ao filtro. Como o deadDestination contém um endereço que não se refere a um serviço em execução, isso resulta em um erro de rede. Em seguida, o serviço de roteamento tenta enviar a mensagem para o ponto de extremidade especificado no backupEndpointList.

    ```xml
    <filterTables>
            <!-- Set up the Routing Service's Message Filter Table -->
            <filterTable name="filterTable1">
                <!-- Add an entity that maps the MatchAllMessageFilter to the dead destination -->
                <!-- If that endpoint is down, tell the Routing Service to try the endpoints -->
                <!-- Listed in the backupEndpointList -->
                <add filterName="MatchAllFilter1" endpointName="deadDestination" backupList="backupEndpointList"/>
            </filterTable>
          </filterTables>
    ```

5. Para avaliar as mensagens de entrada em relação ao filtro contido na tabela de filtros, você deve associar a tabela de filtros aos pontos de extremidade de serviço usando o comportamento de roteamento.  O exemplo a seguir demonstra como associar "filterTable1" aos pontos de extremidade de serviço.

    ```xml
    <behaviors>
      <serviceBehaviors>
        <!-- Set up the Routing Behavior -->
        <behavior name="routingConfiguration">
          <routing filterTableName="filterTable1" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
    ```

## <a name="example"></a>Exemplo

A seguir está uma lista completa do arquivo de configuração:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<!-- Copyright (c) Microsoft Corporation.  All Rights Reserved. -->
<configuration>
  <system.serviceModel>
    <services>
      <service behaviorConfiguration="routingConfiguration"
               name="System.ServiceModel.Routing.RoutingService">
        <host>
          <baseAddresses>
            <add baseAddress="http://localhost/routingservice/" />
          </baseAddresses>
        </host>
        <!-- Create the Routing Service endpoint -->
        <endpoint address="router"
                  binding="basicHttpBinding"
                  name="RoutingServiceEndpoint"
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />
      </service>
    </services>
    <behaviors>
      <serviceBehaviors>
        <!-- Set up the Routing Behavior -->
        <behavior name="routingConfiguration">
          <routing filterTableName="filterTable1" />
        </behavior>
      </serviceBehaviors>
    </behaviors>
    <!-- Create the destination endpoints that we want to send to -->
    <client>
      <!-- Create a dummy endpoint that we know will be down -->
      <endpoint name="deadDestination"
                address="net.tcp://localhost:9090/servicemodelsamples/fakeDestination"
                binding="netTcpBinding"
                contract="*" />

      <!-- Now create the real service endpoint -->
      <endpoint name="realDestination"
                address="net.tcp://localhost:8080/servicemodelsamples/service"
                binding="netTcpBinding"
                contract="*" />
    </client>
    <routing>
      <filters>
        <!-- Create a MatchAll filter which will catch all messages -->
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
        <backupList name="backupEndpointList">
            <add endpointName="realDestination" />
        </backupList>
      </backupLists>
      </routing>
  </system.serviceModel>
</configuration>
```
