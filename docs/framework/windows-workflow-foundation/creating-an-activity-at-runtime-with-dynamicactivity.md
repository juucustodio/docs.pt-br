---
title: Criando uma atividade em runtime com o DynamicActivity
description: DynamicActivity é uma classe concreta e selada com um construtor público. Use a classe para montar a funcionalidade de atividade em tempo de execução usando um DOM de atividade.
ms.date: 03/30/2017
ms.assetid: 1af85cc6-912d-449e-90c5-c5db3eca5ace
ms.openlocfilehash: b65d7e385690b77d44c73e7a8a4ed38b04f30ea6
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96242091"
---
# <a name="creating-an-activity-at-runtime-with-dynamicactivity"></a>Criando uma atividade em runtime com o DynamicActivity

<xref:System.Activities.DynamicActivity> é um concreto, classe lacradas com um construtor público. <xref:System.Activities.DynamicActivity> pode ser usado para reunir a funcionalidade de atividade em runtime usando os DOM de uma atividade.  
  
## <a name="dynamicactivity-features"></a>Recursos de DynamicActivity  

 <xref:System.Activities.DynamicActivity> tem acesso às propriedades de execução, os argumentos e variáveis, mas nenhum o acesso aos serviços de tempo de execução como atividades filhos de programação ou o rastreamento.  
  
 As propriedades de nível superior podem ser definidas usando objetos de <xref:System.Activities.Argument> de fluxo de trabalho. No código obrigatório, esses argumentos são criados usando propriedades de CLR em um novo tipo. Em XAML, são declarados usando `x:Class` e marcas de `x:Member` .  
  
 Atividades construídas usando a interface de <xref:System.Activities.DynamicActivity> com o designer que usa <xref:System.ComponentModel.ICustomTypeDescriptor>. As atividades criadas no designer podem ser carregadas dinamicamente usando <xref:System.Activities.XamlIntegration.ActivityXamlServices.Load%2A>, como demonstrado no procedimento a seguir.  
  
#### <a name="to-create-an-activity-at-runtime-using-imperative-code"></a>Para criar uma atividade em runtime usando o código obrigatório  
  
1. OpenVisual Studio 2010.  
  
2. Selecione **arquivo**, **novo**, **projeto**. Selecione **fluxo de trabalho 4,0** em **Visual C#** na janela **tipos de projeto** e selecione o nó **v2010** . Selecione **aplicativo de console de fluxo de trabalho Sequencial** na janela **modelos** . Nomeie o novo projeto DynamicActivitySample.  
  
3. Clique com o botão direito do mouse em Workflow1. XAML no projeto HelloActivity e selecione **excluir**.  
  
4. Abra Program.cs. Adicione a seguinte diretiva para a parte superior do arquivo.  
  
    ```csharp  
    using System.Collections.Generic;  
    ```  
  
5. Substitua o conteúdo do método de `Main` com o código a seguir, que cria uma atividade de <xref:System.Activities.Statements.Sequence> que contém uma única atividade de <xref:System.Activities.Statements.WriteLine> e a atribui à propriedade de <xref:System.Activities.DynamicActivity.Implementation%2A> de uma nova atividade dinâmico.  
  
    ```csharp  
    //Define the input argument for the activity  
    var textOut = new InArgument<string>();  
    //Create the activity, property, and implementation  
                Activity dynamicWorkflow = new DynamicActivity()  
                {  
                    Properties =
                    {  
                        new DynamicActivityProperty  
                        {  
                            Name = "Text",  
                            Type = typeof(InArgument<String>),  
                            Value = textOut  
                        }  
                    },  
                    Implementation = () => new Sequence()  
                    {  
                        Activities =
                        {  
                            new WriteLine()  
                            {  
                                Text = new InArgument<string>(env => textOut.Get(env))  
                            }  
                        }  
                    }  
                };  
    //Execute the activity with a parameter dictionary  
                WorkflowInvoker.Invoke(dynamicWorkflow, new Dictionary<string, object> { { "Text", "Hello World!" } });  
                Console.ReadLine();  
    ```  
  
6. Execute o aplicativo. Uma janela de console com o texto "Olá, Mundo!" mostra.  
  
#### <a name="to-create-an-activity-at-runtime-using-xaml"></a>Para criar uma atividade em runtime usando XAML  
  
1. Abra o Visual Studio 2010.  
  
2. Selecione **arquivo**, **novo**, **projeto**. Selecione **fluxo de trabalho 4,0** em **Visual C#** na janela **tipos de projeto** e selecione o nó **v2010** . Selecione  **aplicativo de console de fluxo de trabalho** na janela **modelos** . Nomeie o novo projeto DynamicActivitySample.  
  
3. Workflow1.xaml aberto no projeto de HelloActivity. Clique na opção **argumentos** na parte inferior do designer. Crie um novo argumento de `In` chamado `TextToWrite` de tipo `String`.  
  
4. Arraste uma atividade **WriteLine** da seção **primitivas** da caixa de ferramentas para a superfície do designer. Atribua o valor `TextToWrite` à propriedade **Text** da atividade.  
  
5. Abra Program.cs. Adicione a seguinte diretiva para a parte superior do arquivo.  
  
    ```csharp  
    using System.Activities.XamlIntegration;  
    ```  
  
6. Substitua o conteúdo do método `Main` pelo código a seguir.  
  
    ```csharp  
    Activity act2 = ActivityXamlServices.Load(@"Workflow1.xaml");  
                    results = WorkflowInvoker.Invoke(act2, new Dictionary<string, object> { { "TextToWrite", "HelloWorld!" } });  
    Console.ReadLine();  
    ```  
  
7. Execute o aplicativo. Uma janela de console com o texto "Olá, Mundo!"  é exibido.  
  
8. Clique com o botão direito do mouse no arquivo workflow1. XAML na **Gerenciador de soluções** e selecione **Exibir código**. Observe que a classe da atividade é criada com `x:Class` e a propriedade é criada com `x:Property`.  
  
## <a name="see-also"></a>Veja também

- [Criando fluxos de trabalho, atividades e expressões de design usando o código obrigatório](authoring-workflows-activities-and-expressions-using-imperative-code.md)
