---
description: 'Saiba mais sobre: perfis de rastreamento'
title: Controlando perfis
ms.date: 03/30/2017
ms.assetid: 22682566-1cd9-4672-9791-fb3523638e18
ms.openlocfilehash: 9748f0452a1699e08760372f826f2458d82f4b79
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755142"
---
# <a name="tracking-profiles"></a>Controlando perfis

Controlando os perfis contêm consultas de rastreamento que permitem um participante de rastreamento assinar eventos de fluxo de trabalho que são emitidas quando o estado de uma instância de fluxo de trabalho se altera em runtime.

## <a name="tracking-profiles"></a>Controlando perfis

Controlando os perfis são usados para especificar que as informações de rastreamento é emitida para uma instância de fluxo de trabalho. Se nenhum perfil for especificado, então todos os eventos de rastreamento são emitidas. Se um perfil for especificado, então os eventos de rastreamento especificados no perfil serão emitidos. Dependendo dos requisitos de monitoramento, você pode escrever um perfil que é muito geral, que assina um pequeno conjunto de alterações de estado de alto nível em um fluxo de trabalho. Inversamente, você pode criar um perfil muito detalhado cujos eventos resultantes são muito ricos reconstruir posteriormente um fluxo detalhado de execução.

Os perfis de rastreamento se manifestam como elementos XML dentro de um arquivo de configuração .NET Framework padrão ou especificados no código. O exemplo a seguir é de [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] que controla o perfil em um arquivo de configuração que permite que um participante de rastreamento assine os eventos de fluxo de trabalho `Started` e de `Completed` .

```xml
<system.serviceModel>
    ...
    <tracking>
     <profiles>
      <trackingProfile name="Sample Tracking Profile">
        <workflow activityDefinitionId="*">
          <workflowInstanceQueries>
            <workflowInstanceQuery>
              <states>
                <state name="Started"/>
                <state name="Completed"/>
              </states>
            </workflowInstanceQuery>
          </workflowInstanceQueries>
        </workflow>
      </trackingProfile>
    </profiles>
  </tracking>
    ...
</system.serviceModel>
```

O exemplo a seguir mostra o perfil equivalente de rastreamento criado usando código.

```csharp
TrackingProfile profile = new TrackingProfile()
{
    Name = "CustomTrackingProfile",
    Queries =
    {
        new WorkflowInstanceQuery()
        {
            // Limit workflow instance tracking records for started and
            // completed workflow states.
            States = { WorkflowInstanceStates.Started, WorkflowInstanceStates.Completed },
        }
    }
};
```

Controlando registros são filtrados com o modo de visibilidade em um perfil de rastreamento usando o atributo <xref:System.Activities.Tracking.ImplementationVisibility> . Uma atividade composto é uma atividade de nível superior que contém outras atividades que formam a sua implementação. O modo de visibilidade especifica os registros de rastreamento de atividades emissores compostas em uma atividade de fluxo de trabalho, para especificar se as atividades que formam a implementação estão sendo controladas. O modo de visibilidade se aplica a nível de perfil de rastreamento. A filtragem de registros de controle para atividades individuais em um fluxo de trabalho é controlada por consultas no perfil de rastreamento. Para obter mais informações, consulte a seção **tipos de consulta de perfil de rastreamento** neste documento.

Os dois modos de visibilidade especificado pelo atributo de `implementationVisibility` no perfil de rastreamento são `RootScope` e `All`. Usar o modo de `RootScope` suprime os registros de controle para as atividades que formam a implementação de uma atividade em casos onde uma atividade composta não é a raiz de um fluxo de trabalho. Isso significa que, quando uma atividade que é implementada usando outras atividades é adicionada a um fluxo de trabalho, e `implementationVisibility` definido como RootScope, somente a última atividade de nível superior dentro da atividade composto é rastreada. Se uma atividade é a raiz de fluxo de trabalho, então a implementação da atividade é o próprio fluxo de trabalho e os registros de rastreamento são emitidas para as atividades que formam a implementação. Usar qualquer modo permite que todos os registros de rastreamento ser emitida para atividades raiz e todas as suas atividades compostas.

Por exemplo, suponha que *myactivity* é uma atividade composta cuja implementação contém duas atividades, *Atividade1* e *da atividade2*. Quando essa atividade é adicionada a um fluxo de trabalho e o rastreamento é habilitado com um perfil de controle com `implementationVisibility` definido como `RootScope` , os registros de rastreamento são emitidos somente para *myactivity*. No entanto, nenhum registro é emitido para as atividades *Atividade1* e *da atividade2*.

No entanto, se o `implementationVisibility` atributo do perfil de controle for definido como `All` , os registros de rastreamento serão emitidos não apenas para *myactivity*, mas também para as atividades *Atividade1* e *da atividade2*.

O sinalizador de `implementationVisibility` se aplica aos seguintes tipos de registro de acompanhamento:

- ActivityStateRecord

- FaultPropagationRecord

- CancelRequestedRecord

- ActivityScheduledRecord

> [!NOTE]
> CustomTrackingRecords emitiu-se de implementação de atividade não é filtrado para fora pela configuração de implementationVisibility.

A funcionalidade de `implementationVisibility` é especificado como <xref:System.Activities.Tracking.ImplementationVisibility.RootScope> no perfil de rastreamento em código como segue:

```csharp
TrackingProfile sampleTrackingProfile = new TrackingProfile()
{
    Name = "Sample Tracking Profile",
    ImplementationVisibility = ImplementationVisibility.RootScope
};
```

A funcionalidade de `implementationVisibility` é especificado como <xref:System.Activities.Tracking.ImplementationVisibility.All> no perfil de rastreamento em um arquivo de configuração como segue:

```xml
<tracking>
      <profiles>
        <trackingProfile name="Shipping Monitoring" implementationVisibility="All">
          <workflow activityDefinitionId="*">
...
         </workflow>
        </trackingProfile>
      </profiles>
</tracking>
```

`ImplementationVisibility` que define o perfil de rastreamento é opcional. Por padrão, o valor é definido como `RootScope`. Os valores para este atributo são também maiúsculas de minúsculas.

### <a name="tracking-profile-query-types"></a>Controlando tipos de consulta de perfil

Controlando os perfis são estruturados como as assinaturas declarativas para controlar os registros que permitem que você possa ver o runtime de fluxo de trabalho para o controle específico registro. Há vários tipos de consulta que permitem autenticação para classes diferentes de objetos de <xref:System.Activities.Tracking.TrackingRecord> . Controlar perfis pode ser especificado na configuração ou com o código. Aqui estão os tipos de consulta mais comuns:

- <xref:System.Activities.Tracking.WorkflowInstanceQuery> - use isso para controlar as alterações do ciclo de vida de instância de fluxo de trabalho como `Started` precedente- demonstrado e `Completed`. <xref:System.Activities.Tracking.WorkflowInstanceQuery> é usado para assinar seguintes a <xref:System.Activities.Tracking.TrackingRecord> os objetos:

  - <xref:System.Activities.Tracking.WorkflowInstanceRecord>

  - <xref:System.Activities.Tracking.WorkflowInstanceAbortedRecord>

  - <xref:System.Activities.Tracking.WorkflowInstanceUnhandledExceptionRecord>

  - <xref:System.Activities.Tracking.WorkflowInstanceTerminatedRecord>

  - <xref:System.Activities.Tracking.WorkflowInstanceSuspendedRecord>

  Os estados a que pode ser assinado são especificados na classe de <xref:System.Activities.Tracking.WorkflowInstanceStates> .

  A configuração ou código usada para assinar os registros de acompanhamento de instância nível de fluxo de trabalho do estado da instância de `Started` que usa <xref:System.Activities.Tracking.WorkflowInstanceQuery> são mostrados no exemplo a seguir.

  ```xml
  <workflowInstanceQueries>
      <workflowInstanceQuery>
        <states>
          <state name="Started"/>
        </states>
      </workflowInstanceQuery>
  </workflowInstanceQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new WorkflowInstanceQuery()
          {
              States = { WorkflowInstanceStates.Started}
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.ActivityStateQuery> - use isso para controlar as alterações do ciclo de vida de atividades que compõem uma instância de fluxo de trabalho. Por exemplo, talvez você queira manter o controle sempre que a atividade "enviar email" for concluída em uma instância de fluxo de trabalho. Esta consulta é necessária para que <xref:System.Activities.Tracking.TrackingParticipant> assine a <xref:System.Activities.Tracking.ActivityStateRecord> objetos. Os estados disponíveis para assinar a são especificados em <xref:System.Activities.Tracking.ActivityStates>.

  A configuração e o código usados para assinar o estado da atividade que controla os registros que usam <xref:System.Activities.Tracking.ActivityStateQuery> para atividades de `SendEmailActivity` são mostrados no exemplo a seguir.

  ```xml
  <activityStateQueries>
    <activityStateQuery activityName="SendEmailActivity">
      <states>
        <state name="Closed"/>
      </states>
    </activityStateQuery>
  </activityStateQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new ActivityStateQuery()
          {
              ActivityName = "SendEmailActivity",
              States = { ActivityStates.Closed }
          }
      }
  };
  ```

  > [!NOTE]
  > Se vários elementos de activityStateQuery têm o mesmo nome, somente os estados no último elemento são usados no perfil de rastreamento.

- <xref:System.Activities.Tracking.ActivityScheduledQuery> - esta consulta permite que você controla uma atividade agendada para execução por uma atividade pai. A consulta é necessária para que <xref:System.Activities.Tracking.TrackingParticipant> assine a <xref:System.Activities.Tracking.ActivityScheduledRecord> objetos.

  A configuração e o código usados para assinar os registros filho relacionados à atividade de `SendEmailActivity` que está sendo agendada usando <xref:System.Activities.Tracking.ActivityScheduledQuery> são mostrados no exemplo a seguir.

  ```xml
  <activityScheduledQueries>
    <activityScheduledQuery activityName="ProcessNotificationsActivity" childActivityName="SendEmailActivity" />
  </activityScheduledQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new ActivityScheduledQuery()
          {
              ActivityName = "ProcessNotificationsActivity",
              ChildActivityName = "SendEmailActivity"
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.FaultPropagationQuery> - use isso para controlar a manipulação de falhas que ocorrem dentro de uma atividade. A consulta é necessária para que <xref:System.Activities.Tracking.TrackingParticipant> assine a <xref:System.Activities.Tracking.FaultPropagationRecord> objetos.

  A configuração e o código usados para assinar os registros relacionados à propagação de falha que usa <xref:System.Activities.Tracking.FaultPropagationQuery> são mostrados no exemplo a seguir.

  ```xml
  <faultPropagationQueries>
    <faultPropagationQuery faultSourceActivityName="SendEmailActivity" faultHandlerActivityName="NotificationsFaultHandler" />
  </faultPropagationQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new FaultPropagationQuery()
          {
              FaultSourceActivityName = "SendEmailActivity",
              FaultHandlerActivityName = "NotificationsFaultHandler"
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.CancelRequestedQuery> - use isso para controlar solicitações cancelar uma atividade filho pela atividade pai. A consulta é necessária para que <xref:System.Activities.Tracking.TrackingParticipant> assine a <xref:System.Activities.Tracking.CancelRequestedRecord> objetos.

  A configuração e o código usados para assinar registros relacionados ao cancelamento da atividade usando <xref:System.Activities.Tracking.CancelRequestedQuery> o são mostrados no exemplo a seguir.

  ```xml
  <cancelRequestedQueries>
    <cancelRequestedQuery activityName="ProcessNotificationsActivity" childActivityName="SendEmailActivity" />
  </cancelRequestedQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new CancelRequestedQuery()
          {
              ActivityName = "ProcessNotificationsActivity",
              ChildActivityName = "SendEmailActivity"
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.CustomTrackingQuery> - use isso para eventos de rastreamento que você define nas atividades de código. A consulta é necessária para que <xref:System.Activities.Tracking.TrackingParticipant> assine a <xref:System.Activities.Tracking.CustomTrackingRecord> objetos.

  A configuração e o código usados para assinar os registros relacionados aos registros personalizados de rastreamento que usam <xref:System.Activities.Tracking.CustomTrackingQuery> são mostrados no exemplo a seguir.

  ```xml
  <customTrackingQueries>
    <customTrackingQuery name="EmailAddress" activityName="SendEmailActivity" />
  </customTrackingQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new CustomTrackingQuery()
          {
              Name = "EmailAddress",
              ActivityName = "SendEmailActivity"
          }
      }
  };
  ```

- <xref:System.Activities.Tracking.BookmarkResumptionQuery> - use isso para controlar a ressunção de um indexador em uma instância de fluxo de trabalho. Esta consulta é necessária para que <xref:System.Activities.Tracking.TrackingParticipant> assine a <xref:System.Activities.Tracking.BookmarkResumptionRecord> objetos.

  A configuração e o código usados para assinar os registros relacionados à ressunção do indexador que usa <xref:System.Activities.Tracking.BookmarkResumptionQuery> são mostrados no exemplo a seguir.

  ```xml
  <bookmarkResumptionQueries>
    <bookmarkResumptionQuery name="SentEmailBookmark" />
  </bookmarkResumptionQueries>
  ```

  ```csharp
  TrackingProfile sampleTrackingProfile = new TrackingProfile()
  {
      Name = "Sample Tracking Profile",
      Queries =
      {
          new BookmarkResumptionQuery()
          {
              Name = "sentEmailBookmark"
          }
      }
  };
  ```

### <a name="annotations"></a>Anotações

As anotações permitem que você marca arbitrariamente registros de rastreamento com um valor que pode ser configurado após tempo de compilação. Por exemplo, talvez você queira que vários registros de acompanhamento em vários fluxos de trabalho sejam marcados com "servidor de email" = = "Server1 de email". Isso facilita localizar todos os registros com essa marca ao consultar o rastreamento registra posteriormente.

Para fazer isso, uma anotação é adicionada a uma consulta de rastreamento conforme mostrado no exemplo o seguir.

```xml
<activityStateQuery activityName="SendEmailActivity">
  <states>
    <state name="Closed"/>
  </states>
  <annotations>
    <annotation name="MailServer" value="Mail Server1"/>
  </annotations>
</activityStateQuery>
```

### <a name="how-to-create-a-tracking-profile"></a>Como criar um perfil de rastreamento

Os elementos de consulta de rastreamento são usados para criar um perfil de controle usando um código ou arquivo de configuração XML [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] . Aqui está um exemplo de um perfil de rastreamento criado usando um arquivo de configuração.

```xml
<system.serviceModel>
  <tracking>
    <profiles>
      <trackingProfile name="Sample Tracking Profile ">
        <workflow activityDefinitionId="*">
          <!--Specify the tracking profile query elements to subscribe for tracking records-->
        </workflow>
      </trackingProfile>
    </profiles>
  </tracking>
</system.serviceModel>
```

> [!WARNING]
> Para um WF usando o host serviço de fluxo de trabalho, o perfil de rastreamento é normalmente criado usando um arquivo de configuração. Também é possível criar um perfil de rastreamento com o código usando o perfil de rastreamento e a consulta API de rastreamento.

Um perfil configurado como um arquivo de configuração XML é aplicado a um participante de rastreamento que usa uma extensão de comportamento. Isso é adicionado a um WorkflowServiceHost, conforme descrito na seção mais adiante, [Configurando o acompanhamento de um fluxo de trabalho](configuring-tracking-for-a-workflow.md).

A verbosidade de registros de rastreamento emissores pelo host é determinada pelas configurações dentro do perfil de rastreamento. Um participante de rastreamento assina controlar registros adicionando consultas a um perfil de rastreamento. Para assinar todos os registros de acompanhamento, o perfil de controle precisa especificar todas as consultas de controle usando " \* " nos campos de nome em cada uma das consultas.

Aqui estão alguns dos exemplos comuns de perfis de rastreamento.

- Um perfil de controle para obter registros e falhas de instância de fluxo de trabalho.

  ```xml
  <trackingProfile name="Instance and Fault Records">
    <workflow activityDefinitionId="*">
      <workflowInstanceQueries>
        <workflowInstanceQuery>
          <states>
            <state name="*" />
          </states>
        </workflowInstanceQuery>
      </workflowInstanceQueries>
      <activityStateQueries>
        <activityStateQuery activityName="*">
          <states>
            <state name="Faulted"/>
          </states>
        </activityStateQuery>
      </activityStateQueries>
    </workflow>
  </trackingProfile>
  ```

- Um perfil de rastreamento para obter todos os registros personalizados de rastreamento.

  ```xml
  <trackingProfile name="Instance_And_Custom_Records">
    <workflow activityDefinitionId="*">
      <customTrackingQueries>
        <customTrackingQuery name="*" activityName="*" />
      </customTrackingQueries>
    </workflow>
  </trackingProfile>
  ```

## <a name="see-also"></a>Consulte também

- [Rastreamento de SQL](./samples/sql-tracking.md)
- [Monitoramento do Windows Server app Fabric](/previous-versions/appfabric/ee677251(v=azure.10))
- [Monitorando aplicativos com o app Fabric](/previous-versions/appfabric/ee677276(v=azure.10))
