---
title: Atualização dinâmica
ms.date: 03/30/2017
ms.assetid: 8b6ef19b-9691-4b4b-824c-3c651a9db96e
ms.openlocfilehash: cb4b63a67aa6e9033b227198e2ecc2b1b80db927
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98190150"
---
# <a name="dynamic-update"></a>Atualização dinâmica

A atualização dinâmica fornece um mecanismo para que os desenvolvedores de aplicativos de fluxo de trabalho atualizem a definição de fluxo de trabalho de uma instância do fluxo de trabalho persistida. Isso pode ser implementar uma correção de bug, novos requisitos ou acomodar alterações inesperadas. Este tópico fornece uma visão geral da funcionalidade de atualização dinâmica introduzida no .NET Framework 4,5.

## <a name="dynamic-update"></a>Atualização dinâmica

Para aplicar as atualizações dinâmicas em uma instância fluxo de trabalho persistida, um <xref:System.Activities.DynamicUpdate.DynamicUpdateMap> é criado que contém instruções para o runtime que descreve como modificar a instância de fluxo de trabalho persistida para refletir as alterações desejadas. Assim que o mapa de atualização é criado, ele é aplicado às instâncias desejadas do fluxo de trabalho persistido. Assim que a atualização dinâmica é aplicada, a instância do fluxo de trabalho pode ser retomada usando a nova definição do fluxo de trabalho atualizado. Há quatro etapas necessárias para criar e aplicar um mapa de atualização.

1. [Preparar a definição de fluxo de trabalho para atualização dinâmica](dynamic-update.md#Prepare)

2. [Atualizar a definição de fluxo de trabalho para refletir as alterações desejadas](dynamic-update.md#Update)

3. [Criar o mapa de atualização](dynamic-update.md#Create)

4. [Aplicar o mapa de atualização às instâncias de fluxo de trabalho persistentes desejadas](dynamic-update.md#Apply)

> [!NOTE]
> Observe que as etapas de 1 a 3, que abrangem a criação do mapa de atualização, podem ser executadas de maneira independente de aplicar a atualização. Um cenário comum para o qual o desenvolvedor de fluxo de trabalho criará o mapa de atualização offline e, depois, um administrador aplicará a atualização posteriormente.

Este tópico fornece uma visão geral do processo de atualização dinâmica de adicionar uma nova atividade a uma instância persistida de um fluxo de trabalho Xaml compilado.

### <a name="prepare-the-workflow-definition-for-dynamic-update"></a><a name="Prepare"></a> Preparar a definição de fluxo de trabalho para atualização dinâmica

A primeira etapa do processo de atualização dinâmica é preparar a definição desejada do fluxo de trabalho para atualização. Isso é feito chamando o método <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> e transmitindo na definição de fluxo de trabalho para ser modificado. Esse método valida e percorre a árvore de fluxo de trabalho para identificar todos os objetos, como atividades públicas e variáveis que precisam ser marcadas para que possam ser comparadas posteriormente com a definição do fluxo de trabalho alterado. Quando isso estiver concluído, a árvore de fluxo de trabalho será clonada e anexada à definição original do fluxo de trabalho. Quando o mapa de atualização é criado, a versão atualizada da definição de fluxo de trabalho é comparada com a definição original de fluxo de trabalho e o mapa de atualização é gerado com base nas diferenças.

Para preparar um fluxo de trabalho do Xaml para atualização dinâmica, ele pode ser carregado em um <xref:System.Activities.ActivityBuilder> e, em seguida, o <xref:System.Activities.ActivityBuilder> é passado em <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType>.

> [!NOTE]
> Para obter mais informações sobre como trabalhar com fluxos de trabalho serializados e o <xref:System.Activities.ActivityBuilder> , consulte [serializando fluxos de trabalho e atividades de e para XAML](serializing-workflows-and-activities-to-and-from-xaml.md).

No exemplo a seguir, uma definição de `MortgageWorkflow` (que consiste em um <xref:System.Activities.Statements.Sequence> com várias atividades filhos) é carregada em um <xref:System.Activities.ActivityBuilder> e, em seguida, é preparada para atualização dinâmica. Depois que o método retorna, o <xref:System.Activities.ActivityBuilder> contém a definição original de fluxo de trabalho assim como uma cópia.

```csharp
// Load the MortgageWorkflow definition from Xaml into
// an ActivityBuilder.
XamlXmlReaderSettings readerSettings = new XamlXmlReaderSettings()
{
    LocalAssembly = Assembly.GetExecutingAssembly()
};

XamlXmlReader xamlReader = new XamlXmlReader(@"C:\WorkflowDefinitions\MortgageWorkflow.xaml",
    readerSettings);

ActivityBuilder ab = XamlServices.Load(
    ActivityXamlServices.CreateBuilderReader(xamlReader)) as ActivityBuilder;

// Prepare the workflow definition for dynamic update.
DynamicUpdateServices.PrepareForUpdate(ab);
```

### <a name="update-the-workflow-definition-to-reflect-the-desired-changes"></a><a name="Update"></a> Atualizar a definição de fluxo de trabalho para refletir as alterações desejadas

Quando a definição de fluxo de trabalho tiver sido preparada para atualização, as alterações desejadas poderão ser feitas. Você pode adicionar ou remover atividades, adicionar, mover ou excluir variáveis públicas, adicionar ou remover argumentos, e fazer alterações na assinatura de representantes da atividade. Você não pode remover uma atividade em execução ou modificar a assinatura de um representante em execução. Essas alterações podem ser feitas com o uso de código ou em um designer de fluxo de trabalho hospedado novamente. No exemplo a seguir, uma atividade `VerifyAppraisal` personalizada é adicionada à sequência que compõe o corpo do `MortgageWorkflow` do exemplo anterior.

```csharp
// Make desired changes to the definition. In this example, we are
// inserting a new VerifyAppraisal activity as the 3rd child of the root Sequence.
VerifyAppraisal va = new VerifyAppraisal
{
    Result = new VisualBasicReference<bool>("LoanCriteria")
};

// Get the Sequence that makes up the body of the workflow.
Sequence s = ab.Implementation as Sequence;

// Insert the new activity into the Sequence.
s.Activities.Insert(2, va);
```

### <a name="create-the-update-map"></a><a name="Create"></a> Criar o mapa de atualização

Assim que a definição de fluxo de trabalho que foi preparada para atualização tiver sido modificada, o mapa de atualização poderá ser criado. Para criar um mapa de atualização dinâmica, o método <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=nameWithType> será chamado. Isso retorna um <xref:System.Activities.DynamicUpdate.DynamicUpdateMap> que contém as informações que o runtime precisa para modificar uma instância do fluxo de trabalho persistido de forma que pode ser carregado e retomado com a nova definição de fluxo de trabalho. No exemplo a seguir, um mapa dinâmico é criado para a definição alterada de `MortgageWorkflow` do exemplo anterior.

```csharp
// Create the update map.
DynamicUpdateMap map = DynamicUpdateServices.CreateUpdateMap(ab);
```

Esse mapa de atualização pode ser usado imediatamente para modificar as instâncias de fluxo de trabalho, ou normalmente pode ser salvo e as atualizações aplicadas posteriormente. Uma maneira de salvar o mapa de atualização é serializá-lo em um arquivo, conforme mostrado no exemplo a seguir.

```csharp
// Serialize the update map to a file.
DataContractSerializer serializer = new DataContractSerializer(typeof(DynamicUpdateMap));
using (FileStream fs = System.IO.File.Open(@"C:\WorkflowDefinitions\MortgageWorkflow.map", FileMode.Create))
{
    serializer.WriteObject(fs, map);
}
```

Quando o <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=nameWithType> retornar, a definição clonada de fluxo de trabalho e outras informações de atualização dinâmica que foram adicionadas na chamada para o <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=nameWithType> serão removidas e a definição modificada do fluxo de trabalho estará pronta para ser salva para ser usada posteriormente ao retomar as instâncias de fluxo de trabalho atualizado. No exemplo a seguir, a definição modificada do fluxo de trabalho é salva em `MortgageWorkflow_v1.1.xaml`.

```csharp
// Save the modified workflow definition.
StreamWriter sw = File.CreateText(@"C:\WorkflowDefinitions\MortgageWorkflow_v1.1.xaml");
XamlWriter xw = ActivityXamlServices.CreateBuilderWriter(new XamlXmlWriter(sw, new XamlSchemaContext()));
XamlServices.Save(xw, ab);
sw.Close();
```

### <a name="apply-the-update-map-to-the-desired-persisted-workflow-instances"></a><a name="Apply"></a> Aplicar o mapa de atualização às instâncias de fluxo de trabalho persistentes desejadas

Aplicar o mapa da atualização pode ser feito a qualquer momento após criá-lo. Pode ser feito imediatamente usando a instância do <xref:System.Activities.DynamicUpdate.DynamicUpdateMap> que foi retornada pelo <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.CreateUpdateMap%2A?displayProperty=nameWithType> ou pode ser feito posteriormente usando uma cópia salva do mapa da atualização. Para atualizar uma instância de fluxo de trabalho, carregue-a em um <xref:System.Activities.WorkflowApplicationInstance> usando <xref:System.Activities.WorkflowApplication.GetInstance%2A?displayProperty=nameWithType>. Em seguida, crie um <xref:System.Activities.WorkflowApplication> usando a definição de fluxo de trabalho atualizado e o desejado <xref:System.Activities.WorkflowIdentity> . Este <xref:System.Activities.WorkflowIdentity> pode ser diferente do que foi usado para persistir o fluxo de trabalho original, e é normalmente para refletir que a instância persistida foi modificada. Quando o <xref:System.Activities.WorkflowApplication> é criado, ele é carregado usando a sobrecarga de <xref:System.Activities.WorkflowApplication.Load%2A?displayProperty=nameWithType> que usa um <xref:System.Activities.DynamicUpdate.DynamicUpdateMap> e, em seguida, descarregado com uma chamada para <xref:System.Activities.WorkflowApplication.Unload%2A?displayProperty=nameWithType>. Isso aplica a atualização dinâmica e persiste a instância atualizada do fluxo de trabalho.

```csharp
// Load the serialized update map.
DynamicUpdateMap map;
using (FileStream fs = File.Open(@"C:\WorkflowDefinitions\MortgageWorkflow.map", FileMode.Open))
{
    DataContractSerializer serializer = new DataContractSerializer(typeof(DynamicUpdateMap));
    object updateMap = serializer.ReadObject(fs);
    if (updateMap == null)
    {
        throw new ApplicationException("DynamicUpdateMap is null.");
    }

    map = (DynamicUpdateMap)updateMap;
}

// Retrieve a list of workflow instance ids that corresponds to the
// workflow instances to update. This step is the responsibility of
// the application developer.
List<Guid> ids = GetPersistedWorkflowIds();
foreach (Guid id in ids)
{
    // Get a proxy to the persisted workflow instance.
    SqlWorkflowInstanceStore store = new SqlWorkflowInstanceStore(connectionString);
    WorkflowApplicationInstance instance = WorkflowApplication.GetInstance(id, store);

    // If desired, you can inspect the WorkflowIdentity of the instance
    // using the DefinitionIdentity property to determine whether to apply
    // the update.
    Console.WriteLine(instance.DefinitionIdentity);

    // Create a workflow application. You must specify the updated workflow definition, and
    // you may provide an updated WorkflowIdentity if desired to reflect the update.
    WorkflowIdentity identity = new WorkflowIdentity
    {
        Name = "MortgageWorkflow v1.1",
        Version = new Version(1, 1, 0, 0)
    };

    // Load the persisted workflow instance using the updated workflow definition
    // and with an updated WorkflowIdentity. In this example the MortgageWorkflow class
    // contains the updated definition.
    WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);

    // Apply the dynamic update on the loaded instance.
    wfApp.Load(instance, map);

    // Unload the updated instance.
    wfApp.Unload();
}
```

### <a name="resuming-an-updated-workflow-instance"></a>Retomando uma instância atualizada do fluxo de trabalho

Assim que a atualização dinâmica tiver sido aplicada, a instância do fluxo de trabalho poderá ser retomada. Observe que a nova definição atualizada e o <xref:System.Activities.WorkflowIdentity> devem ser usados.

> [!NOTE]
> Para obter mais informações sobre como trabalhar com o <xref:System.Activities.WorkflowApplication> e o <xref:System.Activities.WorkflowIdentity> , consulte [usando a WorkflowIdentity e o controle de versão](using-workflowidentity-and-versioning.md).

No exemplo a seguir, o fluxo de trabalho do `MortgageWorkflow_v1.1.xaml` do exemplo anterior foi compilado, e foi carregado e retomado usando a definição atualizada do fluxo de trabalho.

```csharp
// Load the persisted workflow instance using the updated workflow definition
// and updated WorkflowIdentity.
WorkflowIdentity identity = new WorkflowIdentity
{
    Name = "MortgageWorkflow v1.1",
    Version = new Version(1, 1, 0, 0)
};

WorkflowApplication wfApp = new WorkflowApplication(new MortgageWorkflow(), identity);

// Configure persistence and desired workflow event handlers.
// (Omitted for brevity.)
ConfigureWorkflowApplication(wfApp);

// Load the persisted workflow instance.
wfApp.Load(InstanceId);

// Resume the workflow.
// wfApp.ResumeBookmark(...);
```
