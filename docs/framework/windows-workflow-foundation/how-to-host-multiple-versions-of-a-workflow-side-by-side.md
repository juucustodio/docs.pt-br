---
title: 'Como: hospedar várias versões de um fluxo de trabalho lado a lado'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 09c575df-e0a3-4f3b-9e01-a7ac59d65287
ms.openlocfilehash: e47440110215d8e60744c26c6351211a2ac08f3a
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98191151"
---
# <a name="how-to-host-multiple-versions-of-a-workflow-side-by-side"></a>Como: hospedar várias versões de um fluxo de trabalho lado a lado

O `WorkflowIdentity` fornece uma maneira para que os desenvolvedores de aplicativos de fluxo de trabalho associem um nome e uma versão a uma definição de fluxo de trabalho, e para que essas informações sejam associadas a uma instância de fluxo de trabalho persistida. Essas informações de identidade podem ser usadas por desenvolvedores de aplicativos de fluxo de trabalho para habilitar cenários como execução lado a lado de várias versões de uma definição de fluxo de trabalho, e fornece o pilar para outra funcionalidade como a atualização dinâmica. Esta etapa no tutorial demonstra como usar o `WorkflowIdentity` para hospedar ao mesmo tempo várias versões de um fluxo de trabalho.

## <a name="in-this-topic"></a>Neste tópico

Nesta etapa do tutorial, as atividades `WriteLine` no fluxo de trabalho são modificadas para fornecer informações adicionais e uma nova atividade `WriteLine` é adicionada. Uma cópia do assembly original do fluxo de trabalho é armazenada e o aplicativo host é atualizado de forma que possa executar os fluxos de trabalho atualizados e originais ao mesmo tempo.

- [Para fazer uma cópia do projeto NumberGuessWorkflowActivities](how-to-host-multiple-versions-of-a-workflow-side-by-side.md#BKMK_BackupCopy)

- [Para atualizar os fluxos de trabalho](how-to-host-multiple-versions-of-a-workflow-side-by-side.md#BKMK_UpdateWorkflows)

  - [Para atualizar o fluxo de trabalho de StateMachine](how-to-host-multiple-versions-of-a-workflow-side-by-side.md#BKMK_UpdateStateMachine)

  - [Para atualizar o fluxo de trabalho de Fluxograma](how-to-host-multiple-versions-of-a-workflow-side-by-side.md#BKMK_UpdateFlowchart)

  - [Para atualizar o fluxo de trabalho Sequencial](how-to-host-multiple-versions-of-a-workflow-side-by-side.md#BKMK_UpdateSequential)

- [Para atualizar WorkflowVersionMap para incluir as versões anteriores do fluxo de trabalho](how-to-host-multiple-versions-of-a-workflow-side-by-side.md#BKMK_UpdateWorkflowVersionMap)

- [Para criar e executar o aplicativo](how-to-host-multiple-versions-of-a-workflow-side-by-side.md#BKMK_BuildAndRun)

> [!NOTE]
> Antes de seguir as etapas deste tópico, execute o aplicativo, inicie vários fluxos de trabalho de cada tipo e dê um ou dois palpites para cada um. Esses fluxos de trabalho persistentes são usados nesta etapa e na seguinte etapa [: como atualizar a definição de uma instância de fluxo de trabalho em execução](how-to-update-the-definition-of-a-running-workflow-instance.md).

### <a name="to-make-a-copy-of-the-numberguessworkflowactivities-project"></a><a name="BKMK_BackupCopy"></a> Para fazer uma cópia do projeto NumberGuessWorkflowActivities

1. Abra a solução **WF45GettingStartedTutorial** no Visual Studio 2012 se ela não estiver aberta.

2. Pressione CTRL+SHIFT+B para criar a solução.

3. Feche a solução **WF45GettingStartedTutorial** .

4. Abra o Windows Explorer e navegue até a pasta onde o arquivo da solução do tutorial e as pastas do projeto estão localizados.

5. Crie uma nova pasta chamada **PreviousVersions** na mesma pasta que **NumberGuessWorkflowHost** e **NumberGuessWorkflowActivities**. Essa pasta é usada para conter os assemblies que contêm as versões diferentes dos fluxos de trabalho usados nas etapas subsequentes do tutorial.

6. Navegue até a pasta **NumberGuessWorkflowActivities\bin\debug** (ou **bin\Release** dependendo das configurações do projeto). Copie **NumberGuessWorkflowActivities.dll** e cole-o na pasta **PreviousVersions**

7. Renomeie **NumberGuessWorkflowActivities.dll** na pasta **PreviousVersions** para **NumberGuessWorkflowActivities_v1.dll**.

    > [!NOTE]
    > As etapas deste tópico demonstram uma maneira de gerenciar os assemblies usados para conter várias versões dos fluxos de trabalho. Outros métodos como nomeação forte dos assemblies e registrando deles no cache de assembly global também podem ser usados.

8. Crie uma nova pasta chamada **NumberGuessWorkflowActivities_du** na mesma pasta que **NumberGuessWorkflowHost**, **NumberGuessWorkflowActivities** e a pasta **PreviousVersions** adicionada recentemente e copie todos os arquivos e subpastas da pasta **NumberGuessWorkflowActivities** para a nova pasta **NumberGuessWorkflowActivities_du** . Esta cópia de backup do projeto para a versão inicial das atividades é usada em [como: atualizar a definição de uma instância de fluxo de trabalho em execução](how-to-update-the-definition-of-a-running-workflow-instance.md).

9. Abra novamente a solução **WF45GettingStartedTutorial** no Visual Studio 2012.

### <a name="to-update-the-workflows"></a><a name="BKMK_UpdateWorkflows"></a> Para atualizar os fluxos de trabalho

Nesta seção, as definições de fluxo de trabalho são atualizadas. As duas atividades `WriteLine` que fornecem comentários sobre o palpite do usuário são atualizadas, e uma nova atividade `WriteLine` é adicionada, que fornece informações adicionais sobre o jogo quando o número é acertado.

#### <a name="to-update-the-statemachine-workflow"></a><a name="BKMK_UpdateStateMachine"></a> Para atualizar o fluxo de trabalho StateMachine

1. No **Gerenciador de soluções**, no projeto **NumberGuessWorkflowActivities** , clique duas vezes em **StateMachineNumberGuessWorkflow. XAML**.

2. Clique duas vezes em **adivinhar transição incorreta** na máquina de estado.

3. Atualize o `Text` do `WriteLine` mais à esquerda na atividade `If`.

    ```vb
    Guess & " is too low."
    ```

    ```csharp
    Guess + " is too low."
    ```

4. Atualize o `Text` do `WriteLine` mais à direita na atividade `If`.

    ```vb
    Guess & " is too high."
    ```

    ```csharp
    Guess + " is too high."
    ```

5. Retorne à exibição de máquina de estado geral no designer de fluxo de trabalho clicando em **StateMachine** na exibição de navegação estrutural na parte superior do designer de fluxo de trabalho.

6. Clique duas vezes na transição de **adivinhação correta** no computador de estado.

7. Arraste uma atividade **WriteLine** da seção **primitivas** da caixa de **ferramentas** e solte-a no rótulo **remover atividade de ação aqui** da transição.

8. Digite a seguinte expressão na caixa de propriedades de `Text`.

    ```vb
    Guess & " is correct. You guessed it in " & Turns & " turns."
    ```

    ```csharp
    Guess + " is correct. You guessed it in " + Turns + " turns."
    ```

#### <a name="to-update-the-flowchart-workflow"></a><a name="BKMK_UpdateFlowchart"></a> Para atualizar o fluxo de trabalho de fluxograma

1. No **Gerenciador de soluções**, no projeto **NumberGuessWorkflowActivities** , clique duas vezes em **FlowchartNumberGuessWorkflow. XAML**.

2. Atualize o `Text` do `WriteLine` mais à esquerda.

    ```vb
    Guess & " is too low."
    ```

    ```csharp
    Guess + " is too low."
    ```

3. Atualize o `Text` do `WriteLine` mais à direita.

    ```vb
    Guess & " is too high."
    ```

    ```csharp
    Guess + " is too high."
    ```

4. Arraste uma atividade **WriteLine** da seção **primitivas** da caixa de **ferramentas** e solte-a no ponto de distribuição da `True` ação da extremidade superior `FlowDecision` . A atividade `WriteLine` é adicionada ao fluxograma e vinculada à ação `True` do `FlowDecision`.

5. Digite a seguinte expressão na caixa de propriedades de `Text`.

    ```vb
    Guess & " is correct. You guessed it in " & Turns & " turns."
    ```

    ```csharp
    Guess + " is correct. You guessed it in " + Turns + " turns."
    ```

#### <a name="to-update-the-sequential-workflow"></a><a name="BKMK_UpdateSequential"></a> Para atualizar o fluxo de trabalho Sequencial

1. No **Gerenciador de soluções**, no projeto **NumberGuessWorkflowActivities** , clique duas vezes em **SequentialNumberGuessWorkflow. XAML**.

2. Atualize o `Text` do `WriteLine` mais à esquerda na atividade `If`.

    ```vb
    Guess & " is too low."
    ```

    ```csharp
    Guess + " is too low."
    ```

3. Atualize o `Text` da atividade `WriteLine` mais à direita na atividade `If`.

    ```vb
    Guess & " is too high."
    ```

    ```csharp
    Guess + " is too high."
    ```

4. Arraste uma atividade **WriteLine** da seção **primitivas** da caixa de **ferramentas** e solte-a após a atividade **DoWhile** para que o **WriteLine** seja a atividade final na `Sequence` atividade raiz.

5. Digite a seguinte expressão na caixa de propriedades de `Text`.

    ```vb
    Guess & " is correct. You guessed it in " & Turns & " turns."
    ```

    ```csharp
    Guess + " is correct. You guessed it in " + Turns + " turns."
    ```

### <a name="to-update-workflowversionmap-to-include-the-previous-workflow-versions"></a><a name="BKMK_UpdateWorkflowVersionMap"></a> Para atualizar o WorkflowVersionMap para incluir as versões anteriores do fluxo de trabalho

1. Clique duas vezes em **WorkflowVersionMap.cs** (ou **WorkflowVersionMap. vb**) no projeto **NumberGuessWorkflowHost** para abri-lo.

2. Adicione as seguintes instruções `using` (ou `Imports`) na parte superior do arquivo com as outras instruções `using` (ou `Imports`).

    ```vb
    Imports System.Reflection
    Imports System.IO
    ```

    ```csharp
    using System.Reflection;
    using System.IO;
    ```

3. Adicione três novas identidades de fluxo de trabalho abaixo das três declarações de identidade de fluxo de trabalho existentes. Essas novas identidades de fluxo de trabalho `v1` serão usadas para fornecer a definição correta para fluxos de trabalho iniciados antes que as atualizações foram feitas.

    ```vb
    'Current version identities.
    Public StateMachineNumberGuessIdentity As WorkflowIdentity
    Public FlowchartNumberGuessIdentity As WorkflowIdentity
    Public SequentialNumberGuessIdentity As WorkflowIdentity

    'v1 Identities.
    Public StateMachineNumberGuessIdentity_v1 As WorkflowIdentity
    Public FlowchartNumberGuessIdentity_v1 As WorkflowIdentity
    Public SequentialNumberGuessIdentity_v1 As WorkflowIdentity
    ```

    ```csharp
    // Current version identities.
    static public WorkflowIdentity StateMachineNumberGuessIdentity;
    static public WorkflowIdentity FlowchartNumberGuessIdentity;
    static public WorkflowIdentity SequentialNumberGuessIdentity;

    // v1 identities.
    static public WorkflowIdentity StateMachineNumberGuessIdentity_v1;
    static public WorkflowIdentity FlowchartNumberGuessIdentity_v1;
    static public WorkflowIdentity SequentialNumberGuessIdentity_v1;
    ```

4. No construtor `WorkflowVersionMap`, atualize a propriedade `Version` das três identidades atuais de fluxo de trabalho para `2.0.0.0`.

    ```vb
    'Add the current workflow version identities.
    StateMachineNumberGuessIdentity = New WorkflowIdentity With
    {
        .Name = "StateMachineNumberGuessWorkflow",
        .Version = New Version(2, 0, 0, 0)
    }

    FlowchartNumberGuessIdentity = New WorkflowIdentity With
    {
        .Name = "FlowchartNumberGuessWorkflow",
        .Version = New Version(2, 0, 0, 0)
    }

    SequentialNumberGuessIdentity = New WorkflowIdentity With
    {
        .Name = "SequentialNumberGuessWorkflow",
        .Version = New Version(2, 0, 0, 0)
    }

    map.Add(StateMachineNumberGuessIdentity, New StateMachineNumberGuessWorkflow())
    map.Add(FlowchartNumberGuessIdentity, New FlowchartNumberGuessWorkflow())
    map.Add(SequentialNumberGuessIdentity, New SequentialNumberGuessWorkflow())
    ```

    ```csharp
    // Add the current workflow version identities.
    StateMachineNumberGuessIdentity = new WorkflowIdentity
    {
        Name = "StateMachineNumberGuessWorkflow",
        // Version = new Version(1, 0, 0, 0),
        Version = new Version(2, 0, 0, 0)
    };

    FlowchartNumberGuessIdentity = new WorkflowIdentity
    {
        Name = "FlowchartNumberGuessWorkflow",
        // Version = new Version(1, 0, 0, 0),
        Version = new Version(2, 0, 0, 0)
    };

    SequentialNumberGuessIdentity = new WorkflowIdentity
    {
        Name = "SequentialNumberGuessWorkflow",
        // Version = new Version(1, 0, 0, 0),
        Version = new Version(2, 0, 0, 0)
    };

    map.Add(StateMachineNumberGuessIdentity, new StateMachineNumberGuessWorkflow());
    map.Add(FlowchartNumberGuessIdentity, new FlowchartNumberGuessWorkflow());
    map.Add(SequentialNumberGuessIdentity, new SequentialNumberGuessWorkflow());
    ```

    Esse código adiciona as versões atuais dos fluxos de trabalho para o dicionário que usa as versões atuais que são referenciadas no projeto, de modo que o código que inicializa as definições de fluxo de trabalho não precise ser atualizado.

5. Adicione o seguinte código no construtor imediatamente depois do código que adiciona as versões atuais ao dicionário.

    ```vb
    'Initialize the previous workflow version identities.
    StateMachineNumberGuessIdentity_v1 = New WorkflowIdentity With
    {
        .Name = "StateMachineNumberGuessWorkflow",
        .Version = New Version(1, 0, 0, 0)
    }

    FlowchartNumberGuessIdentity_v1 = New WorkflowIdentity With
    {
        .Name = "FlowchartNumberGuessWorkflow",
        .Version = New Version(1, 0, 0, 0)
    }

    SequentialNumberGuessIdentity_v1 = New WorkflowIdentity With
    {
        .Name = "SequentialNumberGuessWorkflow",
        .Version = New Version(1, 0, 0, 0)
    }
    ```

    ```csharp
    // Initialize the previous workflow version identities.
    StateMachineNumberGuessIdentity_v1 = new WorkflowIdentity
    {
        Name = "StateMachineNumberGuessWorkflow",
        Version = new Version(1, 0, 0, 0)
    };

    FlowchartNumberGuessIdentity_v1 = new WorkflowIdentity
    {
        Name = "FlowchartNumberGuessWorkflow",
        Version = new Version(1, 0, 0, 0)
    };

    SequentialNumberGuessIdentity_v1 = new WorkflowIdentity
    {
        Name = "SequentialNumberGuessWorkflow",
        Version = new Version(1, 0, 0, 0)
    };
    ```

    Essas identidades de fluxo de trabalho são associadas às versões iniciais das definições de fluxo de trabalho correspondentes.

6. Em seguida, carregue o assembly que contém a versão inicial das definições de fluxo de trabalho, e crie e adicione as definições correspondentes do fluxo de trabalho ao dicionário.

    ```vb
    'Add the previous version workflow identities to the dictionary along with
    'the corresponding workflow definitions loaded from the v1 assembly.
    'Assembly.LoadFile requires an absolute path so convert this relative path
    'to an absolute path.
    Dim v1AssemblyPath As String = "..\..\..\PreviousVersions\NumberGuessWorkflowActivities_v1.dll"
    v1AssemblyPath = Path.GetFullPath(v1AssemblyPath)
    Dim v1Assembly As Assembly = Assembly.LoadFile(v1AssemblyPath)

    map.Add(StateMachineNumberGuessIdentity_v1,
        v1Assembly.CreateInstance("NumberGuessWorkflowActivities.StateMachineNumberGuessWorkflow"))

    map.Add(SequentialNumberGuessIdentity_v1,
        v1Assembly.CreateInstance("NumberGuessWorkflowActivities.SequentialNumberGuessWorkflow"))

    map.Add(FlowchartNumberGuessIdentity_v1,
        v1Assembly.CreateInstance("NumberGuessWorkflowActivities.FlowchartNumberGuessWorkflow"))
    ```

    ```csharp
    // Add the previous version workflow identities to the dictionary along with
    // the corresponding workflow definitions loaded from the v1 assembly.
    // Assembly.LoadFile requires an absolute path so convert this relative path
    // to an absolute path.
    string v1AssemblyPath = @"..\..\..\PreviousVersions\NumberGuessWorkflowActivities_v1.dll";
    v1AssemblyPath = Path.GetFullPath(v1AssemblyPath);
    Assembly v1Assembly = Assembly.LoadFile(v1AssemblyPath);

    map.Add(StateMachineNumberGuessIdentity_v1,
        v1Assembly.CreateInstance("NumberGuessWorkflowActivities.StateMachineNumberGuessWorkflow") as Activity);

    map.Add(SequentialNumberGuessIdentity_v1,
        v1Assembly.CreateInstance("NumberGuessWorkflowActivities.SequentialNumberGuessWorkflow") as Activity);

    map.Add(FlowchartNumberGuessIdentity_v1,
        v1Assembly.CreateInstance("NumberGuessWorkflowActivities.FlowchartNumberGuessWorkflow") as Activity);
    ```

    O exemplo a seguir é a listagem completa para a classe `WorkflowVersionMap` atualizada.

    ```vb
    Public Module WorkflowVersionMap
        Dim map As Dictionary(Of WorkflowIdentity, Activity)

        'Current version identities.
        Public StateMachineNumberGuessIdentity As WorkflowIdentity
        Public FlowchartNumberGuessIdentity As WorkflowIdentity
        Public SequentialNumberGuessIdentity As WorkflowIdentity

        'v1 Identities.
        Public StateMachineNumberGuessIdentity_v1 As WorkflowIdentity
        Public FlowchartNumberGuessIdentity_v1 As WorkflowIdentity
        Public SequentialNumberGuessIdentity_v1 As WorkflowIdentity

        Sub New()
            map = New Dictionary(Of WorkflowIdentity, Activity)

            'Add the current workflow version identities.
            StateMachineNumberGuessIdentity = New WorkflowIdentity With
            {
                .Name = "StateMachineNumberGuessWorkflow",
                .Version = New Version(2, 0, 0, 0)
            }

            FlowchartNumberGuessIdentity = New WorkflowIdentity With
            {
                .Name = "FlowchartNumberGuessWorkflow",
                .Version = New Version(2, 0, 0, 0)
            }

            SequentialNumberGuessIdentity = New WorkflowIdentity With
            {
                .Name = "SequentialNumberGuessWorkflow",
                .Version = New Version(2, 0, 0, 0)
            }

            map.Add(StateMachineNumberGuessIdentity, New StateMachineNumberGuessWorkflow())
            map.Add(FlowchartNumberGuessIdentity, New FlowchartNumberGuessWorkflow())
            map.Add(SequentialNumberGuessIdentity, New SequentialNumberGuessWorkflow())

            'Initialize the previous workflow version identities.
            StateMachineNumberGuessIdentity_v1 = New WorkflowIdentity With
            {
                .Name = "StateMachineNumberGuessWorkflow",
                .Version = New Version(1, 0, 0, 0)
            }

            FlowchartNumberGuessIdentity_v1 = New WorkflowIdentity With
            {
                .Name = "FlowchartNumberGuessWorkflow",
                .Version = New Version(1, 0, 0, 0)
            }

            SequentialNumberGuessIdentity_v1 = New WorkflowIdentity With
            {
                .Name = "SequentialNumberGuessWorkflow",
                .Version = New Version(1, 0, 0, 0)
            }

            'Add the previous version workflow identities to the dictionary along with
            'the corresponding workflow definitions loaded from the v1 assembly.
            'Assembly.LoadFile requires an absolute path so convert this relative path
            'to an absolute path.
            Dim v1AssemblyPath As String = "..\..\..\PreviousVersions\NumberGuessWorkflowActivities_v1.dll"
            v1AssemblyPath = Path.GetFullPath(v1AssemblyPath)
            Dim v1Assembly As Assembly = Assembly.LoadFile(v1AssemblyPath)

            map.Add(StateMachineNumberGuessIdentity_v1,
                v1Assembly.CreateInstance("NumberGuessWorkflowActivities.StateMachineNumberGuessWorkflow"))

            map.Add(SequentialNumberGuessIdentity_v1,
                v1Assembly.CreateInstance("NumberGuessWorkflowActivities.SequentialNumberGuessWorkflow"))

            map.Add(FlowchartNumberGuessIdentity_v1,
                v1Assembly.CreateInstance("NumberGuessWorkflowActivities.FlowchartNumberGuessWorkflow"))
        End Sub

        Public Function GetWorkflowDefinition(identity As WorkflowIdentity) As Activity
            Return map(identity)
        End Function

        Public Function GetIdentityDescription(identity As WorkflowIdentity) As String
            Return identity.ToString()
        End Function
    End Module
    ```

    ```csharp
    public static class WorkflowVersionMap
    {
        static Dictionary<WorkflowIdentity, Activity> map;

        // Current version identities.
        static public WorkflowIdentity StateMachineNumberGuessIdentity;
        static public WorkflowIdentity FlowchartNumberGuessIdentity;
        static public WorkflowIdentity SequentialNumberGuessIdentity;

        // v1 identities.
        static public WorkflowIdentity StateMachineNumberGuessIdentity_v1;
        static public WorkflowIdentity FlowchartNumberGuessIdentity_v1;
        static public WorkflowIdentity SequentialNumberGuessIdentity_v1;

        static WorkflowVersionMap()
        {
            map = new Dictionary<WorkflowIdentity, Activity>();

            // Add the current workflow version identities.
            StateMachineNumberGuessIdentity = new WorkflowIdentity
            {
                Name = "StateMachineNumberGuessWorkflow",
                // Version = new Version(1, 0, 0, 0),
                Version = new Version(2, 0, 0, 0)
            };

            FlowchartNumberGuessIdentity = new WorkflowIdentity
            {
                Name = "FlowchartNumberGuessWorkflow",
                // Version = new Version(1, 0, 0, 0),
                Version = new Version(2, 0, 0, 0)
            };

            SequentialNumberGuessIdentity = new WorkflowIdentity
            {
                Name = "SequentialNumberGuessWorkflow",
                // Version = new Version(1, 0, 0, 0),
                Version = new Version(2, 0, 0, 0)
            };

            map.Add(StateMachineNumberGuessIdentity, new StateMachineNumberGuessWorkflow());
            map.Add(FlowchartNumberGuessIdentity, new FlowchartNumberGuessWorkflow());
            map.Add(SequentialNumberGuessIdentity, new SequentialNumberGuessWorkflow());

            // Initialize the previous workflow version identities.
            StateMachineNumberGuessIdentity_v1 = new WorkflowIdentity
            {
                Name = "StateMachineNumberGuessWorkflow",
                Version = new Version(1, 0, 0, 0)
            };

            FlowchartNumberGuessIdentity_v1 = new WorkflowIdentity
            {
                Name = "FlowchartNumberGuessWorkflow",
                Version = new Version(1, 0, 0, 0)
            };

            SequentialNumberGuessIdentity_v1 = new WorkflowIdentity
            {
                Name = "SequentialNumberGuessWorkflow",
                Version = new Version(1, 0, 0, 0)
            };

            // Add the previous version workflow identities to the dictionary along with
            // the corresponding workflow definitions loaded from the v1 assembly.
            // Assembly.LoadFile requires an absolute path so convert this relative path
            // to an absolute path.
            string v1AssemblyPath = @"..\..\..\PreviousVersions\NumberGuessWorkflowActivities_v1.dll";
            v1AssemblyPath = Path.GetFullPath(v1AssemblyPath);
            Assembly v1Assembly = Assembly.LoadFile(v1AssemblyPath);

            map.Add(StateMachineNumberGuessIdentity_v1,
                v1Assembly.CreateInstance("NumberGuessWorkflowActivities.StateMachineNumberGuessWorkflow") as Activity);

            map.Add(SequentialNumberGuessIdentity_v1,
                v1Assembly.CreateInstance("NumberGuessWorkflowActivities.SequentialNumberGuessWorkflow") as Activity);

            map.Add(FlowchartNumberGuessIdentity_v1,
                v1Assembly.CreateInstance("NumberGuessWorkflowActivities.FlowchartNumberGuessWorkflow") as Activity);
        }

        public static Activity GetWorkflowDefinition(WorkflowIdentity identity)
        {
            return map[identity];
        }

        public static string GetIdentityDescription(WorkflowIdentity identity)
        {
            return identity.ToString();
        }
    }
    ```

### <a name="to-build-and-run-the-application"></a><a name="BKMK_BuildAndRun"></a> Para compilar e executar o aplicativo

1. Pressione CTRL+SHIFT+B para criar o aplicativo, e CTRL+F5 para iniciar.

2. Inicie um novo fluxo de trabalho clicando em **novo jogo**. A versão do fluxo de trabalho é exibida abaixo da janela de status e reflete a versão atualizada do `WorkflowIdentity` associado. Faça uma anotação do `InstanceId` para que você possa exibir o arquivo de rastreamento para o fluxo de trabalho quando ele for concluído, e insira os palpites até que o jogo seja concluído. Observe como o palpite do usuário é exibido nas informações exibidas na janela de status com base nas atualizações das atividades `WriteLine`.

    ```console
    Please enter a number between 1 and 10
    5 is too high.
    Please enter a number between 1 and 10
    3 is too high.
    Please enter a number between 1 and 10
    1 is too low.
    Please enter a number between 1 and 10
    Congratulations, you guessed the number in 4 turns.
    ```

    > [!NOTE]
    > O texto atualizado das atividades `WriteLine` é exibido, mas não a saída final da atividade `WriteLine` final que foi adicionada neste tópico. Isso ocorre porque a janela de status é atualizada pelo manipulador `PersistableIdle`. Como o fluxo de trabalho é concluído e não fica ocioso após a atividade final, o manipulador `PersistableIdle` não é chamado. No entanto, uma mensagem semelhante é exibida na janela de status pelo manipulador `Completed`. Se desejar, um código pode ser adicionado ao manipulador `Completed` para extrair o texto de `StringWriter` e exibi-lo na janela de status.

3. Abra o Windows Explorer e navegue até a pasta **NumberGuessWorkflowHost\bin\debug** (ou **bin\Release** dependendo das configurações do projeto) e abra o arquivo de acompanhamento usando o bloco de notas que corresponde ao fluxo de trabalho concluído. Se você não fez uma anotação do `InstanceId` , você pode identificar o arquivo de acompanhamento correto usando as informações de **data de modificação** no Windows Explorer.

    ```console
    Please enter a number between 1 and 10
    5 is too high.
    Please enter a number between 1 and 10
    3 is too high.
    Please enter a number between 1 and 10
    1 is too low.
    Please enter a number between 1 and 10
    2 is correct. You guessed it in 4 turns.
    ```

    A saída `WriteLine` atualizada está contida no arquivo de rastreamento, incluindo a saída de `WriteLine` que foi adicionada neste tópico.

4. Alterne novamente para o aplicativo de palpite de número e selecione um dos fluxos de trabalho que foi iniciado antes que as atualizações foram feitas. Você pode identificar a versão do fluxo de trabalho selecionado no momento examinando as informações de versão que são exibidas embaixo da janela de status. Insira alguns palpites e observe que as atualizações de status correspondem à saída da atividade `WriteLine` da versão anterior, e não incluem o palpite do usuário. Isso ocorre porque esses fluxos de trabalho estão usando a definição do fluxo de trabalho anterior que não tem as atualizações `WriteLine`.

    Na próxima etapa, [como atualizar a definição de uma instância de fluxo de trabalho em execução](how-to-update-the-definition-of-a-running-workflow-instance.md), as `v1` instâncias de fluxo de trabalho em execução são atualizadas para que contenham a nova funcionalidade que as `v2` instâncias.
