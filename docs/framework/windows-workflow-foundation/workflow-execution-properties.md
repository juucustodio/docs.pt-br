---
description: 'Saiba mais sobre: Propriedades de execução do fluxo de trabalho'
title: Propriedades de execução de fluxo de trabalho
ms.date: 03/30/2017
ms.assetid: a50e088e-3a45-4267-bd51-1a3e6c2d246d
ms.openlocfilehash: d6f83109da0a14382098322858a6e0493750a748
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99754895"
---
# <a name="workflow-execution-properties"></a>Propriedades de execução de fluxo de trabalho

Com o armazenamento local (TLS) de segmento, CLR mantém um contexto de execução para cada segmento. Este contexto de execução determina propriedades de segmento conhecidos como a identidade da thread, a transação ambiente, e o conjunto de permissões atual além de propriedades definidos pelo usuário do segmento como slots nomeados.  
  
 Ao contrário dos programas que direcionam diretamente CLR, os programas de fluxo de trabalho são árvores hierarquicamente o escopo de atividades que executam em um ambiente com desconhecido. Isso significa que os mecanismos padrão de TLS diretamente não podem ser usados para determinar qual contexto está no escopo de um item de trabalho determinado. Por exemplo, duas ramificações paralelos de execução podem usar transações diferentes, porém o agendador pode intercalar sua execução no mesmo segmento de CLR.  
  
 As propriedades de execução de fluxo de trabalho fornecem um mecanismo para adicionar propriedades específicas de contexto para o ambiente de uma atividade. Isso permite que uma atividade declare propriedades que estejam no escopo para sua subárvore e também fornece ganchos para configurar e rasgar para baixo TLS para interoperar corretamente com objetos CLR.  
  
## <a name="creating-and-using-workflow-execution-properties"></a>Criando e usando propriedades de execução de fluxo de trabalho  

 As propriedades de execução de fluxo de trabalho geralmente implementam a interface de <xref:System.Activities.IExecutionProperty> , embora as propriedades centradas sobre a mensagem podem implementar <xref:System.ServiceModel.Activities.ISendMessageCallback> e <xref:System.ServiceModel.Activities.IReceiveMessageCallback> em vez disso. Para criar uma propriedade de execução de fluxo de trabalho, crie uma classe que implementa a interface de <xref:System.Activities.IExecutionProperty> e implementar os membros <xref:System.Activities.IExecutionProperty.SetupWorkflowThread%2A> e <xref:System.Activities.IExecutionProperty.CleanupWorkflowThread%2A>. Esses membros fornecem a propriedade de execução com uma oportunidade para configurar e rasgar corretamente para baixo o armazenamento local de segmentos durante cada pulso de trabalho de atividade que contém a propriedade, incluindo todas as atividades filhos. Nesse exemplo, `ConsoleColorProperty` é criado que define `Console.ForegroundColor`.  
  
```csharp  
class ConsoleColorProperty : IExecutionProperty  
{  
    public const string Name = "ConsoleColorProperty";  
  
    ConsoleColor original;  
    ConsoleColor color;  
  
    public ConsoleColorProperty(ConsoleColor color)  
    {  
        this.color = color;  
    }  
  
    void IExecutionProperty.SetupWorkflowThread()  
    {  
        original = Console.ForegroundColor;  
        Console.ForegroundColor = color;  
    }  
  
    void IExecutionProperty.CleanupWorkflowThread()  
    {  
        Console.ForegroundColor = original;  
    }  
}  
```  
  
 Os autores de atividade podem usar essa propriedade para à atividade executam substituição. Nesse exemplo, uma atividade de `ConsoleColorScope` é definida que registra `ConsoleColorProperty` adicionando à coleção de <xref:System.Activities.NativeActivityContext.Properties%2A> de <xref:System.Activities.NativeActivityContext>atual.  
  
```csharp  
public sealed class ConsoleColorScope : NativeActivity  
{  
    public ConsoleColorScope()  
        : base()  
    {  
    }  
  
    public ConsoleColor Color { get; set; }  
    public Activity Body { get; set; }  
  
    protected override void Execute(NativeActivityContext context)  
    {  
        context.Properties.Add(ConsoleColorProperty.Name, new ConsoleColorProperty(this.Color));  
  
        if (this.Body != null)  
        {  
            context.ScheduleActivity(this.Body);  
        }  
    }  
}  
```  
  
 Quando o corpo da atividade inicia um pulso de trabalho, o método de <xref:System.Activities.IExecutionProperty.SetupWorkflowThread%2A> da propriedade é chamado, e quando o pulso de trabalho estiver concluída, <xref:System.Activities.IExecutionProperty.CleanupWorkflowThread%2A> é chamado. Nesse exemplo, um fluxo de trabalho é criado que usa uma atividade de <xref:System.Activities.Statements.Parallel> com três ramificações. Os primeiros dois ramificações usam a atividade de `ConsoleColorScope` e o terceiro ramificação não. Todos os três ramificações contêm duas atividades de <xref:System.Activities.Statements.WriteLine> e uma atividade de <xref:System.Activities.Statements.Delay> . Quando a atividade de <xref:System.Activities.Statements.Parallel> executa, as atividades que estão contidas nas ramificações executam em uma maneira intercalada, mas como cada atividade filho executa a cor correta do console são aplicadas por `ConsoleColorProperty`.  
  
```csharp  
Activity wf = new Parallel  
{  
    Branches =
    {  
        new ConsoleColorScope  
        {  
            Color = ConsoleColor.Blue,  
            Body = new Sequence  
            {  
                Activities =
                {  
                    new WriteLine  
                    {  
                        Text = "Start blue text."  
                    },  
                    new Delay  
                    {  
                        Duration = TimeSpan.FromSeconds(1)  
                    },  
                    new WriteLine  
                    {  
                        Text = "End blue text."  
                    }  
                }  
            }  
        },  
        new ConsoleColorScope  
        {  
            Color = ConsoleColor.Red,  
            Body = new Sequence  
            {  
                Activities =
                {  
                    new WriteLine  
                    {  
                        Text = "Start red text."  
                    },  
                    new Delay  
                    {  
                        Duration = TimeSpan.FromSeconds(1)  
                    },  
                    new WriteLine  
                    {  
                        Text = "End red text."  
                    }  
                }  
            }  
        },  
        new Sequence  
        {  
            Activities =
            {  
                new WriteLine  
                {  
                    Text = "Start default text."  
                },  
                new Delay  
                {  
                    Duration = TimeSpan.FromSeconds(1)  
                },  
                new WriteLine  
                {  
                    Text = "End default text."  
                }  
            }  
        }  
    }  
};  
  
WorkflowInvoker.Invoke(wf);  
```  
  
 Quando o fluxo de trabalho é chamado, a saída a seguir são gravadas para a janela do console.  
  
```console  
Start blue text.  
Start red text.  
Start default text.  
End blue text.  
End red text.  
End default text.  
```  
  
> [!NOTE]
> Embora não são mostradas na saída anteriores, cada linha de texto na janela de console é exibida na cor indicada.  
  
 As propriedades de execução de fluxo de trabalho podem ser usadas por autores personalizados de atividade, e também fornecem um mecanismo para o gerenciamento de forma para atividades como as atividades de <xref:System.ServiceModel.Activities.CorrelationScope> e de <xref:System.Activities.Statements.TransactionScope> .  
  
## <a name="see-also"></a>Confira também

- <xref:System.Activities.IExecutionProperty>
- <xref:System.Activities.IPropertyRegistrationCallback>
- <xref:System.Activities.RegistrationContext>
