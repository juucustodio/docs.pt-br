---
description: 'Saiba mais sobre: como habilitar a persistência de SQL para fluxos de trabalho e serviços de fluxo de trabalho'
title: 'Como: habilitar persistência SQL para fluxos de trabalho e serviços de fluxo de trabalho'
ms.date: 03/30/2017
ms.assetid: ca7bf77f-3e5d-4b23-b17a-d0b60f46411d
ms.openlocfilehash: 5c124c4ec1d75d4b3b24468c04a4fb82236aa29a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99777717"
---
# <a name="how-to-enable-sql-persistence-for-workflows-and-workflow-services"></a>Como: habilitar persistência SQL para fluxos de trabalho e serviços de fluxo de trabalho

Este tópico descreve como configurar o recurso de Store de instância de fluxo de trabalho SQL para ativar persistência para os fluxos de trabalho e fluxo de trabalho serviços de aplicativos por meio e usando um arquivo de configuração.

A tela de aplicativo Windows Server simplifica o processo de configurar a persistência. Para obter mais informações, consulte [configuração de persistência do App Fabric](/previous-versions/appfabric/ee790848(v=azure.10)).

Antes de usar o recurso de Store de instância de fluxo de trabalho SQL, crie um base de dados que o recurso usa para manter instâncias de fluxo de trabalho. Arquivos de script SQL das cópias do programa de instalação de [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] associados com o recurso de Store de instância de fluxo de trabalho SQL ao %WINDIR% \ Microsoft.NET \ Framework \ v4.xxx pasta \ \ EN SQL. Executar esses arquivos de script em um base de dados SQL Server 2005 ou SQL Server 2008 que você deseja a instância Store de fluxo de trabalho SQL para usar para persistir instâncias de fluxo de trabalho. Execute o arquivo de SqlWorkflowInstanceStoreSchema.sql primeiro e execute o arquivo de SqlWorkflowInstanceStoreLogic.sql.

> [!NOTE]
> Para limpar o base de dados de persistência para ter um base de dados atualizado, executar os scripts em %WINDIR% \ Microsoft.NET \ Framework \ \ \ v4.xxx SQL EN na seguinte ordem.
>
> 1. SqlWorkflowInstanceStoreSchema.sql
> 2. SqlWorkflowInstanceStoreLogic.sql

> [!IMPORTANT]
> Se você não criar um base de dados de persistência, o recurso de Store de instância de fluxo de trabalho do SQL gerencie uma exceção similar à seguinte quando um host tenta manter fluxos de trabalho.
>
> System.Data.SqlClient.SqlException: Não foi possível encontrar o procedimento armazenado “System.Activities.DurableInstancing.CreateLockOwner”

As seguintes seções descrevem como ativar persistência para fluxos de trabalho e serviços de fluxo de trabalho usando a instância Store de fluxo de trabalho SQL. Para obter mais informações sobre as propriedades do repositório de instâncias do fluxo de trabalho SQL, consulte [Propriedades do repositório de instâncias do fluxo de trabalho SQL](properties-of-sql-workflow-instance-store.md).

## <a name="enabling-persistence-for-self-hosted-workflows-that-use-workflowapplication"></a>Ativando a persistência para fluxos de trabalho são hospedados que usam WorkflowApplication

Você pode ativar persistência para fluxos de trabalho são hospedados que usam <xref:System.Activities.WorkflowApplication> programaticamente usando o modelo de objeto de <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> . O procedimento a seguir contém as etapas para fazer isso.

#### <a name="to-enable-persistence-for-self-hosted-workflows"></a>Para ativar persistência para fluxos de trabalho são hospedados

1. Adicione uma referência a System.Activities.DurableInstancing.dll.

2. Adicione a seguinte declaração na parte superior do arquivo de origem após a existência declarações “using”.

    ```csharp
    using System.Activities.DurableInstancing;
    ```

3. Construir <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> e o atribui a <xref:System.Activities.WorkflowApplication.InstanceStore%2A> de <xref:System.Activities.WorkflowApplication> conforme mostrado no exemplo de código.

    ```csharp
    SqlWorkflowInstanceStore store =
        new SqlWorkflowInstanceStore("Server=.\\SQLEXPRESS;Initial Catalog=Persistence;Integrated Security=SSPI");

    WorkflowApplication wfApp =
        new WorkflowApplication(new Workflow1());

    wfApp.InstanceStore = store;
    ```

   > [!NOTE]
   > Dependendo de sua edição do SQL Server, o nome do servidor da cadeia de conexão pode ser diferente.

4. Chamar o método de <xref:System.Activities.WorkflowApplication.Persist%2A> no objeto de <xref:System.Activities.WorkflowApplication> para manter um fluxo de trabalho, ou o método de <xref:System.Activities.WorkflowApplication.Unload%2A> para persistir e descarregar um fluxo de trabalho. Você também pode manipular o evento de <xref:System.Activities.WorkflowApplication.PersistableIdle%2A> gerado pelo objeto de <xref:System.Activities.WorkflowApplication> e retornar<xref:System.Activities.PersistableIdleAction.Persist> (ou <xref:System.Activities.PersistableIdleAction.Unload>) o membro apropriado de <xref:System.Activities.PersistableIdleAction>.

   ```csharp
   wfApp.PersistableIdle = delegate(WorkflowApplicationIdleEventArgs e)
   {
       return PersistableIdleAction.Persist;
   };
   ```

> [!NOTE]
> Consulte a etapa [como: criar e executar um fluxo de trabalho de longa execução](how-to-create-and-run-a-long-running-workflow.md) do [tutorial de introdução](getting-started-tutorial.md) para obter instruções passo a passo.

## <a name="enabling-persistence-for-self-hosted-workflow-services-that-use-the-workflowservicehost"></a>Ativando a persistência para os serviços são hospedados de fluxo de trabalho que usam o WorkflowServiceHost

Você pode ativar persistência para os serviços são hospedados de fluxo de trabalho que usam <xref:System.ServiceModel.WorkflowServiceHost> programaticamente usando a classe de <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> ou da classe <xref:System.ServiceModel.Activities.WorkflowServiceHost.DurableInstancingOptions%2A> .

### <a name="using-the-sqlworkflowinstancestorebehavior-class"></a>Usando a classe de SqlWorkflowInstanceStoreBehavior

O procedimento a seguir contém as etapas para usar a classe de <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior> para ativar persistência para serviços são hospedados de fluxo de trabalho.

#### <a name="to-enable-persistence-using-sqlworkflowinstancestorebehavior"></a>Para ativar persistência usando SqlWorkflowInstanceStoreBehavior

1. Adicione uma referência ao System.ServiceModel.dll.

2. Adicione a seguinte declaração na parte superior do arquivo de origem após a existência declarações “using”.

    ```csharp
    using System.ServiceModel.Activities.Description;
    ```

3. Crie uma instância de `WorkflowServiceHost` e adicionar pontos de extremidade para o serviço de fluxo de trabalho.

    ```csharp
    WorkflowServiceHost host = new WorkflowServiceHost(new CountingWorkflow(), new Uri(hostBaseAddress));
    host.AddServiceEndpoint("ICountingWorkflow", new BasicHttpBinding(), "");
    ```

4. Criar um objeto de `SqlWorkflowInstanceStoreBehavior` e para definir propriedades do objeto de comportamento.

    ```csharp
    SqlWorkflowInstanceStoreBehavior instanceStoreBehavior = new SqlWorkflowInstanceStoreBehavior(connectionString);
    instanceStoreBehavior.HostLockRenewalPeriod = new TimeSpan(0, 0, 5);
    instanceStoreBehavior.InstanceCompletionAction = InstanceCompletionAction.DeleteAll;
    instanceStoreBehavior.InstanceLockedExceptionAction = InstanceLockedExceptionAction.AggressiveRetry;
    instanceStoreBehavior.InstanceEncodingOption = InstanceEncodingOption.GZip;
    instanceStoreBehavior.RunnableInstancesDetectionPeriod = new TimeSpan("00:00:02");
    host.Description.Behaviors.Add(instanceStoreBehavior);
    ```

5. Abra o host serviço de fluxo de trabalho.

    ```csharp
    host.Open();
    ```

### <a name="using-the-durableinstancingoptions-property"></a>Usando a propriedade de DurableInstancingOptions

Quando `SqlWorkflowInstanceStoreBehavior` é aplicado, `DurableInstancingOptions.InstanceStore` em `WorkflowServiceHost` está definido para o objeto de `SqlWorkflowInstanceStore` criado usando os valores de configuração. Você pode fazer o mesmo para definir programaticamente a propriedade de <xref:System.ServiceModel.Activities.WorkflowServiceHost.DurableInstancingOptions%2A> de `WorkflowServiceHost` sem usar a classe de `SqlWorkflowInstanceStoreBehavior` conforme mostrado no exemplo de código.

```csharp
workflowServiceHost.DurableInstancingOptions.InstanceStore = sqlInstanceStoreObject;
```

## <a name="enabling-persistence-for-was-hosted-workflow-services-that-use-the-workflowservicehost-using-a-configuration-file"></a>Ativando a persistência para os serviços Estar- hospedados de fluxo de trabalho que usam o WorkflowServiceHost usando um arquivo de configuração

Você pode ativar persistência para serviços são hospedados hospedado ou do Windows do processo de ativação de serviço (-) WAS de fluxo de trabalho usando um arquivo de configuração. Um serviço Estar- hospedado de fluxo de trabalho usa o WorkflowServiceHost como serviços são hospedados de fluxo de trabalho fazem.

O `SqlWorkflowInstanceStoreBehavior` , um comportamento de serviço que permite alterar convenientemente as propriedades de [armazenamento da instância do fluxo de trabalho SQL](sql-workflow-instance-store.md) por meio da configuração XML. Para serviços Estar- hospedados de fluxo de trabalho, use o arquivo web.config. O seguinte exemplo de configuração mostra como configurar a instância Store de fluxo de trabalho do SQL usando o elemento do comportamento de `sqlWorkflowInstanceStore` em um arquivo de configuração.

```xml
<serviceBehaviors>
    <behavior name="">
        <sqlWorkflowInstanceStore
                    connectionString="Data Source=(local);Initial Catalog=DefaultPersistenceProviderDb;Integrated Security=True;Async=true"
                    instanceEncodingOption="GZip | None"
                    instanceCompletionAction="DeleteAll | DeleteNothing"
                    instanceLockedExceptionAction="NoRetry | BasicRetry |AggressiveRetry"
                    hostLockRenewalPeriod="00:00:30"
                    runnableInstancesDetectionPeriod="00:00:05" />

    </behavior>
</serviceBehaviors>
```

Se você não definir valores para `connectionString` ou propriedade de `connectionStringName` , a instância Store de fluxo de trabalho do SQL usa a cadeia de conexão chamado padrão `DefaultSqlWorkflowInstanceStoreConnectionString`.

Quando `SqlWorkflowInstanceStoreBehavior` é aplicado, `DurableInstancingOptions.InstanceStore` em `WorkflowServiceHost` está definido para o objeto de `SqlWorkflowInstanceStore` criado usando os valores de configuração. Você pode fazer o mesmo programaticamente para usar `SqlWorkflowInstanceStore` com `WorkflowServiceHost` sem usar o elemento do comportamento de serviço.

```csharp
workflowServiceHost.DurableInstancingOptions.InstanceStore = sqlInstanceStoreObject;
```

> [!IMPORTANT]
> É recomendável que você não armazene informações sigilosas como nomes de usuário e senhas no arquivo web.config. Se você armazenar informações confidenciais no arquivo web.config, você deve proteger o acesso ao arquivo web.config usando listas de controle de acesso (ACLs) do sistema de arquivos. Além disso, você também pode proteger os valores de configuração em um arquivo de configuração, conforme mencionado na [criptografia de informações de configuração usando a configuração protegida](/previous-versions/aspnet/53tyfkaw(v=vs.100)).

### <a name="machineconfig-elements-related-to-the-sql-workflow-instance-store-feature"></a>Elementos Machine.config relacionados ao recurso de Store de instância de fluxo de trabalho do SQL

A instalação de [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] adicione os seguintes elementos relacionados ao recurso de Store de instância de fluxo de trabalho SQL ao arquivo Machine.config:

- Adiciona o seguinte elemento de extensão de comportamento ao arquivo de Machine.config para que você possa usar o \<sqlWorkflowInstanceStore> elemento de comportamento do serviço no arquivo de configuração para configurar a persistência para seus serviços.

    ```xml
    <configuration>
        <system.serviceModel>
            <extensions>
                <behaviorExtensions>
                    <add name="sqlWorkflowInstanceStore" type="System.Activities.DurableInstancing.SqlWorkflowInstanceStoreElement, System.Activities.DurableInstancing, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35" />
                </behaviorExtensions>
            </extensions>
        </system.serviceModel>
    </configuration>
    ```
