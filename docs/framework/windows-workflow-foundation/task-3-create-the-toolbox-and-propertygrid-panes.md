---
description: 'Saiba mais sobre: tarefa 3: criar os painéis caixa de ferramentas e PropertyGrid'
title: 'Tarefa 3: Criar os painéis de Caixa de ferramentas e PropertyGrid'
ms.date: 03/30/2017
ms.assetid: 72c1546a-eed5-4f0f-a616-719a163414f4
ms.openlocfilehash: c07bfc2f974018cb0d789a6cc1181f9bed861382
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755156"
---
# <a name="task-3-create-the-toolbox-and-propertygrid-panes"></a>Tarefa 3: Criar os painéis de Caixa de ferramentas e PropertyGrid

Nesta tarefa, você criará os painéis **caixa de ferramentas** e **PropertyGrid** e os adicionará à designer de fluxo de trabalho do Windows rehospedada.

Para referência, o código que deve estar no arquivo MainWindow.xaml.cs depois de concluir as três tarefas na série de tópicos de [rehospedagem, a designer de fluxo de trabalho](rehosting-the-workflow-designer.md) é fornecida no final deste tópico.

## <a name="to-create-the-toolbox-and-add-it-to-the-grid"></a>Para criar a caixa de ferramentas e adicioná-la à grade

1. Abra o projeto HostingApplication obtido seguindo o procedimento descrito na [tarefa 2: hospedar o designer de fluxo de trabalho](task-2-host-the-workflow-designer.md).

2. No painel de **Gerenciador de soluções** , clique com o botão direito do mouse no arquivo *MainWindow. XAML* e selecione **Exibir código**.

3. Adicione um `GetToolboxControl` método à `MainWindow` classe que cria um <xref:System.Activities.Presentation.Toolbox.ToolboxControl> , adiciona uma nova categoria da **caixa de ferramentas** à **caixa de ferramentas** e atribui os <xref:System.Activities.Statements.Assign> tipos de <xref:System.Activities.Statements.Sequence> atividade e a essa categoria.

    ```csharp
    private ToolboxControl GetToolboxControl()
    {
        // Create the ToolBoxControl.
        var ctrl = new ToolboxControl();

        // Create a category.
        var category = new ToolboxCategory("category1");

        // Create Toolbox items.
        var tool1 =
            new ToolboxItemWrapper("System.Activities.Statements.Assign",
            typeof(Assign).Assembly.FullName, null, "Assign");

        var tool2 = new ToolboxItemWrapper("System.Activities.Statements.Sequence",
            typeof(Sequence).Assembly.FullName, null, "Sequence");

        // Add the Toolbox items to the category.
        category.Add(tool1);
        category.Add(tool2);

        // Add the category to the ToolBox control.
        ctrl.Categories.Add(category);
        return ctrl;
    }
    ```

4. Adicione um `AddToolbox` método particular à `MainWindow` classe que coloca a caixa de **ferramentas** na coluna esquerda da grade.

    ```csharp
    private void AddToolBox()
    {
        ToolboxControl tc = GetToolboxControl();
        Grid.SetColumn(tc, 0);
        grid1.Children.Add(tc);
    }
    ```

5. Adicione uma chamada para o `AddToolBox` método no `MainWindow()` Construtor de classe, conforme mostrado no código a seguir:

    ```csharp
    public MainWindow()
    {
        InitializeComponent();
        this.RegisterMetadata();
        this.AddDesigner();

        this.AddToolBox();
    }
    ```

6. Pressione <kbd>F5</kbd> para compilar e executar sua solução. A **caixa de ferramentas** que contém as <xref:System.Activities.Statements.Assign> <xref:System.Activities.Statements.Sequence> atividades e deve ser exibida.

## <a name="to-create-the-propertygrid"></a>Para criar o PropertyGrid

1. No painel de **Gerenciador de soluções** , clique com o botão direito do mouse no arquivo *MainWindow. XAML* e selecione **Exibir código**.

2. Adicione o `AddPropertyInspector` método à `MainWindow` classe para posicionar o painel **PropertyGrid** na coluna mais à direita na grade:

    ```csharp
    private void AddPropertyInspector()
    {
        Grid.SetColumn(wd.PropertyInspectorView, 2);
        grid1.Children.Add(wd.PropertyInspectorView);
    }
    ```

3. Adicione uma chamada para o `AddPropertyInspector` método no `MainWindow()` Construtor de classe, conforme mostrado no código a seguir:

    ```csharp
    public MainWindow()
    {
        InitializeComponent();
        this.RegisterMetadata();
        this.AddDesigner();
        this.AddToolBox();

        this.AddPropertyInspector();
    }
    ```

4. Pressione <kbd>F5</kbd> para compilar e executar a solução. A **caixa de ferramentas**, a tela de design do fluxo de trabalho e os painéis de **PropertyGrid** devem ser exibidos e, quando você arrasta uma <xref:System.Activities.Statements.Assign> atividade ou uma <xref:System.Activities.Statements.Sequence> atividade para a tela de design, a grade de propriedades deve ser atualizada dependendo da atividade realçada.

## <a name="example"></a>Exemplo

O arquivo *MainWindow.XAML.cs* agora deve conter o código a seguir:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;
// dlls added.
using System.Activities;
using System.Activities.Core.Presentation;
using System.Activities.Presentation;
using System.Activities.Presentation.Metadata;
using System.Activities.Presentation.Toolbox;
using System.Activities.Statements;
using System.ComponentModel;

namespace HostingApplication
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        private WorkflowDesigner wd;

        public MainWindow()
        {
            InitializeComponent();
            RegisterMetadata();
            AddDesigner();
            this.AddToolBox();
            this.AddPropertyInspector();
        }

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

        private void RegisterMetadata()
        {
            var dm = new DesignerMetadata();
            dm.Register();
        }

        private ToolboxControl GetToolboxControl()
        {
            // Create the ToolBoxControl.
            var ctrl = new ToolboxControl();

            // Create a category.
            var category = new ToolboxCategory("category1");

            // Create Toolbox items.
            var tool1 =
                new ToolboxItemWrapper("System.Activities.Statements.Assign",
                typeof(Assign).Assembly.FullName, null, "Assign");

            var tool2 = new ToolboxItemWrapper("System.Activities.Statements.Sequence",
                typeof(Sequence).Assembly.FullName, null, "Sequence");

            // Add the Toolbox items to the category.
            category.Add(tool1);
            category.Add(tool2);

            // Add the category to the ToolBox control.
            ctrl.Categories.Add(category);
            return ctrl;
        }

        private void AddToolBox()
        {
            ToolboxControl tc = GetToolboxControl();
            Grid.SetColumn(tc, 0);
            grid1.Children.Add(tc);
        }

        private void AddPropertyInspector()
        {
            Grid.SetColumn(wd.PropertyInspectorView, 2);
            grid1.Children.Add(wd.PropertyInspectorView);
        }

    }
}
```

## <a name="see-also"></a>Consulte também

- [Hospedando novamente o designer de fluxo de trabalho](rehosting-the-workflow-designer.md)
- [Tarefa 1: Criar um aplicativo do Windows Presentation Foundation do Windows](task-1-create-a-new-wpf-app.md)
- [Tarefa 2: Hospedar o Designer de Fluxo de Trabalho](task-2-host-the-workflow-designer.md)
