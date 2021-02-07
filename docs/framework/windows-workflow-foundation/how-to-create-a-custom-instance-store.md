---
description: 'Saiba mais sobre: como criar um repositório de instância personalizado'
title: 'Como: criar uma instância de repositório personalizado'
ms.date: 03/30/2017
ms.assetid: 593c4e9d-8a49-4e12-8257-cee5e6b4c075
ms.openlocfilehash: 3a1a511e6a97dffe510c839aceec8c9d91a77ec1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742128"
---
# <a name="how-to-create-a-custom-instance-store"></a>Como: criar uma instância de repositório personalizado

[!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] contém <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>, um armazenamento de instância que usa o SQL Server para persistir dados de fluxo de trabalho. Se seu aplicativo é necessário manter dados de fluxo de trabalho para outro meio, como um base de dados diferente ou um sistema de arquivos, você pode implementar um armazenamento personalizado de instância. Um armazenamento personalizado de instância é criado estendendo a classe abstrata de <xref:System.Runtime.DurableInstancing.InstanceStore> e implementar métodos que são necessários para a implementação. Para obter uma implementação completa de um repositório de instância personalizado, consulte o exemplo de [processo de compra corporativa](./samples/corporate-purchase-process.md) .

## <a name="implementing-the-begintrycommand-method"></a>Implementando o método de BeginTryCommand

O <xref:System.Runtime.DurableInstancing.InstanceStore.BeginTryCommand%2A> é enviado ao armazenamento de instância pelo mecanismo de persistência. O tipo de parâmetro de `command` indica que comando está sendo executado; este parâmetro pode ser um dos seguintes tipos:

- <xref:System.Activities.DurableInstancing.SaveWorkflowCommand>: O mecanismo de persistência envia este comando no armazenamento de instância quando um fluxo de trabalho deve ser mantido para o suporte de memória. Os dados de persistência de fluxo de trabalho são fornecidos para o método no membro de <xref:System.Activities.DurableInstancing.SaveWorkflowCommand.InstanceData%2A> de parâmetro de `command` .

- <xref:System.Activities.DurableInstancing.LoadWorkflowCommand>: O mecanismo de persistência envia este comando no armazenamento de instância quando um fluxo de trabalho deve ser carregado suporte de memória. A identificação de instância de fluxo de trabalho a ser carregado é fornecido para o método no parâmetro de `instanceId` de propriedade de <xref:System.Runtime.DurableInstancing.InstancePersistenceContext.InstanceView%2A> de parâmetro de `context` .

- <xref:System.Activities.DurableInstancing.CreateWorkflowOwnerCommand>: O mecanismo de persistência envia este comando no armazenamento de instância quando <xref:System.ServiceModel.Activities.WorkflowServiceHost> deve ser registrada como um proprietário de bloqueio. A identificação de instância de fluxo de trabalho atual deve ser fornecido para o armazenamento de instância usando o método de <xref:System.Runtime.DurableInstancing.InstancePersistenceContext.BindInstanceOwner%2A> de parâmetro de `context` .

     O seguinte snippet de código demonstra como implementar o comando de CreateWorkflowOwner atribuir um proprietário explícito de bloqueio.

    ```csharp
    XName WFInstanceScopeName = XName.Get(scopeName, "<namespace>");
    ...
    CreateWorkflowOwnerCommand createCommand = new CreateWorkflowOwnerCommand()
    {
        InstanceOwnerMetadata =
        {
            { WorkflowHostTypeName, new InstanceValue(WFInstanceScopeName) },
        }
    };
    InstanceHandle ownerHandle = store.CreateInstanceHandle();
    store.DefaultInstanceOwner = store.Execute(
                                   ownerHandle,
                                   createCommand,
                                   TimeSpan.FromSeconds(30)).InstanceOwner;
    childInstance.AddInitialInstanceValues(new Dictionary<XName, object>() { { WorkflowHostTypeName, WFInstanceScopeName } });
    ```

- <xref:System.Activities.DurableInstancing.DeleteWorkflowOwnerCommand>: O mecanismo de persistência envia este comando no armazenamento de instância quando o ID de instância de um proprietário de bloqueio pode ser removido do armazenamento de instância. Como com <xref:System.Activities.DurableInstancing.CreateWorkflowOwnerCommand>, a identificação do proprietário de bloqueio deve ser fornecido pelo aplicativo.

     O snippet de código a seguir demonstra como liberar um bloqueio usando <xref:System.Activities.DurableInstancing.DeleteWorkflowOwnerCommand>.

    ```csharp
    static void FreeHandleAndDeleteOwner(InstanceStore store, InstanceHandle handle)
    {
        handle.Free();
        handle = store.CreateInstanceHandle(store.DefaultInstanceOwner);
        try
        {
            // We need this sleep so that we dont prematurely delete the owner, we need time to update the database.
            Thread.Sleep(10000);
            store.Execute(handle, new DeleteWorkflowOwnerCommand(), TimeSpan.FromSeconds(10));
        }
        catch (InstancePersistenceCommandException ex) { Log.Inform(ex.Message); }
        catch (InstanceOwnerException ex) { Log.Inform(ex.Message); }
        catch (OperationCanceledException ex) { Log.Inform(ex.Message); }
        catch (Exception ex) { Log.Inform(ex.Message); }
        finally
        {
            handle.Free();
            store.DefaultInstanceOwner = null;
        }
    }
    ```

     O método anterior deve ser chamado em um bloco try/catch quando uma instância filho é executada.

    ```csharp
    try
    {
        childInstance.Run();
    }
    catch (Exception)
    {
        throw ;
    }
    finally
    {
        FreeHandleAndDeleteOwner(store, ownerHandle);
    }
    ```

- <xref:System.Activities.DurableInstancing.LoadWorkflowByInstanceKeyCommand>: O mecanismo de persistência envia este comando no armazenamento de instância quando uma instância de fluxo de trabalho deve ser carregadas usando a chave de instância de fluxo de trabalho. A identificação de chave da instância pode ser determinado usando o parâmetro de <xref:System.Activities.DurableInstancing.LoadWorkflowByInstanceKeyCommand.LookupInstanceKey%2A> de comando.

- <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand>: O mecanismo de persistência envia este comando no armazenamento de instância recuperar parâmetros de ativação para fluxos de trabalho persistidos para criar um host de fluxo de trabalho que pode carregar em fluxos de trabalho. Este comando é enviado pelo mecanismo em resposta ao armazenamento de instância que aumenta <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent> ao host quando encontra uma instância que pode ser ativada. O armazenamento de instância deve ser monitorado para determinar se há fluxos de trabalho que podem ser ativados.

- <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand>: O mecanismo de persistência envia este comando no armazenamento de instância carregar instâncias praticáveis de fluxo de trabalho. Este comando é enviado pelo mecanismo em resposta ao armazenamento de instância que aumenta <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> ao host quando encontra uma instância que pode ser executada. O armazenamento de instância deve pesquisando para fluxos de trabalho que podem ser executados. O snippet de código a seguir demonstra pesquisando um armazenamento de instância para fluxos de trabalho que podem ser executados ou ativado.

    ```csharp
    public void PollForEvents()
    {
        InstanceOwner[] storeOwners = this.GetInstanceOwners();

        foreach (InstanceOwner owner in storeOwners)
        {
            foreach (InstancePersistenceEvent ppEvent in this.GetEvents(owner))
            {
                if (ppEvent.Equals(HasRunnableWorkflowEvent.Value))
                {
                    bool hasRunnable = GetRunnableEvents(this.StoreId, owner.InstanceOwnerId, isActivatable);
                    if (hasRunnable)
                    {
                        this.SignalEvent(ppEvent, owner);
                    }
                    else
                    {
                        this.ResetEvent(ppEvent, owner);
                    }
                }
                else if(ppEvent.Equals(HasActivatableWorkflowEvent.Value))
                {
                   bool hasActivatable = GetActivatableEvents(this.StoreId, owner.InstanceOwnerId);
                   if (hasActivatable)
                    {
                        this.SignalEvent(ppEvent, owner);
                    }
                    else
                    {
                        this.ResetEvent(ppEvent, owner);
                    }
                }
            }
        }
    }
    ```

     No snippet de código anterior, o armazenamento de instância consulta os eventos disponíveis e examina cada um para determinar se ele é um evento de <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> . Se um for encontrado, o <xref:System.Runtime.DurableInstancing.InstanceStore.SignalEvent%2A> é chamado para sinalizar o host para enviar um comando para o armazenamento de instância. O snippet de código a seguir demonstra uma implementação de um manipulador para este comando.

    ```csharp
    If (command is TryLoadRunnableWorkflowCommand)
    {
        Owner owner;
        CheckOwner(context, command.Name, out owner);
        // Checking instance.Owner is like an InstanceLockQueryResult.
        context.QueriedInstanceStore(new InstanceLockQueryResult(context.InstanceView.InstanceId, context.InstanceView.InstanceOwner.InstanceOwnerId));

        XName ownerService = null;
        InstanceValue value;
        Instance runnableInstance = default(Instance);
        bool foundRunnableInstance = false;

        value = QueryPropertyBag(WorkflowNamespace.WorkflowHostType, owner.Data);
        if (value != null && value.Value is XName)
        {
            ownerService = (XName)value.Value;
        }

        foreach (KeyValuePair<Guid, Instance> instance in MemoryStore.instances)
        {
            if (instance.Value.Owner != Guid.Empty || instance.Value.Completed)
            {
                continue;
            }

            if (ownerService != null)
            {
                value = QueryPropertyBag(WorkflowNamespace.WorkflowHostType, instance.Value.Metadata);
                if (value == null || ((XName)value.Value) != ownerService)
                {
                    continue;
                }
            }

            value = QueryPropertyBag(WorkflowServiceNamespace.SuspendReason, instance.Value.Metadata);
            if (value != null && value.Value != null && value.Value is string)
            {
                continue;
            }

            value = QueryPropertyBag(WorkflowNamespace.Status, instance.Value.Data);
            if (value != null && value.Value is string && ((string)value.Value) == "Executing")
            {
                runnableInstance = instance.Value;
                foundRunnableInstance = true;
            }

            if (!foundRunnableInstance)
            {
                value = QueryPropertyBag(XNamespace.Get("urn:schemas-microsoft-com:System.Activities/4.0/properties").GetName("TimerExpirationTime"), instance.Value.Data);
                if (value != null && value.Value is DateTime && ((DateTime)value.Value) <= DateTime.UtcNow)
                {
                    runnableInstance = instance.Value;
                    foundRunnableInstance = true;
                }
            }

            if (foundRunnableInstance)
            {
                runnableInstance.LockVersion++;
                runnableInstance.Owner = context.InstanceView.InstanceOwner.InstanceOwnerId;
                MemoryStore.instances[instance.Key] = runnableInstance;
                context.BindInstance(instance.Key);
                context.BindAcquiredLock(runnableInstance.LockVersion);

                Dictionary<Guid, IDictionary<XName, InstanceValue>> associatedKeys = new Dictionary<Guid, IDictionary<XName, InstanceValue>>();
                Dictionary<Guid, IDictionary<XName, InstanceValue>> completedKeys = new Dictionary<Guid, IDictionary<XName, InstanceValue>>();
                foreach (KeyValuePair<Guid, Key> keyEntry in MemoryStore.keys)
                {
                if (keyEntry.Value.Instance == context.InstanceView.InstanceId)
                {
                    if (keyEntry.Value.Completed)
                    {
                        completedKeys.Add(keyEntry.Key, DeserializePropertyBag(keyEntry.Value.Metadata));
                    }
                    else
                    {
                        associatedKeys.Add(keyEntry.Key, DeserializePropertyBag(keyEntry.Value.Metadata));
                    }
                }
            }

            context.LoadedInstance(InstanceState.Initialized, DeserializePropertyBag(runnableInstance.Data), DeserializePropertyBag(runnableInstance.Metadata), associatedKeys, completedKeys);
            break;
        }
    }
    ```

    No snippet de código anterior, o armazenamento de instância procura pelas instâncias praticáveis. Se uma instância é encontrada, está associado ao contexto de execução e carregado.

## <a name="using-a-custom-instance-store"></a>Usando um armazenamento personalizado de instância

Para implementar um armazenamento personalizado de instância, atribua uma instância da instância a <xref:System.Activities.WorkflowApplication.InstanceStore%2A>, e implementar o método <xref:System.Activities.WorkflowApplication.PersistableIdle%2A> . Consulte o tutorial [como: criar e executar um fluxo de trabalho de longa execução](how-to-create-and-run-a-long-running-workflow.md) para obter informações específicas.

## <a name="a-sample-instance-store"></a>Um armazenamento de instância de exemplo

O exemplo de código a seguir é uma implementação de repositório de instância completa, obtida do exemplo de [processo de compra corporativa](./samples/corporate-purchase-process.md) . Esse armazenamento de instância persistir dados de fluxo de trabalho a um arquivo XML usando.

```csharp
using System;
using System.Activities.DurableInstancing;
using System.Collections.Generic;
using System.IO;
using System.Runtime.DurableInstancing;
using System.Runtime.Serialization;
using System.ServiceModel.Persistence;
using System.Xml;
using System.Xml.Linq;

namespace Microsoft.Samples.WF.PurchaseProcess
{

    public class XmlWorkflowInstanceStore : InstanceStore
    {
        Guid ownerInstanceID;

        public XmlWorkflowInstanceStore() : this(Guid.NewGuid())
        {

        }

        public XmlWorkflowInstanceStore(Guid id)
        {
            ownerInstanceID = id;
        }

        //Synchronous version of the Begin/EndTryCommand functions
        protected override bool TryCommand(InstancePersistenceContext context, InstancePersistenceCommand command, TimeSpan timeout)
        {
            return EndTryCommand(BeginTryCommand(context, command, timeout, null, null));
        }

        //The persistence engine will send a variety of commands to the configured InstanceStore,
        //such as CreateWorkflowOwnerCommand, SaveWorkflowCommand, and LoadWorkflowCommand.
        //This method is where we will handle those commands
        protected override IAsyncResult BeginTryCommand(InstancePersistenceContext context, InstancePersistenceCommand command, TimeSpan timeout, AsyncCallback callback, object state)
        {
            IDictionary<XName, InstanceValue> data = null;

            //The CreateWorkflowOwner command instructs the instance store to create a new instance owner bound to the instanace handle
            if (command is CreateWorkflowOwnerCommand)
            {
                context.BindInstanceOwner(ownerInstanceID, Guid.NewGuid());
            }
            //The SaveWorkflow command instructs the instance store to modify the instance bound to the instance handle or an instance key
            else if (command is SaveWorkflowCommand)
            {
                SaveWorkflowCommand saveCommand = (SaveWorkflowCommand)command;
                data = saveCommand.InstanceData;

                Save(data);
            }
            //The LoadWorkflow command instructs the instance store to lock and load the instance bound to the identifier in the instance handle
            else if (command is LoadWorkflowCommand)
            {
                string fileName = IOHelper.GetFileName(this.ownerInstanceID);

                try
                {
                    using (FileStream inputStream = new FileStream(fileName, FileMode.Open))
                    {
                        data = LoadInstanceDataFromFile(inputStream);
                        //load the data into the persistence Context
                        context.LoadedInstance(InstanceState.Initialized, data, null, null, null);
                    }
                }
                catch (Exception exception)
                {
                    throw new PersistenceException(exception.Message);
                }
            }

            return new CompletedAsyncResult<bool>(true, callback, state);
        }

        protected override bool EndTryCommand(IAsyncResult result)
        {
            return CompletedAsyncResult<bool>.End(result);
        }

        //Reads data from xml file and creates a dictionary based off of that.
        IDictionary<XName, InstanceValue> LoadInstanceDataFromFile(Stream inputStream)
        {
            IDictionary<XName, InstanceValue> data = new Dictionary<XName, InstanceValue>();

            NetDataContractSerializer s = new NetDataContractSerializer();

            XmlReader rdr = XmlReader.Create(inputStream);
            XmlDocument doc = new XmlDocument();
            doc.Load(rdr);

            XmlNodeList instances = doc.GetElementsByTagName("InstanceValue");
            foreach (XmlElement instanceElement in instances)
            {
                XmlElement keyElement = (XmlElement)instanceElement.SelectSingleNode("descendant::key");
                XName key = (XName)DeserializeObject(s, keyElement);

                XmlElement valueElement = (XmlElement)instanceElement.SelectSingleNode("descendant::value");
                object value = DeserializeObject(s, valueElement);
                InstanceValue instVal = new InstanceValue(value);

                data.Add(key, instVal);
            }

            return data;
        }

        object DeserializeObject(NetDataContractSerializer serializer, XmlElement element)
        {
            object deserializedObject = null;

            MemoryStream stm = new MemoryStream();
            XmlDictionaryWriter wtr = XmlDictionaryWriter.CreateTextWriter(stm);
            element.WriteContentTo(wtr);
            wtr.Flush();
            stm.Position = 0;

            deserializedObject = serializer.Deserialize(stm);

            return deserializedObject;
        }

        //Saves the persistence data to an xml file.
        void Save(IDictionary<XName, InstanceValue> instanceData)
        {
            string fileName = IOHelper.GetFileName(this.ownerInstanceID);
            XmlDocument doc = new XmlDocument();
            doc.LoadXml("<InstanceValues/>");

            foreach (KeyValuePair<XName,InstanceValue> valPair in instanceData)
            {
                XmlElement newInstance = doc.CreateElement("InstanceValue");

                XmlElement newKey = SerializeObject("key", valPair.Key, doc);
                newInstance.AppendChild(newKey);

                XmlElement newValue = SerializeObject("value", valPair.Value.Value, doc);
                newInstance.AppendChild(newValue);

                doc.DocumentElement.AppendChild(newInstance);
            }
            doc.Save(fileName);
       }

        XmlElement SerializeObject(string elementName, object o, XmlDocument doc)
        {
            NetDataContractSerializer s = new NetDataContractSerializer();
            XmlElement newElement = doc.CreateElement(elementName);
            MemoryStream stm = new MemoryStream();

            s.Serialize(stm, o);
            stm.Position = 0;
            StreamReader rdr = new StreamReader(stm);
            newElement.InnerXml = rdr.ReadToEnd();

            return newElement;
        }
    }
}
```
