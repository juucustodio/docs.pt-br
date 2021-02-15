---
description: 'Saiba mais sobre: integração do WPF e do Windows Workflow Foundation em XAML'
title: Integração de WPF e WF em XAML
ms.date: 03/30/2017
ms.assetid: a4f53b48-fc90-4315-bca0-ba009562f488
ms.openlocfilehash: 3cc2d0336a2507dcf36fea3f3d240b95d22193e6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99798102"
---
# <a name="wpf-and-windows-workflow-foundation-integration-in-xaml"></a>Integração do WPF e do Windows Workflow Foundation em XAML

Este exemplo demonstra como criar um aplicativo que usa recursos de Windows Presentation Foundation (WPF) e Windows Workflow Foundation (WF) em um único documento XAML. Para fazer isso, o exemplo usa a extensibilidade Windows Workflow Foundation e XAML.

## <a name="sample-details"></a>Detalhes de exemplo

 O arquivo de ShowWindow.xaml desserializa em uma atividade de <xref:System.Activities.Statements.Sequence> com duas variáveis de cadeia de caracteres que são manipulados por atividades de sequência: `ShowWindow` e `WriteLine`. A saída de atividade de <xref:System.Activities.Statements.WriteLine> para a janela do console a expressão que atribui a <xref:System.Activities.Statements.WriteLine.Text%2A> à propriedade. A `ShowWindow` atividade exibe uma janela do WPF como parte de sua lógica de execução. <xref:System.Activities.ActivityContext.DataContext%2A> da janela inclui as variáveis declaradas na sequência. Os controles window declarada na atividade de `ShowWindow` usam a associação de dados para manipular esses variáveis. Finalmente, a janela contém um controle de botão. O evento de `Click` para o botão é tratado por <xref:System.Activities.ActivityDelegate> chamado `MarkupExtension` que contém uma atividade de `CloseWindow` . `MarkUpExtension` chama a atividade contida que fornece, como o contexto, todos os objetos identificados por `x:Name`, bem como o <xref:System.Activities.ActivityContext.DataContext%2A> da janela recipiente. Assim, `CloseWindow.InArgument<Window>` pode ser associado usando uma expressão que referencia o nome da janela.

 A `ShowWindow` atividade deriva da <xref:System.Activities.AsyncCodeActivity%601> classe para exibir uma janela do WPF e é concluída quando a janela é fechada. A propriedade de `Window` é do tipo `Func<Window>` que permite que a janela é criado sob demanda para cada execução de atividade. A propriedade de `Window` usa <xref:System.Xaml.XamlDeferringLoader> para ativar este modelo adiado de avaliação. `FuncFactoryDeferringLoader` permite que `XamlReader` é capturado durante a serialização e ler durante a execução da atividade.

 Uma atividade bem escrita nunca bloqueia o segmento de agendador. No entanto, a atividade de `ShowWindow` não pode concluir até a janela que está exibindo é fechada. A atividade de `ShowWindow` obtém esse comportamento derivando de <xref:System.Activities.AsyncCodeActivity>, chamando o método <xref:System.Activities.WorkflowInvoker.BeginInvoke%2A> no método de <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> , e mostrando a janela restrita (modal). O representante é chamado com WPF <xref:System.ServiceModel.InstanceContext.SynchronizationContext%2A>. A atividade de `ShowWindow` atribui a propriedade de <xref:System.Activities.ActivityContext.DataContext%2A> à propriedade de `Window.DataContext` para fornecer qualquer acesso de controles associados a dados a variáveis de em- escopo.

 O ponto em que o último de interesse nesse exemplo é <xref:System.Workflow.ComponentModel.Serialization.MarkupExtension> chamado `DelegateActivityExtension`. O método de `ProvideValue` desta extensão de marcação retorna um delegado que invoca uma atividade inserido. Essa atividade é executada em um ambiente que inclui o contexto de dados do WPF e quaisquer `x:Name` valores no escopo. No método de `GenericInvoke` , esse ambiente a atividade é fornecido por um extensão de <xref:System.Activities.Hosting.SymbolResolver> . Esta extensão é adicionada a <xref:System.Activities.WorkflowInvoker> que é usada para chamar a atividade inserido sempre que o delegado de extensão de marcação é chamado.

> [!NOTE]
> O designer padrão não oferece suporte a atividade de ShowWindow; como tal, o arquivo de ShowWindow.Xaml não exibe corretamente no designer.

## <a name="run-the-sample"></a>Execute o exemplo

1. Usando o Visual Studio, abra o arquivo de solução WPFWFIntegration. sln.

2. Para criar a solução, pressione **Ctrl** + **Shift** + **B**.

3. Para executar a solução, pressione **F5**.

4. Digite seu primeiro e último nome na caixa de diálogo.

5. Fechar a caixa de diálogo e o console ecoa seu nome.

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.
>
> `<InstallDrive>:\WF_WCF_Samples`
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Scenario\WPFWFIntegration`
