---
description: 'Saiba mais sobre: usando extensões de atividade'
title: Usando extensões de atividade
ms.date: 03/30/2017
ms.assetid: 500eb96a-c009-4247-b6b5-b36faffdf715
ms.openlocfilehash: d0286850bf685497d3a2471a3b4e0db4630070b1
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99755064"
---
# <a name="using-activity-extensions"></a>Usando extensões de atividade

As atividades podem interagir com as extensões do aplicativo de fluxo de trabalho que permitem que o host fornece funcionalidade adicional que não é modelada explicitamente no fluxo de trabalho.  Este tópico descreve como criar e usar uma extensão para contar o número de vezes que a atividade é executado.

### <a name="to-use-an-activity-extension-to-count-executions"></a>Para usar uma extensão de atividade para contar executa

1. Abra o Visual Studio 2010. Selecione **novo**, **projeto**. No nó do **Visual C#** , selecione **fluxo de trabalho**.  Selecione **aplicativo de console de fluxo de trabalho** na lista de modelos. Dê ao projeto o nome de `Extensions`. Clique em **OK** para criar o projeto.

2. Adicione uma `using` instrução no arquivo Program.cs para o namespace **System. Collections. Generic** .

    ```csharp
    using System.Collections.Generic;
    ```

3. No arquivo Program.cs, crie uma nova classe chamada **ExecutionCountExtension**. O código a seguir cria uma extensão de fluxo de trabalho que controla IDs de instância quando seu método **Register** é chamado.

    ```csharp
    // This extension collects a list of workflow Ids
    public class ExecutionCountExtension
    {
        IList<Guid> instances = new List<Guid>();

        public int ExecutionCount
        {
            get
            {
                return this.instances.Count;
            }
        }

        public IEnumerable<Guid> InstanceIds
        {
            get
            {
                return this.instances;
            }
        }

        public void Register(Guid activityInstanceId)
        {
            if (!this.instances.Contains<Guid>(activityInstanceId))
            {
                instances.Add(activityInstanceId);
            }
        }
    }
    ```

4. Crie uma atividade que consome o **ExecutionCountExtension**. O código a seguir define uma atividade que recupera o objeto **ExecutionCountExtension** do tempo de execução e chama seu método **Register** quando a atividade é executada.

    ```csharp
    // Activity that consumes an extension provided by the host. If the extension is available
    // in the context, it will invoke (in this case, registers the Id of the executing workflow)
    public class MyActivity: CodeActivity
    {
        protected override void Execute(CodeActivityContext context)
        {
            ExecutionCountExtension ext = context.GetExtension<ExecutionCountExtension>();
            if (ext != null)
            {
                ext.Register(context.WorkflowInstanceId);
            }

        }
    }
    ```

5. Implemente a atividade no método **Main** do arquivo Program.cs. O código a seguir contém métodos para gerar dois fluxos de trabalho diferentes, para executar cada fluxo de trabalho várias vezes, e exibir os dados resultante que estão contidos na extensão.

    ```csharp
    class Program
    {
        // Creates a workflow that uses the activity that consumes the extension
        static Activity CreateWorkflow1()
        {
            return new Sequence
            {
                Activities =
                {
                    new MyActivity()
                }
            };
        }

        // Creates a workflow that uses two instances of the activity that consumes the extension
        static Activity CreateWorkflow2()
        {
            return new Sequence
            {
                Activities =
                {
                    new MyActivity(),
                    new MyActivity()
                }
            };
        }

        static void Main(string[] args)
        {
            // create the extension
            ExecutionCountExtension executionCountExt = new ExecutionCountExtension();

            // configure the first invoker and execute 3 times
            WorkflowInvoker invoker = new WorkflowInvoker(CreateWorkflow1());
            invoker.Extensions.Add(executionCountExt);
            invoker.Invoke();
            invoker.Invoke();
            invoker.Invoke();

            // configure the second invoker and execute 2 times
            WorkflowInvoker invoker2 = new WorkflowInvoker(CreateWorkflow2());
            invoker2.Extensions.Add(executionCountExt);
            invoker2.Invoke();
            invoker2.Invoke();

            // show the data in the extension
            Console.WriteLine("Executed {0} times", executionCountExt.ExecutionCount);
            executionCountExt.InstanceIds.ToList().ForEach(i => Console.WriteLine("...{0}", i));
        }
    }
    ```
