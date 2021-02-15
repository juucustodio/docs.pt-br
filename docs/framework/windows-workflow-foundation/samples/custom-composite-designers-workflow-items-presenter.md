---
description: 'Saiba mais sobre: designers compostos personalizados-apresentador de itens de fluxo de trabalho'
title: Designer de compostos personalizados - apresentador de itens de fluxo de trabalho
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 70055c4b-1173-47a3-be80-b5bce6f59e9a
ms.openlocfilehash: 07970763e12eccd981370f1241642cc28f675824
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792577"
---
# <a name="custom-composite-designers---workflow-items-presenter"></a>Designer de compostos personalizados - apresentador de itens de fluxo de trabalho

<xref:System.Activities.Presentation.WorkflowItemsPresenter?displayProperty=nameWithType> é um principal no modelo de programação do designer de WF que permite a edição de uma coleção de elementos contidos. Este exemplo mostra como criar um designer de atividade que surija uma coleção tão editável.

Este exemplo demonstra:

- Criando um designer personalizado de atividade com <xref:System.Activities.Presentation.WorkflowItemsPresenter?displayProperty=nameWithType>.

- Criar um designer de atividade com uma exibição "recolhida" e "expandida".

- Substituindo um designer padrão em um aplicativo rehosted.

## <a name="set-up-build-and-run-the-sample"></a>Configurar, compilar e executar o exemplo

1. Abra a solução de exemplo **UsingWorkflowItemsPresenter. sln** para C# ou para Visual Basic no Visual Studio 2010.

2. Compile e execute a solução.

   Um aplicativo de designer de fluxo de trabalho rehospedado é aberto e você pode arrastar atividades para a tela.

## <a name="sample-highlights"></a>Realces de exemplo

O código para esse exemplo mostra o seguinte:

- A atividade um designer é compilada para:  `Parallel`

- A criação de um designer personalizado de atividade com <xref:System.Activities.Presentation.WorkflowItemsPresenter?displayProperty=nameWithType>. Algumas coisas para indicar:

  - Observe o uso de associação de dados de WPF associar a `ModelItem.Branches`. `ModelItem` é a propriedade em `WorkflowElementDesigner` que refere-se ao objeto subjacente que o designer está sendo usado para, nesse caso, nosso `Parallel`.

  - <xref:System.Activities.Presentation.WorkflowItemsPresenter.SpacerTemplate?displayProperty=nameWithType> pode ser usado para colocar um visual para exibir entre os itens individuais na coleção.

  - <xref:System.Activities.Presentation.WorkflowItemsPresenter.ItemsPanel?displayProperty=nameWithType> é um modelo que pode ser fornecido para determinar o layout dos itens na coleção. Nesse caso, um painel horizontal de pilha é usado.

  Esse código de exemplo a seguir mostra isso.

  ```xaml
  <sad:WorkflowItemsPresenter HintText="Drop Activities Here"
                                Items="{Binding Path=ModelItem.Branches}">
      <sad:WorkflowItemsPresenter.SpacerTemplate>
        <DataTemplate>
          <Ellipse Width="10" Height="10" Fill="Black"/>
        </DataTemplate>
      </sad:WorkflowItemsPresenter.SpacerTemplate>
      <sad:WorkflowItemsPresenter.ItemsPanel>
        <ItemsPanelTemplate>
          <StackPanel Orientation="Horizontal"/>
        </ItemsPanelTemplate>
      </sad:WorkflowItemsPresenter.ItemsPanel>
    </sad:WorkflowItemsPresenter>
  ```

- Executar uma associação de `DesignerAttribute` para o tipo de `Parallel` e então saída que atributos relataram.

  - Primeiro, para todos os designers padrão.

    A seguir está o exemplo de código.

    ```csharp
    // register metadata
    (new DesignerMetadata()).Register();
    RegisterCustomMetadata();
    ```

    ```vb
    ' register metadata
    Dim metadata = New DesignerMetadata()
    metadata.Register()
    ' register custom metadata
    RegisterCustomMetadata()
    ```

  - Em seguida, substituir a paralela no método de `RegisterCustomMetadata` .

    O código a seguir mostra esse em C# e Visual Basic.

    ```csharp
    void RegisterCustomMetadata()
    {
          AttributeTableBuilder builder = new AttributeTableBuilder();
          builder.AddCustomAttributes(typeof(Parallel), new DesignerAttribute(typeof(CustomParallelDesigner)));
          MetadataStore.AddAttributeTable(builder.CreateTable());
    }
    ```

    ```vb
    Sub RegisterCustomMetadata()
       Dim builder As New AttributeTableBuilder()
       builder.AddCustomAttributes(GetType(Parallel), New DesignerAttribute(GetType(CustomParallelDesigner)))
       MetadataStore.AddAttributeTable(builder.CreateTable())
    End Sub
    ```

- Finalmente, observe o uso de modelos e disparadores de diferentes de dados selecione o modelo apropriado com base na propriedade de `IsRootDesigner` .

  A seguir está o exemplo de código.

  ```xaml
  <sad:ActivityDesigner x:Class="Microsoft.Samples.CustomParallelDesigner"
      xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
      xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
      xmlns:sad="clr-namespace:System.Activities.Design;assembly=System.Activities.Design"
      xmlns:sadv="clr-namespace:System.Activities.Design.View;assembly=System.Activities.Design">
    <sad:ActivityDesigner.Resources>
      <DataTemplate x:Key="Expanded">
        <StackPanel>
          <TextBlock>This is the Expanded View</TextBlock>
          <sad:WorkflowItemsPresenter HintText="Drop Activities Here"
                                      Items="{Binding Path=ModelItem.Branches}">
            <sad:WorkflowItemsPresenter.SpacerTemplate>
              <DataTemplate>
                <Ellipse Width="10" Height="10" Fill="Black"/>
              </DataTemplate>
            </sad:WorkflowItemsPresenter.SpacerTemplate>
            <sad:WorkflowItemsPresenter.ItemsPanel>
              <ItemsPanelTemplate>
                <StackPanel Orientation="Horizontal"/>
              </ItemsPanelTemplate>
            </sad:WorkflowItemsPresenter.ItemsPanel>
          </sad:WorkflowItemsPresenter>
        </StackPanel>
      </DataTemplate>
      <DataTemplate x:Key="Collapsed">
        <TextBlock>This is the Collapsed View</TextBlock>
      </DataTemplate>
      <Style x:Key="ExpandOrCollapsedStyle" TargetType="{x:Type ContentPresenter}">
        <Setter Property="ContentTemplate" Value="{DynamicResource Collapsed}"/>
        <Style.Triggers>
          <DataTrigger Binding="{Binding Path=IsRootDesigner}" Value="true">
            <Setter Property="ContentTemplate" Value="{DynamicResource Expanded}"/>
          </DataTrigger>
        </Style.Triggers>
      </Style>
    </sad: ActivityDesigner.Resources>
    <Grid>
      <ContentPresenter Style="{DynamicResource ExpandOrCollapsedStyle}" Content="{Binding}"/>
    </Grid>
  </sad: ActivityDesigner>
  ```

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\WorkflowItemsPresenter`

## <a name="see-also"></a>Consulte também

- <xref:System.Activities.Presentation.WorkflowItemsPresenter>
- [Desenvolvendo aplicativos com o Designer de Fluxo de Trabalho](/visualstudio/workflow-designer/developing-applications-with-the-workflow-designer)
