---
description: 'Saiba mais sobre: visão geral do fluxo de mensagens'
title: Visão geral de fluxo de mensagens
ms.date: 03/30/2017
ms.assetid: fb0899e1-84cc-4d90-b45b-dc5a50063943
ms.openlocfilehash: ec26824db51e65eff75f4b705c0a2ed966a7aa3a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99759751"
---
# <a name="message-flow-overview"></a>Visão geral de fluxo de mensagens

Em um sistema distribuído que contém serviços interconectados, é necessário determinar as relações de causal entre os serviços. É importante entender os vários componentes que faziam parte de um fluxo de solicitação para dar suporte a cenários críticos, como monitoramento de integridade, solução de problemas e análise de causa raiz. Para habilitar a correlação de rastreamentos entre vários serviços, no .NET Framework 4, adicionamos suporte por meio dos seguintes recursos:

- Rastreamento analítico: um recurso de rastreamento de alto desempenho e baixo nível baixo usando o ETW (rastreamento de eventos para Windows).

- Modelo de atividade de ponta a ponta para serviços WCF/WF: esse recurso dá suporte à correlação de rastreamentos gerados pelos <xref:System.ServiceModel> <xref:System.Workflow.ComponentModel> namespaces e.

- Rastreamento de ETW para WF: esse recurso usa registros de rastreamento gerados pelos serviços do WF para fornecer visibilidade do estado atual do fluxo de trabalho e do andamento.

 Os erros registrados em um registro rastreamento ou rastreamento podem ser usados para encontrar defeitos de código ou mensagens formadas incorretamente. A propriedade ActivityId do nó de correlação no cabeçalho da mensagem do evento pode ser usada para determinar a atividade com falha. Para habilitar o rastreamento de fluxo de mensagens por ID de atividade, consulte [Configurando o rastreamento de fluxo de mensagens](./etw/configuring-message-flow-tracing.md). Este tópico demonstra como habilitar o rastreamento de fluxo de mensagens no projeto criado no tutorial de Introdução.

### <a name="to-enable-message-flow-tracing-in-the-getting-started-tutorial"></a>Para habilitar o rastreamento de fluxo de mensagens no tutorial de Introdução

1. Abra Visualizador de Eventos clicando em **Iniciar**, **executar** e inserindo `eventvwr.exe` .

2. Se você não tiver habilitado o rastreamento analítico, expanda **logs de aplicativos e serviços**, **Microsoft**, **Windows**, **servidor de aplicativos-aplicativos**. Selecione **Exibir**, **Mostrar logs analíticos e de depuração**. Clique com o botão direito do mouse em **analítica** e selecione **habilitar log**. Deixe Visualizador de Eventos aberto para que os rastreamentos possam ser exibidos.

3. Abra o exemplo criado no [tutorial de introdução](../getting-started-tutorial.md) no Visual Studio 2012. Observe que você deve executar o Visual Studio 2012 como administrador para que o serviço possa ser criado. Se você tiver os exemplos do WCF instalados, poderá abrir o [introdução](../samples/getting-started-sample.md), que contém o projeto concluído criado no tutorial.

4. Clique com o botão direito do mouse no projeto de **serviço** e selecione **Adicionar**, **novo item**. Selecione o **arquivo de configuração do aplicativo** e clique em **OK**.

5. Adicione o código a seguir ao arquivo App.Config criado na etapa anterior.

    ```xml
    <system.serviceModel>
      <diagnostics>
        <endToEndTracing propagateActivity="true" messageFlowTracing="true"/>
      </diagnostics>
    </system.serviceModel>
    ```

6. Execute o aplicativo de servidor sem depuração pressionando CTRL + F5. Execute o projeto cliente clicando com o botão direito do mouse no projeto **cliente** e selecionando **depurar**, **Iniciar nova instância**.

7. Para rastrear os eventos do cliente para o servidor, adicione o seguinte ao arquivo de configuração do aplicativo no projeto do cliente.

    ```xml
    <diagnostics>
      <endToEndTracing propagateActivity="true" messageFlowTracing="true"/>
    </diagnostics>
    ```

8. Em Program.cs no cliente, adicione a seguinte instrução using.

    ```csharp
    using System.Diagnostics;
    ```

9. No método principal no arquivo program.cs no projeto cliente, defina o GUID de rastreamento a ser propagado no log de eventos.

    ```csharp
    Guid guid = Guid.NewGuid();
    Trace.CorrelationManager.ActivityId = guid;
    ```

10. Atualize e examine o log **analítico**  .  Procure um evento com a ID de evento 220.  Selecione o evento e clique na guia **detalhes** no painel de visualização. Esse evento conterá a ID de correlação para a atividade de chamada.

    ```xml
    <Correlation ActivityID="{A066CCF1-8AB3-459B-B62F-F79F957A5036}" />
    ```

    > [!NOTE]
    > Todos os eventos com o mesmo GUID na ActivityId estão relacionados a uma solicitação. Isso pode ser usado para correlacionar mensagens de um cliente específico a um serviço específico. Se o cliente tiver chamado outro serviço, o mesmo cliente poderá ser identificado por ActivityId.

11. Em alguns casos, o ActivityId pode ser alterado do GUID original para um novo ActivityId. Nesse caso, um evento de transferência é emitido. Essa ID de evento é 499 e o evento conterá os dados a seguir no cabeçalho.

    ```xml
    <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
        <System>
            <Provider Name="Microsoft-Windows-Application Server-Applications" Guid="{c651f5f6-1c0d-492e-8ae1-b4efd7c9d503}" />
            <EventID>499</EventID>
            ...
            <Correlation ActivityID="{A066CCF1-8AB3-459B-B62F-F79F957A5036}" RelatedActivityID="{85FC0930-9C49-42DA-804B-A7368104BD1B}" />
            ...
       </System>
    </Event>
    ```

    > [!NOTE]
    > O evento de transferência registra a alteração do ActivityId ativo do GUID especificado como ActivityId para o GUID especificado como RelatedActivityID. Depois que o evento de transferência for emitido, todos os eventos conterão o novo GUID como ActivityId.
