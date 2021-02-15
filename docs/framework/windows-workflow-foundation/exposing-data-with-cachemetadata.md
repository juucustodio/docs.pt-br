---
description: 'Saiba mais sobre: expondo dados com CacheMetadata'
title: Expõem dados com CacheMetadata
ms.date: 03/30/2017
ms.assetid: 34832f23-e93b-40e6-a80b-606a855a00d9
ms.openlocfilehash: ac4623881ebd76270f773a3b7acfe205ad365118
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742336"
---
# <a name="exposing-data-with-cachemetadata"></a>Expõem dados com CacheMetadata

Antes de executar uma atividade, o runtime de fluxo de trabalho obtém qualquer informação sobre a atividade que precisa para manter sua execução. O runtime de fluxo de trabalho obtém essas informações durante a execução do método de <xref:System.Activities.Activity.CacheMetadata%2A> . A implementação padrão desse método oferece o runtime com todos os argumentos públicos, variáveis, e atividades filhos exposto pela atividade é então executada; se a atividade precisará fornecer mais informações em runtime desta (como membros particulares, ou atividades a ser agendadas pela atividade), esse método pode ser substituído para oferece.

## <a name="default-cachemetadata-behavior"></a>Comportamento padrão de CacheMetadata

A implementação padrão de <xref:System.Activities.NativeActivity.CacheMetadata%2A> para as atividades que derivam de <xref:System.Activities.NativeActivity> processa os tipos de seguinte método das seguintes maneiras:

- <xref:System.Activities.InArgument%601>, <xref:System.Activities.OutArgument%601>, ou <xref:System.Activities.InOutArgument%601> (argumentos genéricos): Esses argumentos são expostos no runtime como argumentos com um nome e tipo igual ao nome e o tipo expõe de propriedade, a direção apropriado do argumento, e alguns dados de validação.

- <xref:System.Activities.Variable> ou alguma subclasse disso: Esses membros são expostos no runtime como variáveis públicas.

- <xref:System.Activities.Activity> ou alguma subclasse disso: Esses membros são expostos ao runtime como atividades filhos públicas. O comportamento padrão pode ser implementado explicitamente chamando <xref:System.Activities.ActivityMetadata.AddImportedChild%2A> , passando a atividade filho.

- <xref:System.Activities.ActivityDelegate> ou alguma subclasse disso: Esses membros são expostos no runtime como representantes públicos.

- <xref:System.Collections.ICollection> de tipo <xref:System.Activities.Variable>: Todos os elementos na coleção é retornado para o runtime como variáveis públicas.

- <xref:System.Collections.ICollection> de tipo <xref:System.Activities.Activity>: Todos os elementos na coleção expostos no runtime como filhos públicos.

- <xref:System.Collections.ICollection> de tipo <xref:System.Activities.ActivityDelegate>: Todos os elementos na coleção são expostos ao runtime como representantes públicos.

<xref:System.Activities.Activity.CacheMetadata%2A> para as atividades que derivam de <xref:System.Activities.Activity>, <xref:System.Workflow.Activities.CodeActivity>, e <xref:System.Activities.AsyncCodeActivity> também funcionam como anterior, exceto as seguintes diferenças:

- As classes que derivam de <xref:System.Activities.Activity> não pode agendar atividades filho ou representantes, para que esses membros são expostos como filhos e delegados importados; 

- As classes que derivam de <xref:System.Activities.CodeActivity> e <xref:System.Activities.AsyncCodeActivity> não suporta variáveis, filhos, ou representantes, portanto somente argumentos serão expostas.

## <a name="overriding-cachemetadata-to-provide-information-to-the-runtime"></a>Substituindo CacheMetadata para fornecer informações em runtime

O snippet de código a seguir demonstra como adicionar informações sobre membros para metadados de uma atividade durante a execução do método de <xref:System.Activities.Activity.CacheMetadata%2A> . Observe que a base do método é chamada para armazenar em cachê todos os dados públicos sobre a atividade.

```csharp
protected override void CacheMetadata(NativeActivityMetadata metadata)
{
    base.CacheMetadata(metadata);
    metadata.AddImplementationChild(this._writeLine);
    metadata.AddVariable(this._myVariable);
    metadata.AddImplementationVariable(this._myImplementationVariable);

    RuntimeArgument argument = new RuntimeArgument("MyArgument", ArgumentDirection.In, typeof(SomeType));
    metadata.Bind(argument, this.SomeName);
    metadata.AddArgument(argument);
}
```

## <a name="using-cachemetadata-to-expose-implementation-children"></a>Usando CacheMetadata para expor filhos de implementação

Para passar dados para atividades filhos que devem ser agendadas por uma atividade usando variáveis, é necessário adicionar variáveis como variáveis de implementação; variáveis públicas não podem ter seus valores definidos essa maneira. A razão para isso é que as atividades são feitos para ser executadas mais como implementações das funções (que têm parâmetros), em vez das classes encapsuladas (que tem propriedades). No entanto, há situações em que os argumentos devem ser explicitamente definidos, como ao usar <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>, desde que a atividade agendada não tem acesso aos argumentos pai de atividade da maneira que uma atividade filho.

O snippet de código a seguir demonstra como passar um formulário do argumento uma atividade nativo em uma atividade agendada usando <xref:System.Activities.Activity.CacheMetadata%2A>.

```csharp
public sealed class ChildActivity : NativeActivity
{
    public WriteLine _writeLine;
    public InArgument<string> Message { get; set; }
    private Variable<string> MessageVariable { get; set; }
    public ChildActivity()
    {
        MessageVariable = new Variable<string>();
        _writeLine = new WriteLine
        {
            Text = new InArgument<string>(MessageVariable),
        };
    }
    protected override void CacheMetadata(NativeActivityMetadata metadata)
    {
        base.CacheMetadata(metadata);
        metadata.AddImplementationVariable(this.MessageVariable);
        metadata.AddImplementationChild(this._writeLine);
    }
    protected override void Execute(NativeActivityContext context)
    {
        string configuredMessage = context.GetValue(Message);
        context.SetValue(MessageVariable, configuredMessage);
        context.ScheduleActivity(this._writeLine);
    }
}
```
