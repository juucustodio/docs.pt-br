---
description: 'Saiba mais sobre: criação de atividade de fluxo de trabalho usando a classe CodeActivity'
title: Criação de atividade de fluxo de trabalho usando a classe de CodeActivity
ms.date: 03/30/2017
ms.assetid: cfe315c1-f86d-43ec-b9ce-2f8c469b1106
ms.openlocfilehash: 393b6c586a88e876484f6888441d5bb82b4c0dad
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754908"
---
# <a name="workflow-activity-authoring-using-the-codeactivity-class"></a>Criação de atividade de fluxo de trabalho usando a classe de CodeActivity

As atividades criadas por herança de <xref:System.Activities.CodeActivity> podem implementar o comportamento básico obrigatório substituindo o método de <xref:System.Activities.CodeActivity.Execute%2A> .

## <a name="using-codeactivitycontext"></a>Usando CodeActivityContext

 Recursos de runtime de fluxo de trabalho podem ser acessados de dentro do método de <xref:System.Activities.CodeActivity.Execute%2A> usando membros de parâmetro de `context` , do tipo <xref:System.Activities.CodeActivityContext>. Os recursos <xref:System.Activities.CodeActivityContext> direto disponível incluem o seguinte:

- Definindo e obtendo os valores das variáveis e os argumentos.

- Recursos personalizados de rastreamento que usam <xref:System.Activities.CodeActivityContext.Track%2A>.

- Acesso às propriedades de execução da atividade usando <xref:System.Activities.CodeActivityContext.GetProperty%2A>.

#### <a name="to-create-a-custom-activity-that-inherits-from-codeactivity"></a>Para criar uma atividade personalizado que herda de CodeActivity

1. Abra o Visual Studio 2010.

2. Selecione **arquivo**, **novo** e **projeto**. Selecione **fluxo de trabalho 4,0** em **Visual C#** na janela **tipos de projeto** e selecione o nó **v2010** . Selecione **biblioteca de atividades** na janela **modelos** . Nomeie o novo projeto HelloActivity.

3. Clique com o botão direito do mouse em Atividade1. XAML no projeto HelloActivity e selecione **excluir**.

4. Clique com o botão direito do mouse no projeto HelloActivity e selecione **Adicionar** e, em seguida, **classe**. Nomeie a nova classe HelloActivity.cs.

5. No arquivo de HelloActivity.cs, adicione as seguintes diretivas de `using` .

    ```csharp
    using System.Activities;
    using System.Activities.Statements;
    ```

6. Faça a nova classe herdar de <xref:System.Activities.CodeActivity> adicionando uma classe base para a declaração de classe.

    ```csharp
    class HelloActivity : CodeActivity
    ```

7. Adicionar funcionalidade à classe adicionando um método de <xref:System.Activities.CodeActivity.Execute%2A> .

    ```csharp
    protected override void Execute(CodeActivityContext context)
    {
        Console.WriteLine("Hello World!");
    }
    ```

8. Use <xref:System.Activities.CodeActivityContext> para criar um registro de rastreamento.

    ```csharp
    protected override void Execute(CodeActivityContext context)
    {
        Console.WriteLine("Hello World!");
        CustomTrackingRecord record = new CustomTrackingRecord("MyRecord");
        record.Data.Add(new KeyValuePair<String, Object>("ExecutionTime", DateTime.Now));
        context.Track(record);
    }
    ```
