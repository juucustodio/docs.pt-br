---
description: 'Saiba mais sobre: associando uma propriedade de atividade personalizada a um controle de designer'
title: Associando uma propriedade personalizada de atividade a um controle de designer
ms.date: 03/30/2017
ms.assetid: 2e8061ea-10f5-407c-a31f-d0d74ce12f27
ms.openlocfilehash: 522e3df3028270d42f7654026383c628ec951e8d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787936"
---
# <a name="binding-a-custom-activity-property-to-a-designer-control"></a>Associando uma propriedade personalizada de atividade a um controle de designer

Associar um controle de designer caixa de texto para um argumento de atividade é relativamente simples; associar um controle complexo do designer (como uma caixa combo) para um argumento de atividade pode apresentar desafios, no entanto. Este tópico discute como associar um argumento de atividade a um controle caixa de combinação em um designer personalizado de atividade.

## <a name="creating-the-combo-box-item-converter"></a>Criando o conversor de item da caixa de combinação

1. Crie uma nova solução vazia no Visual Studio chama CustomProperty.

2. Crie uma nova classe chamada ComboBoxItemConverter. Adicione uma referência a System.Windows.Data, e tem a classe derivar de <xref:System.Windows.Data.IValueConverter>. Tenha o Visual Studio fornecedores da interface para gerar stub para `Convert` e `ConvertBack`.

3. Adicione o seguinte código ao `Convert` método. Este código a seguir converte <xref:System.Activities.InArgument%601> de atividade do tipo <xref:System.String> para o valor a ser colocado no designer.

    ```csharp
    ModelItem modelItem = value as ModelItem;
    if (value != null)
    {
        InArgument<string> inArgument = modelItem.GetCurrentValue() as InArgument<string>;

        if (inArgument != null)
        {
            Activity<string> expression = inArgument.Expression;
            VisualBasicValue<string> vbexpression = expression as VisualBasicValue<string>;
            Literal<string> literal = expression as Literal<string>;

            if (literal != null)
            {
                return "\"" + literal.Value + "\"";
            }
            else if (vbexpression != null)
            {
                return vbexpression.ExpressionText;
            }
        }
    }
    return null;
    ```

     A expressão no snippet de código anterior também pode ser criada usando <xref:Microsoft.CSharp.Activities.CSharpValue%601> em vez de <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>.

    ```csharp
    ModelItem modelItem = value as ModelItem;
    if (value != null)
    {
        InArgument<string> inArgument = modelItem.GetCurrentValue() as InArgument<string>;

        if (inArgument != null)
        {
            Activity<string> expression = inArgument.Expression;
            CSharpValue<string> csexpression = expression as CSharpValue<string>;
            Literal<string> literal = expression as Literal<string>;

            if (literal != null)
            {
                return "\"" + literal.Value + "\"";
            }
            else if (csexpression != null)
            {
                return csexpression.ExpressionText;
            }
        }
    }
    return null;
    ```

4. Adicione o seguinte código ao `ConvertBack` método. Este código a seguir converte o item de entrada da caixa de combinação de volta a <xref:System.Activities.InArgument%601>.

    ```csharp
    // Convert combo box value to InArgument<string>
                string itemContent = (string)((ComboBoxItem)value).Content;
                VisualBasicValue<string> vbArgument = new VisualBasicValue<string>(itemContent);
                InArgument<string> inArgument = new InArgument<string>(vbArgument);
                return inArgument;
    ```

     A expressão no snippet de código anterior também pode ser criada usando <xref:Microsoft.CSharp.Activities.CSharpValue%601> em vez de <xref:Microsoft.VisualBasic.Activities.VisualBasicValue%601>.

    ```csharp
    // Convert combo box value to InArgument<string>
                string itemContent = (string)((ComboBoxItem)value).Content;
                CSharpValue<string> csArgument = new CSharpValue<string>(itemContent);
                InArgument<string> inArgument = new InArgument<string>(csArgument);
                return inArgument;
    ```

## <a name="adding-the-comboboxitemconverter-to-the-custom-designer-of-an-activity"></a>Adicionando o ComboBoxItemConverter o designer personalizado de uma atividade

1. Adicionar um novo item ao projeto. Na caixa de diálogo add new item, selecione o nó de fluxo de trabalho e selecione o designer de atividade como o tipo do novo item. Nomeie o item CustomPropertyDesigner.

2. Adicione uma caixa de combinação para o novo designer. A propriedade itens, adicione um par itens à caixa de combinação, com valores de conteúdo de “Item1” e “de” Item2.

3. Modifique o XAML caixa de combinação para adicionar o novo conversor de item como o conversor de item a ser usado para a caixa de combinação. O conversor é adicionado como um recurso no segmento de ActivityDesigner.Resources, e especifica o conversor no atributo de conversor para <xref:System.Windows.Controls.ComboBox>. Observe que o namespace do projeto está especificada em atributos namespaces para o designer de atividade; se o designer deve ser usada em um projeto diferente, esse namespace deverá ser alterada.

    ```xaml
    <sap:ActivityDesigner x:Class="CustomProperty.CustomPropertyDesigner"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:c="clr-namespace:CustomProperty"
        xmlns:sap="clr-namespace:System.Activities.Presentation;assembly=System.Activities.Presentation"
        xmlns:sapv="clr-namespace:System.Activities.Presentation.View;assembly=System.Activities.Presentation">

        <sap:ActivityDesigner.Resources>
            <ResourceDictionary>
                <c:ComboBoxItemConverter x:Key="comboBoxItemConverter"/>
            </ResourceDictionary>
        </sap:ActivityDesigner.Resources>
        <Grid>
            <ComboBox SelectedValue="{Binding Path=ModelItem.Text, Mode=TwoWay, Converter={StaticResource comboBoxItemConverter}}"  Height="23" HorizontalAlignment="Left" Margin="132,5,0,0" Name="comboBox1" VerticalAlignment="Top" Width="120" ItemsSource="{Binding}">
                <ComboBoxItem>item1</ComboBoxItem>
                <ComboBoxItem>item2</ComboBoxItem>
            </ComboBox>
        </Grid>
    </sap:ActivityDesigner>
    ```

4. Crie um novo item do tipo <xref:System.Activities.CodeActivity>. O código padrão criado pelo IDE para atividades será suficiente para esse exemplo.

5. Adicione o atributo a seguir para a definição de classe:

    ```csharp
    [Designer(typeof(CustomPropertyDesigner))]
    ```

     Esta linha associa o novo designer com a nova classe.

 A nova atividade agora deve ser associada com o designer. Para testar a nova atividade, adicioná-lo a um fluxo de trabalho, e defina a caixa de combinação para dois valores. A janela propriedades deve atualizar para refletir o valor de caixa combo.
