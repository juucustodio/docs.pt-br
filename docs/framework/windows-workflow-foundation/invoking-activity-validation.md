---
description: 'Saiba mais sobre: invocando a validação da atividade'
title: Invocando a validação de atividades
ms.date: 03/30/2017
ms.assetid: 22bef766-c505-4fd4-ac0f-7b363b238969
ms.openlocfilehash: dc710e76134fbd76f5217df4ea569f20e6de4445
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792655"
---
# <a name="invoking-activity-validation"></a>Invocando a validação de atividades

Validação de atividade fornece um método para identificar e relatar erros na configuração de quaisquer atividades antes da execução. A validação ocorre quando um trabalho são alterados no designer de trabalho e todos os erros ou avisos de validação são exibidos no designer de fluxo de trabalho. Validação também ocorre em tempo de execução quando um fluxo de trabalho é chamado e se qualquer erro de validação ocorre, <xref:System.Activities.InvalidWorkflowException> é acionada pela lógica padrão de validação. Windows Workflow Foundation (WF) fornece a <xref:System.Activities.Validation.ActivityValidationServices> classe que pode ser usada pelo aplicativo de fluxo de trabalho e pelos desenvolvedores de ferramentas para validar explicitamente uma atividade. Este tópico descreve como usar <xref:System.Activities.Validation.ActivityValidationServices> para executar a validação de atividade.  
  
## <a name="using-activityvalidationservices"></a>Usando ActivityValidationServices  

 <xref:System.Activities.Validation.ActivityValidationServices> tem duas sobrecargas de <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> que são usadas para chamar a lógica de validação de uma atividade. A primeira sobrecarga toma a atividade raiz para ser validadas e retorna uma coleção de erros e avisos de validação. No exemplo a seguir, uma atividade de `Add` personalizado é usada que tem dois argumentos necessários.  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 A atividade de `Add` é usada dentro de <xref:System.Activities.Statements.Sequence>, mas os dois argumentos necessárias não são associados, conforme mostrado no exemplo o seguir.  
  
```csharp  
Variable<int> Operand1 = new Variable<int>{ Default = 10 };  
Variable<int> Operand2 = new Variable<int>{ Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 Este fluxo de trabalho pode ser validado chamando <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>. <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> retorna uma coleção de todos os erros ou avisos de validação contidos pela atividade e por quaisquer filhos, conforme mostrado no exemplo o seguir.  
  
```csharp  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 Quando <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> é chamado esse fluxo de trabalho de exemplo, dois erros de validação são retornados.  
  
 **Erro: O valor de um argumento necessário “Operando2” de atividade não foi fornecido.**  
**Erro: O valor de um argumento necessário “Operando1” de atividade não foi fornecido.**  Se esse fluxo de trabalho foi chamado, <xref:System.Activities.InvalidWorkflowException> seria acionada, conforme mostrado no exemplo o seguir.  
  
```csharp  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 **System.Activities.InvalidWorkflowException:**  
**Os seguintes erros foram encontrados durante o processamento da árvore de fluxo de trabalho:** 
 **' Add ': o valor para um argumento de atividade necessário ' operand2 ' não foi fornecido.** 
 **' Add ': o valor para um argumento de atividade necessário ' Operand1 ' não foi fornecido.**  Para que este fluxo de trabalho de exemplo é válida, os dois argumentos pré-requisito de atividade de `Add` devem ser associados. No exemplo a seguir, os dois argumentos são necessárias associados a variáveis de fluxo de trabalho juntamente com o valor de resultado. Nesse exemplo o argumento de <xref:System.Activities.Activity%601.Result%2A> está associado juntamente com os dois argumentos necessários. O argumento de <xref:System.Activities.Activity%601.Result%2A> não é necessário para ser associado e não causa um erro de validação se não é. É responsabilidade do autor de fluxo de trabalho associar <xref:System.Activities.Activity%601.Result%2A> se seu valor é usado em outro lugar no fluxo de trabalho.  
  
```csharp  
new Add  
{  
    Operand1 = Operand1,  
    Operand2 = Operand2,  
    Result = Result  
}  
```  
  
### <a name="validating-required-arguments-on-the-root-activity"></a>Validando argumentos necessários na atividade raiz  

 Se a atividade raiz de um fluxo de trabalho tem argumentos, eles não estão associados até que o fluxo de trabalho é chamado e os parâmetros são passados para o fluxo de trabalho. O seguinte fluxo de trabalho passa a validação, mas uma exceção é lançada se o fluxo de trabalho é chamado sem passar os argumentos necessários, conforme mostrado no exemplo o seguir.  
  
```csharp  
Activity wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, but when the workflow  
// is invoked, an InvalidWorkflowException is thrown.  
try  
{  
    WorkflowInvoker.Invoke(wf);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
 **System.ArgumentException: As configurações do argumento de atividade de raiz são incorretas.**  
**Corrija a definição de fluxo de trabalho ou forneça valores de entrada para corrigir esses erros:** 
 **' Add ': o valor para um argumento de atividade necessário ' operand2 ' não foi fornecido.** 
 **' Add ': o valor para um argumento de atividade necessário ' Operand1 ' não foi fornecido.**  Após os argumentos corretos são passados, o fluxo de trabalho concluída com sucesso, conforme mostrado no exemplo o seguir.  
  
```csharp  
Add wf = new Add();  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
// results has no errors or warnings, and the workflow completes  
// successfully because the required arguments were passed.  
try  
{  
    Dictionary<string, object> wfparams = new Dictionary<string, object>  
    {  
        { "Operand1", 10 },  
        { "Operand2", 15 }  
    };  
  
    int result = WorkflowInvoker.Invoke(wf, wfparams);  
    Console.WriteLine("Result: {0}", result);  
}  
catch (Exception ex)  
{  
    Console.WriteLine(ex);  
}  
```  
  
> [!NOTE]
> Nesse exemplo, a atividade de raiz ter sido declarada como `Add` em vez de `Activity` como no exemplo anterior. Isso permite que o método de `WorkflowInvoker.Invoke` retorna um único número inteiro que representa os resultados de atividade de `Add` em vez de um dicionário de argumentos de `out` . `wf` variável pode também ter sido declarado como `Activity<int>`.  
  
 Para validar argumentos de raiz, é responsabilidade do aplicativo host garantir que todos os argumentos necessários são passados quando o fluxo de trabalho é chamado.  
  
### <a name="invoking-imperative-code-based-validation"></a>Invocando a validação classe base imperativa

A validação classe base imperativa fornece uma maneira simples para uma atividade fornece validação sobre se, e está disponível para as atividades que derivam de <xref:System.Activities.CodeActivity>, de <xref:System.Activities.AsyncCodeActivity>, e de <xref:System.Activities.NativeActivity>. O código de validação que determina os erros ou avisos de validação é adicionado à atividade. Quando a validação é chamada na atividade, esses erros ou avisos estão contidos na coleção retornada pela chamada a <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>. No exemplo a seguir, uma atividade de `CreateProduct` é definida. Se `Cost` é maior do que `Price`, um erro de validação é adicionado aos metadados em uma substituição de <xref:System.Activities.CodeActivity.CacheMetadata%2A> .  
  
```csharp  
public sealed class CreateProduct : CodeActivity  
{  
    public double Price { get; set; }  
    public double Cost { get; set; }  
  
    // [RequiredArgument] attribute will generate a validation error
    // if the Description argument is not set.  
    [RequiredArgument]  
    public InArgument<string> Description { get; set; }  
  
    protected override void CacheMetadata(CodeActivityMetadata metadata)  
    {  
        base.CacheMetadata(metadata);  
        // Determine when the activity has been configured in an invalid way.  
        if (this.Cost > this.Price)  
        {  
            // Add a validation error with a custom message.  
            metadata.AddValidationError("The Cost must be less than or equal to the Price.");  
        }  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // Not needed for the sample.  
    }  
}  
```  
  
 Nesse exemplo, um fluxo de trabalho é configurado usando a atividade de `CreateProduct` . Nesse fluxo de trabalho, `Cost` é maior do que `Price`, e o argumento necessário de `Description` não está definido. Quando a validação é chamada, os seguintes erros são retornados.  
  
```csharp  
Activity wf = new Sequence  
{  
    Activities =
    {  
        new CreateProduct  
        {  
            Cost = 75.00,  
            Price = 55.00  
            // Cost > Price and required Description argument not set.  
        },  
        new WriteLine  
        {  
            Text = "Product added."  
        }  
    }  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 **Erro: O custo devem ser menor ou igual ao preço.**  
**Erro: O valor de um argumento necessário “descrição de atividade” não foi fornecido.**
> [!NOTE]
> Os autores de atividade personalizados podem fornecer a lógica de validação em uma substituição de <xref:System.Activities.CodeActivity.CacheMetadata%2A> de uma atividade. Nenhuma exceções que são geradas de <xref:System.Activities.CodeActivity.CacheMetadata%2A> não são tratados como erros de validação. Essas exceções escaparão de chamada para <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> e devem ser tratadas pelo chamador.  
  
## <a name="using-validationsettings"></a>Usando ValidationSettings  

 Por padrão, todas as atividades na árvore de atividade são avaliadas quando a validação é chamada por <xref:System.Activities.Validation.ActivityValidationServices>. <xref:System.Activities.Validation.ValidationSettings> permite que a validação seja adequada em várias maneiras diferentes configurando as três propriedades. <xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> especifica se o validador deve percorrer a árvore de atividade inteiro ou apenas aplicar lógica de validação à atividade fornecida. O padrão para este valor é `false`. <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> especifica a restrição adicional que mapeia de um tipo em uma lista de restrições. Para o tipo de base de cada atividade na árvore de atividade que está sendo validada há uma pesquisa em <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>. Se uma lista de restrição correspondente for encontrada, todas as restrições na lista são avaliadas para atividades. <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> especifica se o validador deve avaliar todas as restrições ou somente aquelas especificadas em <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>. O valor padrão é `false`. <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> e <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> são úteis para que os autores de host de fluxo de trabalho adicionar validação adicional para fluxos de trabalho, como restrições de política para ferramentas como o FxCop. Para obter mais informações sobre restrições, consulte [restrições declarativas](declarative-constraints.md).  
  
 Para usar <xref:System.Activities.Validation.ValidationSettings>, configurar as propriedades desejadas, e passá-las na chamada ao <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>. Nesse exemplo, um fluxo de trabalho que consiste <xref:System.Activities.Statements.Sequence> com uma atividade de `Add` personalizado é validado. A atividade de `Add` tem dois argumentos necessários.  
  
```csharp  
public sealed class Add : CodeActivity<int>  
{  
    [RequiredArgument]  
    public InArgument<int> Operand1 { get; set; }  
  
    [RequiredArgument]  
    public InArgument<int> Operand2 { get; set; }  
  
    protected override int Execute(CodeActivityContext context)  
    {  
        return Operand1.Get(context) + Operand2.Get(context);  
    }  
}  
```  
  
 A seguir atividade de `Add` é usada em <xref:System.Activities.Statements.Sequence>, mas os dois argumentos necessárias não são associados.  
  
```csharp  
Variable<int> Operand1 = new Variable<int> { Default = 10 };  
Variable<int> Operand2 = new Variable<int> { Default = 15 };  
Variable<int> Result = new Variable<int>();  
  
Activity wf = new Sequence  
{  
    Variables = { Operand1, Operand2, Result },  
    Activities =
    {  
        new Add(),  
        new WriteLine  
        {  
            Text = new InArgument<string>(env => "The result is " + Result.Get(env))  
        }  
    }  
};  
```  
  
 Para o exemplo a seguir, a validação é executada com <xref:System.Activities.Validation.ValidationSettings.SingleLevel%2A> definido como `true`, portanto somente a atividade de <xref:System.Activities.Statements.Sequence> raiz é validada.  
  
```csharp  
ValidationSettings settings = new ValidationSettings  
{  
    SingleLevel = true  
};  
  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error: {0}", error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning: {0}", warning.Message);  
    }  
}  
```  
  
 Este código exibe a saída a seguir:  
  
 **Nenhum aviso ou erro** Embora a `Add` atividade tenha argumentos necessários que não estejam associados, a validação é bem-sucedida porque apenas a atividade raiz é avaliada. Esse tipo de validação é útil para validar somente os elementos específicos em uma árvore de atividade, como validação de uma alteração de propriedade de uma única atividade em um designer. Observe que se esse fluxo de trabalho é chamado, a validação completa configurado no fluxo de trabalho é avaliado e <xref:System.Activities.InvalidWorkflowException> será lançada. <xref:System.Activities.Validation.ActivityValidationServices> e configurar <xref:System.Activities.Validation.ValidationSettings> somente validação chamada explicitamente pelo host, e não a validação que ocorre quando um fluxo de trabalho é chamado.
