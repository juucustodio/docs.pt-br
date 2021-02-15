---
description: 'Saiba mais sobre: tarefa 2: hospedar o Designer de Fluxo de Trabalho'
title: 'Tarefa 2: Hospedar o Designer de Fluxo de Trabalho'
ms.date: 03/30/2017
ms.assetid: 0a29b138-270d-4846-b78e-2b875e34e501
ms.openlocfilehash: 5a00c9db831575dfe7f6f2b6e041f18877c60118
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755194"
---
# <a name="task-2-host-the-workflow-designer"></a>Tarefa 2: Hospedar o Designer de Fluxo de Trabalho

Este tópico descreve o procedimento para hospedar uma instância do Designer de Fluxo de Trabalho do Windows em um aplicativo do Windows Presentation Foundation (WPF).

O procedimento configura o controle de **grade** que contém o designer, cria programaticamente uma instância do <xref:System.Activities.Presentation.WorkflowDesigner> que contém uma <xref:System.Activities.Statements.Sequence> atividade padrão, registra os metadados do designer para fornecer suporte de designer para todas as atividades internas e hospeda o designer de fluxo de trabalho no aplicativo WPF.

## <a name="to-host-the-workflow-designer"></a>Para hospedar o designer de fluxo de trabalho

1. Abra o projeto HostingApplication que você criou na [tarefa 1: criar um novo aplicativo Windows Presentation Foundation](task-1-create-a-new-wpf-app.md).

2. Ajuste o tamanho da janela para facilitar o uso do Designer de Fluxo de Trabalho. Para fazer isso, selecione **MainWindow** no designer, pressione F4 para exibir a janela **Propriedades** e, na seção **layout** , defina a **largura** como um valor de 600 e a **altura** como um valor de 350.

3. Defina o nome da grade selecionando o painel de **grade** no designer (clique na caixa dentro de **MainWindow**) e definindo a propriedade **Name** na parte superior da janela **Properties** como "grid1".

4. Na janela **Propriedades** , clique nas reticências (**...**) ao lado da `ColumnDefinitions` propriedade para abrir a caixa de diálogo **Editor de coleção** .

5. Na caixa de diálogo **Editor de coleção** , clique no botão **Adicionar** três vezes para inserir três colunas no layout. A primeira coluna conterá a **caixa de ferramentas**, a segunda coluna hospedará o designer de fluxo de trabalho e a terceira coluna será usada para o Inspetor de propriedades.

6. Defina a `Width` propriedade da coluna intermediária com o valor "4 *".

7. Clique em **OK** para salvar as alterações. O XAML a seguir é adicionado ao seu arquivo *MainWindow. XAML* :

    ```xaml
    <Grid Name="grid1">
        <Grid.ColumnDefinitions>
            <ColumnDefinition />
            <ColumnDefinition Width="4*" />
            <ColumnDefinition />
        </Grid.ColumnDefinitions>
    </Grid>
    ```

8. Em **Gerenciador de soluções**, clique com o botão direito do mouse em *MainWindow. XAML* e selecione **Exibir código**. Modifique o código seguindo estas etapas:

    1. Adicione os seguintes namespaces:

        ```csharp
        using System.Activities;
        using System.Activities.Core.Presentation;
        using System.Activities.Presentation;
        using System.Activities.Presentation.Metadata;
        using System.Activities.Presentation.Toolbox;
        using System.Activities.Statements;
        using System.ComponentModel;
        ```

    2. Para declarar um campo de membro privado para manter uma instância do <xref:System.Activities.Presentation.WorkflowDesigner> , adicione o seguinte código à `MainWindow` classe:

        ```csharp
        public partial class MainWindow : Window
        {
            private WorkflowDesigner wd;

            public MainWindow()
            {
                InitializeComponent();
            }
        }
        ```

    3. Adicione o seguinte método `AddDesigner` à classe `MainWindow`. A implementação cria uma instância do <xref:System.Activities.Presentation.WorkflowDesigner> , adiciona uma <xref:System.Activities.Statements.Sequence> atividade a ela e a coloca na coluna intermediária da **grade** grid1.

        ```csharp
        private void AddDesigner()
        {
            // Create an instance of WorkflowDesigner class.
            this.wd = new WorkflowDesigner();

            // Place the designer canvas in the middle column of the grid.
            Grid.SetColumn(this.wd.View, 1);

            // Load a new Sequence as default.
            this.wd.Load(new Sequence());

            // Add the designer canvas to the grid.
            grid1.Children.Add(this.wd.View);
        }
        ```

    4. Registrar os metadados de designer para adicionar suporte do designer para todas as atividades internos. Isso permite que você remova atividades da caixa de ferramentas para a <xref:System.Activities.Statements.Sequence> atividade original no designer de fluxo de trabalho. Para fazer isso, adicione o `RegisterMetadata` método à `MainWindow` classe:

        ```csharp
        private void RegisterMetadata()
        {
            var dm = new DesignerMetadata();
            dm.Register();
        }
        ```

        Para obter mais informações sobre como registrar os designers de atividade, consulte [como criar um designer de atividade personalizado](how-to-create-a-custom-activity-designer.md).

    5. No construtor da classe de `MainWindow` , adicione chamadas para métodos previamente declaradas para registrar os metadados para o suporte de designer e criar <xref:System.Activities.Presentation.WorkflowDesigner>.

        ```csharp
        public MainWindow()
        {
            InitializeComponent();

            // Register the metadata.
            RegisterMetadata();

            // Add the WFF Designer.
            AddDesigner();
        }
        ```

        > [!NOTE]
        > O método de `RegisterMetadata` registra metadados de designer de atividades internos que incluem a atividade de <xref:System.Activities.Statements.Sequence> . Porque o método de `AddDesigner` usa a atividade de <xref:System.Activities.Statements.Sequence> , o método de `RegisterMetadata` deve ser chamado primeiro.

9. Pressione <kbd>F5</kbd> para compilar e executar a solução.

10. Consulte [tarefa 3: criar os painéis caixa de ferramentas e PropertyGrid](task-3-create-the-toolbox-and-propertygrid-panes.md) para saber como adicionar suporte a **caixa de ferramentas** e **PropertyGrid** ao designer de fluxo de trabalho rehospedado.

## <a name="see-also"></a>Consulte também

- [Hospedando novamente o designer de fluxo de trabalho](rehosting-the-workflow-designer.md)
- [Tarefa 1: Criar um aplicativo do Windows Presentation Foundation do Windows](task-1-create-a-new-wpf-app.md)
- [Tarefa 3: Criar os painéis de Caixa de ferramentas e PropertyGrid](task-3-create-the-toolbox-and-propertygrid-panes.md)
