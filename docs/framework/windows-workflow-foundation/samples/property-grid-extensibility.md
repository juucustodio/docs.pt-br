---
description: 'Saiba mais sobre: extensibilidade da grade de propriedades'
title: Extensibilidade da grade de propriedades – exemplo do WF
ms.date: 03/30/2017
ms.assetid: 3530c3a3-756d-4712-9f10-fb2897414d3a
ms.openlocfilehash: 784705146974ffca5cd2e6c21dba722598544771
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741803"
---
# <a name="property-grid-extensibility"></a>Extensibilidade da grade de propriedades

Um desenvolvedor pode personalizar a grade de propriedade que é exibida quando uma determinada atividade é selecionada no designer. Isso pode ser feito para criar uma experiência rica de edição. Este exemplo mostra como isso pode ser feito.

## <a name="demonstrates"></a>Demonstra

Extensibilidade da grade de propriedade do designer de fluxo de trabalho.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\PropertyGridExtensibility`

## <a name="discussion"></a>Discussão

Para estender a grade de propriedade, um desenvolvedor tem opções personalizar a aparência de um editor embutido da grade de propriedade ou fornecer uma caixa de diálogo que aparece para uma superfície mais avançado de edição. Há dois editores diferentes demonstrados nesse exemplo; um editor embutido e um editor caixa de diálogo.

## <a name="inline-editor"></a>Editor embutido

O exemplo editor embutido demonstra o seguinte:

- Cria um tipo deriva de <xref:System.Activities.Presentation.PropertyEditing.PropertyValueEditor>.

- No construtor, o <xref:System.Activities.Presentation.PropertyEditing.PropertyValueEditor.InlineEditorTemplate%2A> valor é definido com um modelo de dados Windows Presentation Foundation (WPF). Isso pode ser associado a um modelo XAML, mas nesse exemplo, o código é usado para inicializar a associação de dados.

- O modelo de dados tem um contexto de dados de <xref:System.Activities.Presentation.PropertyEditing.PropertyValue> de item processado na grade de propriedade. Observe o seguinte código (de CustomInlineEditor.cs) que este contexto associando a propriedade de `Value` .

    ```csharp
    FrameworkElementFactory stack = new FrameworkElementFactory(typeof(StackPanel));
    FrameworkElementFactory slider = new FrameworkElementFactory(typeof(Slider));
    Binding sliderBinding = new Binding("Value");
    sliderBinding.Mode = BindingMode.TwoWay;
    slider.SetValue(Slider.MinimumProperty, 0.0);
    slider.SetValue(Slider.MaximumProperty, 100.0);
    slider.SetValue(Slider.ValueProperty, sliderBinding);
    stack.AppendChild(slider);
    ```

- Porque a atividade e o designer estão no mesmo assembly, o registro dos atributos do designer de atividade é feito no construtor estático de atividade próprio, conforme mostrado no exemplo de SimpleCodeActivity.cs.

    ```csharp
    static SimpleCodeActivity()
    {
        AttributeTableBuilder builder = new AttributeTableBuilder();
        builder.AddCustomAttributes(typeof(SimpleCodeActivity), "RepeatCount", new EditorAttribute(typeof(CustomInlineEditor), typeof(PropertyValueEditor)));
        builder.AddCustomAttributes(typeof(SimpleCodeActivity), "FileName", new EditorAttribute(typeof(FilePickerEditor), typeof(DialogPropertyValueEditor)));
        MetadataStore.AddAttributeTable(builder.CreateTable());
    }
    ```

## <a name="dialog-editor"></a>Editor de caixa de diálogo

O exemplo do editor de diálogo demonstra o seguinte:

1. Cria um tipo deriva de <xref:System.Activities.Presentation.PropertyEditing.DialogPropertyValueEditor>.

2. Define o <xref:System.Activities.Presentation.PropertyEditing.PropertyValueEditor.InlineEditorTemplate%2A> valor no construtor com um modelo de dados do WPF. Isso pode ser criado em XAML, mas nesse exemplo, este é criado em código.

3. O modelo de dados tem um contexto de dados de <xref:System.Activities.Presentation.PropertyEditing.PropertyValue> de item processado na grade de propriedade. No código a seguir, ou associação à propriedade de `Value` . É importante incluir também <xref:System.Activities.Presentation.PropertyEditing.EditModeSwitchButton> para fornecer o botão que aumenta a caixa de diálogo em FilePickerEditor.cs.

    ```csharp
    this.InlineEditorTemplate = new DataTemplate();

    FrameworkElementFactory stack = new FrameworkElementFactory(typeof(StackPanel));
    stack.SetValue(StackPanel.OrientationProperty, Orientation.Horizontal);
    FrameworkElementFactory label = new FrameworkElementFactory(typeof(Label));
    Binding labelBinding = new Binding("Value");
    label.SetValue(Label.ContentProperty, labelBinding);
    label.SetValue(Label.MaxWidthProperty, 90.0);

    stack.AppendChild(label);

    FrameworkElementFactory editModeSwitch = new FrameworkElementFactory(typeof(EditModeSwitchButton));

    editModeSwitch.SetValue(EditModeSwitchButton.TargetEditModeProperty, PropertyContainerEditMode.Dialog);

    stack.AppendChild(editModeSwitch);

    this.InlineEditorTemplate.VisualTree = stack;
    ```

4. Substitui o método de <xref:System.Activities.Presentation.PropertyEditing.DialogPropertyValueEditor.ShowDialog%2A> no tipo de designer para manipular a exibição da caixa de diálogo. Nesse exemplo, <xref:System.Windows.Forms.FileDialog> básico é mostrado.

    ```csharp
    public override void ShowDialog(PropertyValue propertyValue, IInputElement commandSource)
    {
        Microsoft.Win32.OpenFileDialog ofd = new Microsoft.Win32.OpenFileDialog();
        if (ofd.ShowDialog() == true)
        {
            propertyValue.Value = ofd.FileName;
        }
    }
    ```

5. Porque a atividade e o designer estão no mesmo assembly, o registro dos atributos do designer de atividade é feito no construtor estático de atividade próprio, conforme mostrado no exemplo de SimpleCodeActivity.cs.

    ```csharp
    static SimpleCodeActivity()
    {
        AttributeTableBuilder builder = new AttributeTableBuilder();
        builder.AddCustomAttributes(typeof(SimpleCodeActivity), "RepeatCount", new EditorAttribute(typeof(CustomInlineEditor), typeof(PropertyValueEditor)));
        builder.AddCustomAttributes(typeof(SimpleCodeActivity), "FileName", new EditorAttribute(typeof(FilePickerEditor), typeof(DialogPropertyValueEditor)));
        MetadataStore.AddAttributeTable(builder.CreateTable());
    }
    ```

## <a name="to-set-up-build-and-run-the-sample"></a>Para configurar, compilar, e executar o exemplo

1. Crie a solução, e abra Workflow1.xaml.

2. Arraste um **SimpleCodeActivity** da caixa de ferramentas para a tela do designer.

3. Clique em **SimpleCodeActivity** e, em seguida, abra a grade de propriedades onde há um controle deslizante e um controle de seleção de arquivo.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\PropertyGridExtensibility`
