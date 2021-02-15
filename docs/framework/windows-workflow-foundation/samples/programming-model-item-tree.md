---
description: 'Saiba mais sobre: árvore de itens de modelo de programação'
title: Árvore modelo de programação de item
ms.date: 03/30/2017
ms.assetid: 0229efde-19ac-4bdc-a187-c6227a7bd1a5
ms.openlocfilehash: 8dfcab99bb5e32d202fe2bdc09d63d8b7da6e748
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741842"
---
# <a name="programming-model-item-tree"></a>Árvore modelo de programação de item

Este exemplo demonstra como navegar na <xref:System.Activities.Presentation.Model.ModelItem> árvore usando a associação de dados declarativa da exibição de árvore Windows Presentation Foundation (WPF).

## <a name="sample-details"></a>Detalhes de exemplo

 A <xref:System.Activities.Presentation.Model.ModelItem> árvore é a abstração usada pela infraestrutura de designer de fluxo de trabalho do Windows para expor os dados sobre a instância subjacente que está sendo editada. A ilustração a seguir é uma representação das várias camadas de infraestrutura dentro do Designer de Fluxo de Trabalho.

 ![Diagrama que mostra a arquitetura de Designer de Fluxo de Trabalho.](./media/programming-model-item-tree/workflow-designer-architecture.jpg)

 <xref:System.Activities.Presentation.Model.ModelItem> consiste em um ponteiro para o valor subjacente, bem como uma coleção de objetos <xref:System.Activities.Presentation.Model.ModelProperty> . Um objeto de <xref:System.Activities.Presentation.Model.ModelProperty> por sua vez, consiste dados como nome e tipo da propriedade e então um ponteiro para o valor que, por sua vez, é outro <xref:System.Activities.Presentation.Model.ModelItem>. Um conversor de valor é usado para manipular qualquer um de <xref:System.Activities.Presentation.Model.ModelItem>s retornado de <xref:System.Activities.Presentation.Model.ModelProperty> para fazê-lo aparecer corretamente no modo de exibição de árvore. O exemplo demonstra como programar em imperativa contra a árvore de <xref:System.Activities.Presentation.Model.ModelItem> usando a sintaxe imperativa, como visto no exemplo a seguir.

```csharp
ModelItem mi = wd.Context.Services.GetService<ModelService>().Root;
ModelProperty mp = mi.Properties["Activities"];
mp.Collection.Add(new Persist());
ModelItem justAdded = mp.Collection.Last();
justAdded.Properties["DisplayName"].SetValue("new name");
```

#### <a name="to-use-this-sample"></a>Para usar este exemplo

1. Abra a solução ProgrammingModelItemTree. sln no Visual Studio 2010.

2. Crie a solução selecionando **Compilar solução** no menu **Compilar** .

3. Pressione F5 para executar o aplicativo. Em seguida, o formulário do WPF é exibido.

4. Clique no botão **carregar o WF** para carregar o <xref:System.Activities.Presentation.Model.ModelItem> e associá-lo ao modo de exibição de árvore.

5. Clicar no botão **alterar árvore do item do modelo** executa o código anterior para adicionar um item à árvore e definir uma propriedade.

> [!IMPORTANT]
> Os exemplos podem mais ser instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Basic\Designer\ProgrammingModelItemTree`  
  
## <a name="see-also"></a>Confira também

- <xref:System.Windows.Data.IValueConverter>
