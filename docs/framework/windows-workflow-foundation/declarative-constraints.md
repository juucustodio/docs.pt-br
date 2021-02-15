---
description: 'Saiba mais sobre: restrições declarativas'
title: Restrições declarativas
ms.date: 03/30/2017
ms.assetid: 67001ed1-7f4d-4ada-ae57-a31176901a53
ms.openlocfilehash: 7eeee5577e9c98db52af579749a59bc76a59b411
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99742505"
---
# <a name="declarative-constraints"></a>Restrições declarativas

As restrições declarativas fornecem um método poderoso de validação para uma atividade e suas relações com outras atividades. As restrições são configuradas para uma atividade durante o processo de design, mas as restrições adicionais podem também ser especificadas pelo host de fluxo de trabalho. Este tópico fornece uma visão geral do uso de restrições declarativas para fornecer validação de atividade.  
  
## <a name="using-declarative-constraints"></a>Usando restrições declarativas  

 Uma restrição é uma atividade que contém a lógica de validação. Esta atividade de restrição pode ser criada no código ou em XAML. Depois que uma atividade de restrição é criada, os autores de atividade adicionam esta restrição à propriedade de <xref:System.Activities.Activity.Constraints%2A> de atividade para validar, ou usam a restrição para fornecer validação adicionais usando a propriedade de <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> de uma instância de <xref:System.Activities.Validation.ValidationSettings> . A lógica de validação pode consistir de validações simples como validar os metadados de uma atividade, mas também pode executar a validação que leva em consideração a relação de atividade atual para seus pais, filhos, e atividades irmãos. As restrições são criadas usando a atividade de <xref:System.Activities.Validation.Constraint%601> , e várias atividades de validação adicionais são fornecidas para auxiliar na criação de erros e avisos de validação e fornecer informações sobre atividades relacionadas no fluxo de trabalho.  
  
### <a name="assertvalidation-and-addvalidationerror"></a>AssertValidation e AddValidationError  

 A atividade de <xref:System.Activities.Validation.AssertValidation> avalia a expressão referenciada por sua propriedade de <xref:System.Activities.Validation.AssertValidation.Assertion%2A> , e se a expressão avaliada como `false`, um erro de validação ou aviso é adicionado a <xref:System.Activities.Validation.ValidationResults>. A propriedade de <xref:System.Activities.Validation.AssertValidation.Message%2A> descreve o erro de validação e a propriedade <xref:System.Activities.Validation.AssertValidation.IsWarning%2A> indica se a falha de validação é um erro ou um aviso. O valor padrão para <xref:System.Activities.Validation.AssertValidation.IsWarning%2A> é `false`.  
  
 No exemplo a seguir, uma restrição é declarada que retorna um aviso de validação se <xref:System.Activities.Activity.DisplayName%2A> atividade estão sendo validada é dois caracteres ou menos de tamanho. O parâmetro de tipo genérico usado para <xref:System.Activities.Validation.Constraint%601> especifica o tipo de atividade que é validada pela restrição. Esta restrição usa <xref:System.Activities.Activity> como o tipo genérico e pode ser usada para validar todos os tipos de atividades.  
  
```csharp  
public static Constraint ActivityDisplayNameIsNotSetWarning()  
{  
    DelegateInArgument<Activity> element = new DelegateInArgument<Activity>();  
  
    return new Constraint<Activity>  
    {  
        Body = new ActivityAction<Activity, ValidationContext>  
        {  
            Argument1 = element,  
            Handler = new AssertValidation  
            {  
                IsWarning = true,  
                Assertion = new InArgument<bool>(env => (element.Get(env).DisplayName.Length > 2)),  
                Message = new InArgument<string>("It is a best practice to have a DisplayName of more than 2 characters."),  
            }  
        }  
    };  
}  
```  
  
 Para especificar esta restrição para uma atividade, é adicionada a <xref:System.Activities.Activity.Constraints%2A> de atividade, conforme mostrado no código de exemplo a seguir.  
  
```csharp  
public sealed class SampleActivity : CodeActivity  
{  
    public SampleActivity()  
    {  
        base.Constraints.Add(ActivityDisplayNameIsNotSetWarning());  
    }  
  
    // Activity implementation omitted.  
}  
```  
  
 O host também pode especificar esta restrição para atividades em um fluxo de trabalho usando <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A>, que é abordado na seção a seguir.  
  
 A atividade de <xref:System.Activities.Validation.AddValidationError> é usada para gerar um erro ou um aviso de validação sem exigir a avaliação de uma expressão. Suas propriedades são semelhantes a <xref:System.Activities.Validation.AssertValidation> e pode ser usado em conjunto com atividades de controle de fluxo de uma restrição como a atividade de <xref:System.Activities.Statements.If> .
  
### <a name="workflow-relationship-activities"></a>Atividades de relação de fluxo de trabalho

Várias atividades de validação estão disponíveis que fornecem informações sobre as outras atividades no fluxo de trabalho com relação a atividade que está sendo validada. <xref:System.Activities.Validation.GetParentChain> retorna uma coleção de atividades que contém todas as atividades entre a atividade atual e a atividade de raiz. <xref:System.Activities.Validation.GetChildSubtree> fornece uma coleção de atividades que contém as atividades filho em um padrão recursiva, e <xref:System.Activities.Validation.GetWorkflowTree> obtém todas as atividades no fluxo de trabalho.  
  
No exemplo a seguir, uma atividade de `CreateState` é definida. A atividade de `CreateState` deve estar contido dentro de uma atividade de `CreateCountry` , e o método de `GetParent` retorna uma restrição que impõe esse requisito. `GetParent` usa a atividade de <xref:System.Activities.Validation.GetParentChain> em conjunto com uma atividade de <xref:System.Activities.Statements.ForEach%601> verificar as atividades pai de atividade de `CreateState` para determinar se o requisito é atingido.  
  
```csharp  
public sealed class CreateState : CodeActivity  
{  
    public CreateState()  
    {  
        base.Constraints.Add(CheckParent());  
        this.Cities = new List<Activity>();
    }  
  
    public List<Activity> Cities { get; set; }  
  
    public string Name { get; set; }
  
    static Constraint CheckParent()  
    {  
        DelegateInArgument<CreateState> element = new DelegateInArgument<CreateState>();  
        DelegateInArgument<ValidationContext> context = new DelegateInArgument<ValidationContext>();
        Variable<bool> result = new Variable<bool>();  
        DelegateInArgument<Activity> parent = new DelegateInArgument<Activity>();  
  
        return new Constraint<CreateState>  
        {
            Body = new ActivityAction<CreateState,ValidationContext>  
            {
                Argument1 = element,  
                Argument2 = context,  
                Handler = new Sequence  
                {  
                    Variables =  
                    {  
                        result
                    },  
                    Activities =  
                    {  
                        new ForEach<Activity>  
                        {
                            Values = new GetParentChain  
                            {  
                                ValidationContext = context
                            },  
                            Body = new ActivityAction<Activity>  
                            {
                                Argument = parent,
                                Handler = new If()  
                                {
                                    Condition = new InArgument<bool>((env) => object.Equals(parent.Get(env).GetType(),typeof(CreateCountry))),
                                    Then = new Assign<bool>  
                                    {  
                                        Value = true,  
                                        To = result  
                                    }  
                                }  
                            }
                        },  
                        new AssertValidation  
                        {  
                            Assertion = new InArgument<bool>(result),  
                            Message = new InArgument<string> ("CreateState has to be inside a CreateCountry activity"),
                        }  
                    }  
                }  
            }  
        };  
    }  
  
    protected override void Execute(CodeActivityContext context)  
    {  
        // not needed for the sample  
    }  
}  
```
  
## <a name="additional-constraints"></a>Restrições adicionais  

 Os autores de host de fluxo de trabalho podem especificar restrições adicionais de validação para atividades em um fluxo de trabalho criando as restrições e adicionando ao dicionário de <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> de uma instância de <xref:System.Activities.Validation.ValidationSettings> . Cada item em <xref:System.Activities.Validation.ValidationSettings.AdditionalConstraints%2A> contém o tipo de atividade para que as restrições se aplicam e uma lista de restrições adicionais para esse tipo de atividade. Quando a validação é chamada para o fluxo de trabalho, cada atividade do tipo especificado, incluindo classes derivadas, avalia as restrições. Nesse exemplo, a restrição de `ActivityDisplayNameIsNotSetWarning` a seção anterior é aplicado a todas as atividades em um fluxo de trabalho.  
  
```csharp  
Activity wf = new Sequence  
{  
    // Workflow Details Omitted.  
};  
  
ValidationSettings settings = new ValidationSettings()  
{  
  
    AdditionalConstraints =  
    {  
        {typeof(Activity), new List<Constraint> {ActivityDisplayNameIsNotSetWarning()}},
    }  
};  
  
// Validate the workflow.  
ValidationResults results = ActivityValidationServices.Validate(wf, settings);  
  
// Evaluate the results.  
if (results.Errors.Count == 0 && results.Warnings.Count == 0)  
{  
    Console.WriteLine("No warnings or errors");  
}  
else  
{  
    foreach (ValidationError error in results.Errors)  
    {  
        Console.WriteLine("Error in " + error.Source.DisplayName + ": " + error.Message);  
    }  
    foreach (ValidationError warning in results.Warnings)  
    {  
        Console.WriteLine("Warning in " + warning.Source.DisplayName + ": " + warning.Message);  
    }  
}  
```  
  
 Se a propriedade de <xref:System.Activities.Validation.ValidationSettings.OnlyUseAdditionalConstraints%2A> de <xref:System.Activities.Validation.ValidationSettings> é `true`, então somente as restrições adicionais especificadas são avaliadas quando a validação é chamada chamando o <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>. Isso pode ser útil para inspecionar fluxos de trabalho para configurações específicas de validação. Observe entretanto que quando o fluxo de trabalho é chamado, a lógica de validação configurou no fluxo de trabalho é avaliado e deve passar para o fluxo de trabalho inicia com êxito. Para obter mais informações sobre como invocar a validação, consulte [invocando a validação da atividade](invoking-activity-validation.md).
