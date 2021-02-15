---
title: Como criar e executar um fluxo de trabalho de execução longa
description: Este artigo mostra como criar um aplicativo de host Windows Forms que dá suporte ao início e à retomada de várias instâncias de fluxo de trabalho e persistência de fluxo de trabalho.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: c0043c89-2192-43c9-986d-3ecec4dd8c9c
ms.openlocfilehash: 701788ac5575ad671afd56db3af4bd247efac8b1
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188459"
---
# <a name="how-to-create-and-run-a-long-running-workflow"></a>Como criar e executar um fluxo de trabalho de execução longa

Um dos recursos centrais do Windows Workflow Foundation (WF) é a capacidade do tempo de execução de persistir e descarregar fluxos de trabalho ociosos em um banco de dados. As etapas em [como executar um fluxo de trabalho](how-to-run-a-workflow.md) demonstraram os conceitos básicos da hospedagem do fluxo de trabalho usando um aplicativo de console. Foram mostrados exemplos de iniciação de fluxos de trabalho, manipuladores do ciclo de vida de fluxo de trabalho e retomada de indicadores. Para demonstrar efetivamente a persistência do fluxo de trabalho, um host de fluxo de trabalho mais complexo é necessário que dá suporte a início e retomada de várias instâncias de fluxo de trabalho. Esta etapa no tutorial demonstra como criar um aplicativo de host do Windows Form que dê suporte ao início e à retomada de várias instâncias de fluxo de trabalho, persistência de fluxo de trabalho e fornece uma base para os recursos avançados como o rastreamento e o controle de versão que são demonstrados em etapas tutoriais subsequentes.

> [!NOTE]
> Esta etapa do tutorial e as etapas subsequentes usam todos os três tipos de fluxo de trabalho de [como: criar um fluxo de trabalho](how-to-create-a-workflow.md).

## <a name="to-create-the-persistence-database"></a>Para criar o banco de dados de persistência

1. Abra SQL Server Management Studio e conecte-se ao servidor local, por exemplo, **.\sqlexpress**. Clique com o botão direito do mouse no nó **bancos** de dados no servidor local e selecione **novo Database**. Nomeie o novo banco de dados **WF45GettingStartedTutorial**, aceite todos os outros valores e selecione **OK**.

    > [!NOTE]
    > Verifique se você tem a permissão **CREATE DATABASE** no servidor local antes de criar o banco de dados.

2. Escolha **abrir**, **arquivo** no menu **arquivo** . Navegue até a seguinte pasta: *C:\Windows\Microsoft.NET\Framework\v4.0.30319\sql\en*

    Selecione os dois arquivos a seguir e clique em **abrir**.

    - *SqlWorkflowInstanceStoreLogic.sql*

    - *SqlWorkflowInstanceStoreSchema.sql*

3. Escolha **SqlWorkflowInstanceStoreSchema. SQL** no menu **janela** . Verifique se **WF45GettingStartedTutorial** está selecionado na lista suspensa **bancos de dados disponíveis** e escolha **executar** no menu **consulta** .

4. Escolha **SqlWorkflowInstanceStoreLogic. SQL** no menu **janela** . Verifique se **WF45GettingStartedTutorial** está selecionado na lista suspensa **bancos de dados disponíveis** e escolha **executar** no menu **consulta** .

    > [!WARNING]
    > É importante executar as duas etapas anteriores na ordem correta. Se as consultas forem executadas fora de ordem, ocorrerão erros e o banco de dados de persistência não estará configurado corretamente.

## <a name="to-add-the-reference-to-the-durableinstancing-assemblies"></a>Para adicionar a referência aos assemblies do DurableInstancing

1. Clique com o botão direito do mouse em **NumberGuessWorkflowHost** em **Gerenciador de soluções** e selecione **Adicionar referência**.

2. Selecione **assemblies** na lista **Adicionar referência** e digite `DurableInstancing` na caixa **Pesquisar assemblies** . Isso filtra os assemblies e facilita a seleção das referências desejadas.

3. Marque a caixa de seleção ao lado de **System. Activities. DurableInstancing** e **System. Runtime. DurableInstancing** na lista de **resultados da pesquisa** e clique em **OK**.

## <a name="to-create-the-workflow-host-form"></a>Para criar o formulário de host de fluxo de trabalho

1. Clique com o botão direito do mouse em **NumberGuessWorkflowHost** em **Gerenciador de soluções** e escolha **Adicionar**, **novo item**.

2. Na lista modelos **instalados** , escolha **Windows Form**, digite `WorkflowHostForm` na caixa **nome** e clique em **Adicionar**.

3. Configure as propriedades a seguir no formulário.

    |Propriedade|Valor|
    |--------------|-----------|
    |FormBorderStyle|FixedSingle|
    |MaximizeBox|Falso|
    |Tamanho|400, 420|

4. Adicione os seguintes controles ao formulário na ordem especificada e configure as propriedades como direcionadas.

    |Control|Propriedade: valor|
    |-------------|---------------------|
    |**Botão**|Nome: NewGame<br /><br /> Local: 13, 13<br /><br /> Tamanho: 75, 23<br /><br /> Texto: novo jogo|
    |**Label**|Local: 94, 18<br /><br /> Texto: Adivinhe um número de 1 a|
    |**ComboBox**|Nome: NumberRange<br /><br /> DropDownstyle: DropDownList<br /><br /> Itens: 10, 100, 1000<br /><br /> Local: 228, 12<br /><br /> Tamanho: 143, 21|
    |**Label**|Local: 13, 43<br /><br /> Texto: tipo de fluxo de trabalho|
    |**ComboBox**|Nome: fluxo de trabalho<br /><br /> DropDownstyle: DropDownList<br /><br /> Itens: StateMachineNumberGuessWorkflow, FlowchartNumberGuessWorkflow, SequentialNumberGuessWorkflow<br /><br /> Local: 94, 40<br /><br /> Tamanho: 277, 21|
    |**Label**|Nome: WorkflowVersion<br /><br /> Local: 13, 362<br /><br /> Texto: versão do fluxo de trabalho|
    |**GroupBox**|Local: 13, 67<br /><br /> Tamanho: 358, 287<br /><br /> Texto: jogo|

    > [!NOTE]
    > Ao adicionar os seguintes controles, coloque-os na GroupBox.

    |Control|Propriedade: valor|
    |-------------|---------------------|
    |**Label**|Local: 7, 20<br /><br /> Texto: ID da instância do fluxo de trabalho|
    |**ComboBox**|Nome: InstanceId<br /><br /> DropDownstyle: DropDownList<br /><br /> Local: 121, 17<br /><br /> Tamanho: 227, 21|
    |**Label**|Local: 7, 47<br /><br /> Texto: estimativa|
    |**TextBox**|Nome: palpite<br /><br /> Local: 50, 44<br /><br /> Tamanho: 65, 20|
    |**Botão**|Nome: EnterGuess<br /><br /> Local: 121, 42<br /><br /> Tamanho: 75, 23<br /><br /> Texto: Insira uma estimativa|
    |**Botão**|Nome: QuitGame<br /><br /> Local: 274, 42<br /><br /> Tamanho: 75, 23<br /><br /> Texto: sair|
    |**TextBox**|Nome: WorkflowStatus<br /><br /> Local: 10, 73<br /><br /> Multiline: true<br /><br /> ReadOnly: verdadeiro<br /><br /> Barras de rolagem: vertical<br /><br /> Tamanho: 338, 208|

5. Defina a propriedade **AcceptButton** do formulário como **EnterGuess**.

 O exemplo a seguir ilustra o formato concluído.

 ![Captura de tela de um formulário de host Windows Workflow Foundation fluxo de trabalho.](./media/how-to-create-and-run-a-long-running-workflow/windows-workflow-foundation-workflowhostform.png)

## <a name="to-add-the-properties-and-helper-methods-of-the-form"></a>Para adicionar as propriedades e os métodos auxiliares do formulário

As etapas nesta seção adicionam propriedades e métodos auxiliares para a classe de formulário que configura a interface de usuário do formulário para dar suporte à execução e à retomada de fluxos de trabalho de palpite de número.

1. Clique com o botão direito do mouse em **WorkflowHostForm** em **Gerenciador de soluções** e escolha **Exibir código**.

2. Adicione as seguintes instruções `using` (ou `Imports`) na parte superior do arquivo com as outras instruções `using` (ou `Imports`).

    ```vb
    Imports System.Activities
    Imports System.Activities.DurableInstancing
    Imports System.Data.SqlClient
    Imports System.IO
    Imports System.Windows.Forms
    ```

    ```csharp
    using System.Activities;
    using System.Activities.DurableInstancing;
    using System.Data.SqlClient;
    using System.IO;
    using System.Windows.Forms;
    ```

3. Adicione as seguintes declarações de membro à classe **WorkflowHostForm** .

    ```vb
    Const connectionString = "Server=.\SQLEXPRESS;Initial Catalog=WF45GettingStartedTutorial;Integrated Security=SSPI"
    Dim store As SqlWorkflowInstanceStore
    Dim workflowStarting As Boolean
    ```

    ```csharp
    const string connectionString = "Server=.\\SQLEXPRESS;Initial Catalog=WF45GettingStartedTutorial;Integrated Security=SSPI";
    SqlWorkflowInstanceStore store;
    bool workflowStarting;
    ```

    > [!NOTE]
    > Se sua cadeia de conexão for diferente, atualize `connectionString` para se referir a seu banco de dados.

4. Adicione uma propriedade `WorkflowInstanceId` à classe `WorkflowFormHost`.

    ```vb
    Public ReadOnly Property WorkflowInstanceId() As Guid
        Get
            If InstanceId.SelectedIndex = -1 Then
                Return Guid.Empty
            Else
                Return New Guid(InstanceId.SelectedItem.ToString())
            End If
        End Get
    End Property
    ```

    ```csharp
    public Guid WorkflowInstanceId
    {
        get
        {
            return InstanceId.SelectedIndex == -1 ? Guid.Empty : (Guid)InstanceId.SelectedItem;
        }
    }
    ```

    A `InstanceId` caixa de combinação exibe uma lista de IDs de instância de fluxo de trabalho persistentes e a `WorkflowInstanceId` propriedade retorna o fluxo de trabalho selecionado no momento.

5. Adicione um manipulador para o evento `Load` do formulário. Para adicionar o manipulador, alterne para o **modo de exibição de design** do formulário, clique no ícone **eventos** na parte superior da janela **Propriedades** e clique duas vezes em **carregar**.

    ```vb
    Private Sub WorkflowHostForm_Load(sender As Object, e As EventArgs) Handles Me.Load

    End Sub
    ```

    ```csharp
    private void WorkflowHostForm_Load(object sender, EventArgs e)
    {

    }
    ```

6. Adicione o código a seguir a `WorkflowHostForm_Load`.

    ```vb
    ' Initialize the store and configure it so that it can be used for
    ' multiple WorkflowApplication instances.
    store = New SqlWorkflowInstanceStore(connectionString)
    WorkflowApplication.CreateDefaultInstanceOwner(store, Nothing, WorkflowIdentityFilter.Any)

    ' Set default ComboBox selections.
    NumberRange.SelectedIndex = 0
    WorkflowType.SelectedIndex = 0

    ListPersistedWorkflows()
    ```

    ```csharp
    // Initialize the store and configure it so that it can be used for
    // multiple WorkflowApplication instances.
    store = new SqlWorkflowInstanceStore(connectionString);
    WorkflowApplication.CreateDefaultInstanceOwner(store, null, WorkflowIdentityFilter.Any);

    // Set default ComboBox selections.
    NumberRange.SelectedIndex = 0;
    WorkflowType.SelectedIndex = 0;

    ListPersistedWorkflows();
    ```

    Quando o formulário carrega, o `SqlWorkflowInstanceStore` é configurado, as caixas de combinação de intervalo e tipo de fluxo de trabalho são definidas com valores padrão, as instâncias de fluxo de trabalho persistidas são adicionadas à caixa de combinação `InstanceId`.

7. Adicione um manipulador `SelectedIndexChanged` para `InstanceId`. Para adicionar o manipulador, alterne para o **modo de exibição de design** do formulário, selecione a caixa de `InstanceId` combinação, clique no ícone **eventos** na parte superior da janela **Propriedades** e clique duas vezes em **SelectedIndexChanged**.

    ```vb
    Private Sub InstanceId_SelectedIndexChanged(sender As Object, e As EventArgs) Handles InstanceId.SelectedIndexChanged

    End Sub
    ```

    ```csharp
    private void InstanceId_SelectedIndexChanged(object sender, EventArgs e)
    {

    }
    ```

8. Adicione o código a seguir a `InstanceId_SelectedIndexChanged`. Sempre que o usuário seleciona um fluxo de trabalho usando a caixa de combinação, esse manipulador atualiza a janela de status.

    ```vb
    If InstanceId.SelectedIndex = -1 Then
        Return
    End If

    ' Clear the status window.
    WorkflowStatus.Clear()

    ' Get the workflow version and display it.
    ' If the workflow is just starting then this info will not
    ' be available in the persistence store so do not try and retrieve it.
    If Not workflowStarting Then
        Dim instance As WorkflowApplicationInstance = _
            WorkflowApplication.GetInstance(WorkflowInstanceId, store)

        WorkflowVersion.Text = _
            WorkflowVersionMap.GetIdentityDescription(instance.DefinitionIdentity)

        ' Unload the instance.
        instance.Abandon()
    End If
    ```

    ```csharp
    if (InstanceId.SelectedIndex == -1)
    {
        return;
    }

    // Clear the status window.
    WorkflowStatus.Clear();

    // Get the workflow version and display it.
    // If the workflow is just starting then this info will not
    // be available in the persistence store so do not try and retrieve it.
    if (!workflowStarting)
    {
        WorkflowApplicationInstance instance =
            WorkflowApplication.GetInstance(this.WorkflowInstanceId, store);

        WorkflowVersion.Text =
            WorkflowVersionMap.GetIdentityDescription(instance.DefinitionIdentity);

        // Unload the instance.
        instance.Abandon();
    }
    ```

9. Adicione o seguinte método `ListPersistedWorkflows` à classe do formulário.

    ```vb
    Private Sub ListPersistedWorkflows()
        Using localCon As New SqlConnection(connectionString)
            Dim localCmd As String = _
                "SELECT [InstanceId] FROM [System.Activities.DurableInstancing].[Instances] ORDER BY [CreationTime]"

            Dim cmd As SqlCommand = localCon.CreateCommand()
            cmd.CommandText = localCmd
            localCon.Open()
            Using reader As SqlDataReader = cmd.ExecuteReader(CommandBehavior.CloseConnection)

                While (reader.Read())
                    ' Get the InstanceId of the persisted Workflow.
                    Dim id As Guid = Guid.Parse(reader(0).ToString())
                    InstanceId.Items.Add(id)
                End While
            End Using
        End Using
    End Sub
    ```

    ```csharp
    using (var localCon = new SqlConnection(connectionString))
    {
        string localCmd =
            "SELECT [InstanceId] FROM [System.Activities.DurableInstancing].[Instances] ORDER BY [CreationTime]";

        SqlCommand cmd = localCon.CreateCommand();
        cmd.CommandText = localCmd;
        localCon.Open();
        using (SqlDataReader reader = cmd.ExecuteReader(CommandBehavior.CloseConnection))
        {
            while (reader.Read())
            {
                // Get the InstanceId of the persisted Workflow.
                Guid id = Guid.Parse(reader[0].ToString());
                InstanceId.Items.Add(id);
            }
        }
    }
    ```

    `ListPersistedWorkflows` consulta o repositório de instâncias em busca de instâncias de fluxo de trabalho persistidas, e adiciona as ids de instância à caixa de combinação `cboInstanceId`.

10. Adicione o seguinte método `UpdateStatus` e o delegado correspondente à classe de formulário. Este método atualiza a janela de status no formulário com o status do fluxo de trabalho em execução no momento.

    ```vb
    Private Delegate Sub UpdateStatusDelegate(msg As String)
    Public Sub UpdateStatus(msg As String)
        ' We may be on a different thread so we need to
        ' make this call using BeginInvoke.
        If InvokeRequired Then
            BeginInvoke(New UpdateStatusDelegate(AddressOf UpdateStatus), msg)
        Else
            If Not msg.EndsWith(vbCrLf) Then
                msg = msg & vbCrLf
            End If

            WorkflowStatus.AppendText(msg)

            ' Ensure that the newly added status is visible.
            WorkflowStatus.SelectionStart = WorkflowStatus.Text.Length
            WorkflowStatus.ScrollToCaret()
        End If
    End Sub
    ```

    ```csharp
    private delegate void UpdateStatusDelegate(string msg);
    public void UpdateStatus(string msg)
    {
        // We may be on a different thread so we need to
        // make this call using BeginInvoke.
        if (InvokeRequired)
        {
            BeginInvoke(new UpdateStatusDelegate(UpdateStatus), msg);
        }
        else
        {
            if (!msg.EndsWith("\r\n"))
            {
                msg += "\r\n";
            }
            WorkflowStatus.AppendText(msg);

            WorkflowStatus.SelectionStart = WorkflowStatus.Text.Length;
            WorkflowStatus.ScrollToCaret();
        }
    }
    ```

11. Adicione o seguinte método `GameOver` e o delegado correspondente à classe de formulário. Quando um fluxo de trabalho é concluído, esse método atualiza a interface do usuário do formulário removendo a ID da instância do fluxo de trabalho concluído da caixa de combinação **InstanceId** .

    ```vb
    Private Delegate Sub GameOverDelegate()
    Private Sub GameOver()
        If InvokeRequired Then
            BeginInvoke(New GameOverDelegate(AddressOf GameOver))
        Else
            ' Remove this instance from the InstanceId combo box.
            InstanceId.Items.Remove(InstanceId.SelectedItem)
            InstanceId.SelectedIndex = -1
        End If
    End Sub
    ```

    ```csharp
    private delegate void GameOverDelegate();
    private void GameOver()
    {
        if (InvokeRequired)
        {
            BeginInvoke(new GameOverDelegate(GameOver));
        }
        else
        {
            // Remove this instance from the combo box.
            InstanceId.Items.Remove(InstanceId.SelectedItem);
            InstanceId.SelectedIndex = -1;
        }
    }
    ```

## <a name="to-configure-the-instance-store-workflow-lifecycle-handlers-and-extensions"></a>Para configurar o repositório de instâncias, os manipuladores do ciclo de vida de fluxo de trabalho e as extensões

1. Adicione o método `ConfigureWorkflowApplication` à classe do formulário.

    ```vb
    Private Sub ConfigureWorkflowApplication(wfApp As WorkflowApplication)

    End Sub
    ```

    ```csharp
    private void ConfigureWorkflowApplication(WorkflowApplication wfApp)
    {
    }
    ```

    Esse método configura o `WorkflowApplication`, adiciona as extensões desejadas e adicionar manipuladores aos eventos de ciclo de vida do fluxo de trabalho.

2. Em `ConfigureWorkflowApplication`, especifique o `SqlWorkflowInstanceStore` para o `WorkflowApplication`.

    ```vb
    ' Configure the persistence store.
    wfApp.InstanceStore = store
    ```

    ```csharp
    // Configure the persistence store.
    wfApp.InstanceStore = store;
    ```

3. Em seguida, crie uma instância `StringWriter` e adicione-a à coleção de `Extensions` do `WorkflowApplication`. Quando um `StringWriter` é adicionado às extensões, ele captura toda a `WriteLine` saída da atividade. Quando o fluxo de trabalho fica ocioso, a saída de `WriteLine` pode ser extraída de `StringWriter` e exibida no formulário.

    ```vb
    ' Add a StringWriter to the extensions. This captures the output
    ' from the WriteLine activities so we can display it in the form.
    Dim sw As New StringWriter()
    wfApp.Extensions.Add(sw)
    ```

    ```csharp
    // Add a StringWriter to the extensions. This captures the output
    // from the WriteLine activities so we can display it in the form.
    var sw = new StringWriter();
    wfApp.Extensions.Add(sw);
    ```

4. Adicione o seguinte manipulador para o evento `Completed`. Quando um fluxo de trabalho for concluído com êxito, o número de sequências realizadas para dar um palpite do número é exibido na janela de status. Se o fluxo de trabalho terminar, as informações da exceção que causaram a conclusão serão exibidas. No final do manipulador, o método `GameOver` é chamado, o que remove o fluxo de trabalho concluído da lista de fluxo de trabalho.

    ```vb
    wfApp.Completed = _
        Sub(e As WorkflowApplicationCompletedEventArgs)
            If e.CompletionState = ActivityInstanceState.Faulted Then
                UpdateStatus($"Workflow Terminated. Exception: {e.TerminationException.GetType().FullName}{vbCrLf}{e.TerminationException.Message}")
            ElseIf e.CompletionState = ActivityInstanceState.Canceled Then
                UpdateStatus("Workflow Canceled.")
            Else
                Dim turns As Integer = Convert.ToInt32(e.Outputs("Turns"))
                UpdateStatus($"Congratulations, you guessed the number in {turns} turns.")
            End If
            GameOver()
        End Sub
    ```

    ```csharp
    wfApp.Completed = delegate(WorkflowApplicationCompletedEventArgs e)
    {
        if (e.CompletionState == ActivityInstanceState.Faulted)
        {
            UpdateStatus($"Workflow Terminated. Exception: {e.TerminationException.GetType().FullName}\r\n{e.TerminationException.Message}");
        }
        else if (e.CompletionState == ActivityInstanceState.Canceled)
        {
            UpdateStatus("Workflow Canceled.");
        }
        else
        {
            int turns = Convert.ToInt32(e.Outputs["Turns"]);
            UpdateStatus($"Congratulations, you guessed the number in {turns} turns.");
        }
        GameOver();
    };
    ```

5. Adicione os seguintes manipuladores `Aborted` e `OnUnhandledException`. O método `GameOver` não é chamado do manipulador `Aborted` porque, quando uma instância de fluxo de trabalho é cancelada, ela não termina e é possível retomar a instância posteriormente.

    ```vb
    wfApp.Aborted = _
        Sub(e As WorkflowApplicationAbortedEventArgs)
            UpdateStatus($"Workflow Aborted. Exception: {e.Reason.GetType().FullName}{vbCrLf}{e.Reason.Message}")
        End Sub

    wfApp.OnUnhandledException = _
        Function(e As WorkflowApplicationUnhandledExceptionEventArgs)
            UpdateStatus($"Unhandled Exception: {e.UnhandledException.GetType().FullName}{vbCrLf}{e.UnhandledException.Message}")
            GameOver()
            Return UnhandledExceptionAction.Terminate
        End Function
    ```

    ```csharp
    wfApp.Aborted = delegate(WorkflowApplicationAbortedEventArgs e)
    {
        UpdateStatus($"Workflow Aborted. Exception: {e.Reason.GetType().FullName}\r\n{e.Reason.Message}");
    };

    wfApp.OnUnhandledException = delegate(WorkflowApplicationUnhandledExceptionEventArgs e)
    {
        UpdateStatus($"Unhandled Exception: {e.UnhandledException.GetType().FullName}\r\n{e.UnhandledException.Message}");
        GameOver();
        return UnhandledExceptionAction.Terminate;
    };
    ```

6. Adicione o seguinte manipulador `PersistableIdle`. Este manipulador recupera a extensão `StringWriter` que foi adicionada, extrai a saída das atividades de `WriteLine` e as exibe na janela de status.

    ```vb
    wfApp.PersistableIdle = _
        Function(e As WorkflowApplicationIdleEventArgs)
            ' Send the current WriteLine outputs to the status window.
            Dim writers = e.GetInstanceExtensions(Of StringWriter)()
            For Each writer In writers
                UpdateStatus(writer.ToString())
            Next
            Return PersistableIdleAction.Unload
        End Function
    ```

    ```csharp
    wfApp.PersistableIdle = delegate(WorkflowApplicationIdleEventArgs e)
    {
        // Send the current WriteLine outputs to the status window.
        var writers = e.GetInstanceExtensions<StringWriter>();
        foreach (var writer in writers)
        {
            UpdateStatus(writer.ToString());
        }
        return PersistableIdleAction.Unload;
    };
    ```

    A enumeração <xref:System.Activities.PersistableIdleAction> tem três valores: <xref:System.Activities.PersistableIdleAction.None>, <xref:System.Activities.PersistableIdleAction.Persist> e <xref:System.Activities.PersistableIdleAction.Unload>. <xref:System.Activities.PersistableIdleAction.Persist> faz com o fluxo de trabalho persistir, mas não faz o fluxo de trabalho descarregar. <xref:System.Activities.PersistableIdleAction.Unload> faz o fluxo de trabalho persistir e ser descarregado.

    O exemplo a seguir é o método `ConfigureWorkflowApplication` concluído.

    ```vb
    Private Sub ConfigureWorkflowApplication(wfApp As WorkflowApplication)
        ' Configure the persistence store.
        wfApp.InstanceStore = store

        ' Add a StringWriter to the extensions. This captures the output
        ' from the WriteLine activities so we can display it in the form.
        Dim sw As New StringWriter()
        wfApp.Extensions.Add(sw)

        wfApp.Completed = _
            Sub(e As WorkflowApplicationCompletedEventArgs)
                If e.CompletionState = ActivityInstanceState.Faulted Then
                    UpdateStatus($"Workflow Terminated. Exception: {e.TerminationException.GetType().FullName}{vbCrLf}{e.TerminationException.Message}")
                ElseIf e.CompletionState = ActivityInstanceState.Canceled Then
                    UpdateStatus("Workflow Canceled.")
                Else
                    Dim turns As Integer = Convert.ToInt32(e.Outputs("Turns"))
                    UpdateStatus($"Congratulations, you guessed the number in {turns} turns.")
                End If
                GameOver()
            End Sub

        wfApp.Aborted = _
            Sub(e As WorkflowApplicationAbortedEventArgs)
                UpdateStatus($"Workflow Aborted. Exception: {e.Reason.GetType().FullName}{vbCrLf}{e.Reason.Message}")
            End Sub

        wfApp.OnUnhandledException = _
            Function(e As WorkflowApplicationUnhandledExceptionEventArgs)
                UpdateStatus($"Unhandled Exception: {e.UnhandledException.GetType().FullName}{vbCrLf}{e.UnhandledException.Message}")
                GameOver()
                Return UnhandledExceptionAction.Terminate
            End Function

        wfApp.PersistableIdle = _
            Function(e As WorkflowApplicationIdleEventArgs)
                ' Send the current WriteLine outputs to the status window.
                Dim writers = e.GetInstanceExtensions(Of StringWriter)()
                For Each writer In writers
                    UpdateStatus(writer.ToString())
                Next
                Return PersistableIdleAction.Unload
            End Function
    End Sub
    ```

    ```csharp
    private void ConfigureWorkflowApplication(WorkflowApplication wfApp)
    {
        // Configure the persistence store.
        wfApp.InstanceStore = store;

        // Add a StringWriter to the extensions. This captures the output
        // from the WriteLine activities so we can display it in the form.
        var sw = new StringWriter();
        wfApp.Extensions.Add(sw);

        wfApp.Completed = delegate(WorkflowApplicationCompletedEventArgs e)
        {
            if (e.CompletionState == ActivityInstanceState.Faulted)
            {
                UpdateStatus($"Workflow Terminated. Exception: {e.TerminationException.GetType().FullName}\r\n{e.TerminationException.Message}");
            }
            else if (e.CompletionState == ActivityInstanceState.Canceled)
            {
                UpdateStatus("Workflow Canceled.");
            }
            else
            {
                int turns = Convert.ToInt32(e.Outputs["Turns"]);
                UpdateStatus($"Congratulations, you guessed the number in {turns} turns.");
            }
            GameOver();
        };

        wfApp.Aborted = delegate(WorkflowApplicationAbortedEventArgs e)
        {
            UpdateStatus($"Workflow Aborted. Exception: {e.Reason.GetType().FullName}\r\n{e.Reason.Message}");
        };

        wfApp.OnUnhandledException = delegate(WorkflowApplicationUnhandledExceptionEventArgs e)
        {
            UpdateStatus($"Unhandled Exception: {e.UnhandledException.GetType().FullName}\r\n{e.UnhandledException.Message}");
            GameOver();
            return UnhandledExceptionAction.Terminate;
        };

        wfApp.PersistableIdle = delegate(WorkflowApplicationIdleEventArgs e)
        {
            // Send the current WriteLine outputs to the status window.
            var writers = e.GetInstanceExtensions<StringWriter>();
            foreach (var writer in writers)
            {
                UpdateStatus(writer.ToString());
            }
            return PersistableIdleAction.Unload;
        };
    }
    ```

## <a name="to-enable-starting-and-resuming-multiple-workflow-types"></a>Para habilitar o início e a retomada de vários tipos de fluxo de trabalho

Para retomar uma instância de fluxo de trabalho, o host precisa fornecer a definição de fluxo de trabalho. Neste tutorial, há três tipos de fluxo de trabalho e as etapas tutoriais subsequentes trazem várias versões desses tipos. `WorkflowIdentity` fornece uma maneira de um aplicativo de host associar informações de identificação a uma instância do fluxo de trabalho persistida. As etapas nesta seção demonstram como criar uma classe de utilitário para ajudar com o mapeamento da identidade de fluxo de trabalho de uma instância do fluxo de trabalho persistida para a definição do fluxo de trabalho correspondente. Para obter mais informações sobre o `WorkflowIdentity` e o controle de versão, consulte [usando a WorkflowIdentity e o controle de versão](using-workflowidentity-and-versioning.md).

1. Clique com o botão direito do mouse em **NumberGuessWorkflowHost** em **Gerenciador de soluções** e escolha **Adicionar**, **classe**. Digite `WorkflowVersionMap` na caixa **nome** e clique em **Adicionar**.

2. Adicione as seguintes instruções `using` ou `Imports` na parte superior do arquivo com as outras instruções `using` ou `Imports`.

    ```vb
    Imports System.Activities
    Imports NumberGuessWorkflowActivities
    ```

    ```csharp
    using System.Activities;
    using NumberGuessWorkflowActivities;
    ```

3. Substitua a declaração de classe `WorkflowVersionMap` pela seguinte declaração.

    ```vb
    Public Module WorkflowVersionMap
        Dim map As Dictionary(Of WorkflowIdentity, Activity)

        ' Current version identities.
        Public StateMachineNumberGuessIdentity As WorkflowIdentity
        Public FlowchartNumberGuessIdentity As WorkflowIdentity
        Public SequentialNumberGuessIdentity As WorkflowIdentity

        Sub New()
            map = New Dictionary(Of WorkflowIdentity, Activity)

            ' Add the current workflow version identities.
            StateMachineNumberGuessIdentity = New WorkflowIdentity With
            {
                .Name = "StateMachineNumberGuessWorkflow",
                .Version = New Version(1, 0, 0, 0)
            }

            FlowchartNumberGuessIdentity = New WorkflowIdentity With
            {
                .Name = "FlowchartNumberGuessWorkflow",
                .Version = New Version(1, 0, 0, 0)
            }

            SequentialNumberGuessIdentity = New WorkflowIdentity With
            {
                .Name = "SequentialNumberGuessWorkflow",
                .Version = New Version(1, 0, 0, 0)
            }

            map.Add(StateMachineNumberGuessIdentity, New StateMachineNumberGuessWorkflow())
            map.Add(FlowchartNumberGuessIdentity, New FlowchartNumberGuessWorkflow())
            map.Add(SequentialNumberGuessIdentity, New SequentialNumberGuessWorkflow())
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

        static WorkflowVersionMap()
        {
            map = new Dictionary<WorkflowIdentity, Activity>();

            // Add the current workflow version identities.
            StateMachineNumberGuessIdentity = new WorkflowIdentity
            {
                Name = "StateMachineNumberGuessWorkflow",
                Version = new Version(1, 0, 0, 0)
            };

            FlowchartNumberGuessIdentity = new WorkflowIdentity
            {
                Name = "FlowchartNumberGuessWorkflow",
                Version = new Version(1, 0, 0, 0)
            };

            SequentialNumberGuessIdentity = new WorkflowIdentity
            {
                Name = "SequentialNumberGuessWorkflow",
                Version = new Version(1, 0, 0, 0)
            };

            map.Add(StateMachineNumberGuessIdentity, new StateMachineNumberGuessWorkflow());
            map.Add(FlowchartNumberGuessIdentity, new FlowchartNumberGuessWorkflow());
            map.Add(SequentialNumberGuessIdentity, new SequentialNumberGuessWorkflow());
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

    O `WorkflowVersionMap` contém três identidades de fluxo de trabalho que mapeiam para as três definições de fluxo de trabalho deste tutorial e é usado nas seções a seguir quando os fluxos de trabalho são iniciados e retomados.

## <a name="to-start-a-new-workflow"></a>Para iniciar um novo fluxo de trabalho

1. Adicione um manipulador `Click` para `NewGame`. Para adicionar o manipulador, alterne para o **modo de exibição de design** do formulário e clique duas vezes em `NewGame` . Um manipulador `NewGame_Click` é adicionado e a exibição alterna para a exibição do código para o formulário. Sempre que o usuário clicar nesse botão, um novo fluxo de trabalho será iniciado.

    ```vb
    Private Sub NewGame_Click(sender As Object, e As EventArgs) Handles NewGame.Click

    End Sub
    ```

    ```csharp
    private void NewGame_Click(object sender, EventArgs e)
    {

    }
    ```

2. Adicione o seguinte código ao manipulador de cliques. O código cria um dicionário de argumentos de entrada para o fluxo de trabalho, fechados pelo nome do argumento. Esse dicionário tem uma entrada que contém o intervalo de números gerados aleatoriamente recuperados da caixa de combinação do intervalo.

    ```vb
    Dim inputs As New Dictionary(Of String, Object)()
    inputs.Add("MaxNumber", Convert.ToInt32(NumberRange.SelectedItem))
    ```

    ```csharp
    var inputs = new Dictionary<string, object>();
    inputs.Add("MaxNumber", Convert.ToInt32(NumberRange.SelectedItem));
    ```

3. Em seguida, adicione o código a seguir que inicia o fluxo de trabalho. O `WorkflowIdentity` e a definição de fluxo de trabalho que corresponde ao tipo de fluxo de trabalho selecionado são recuperados usando a classe auxiliar `WorkflowVersionMap`. Em seguida, uma nova instância de `WorkflowApplication` é criada usando a definição de fluxo de trabalho, `WorkflowIdentity`, e o dicionário de argumentos de entrada.

    ```vb
    Dim identity As WorkflowIdentity = Nothing
    Select Case WorkflowType.SelectedItem.ToString()
        Case "SequentialNumberGuessWorkflow"
            identity = WorkflowVersionMap.SequentialNumberGuessIdentity

        Case "StateMachineNumberGuessWorkflow"
            identity = WorkflowVersionMap.StateMachineNumberGuessIdentity

        Case "FlowchartNumberGuessWorkflow"
            identity = WorkflowVersionMap.FlowchartNumberGuessIdentity
    End Select

    Dim wf As Activity = WorkflowVersionMap.GetWorkflowDefinition(identity)

    Dim wfApp = New WorkflowApplication(wf, inputs, identity)
    ```

    ```csharp
    WorkflowIdentity identity = null;
    switch (WorkflowType.SelectedItem.ToString())
    {
        case "SequentialNumberGuessWorkflow":
            identity = WorkflowVersionMap.SequentialNumberGuessIdentity;
            break;

        case "StateMachineNumberGuessWorkflow":
            identity = WorkflowVersionMap.StateMachineNumberGuessIdentity;
            break;

        case "FlowchartNumberGuessWorkflow":
            identity = WorkflowVersionMap.FlowchartNumberGuessIdentity;
            break;
    };

    Activity wf = WorkflowVersionMap.GetWorkflowDefinition(identity);

    WorkflowApplication wfApp = new WorkflowApplication(wf, inputs, identity);
    ```

4. Em seguida, adicione o código a seguir, que adiciona o fluxo de trabalho à lista de fluxo de trabalho e exibe as informações de versão do fluxo de trabalho no formulário.

    ```vb
    ' Add the workflow to the list and display the version information.
    workflowStarting = True
    InstanceId.SelectedIndex = InstanceId.Items.Add(wfApp.Id)
    WorkflowVersion.Text = identity.ToString()
    workflowStarting = False
    ```

    ```csharp
    // Add the workflow to the list and display the version information.
    workflowStarting = true;
    InstanceId.SelectedIndex = InstanceId.Items.Add(wfApp.Id);
    WorkflowVersion.Text = identity.ToString();
    workflowStarting = false;
    ```

5. Chame `ConfigureWorkflowApplication` para configurar o repositório de instâncias, as extensões e os manipuladores do ciclo de vida de fluxo de trabalho para essa instância `WorkflowApplication`.

    ```vb
    ' Configure the instance store, extensions, and
    ' workflow lifecycle handlers.
    ConfigureWorkflowApplication(wfApp)
    ```

    ```csharp
    // Configure the instance store, extensions, and
    // workflow lifecycle handlers.
    ConfigureWorkflowApplication(wfApp);
    ```

6. Finalmente, chame `Run`.

    ```vb
    ' Start the workflow.
    wfApp.Run()
    ```

    ```csharp
    // Start the workflow.
    wfApp.Run();
    ```

     O exemplo a seguir é o manipulador `NewGame_Click` concluído.

    ```vb
    Private Sub NewGame_Click(sender As Object, e As EventArgs) Handles NewGame.Click
        ' Start a new workflow.
        Dim inputs As New Dictionary(Of String, Object)()
        inputs.Add("MaxNumber", Convert.ToInt32(NumberRange.SelectedItem))

        Dim identity As WorkflowIdentity = Nothing
        Select Case WorkflowType.SelectedItem.ToString()
            Case "SequentialNumberGuessWorkflow"
                identity = WorkflowVersionMap.SequentialNumberGuessIdentity

            Case "StateMachineNumberGuessWorkflow"
                identity = WorkflowVersionMap.StateMachineNumberGuessIdentity

            Case "FlowchartNumberGuessWorkflow"
                identity = WorkflowVersionMap.FlowchartNumberGuessIdentity
        End Select

        Dim wf As Activity = WorkflowVersionMap.GetWorkflowDefinition(identity)

        Dim wfApp = New WorkflowApplication(wf, inputs, identity)

        ' Add the workflow to the list and display the version information.
        workflowStarting = True
        InstanceId.SelectedIndex = InstanceId.Items.Add(wfApp.Id)
        WorkflowVersion.Text = identity.ToString()
        workflowStarting = False

        ' Configure the instance store, extensions, and
        ' workflow lifecycle handlers.
        ConfigureWorkflowApplication(wfApp)

        ' Start the workflow.
        wfApp.Run()
    End Sub
    ```

    ```csharp
    private void NewGame_Click(object sender, EventArgs e)
    {
        var inputs = new Dictionary<string, object>();
        inputs.Add("MaxNumber", Convert.ToInt32(NumberRange.SelectedItem));

        WorkflowIdentity identity = null;
        switch (WorkflowType.SelectedItem.ToString())
        {
            case "SequentialNumberGuessWorkflow":
                identity = WorkflowVersionMap.SequentialNumberGuessIdentity;
                break;

            case "StateMachineNumberGuessWorkflow":
                identity = WorkflowVersionMap.StateMachineNumberGuessIdentity;
                break;

            case "FlowchartNumberGuessWorkflow":
                identity = WorkflowVersionMap.FlowchartNumberGuessIdentity;
                break;
        };

        Activity wf = WorkflowVersionMap.GetWorkflowDefinition(identity);

        var wfApp = new WorkflowApplication(wf, inputs, identity);

        // Add the workflow to the list and display the version information.
        workflowStarting = true;
        InstanceId.SelectedIndex = InstanceId.Items.Add(wfApp.Id);
        WorkflowVersion.Text = identity.ToString();
        workflowStarting = false;

        // Configure the instance store, extensions, and
        // workflow lifecycle handlers.
        ConfigureWorkflowApplication(wfApp);

        // Start the workflow.
        wfApp.Run();
    }
    ```

## <a name="to-resume-a-workflow"></a>Para retomar um fluxo de trabalho

1. Adicione um manipulador `Click` para `EnterGuess`. Para adicionar o manipulador, alterne para o **modo de exibição de design** do formulário e clique duas vezes em `EnterGuess` . Sempre que o usuário clicar nesse botão, um fluxo de trabalho é retomado.

    ```vb
    Private Sub EnterGuess_Click(sender As Object, e As EventArgs) Handles EnterGuess.Click

    End Sub
    ```

    ```csharp
    private void EnterGuess_Click(object sender, EventArgs e)
    {

    }
    ```

2. Adicione o código a seguir para garantir que um fluxo de trabalho seja selecionado na lista de fluxo de trabalho, e que o palpite do usuário seja válido.

    ```vb
    If WorkflowInstanceId = Guid.Empty Then
        MessageBox.Show("Please select a workflow.")
        Return
    End If

    Dim userGuess As Integer
    If Not Int32.TryParse(Guess.Text, userGuess) Then
        MessageBox.Show("Please enter an integer.")
        Guess.SelectAll()
        Guess.Focus()
        Return
    End If
    ```

    ```csharp
    if (WorkflowInstanceId == Guid.Empty)
    {
        MessageBox.Show("Please select a workflow.");
        return;
    }

    int guess;
    if (!Int32.TryParse(Guess.Text, out guess))
    {
        MessageBox.Show("Please enter an integer.");
        Guess.SelectAll();
        Guess.Focus();
        return;
    }
    ```

3. Em seguida, recupere o `WorkflowApplicationInstance` da instância do fluxo de trabalho persistida. Um `WorkflowApplicationInstance` representa uma instância do fluxo de trabalho persistida que ainda não esteja associada a uma definição de fluxo de trabalho. O `DefinitionIdentity` do `WorkflowApplicationInstance` contém o `WorkflowIdentity` da instância do fluxo de trabalho persistida. Neste tutorial, a classe de utilitário `WorkflowVersionMap` é usada para mapear o `WorkflowIdentity` para a definição correta de fluxo de trabalho. Quando a definição de fluxo de trabalho é recuperada, um `WorkflowApplication` é criado, usando a definição correta de fluxo de trabalho.

    ```vb
    Dim instance As WorkflowApplicationInstance = _
        WorkflowApplication.GetInstance(WorkflowInstanceId, store)

    ' Use the persisted WorkflowIdentity to retrieve the correct workflow
    ' definition from the dictionary.
    Dim wf As Activity = _
        WorkflowVersionMap.GetWorkflowDefinition(instance.DefinitionIdentity)

    ' Associate the WorkflowApplication with the correct definition
    Dim wfApp As New WorkflowApplication(wf, instance.DefinitionIdentity)
    ```

    ```csharp
    WorkflowApplicationInstance instance =
        WorkflowApplication.GetInstance(WorkflowInstanceId, store);

    // Use the persisted WorkflowIdentity to retrieve the correct workflow
    // definition from the dictionary.
    Activity wf =
        WorkflowVersionMap.GetWorkflowDefinition(instance.DefinitionIdentity);

    // Associate the WorkflowApplication with the correct definition
    var wfApp = new WorkflowApplication(wf, instance.DefinitionIdentity);
    ```

4. Quando a `WorkflowApplication` é criada, configure o repositório de instâncias, os manipuladores do ciclo de vida de fluxo de trabalho e as extensões chamando `ConfigureWorkflowApplication`. Essas etapas devem ser executadas toda vez que um `WorkflowApplication` novo é criado, e devem ser feitas antes que a instância de fluxo de trabalho seja carregada no `WorkflowApplication`. Depois que o fluxo de trabalho é carregado, ele será retomado com o palpite do usuário.

    ```vb
    ' Configure the extensions and lifecycle handlers.
    ' Do this before the instance is loaded. Once the instance is
    ' loaded it is too late to add extensions.
    ConfigureWorkflowApplication(wfApp)

    ' Load the workflow.
    wfApp.Load(instance)

    ' Resume the workflow.
    wfApp.ResumeBookmark("EnterGuess", userGuess)
    ```

    ```csharp
    // Configure the extensions and lifecycle handlers.
    // Do this before the instance is loaded. Once the instance is
    // loaded it is too late to add extensions.
    ConfigureWorkflowApplication(wfApp);

    // Load the workflow.
    wfApp.Load(instance);

    // Resume the workflow.
    wfApp.ResumeBookmark("EnterGuess", guess);
    ```

5. Finalmente, desmarque a caixa de texto de palpite e prepare o formulário para aceitar outro palpite.

    ```vb
    ' Clear the Guess textbox.
    Guess.Clear()
    Guess.Focus()
    ```

    ```csharp
    // Clear the Guess textbox.
    Guess.Clear();
    Guess.Focus();
    ```

    O exemplo a seguir é o manipulador `EnterGuess_Click` concluído.

    ```vb
    Private Sub EnterGuess_Click(sender As Object, e As EventArgs) Handles EnterGuess.Click
        If WorkflowInstanceId = Guid.Empty Then
            MessageBox.Show("Please select a workflow.")
            Return
        End If

        Dim userGuess As Integer
        If Not Int32.TryParse(Guess.Text, userGuess) Then
            MessageBox.Show("Please enter an integer.")
            Guess.SelectAll()
            Guess.Focus()
            Return
        End If

        Dim instance As WorkflowApplicationInstance = _
            WorkflowApplication.GetInstance(WorkflowInstanceId, store)

        ' Use the persisted WorkflowIdentity to retrieve the correct workflow
        ' definition from the dictionary.
        Dim wf As Activity = _
            WorkflowVersionMap.GetWorkflowDefinition(instance.DefinitionIdentity)

        ' Associate the WorkflowApplication with the correct definition
        Dim wfApp As New WorkflowApplication(wf, instance.DefinitionIdentity)

        ' Configure the extensions and lifecycle handlers.
        ' Do this before the instance is loaded. Once the instance is
        ' loaded it is too late to add extensions.
        ConfigureWorkflowApplication(wfApp)

        ' Load the workflow.
        wfApp.Load(instance)

        ' Resume the workflow.
        wfApp.ResumeBookmark("EnterGuess", userGuess)

        ' Clear the Guess textbox.
        Guess.Clear()
        Guess.Focus()
    End Sub
    ```

    ```csharp
    private void EnterGuess_Click(object sender, EventArgs e)
    {
        if (WorkflowInstanceId == Guid.Empty)
        {
            MessageBox.Show("Please select a workflow.");
            return;
        }

        int guess;
        if (!Int32.TryParse(Guess.Text, out guess))
        {
            MessageBox.Show("Please enter an integer.");
            Guess.SelectAll();
            Guess.Focus();
            return;
        }

        WorkflowApplicationInstance instance =
            WorkflowApplication.GetInstance(WorkflowInstanceId, store);

        // Use the persisted WorkflowIdentity to retrieve the correct workflow
        // definition from the dictionary.
        Activity wf =
            WorkflowVersionMap.GetWorkflowDefinition(instance.DefinitionIdentity);

        // Associate the WorkflowApplication with the correct definition
        var wfApp = new WorkflowApplication(wf, instance.DefinitionIdentity);

        // Configure the extensions and lifecycle handlers.
        // Do this before the instance is loaded. Once the instance is
        // loaded it is too late to add extensions.
        ConfigureWorkflowApplication(wfApp);

        // Load the workflow.
        wfApp.Load(instance);

        // Resume the workflow.
        wfApp.ResumeBookmark("EnterGuess", guess);

        // Clear the Guess textbox.
        Guess.Clear();
        Guess.Focus();
    }
    ```

## <a name="to-terminate-a-workflow"></a>Para encerrar um fluxo de trabalho

1. Adicione um manipulador `Click` para `QuitGame`. Para adicionar o manipulador, alterne para o **modo de exibição de design** do formulário e clique duas vezes em `QuitGame` . Sempre que o usuário clicar nesse botão, o fluxo de trabalho selecionado atual será encerrado.

    ```vb
    Private Sub QuitGame_Click(sender As Object, e As EventArgs) Handles QuitGame.Click

    End Sub
    ```

    ```csharp
    private void QuitGame_Click(object sender, EventArgs e)
    {

    }
    ```

2. Adicione o seguinte código ao manipulador `QuitGame_Click`. Esse código primeiro verifica para garantir que um fluxo de trabalho esteja selecionado na lista de fluxo de trabalho. Em seguida, ele carrega a instância persistida em um `WorkflowApplicationInstance`, use a `DefinitionIdentity` para determinar a definição correta de fluxo de trabalho e depois inicializa o `WorkflowApplication`. Em seguida, as extensões e os manipuladores de ciclo de vida de fluxo de trabalho são configurados com uma chamada para `ConfigureWorkflowApplication`. Quando o `WorkflowApplication` é configurado, ele será carregado e, em seguida, `Terminate` será chamado.

    ```vb
    If WorkflowInstanceId = Guid.Empty Then
        MessageBox.Show("Please select a workflow.")
        Return
    End If

    Dim instance As WorkflowApplicationInstance = _
        WorkflowApplication.GetInstance(WorkflowInstanceId, store)

    ' Use the persisted WorkflowIdentity to retrieve the correct workflow
    ' definition from the dictionary.
    Dim wf As Activity = WorkflowVersionMap.GetWorkflowDefinition(instance.DefinitionIdentity)

    ' Associate the WorkflowApplication with the correct definition.
    Dim wfApp As New WorkflowApplication(wf, instance.DefinitionIdentity)

    ' Configure the extensions and lifecycle handlers.
    ConfigureWorkflowApplication(wfApp)

    ' Load the workflow.
    wfApp.Load(instance)

    ' Terminate the workflow.
    wfApp.Terminate("User resigns.")
    ```

    ```csharp
    if (WorkflowInstanceId == Guid.Empty)
    {
        MessageBox.Show("Please select a workflow.");
        return;
    }

    WorkflowApplicationInstance instance =
        WorkflowApplication.GetInstance(WorkflowInstanceId, store);

    // Use the persisted WorkflowIdentity to retrieve the correct workflow
    // definition from the dictionary.
    Activity wf = WorkflowVersionMap.GetWorkflowDefinition(instance.DefinitionIdentity);

    // Associate the WorkflowApplication with the correct definition
    var wfApp = new WorkflowApplication(wf, instance.DefinitionIdentity);

    // Configure the extensions and lifecycle handlers
    ConfigureWorkflowApplication(wfApp);

    // Load the workflow.
    wfApp.Load(instance);

    // Terminate the workflow.
    wfApp.Terminate("User resigns.");
    ```

## <a name="to-build-and-run-the-application"></a>Para criar e executar o aplicativo

1. Clique duas vezes em **Program.cs** (ou **Module1. vb**) em **Gerenciador de soluções** para exibir o código.

2. Adicione a seguinte instrução `using` (ou `Imports`) na parte superior do arquivo com as outras instruções `using` (ou `Imports`).

    ```vb
    Imports System.Windows.Forms
    ```

    ```csharp
    using System.Windows.Forms;
    ```

3. Remova ou comente o código de hospedagem do fluxo de trabalho existente de [como executar um fluxo de trabalho](how-to-run-a-workflow.md)e substitua-o pelo código a seguir.

    ```vb
    Sub Main()
        Application.EnableVisualStyles()
        Application.Run(New WorkflowHostForm())
    End Sub
    ```

    ```csharp
    static void Main(string[] args)
    {
        Application.EnableVisualStyles();
        Application.Run(new WorkflowHostForm());
    }
    ```

4. Clique com o botão direito do mouse em **NumberGuessWorkflowHost** em **Gerenciador de soluções** e escolha **Propriedades**. Na guia **aplicativo** , especifique **aplicativo do Windows** para o **tipo de saída**. Essa etapa é opcional, mas se não for seguida, a janela do console será exibida além do formulário.

5. Pressione Ctrl+Shift+B para criar o aplicativo.

6. Verifique se **NumberGuessWorkflowHost** está definido como o aplicativo de inicialização e pressione CTRL + F5 para iniciar o aplicativo.

7. Selecione um intervalo para o jogo de adivinhação e o tipo de fluxo de trabalho a ser iniciado e clique em **novo jogo**. Insira uma estimativa na caixa de **estimativa** e clique em **ir** para enviar sua estimativa. Observe que a saída das atividades de `WriteLine` são exibidas no formulário.

8. Inicie vários fluxos de trabalho usando diferentes tipos de fluxo de trabalho e intervalos de números, insira alguns palpites e alterne entre os fluxos de trabalho selecionando na lista **ID da instância do fluxo de trabalho** .

    Observe que, quando você alterna para um novo fluxo de trabalho, os palpites anteriores e o progresso do fluxo de trabalho não são exibidos na janela de status. A razão pela qual o status não está disponível é porque ele não é capturado e salvo em nenhum lugar. Na próxima etapa do tutorial, [como criar um participante de acompanhamento personalizado](how-to-create-a-custom-tracking-participant.md), você cria um participante de acompanhamento personalizado que salva essas informações.
