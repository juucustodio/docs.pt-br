---
description: 'Saiba mais sobre: argumentos necessários e grupos de sobrecarga'
title: Argumentos necessários e grupos de sobrecarga
ms.date: 03/30/2017
ms.assetid: 4ca3ed06-b9af-4b85-8b70-88c2186aefa3
ms.openlocfilehash: 1eea77276ad976c81d891e45cfbe5217b298b4fd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99720027"
---
# <a name="required-arguments-and-overload-groups"></a>Argumentos necessários e grupos de sobrecarga

As atividades podem ser configuradas de modo que determinados argumentos são necessários para ser associados para que a atividade é válido para a execução. O atributo de `RequiredArgument` é usado para indicar que determinados argumentos em uma atividade são necessários e o atributo de `OverloadGroup` é usado para agrupar categorias de argumentos necessários. Usando atributos, os autores de atividade podem fornecer configurações simples ou complexas de validação de atividade.  
  
## <a name="using-required-arguments"></a>Usando argumentos necessários  

 Para usar o atributo de `RequiredArgument` em uma atividade, indica os argumentos desejados usando <xref:System.Activities.RequiredArgumentAttribute>. Nesse exemplo, uma atividade de `Add` é definida que possui dois argumentos necessários.  
  
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
  
 Em XAML, os argumentos necessários são indicados também usando <xref:System.Activities.RequiredArgumentAttribute>. Nesse exemplo a atividade de `Add` é definida usando três argumentos e usa uma atividade de <xref:System.Activities.Statements.Assign%601> para executar a operação adicionar.  
  
```xaml  
<Activity x:Class="ValidationDemo.Add" ...>  
  <x:Members>  
    <x:Property Name="Operand1" Type="InArgument(x:Int32)">  
      <x:Property.Attributes>  
        <RequiredArgumentAttribute />  
      </x:Property.Attributes>  
    </x:Property>  
    <x:Property Name="Operand2" Type="InArgument(x:Int32)">  
      <x:Property.Attributes>  
        <RequiredArgumentAttribute />  
      </x:Property.Attributes>  
    </x:Property>  
    <x:Property Name="Result" Type="OutArgument(x:Int32)" />  
  </x:Members>  
  <Assign>  
    <Assign.To>  
      <OutArgument x:TypeArguments="x:Int32">[Result]</OutArgument>  
    </Assign.To>  
    <Assign.Value>  
      <InArgument x:TypeArguments="x:Int32">[Operand1 + Operand2]</InArgument>  
    </Assign.Value>  
  </Assign>  
</Activity>  
```  
  
 Se a atividade é usada e qualquer um dos argumentos necessários não está associado ao seguinte erro de validação é retornado.  
  
 **O valor de um argumento necessário “Operando1” de atividade não foi fornecido.**  
> [!NOTE]
> Para obter mais informações sobre como verificar e tratar erros e avisos de validação, consulte [invocando a validação da atividade](invoking-activity-validation.md).  
  
## <a name="using-overload-groups"></a>Usando grupos de sobrecarga

Grupos de sobrecarga fornecem um método para indicar que combinações de argumentos são válidos em uma atividade. Os argumentos são agrupados usando <xref:System.Activities.OverloadGroupAttribute>. Cada grupo recebe um nome que é especificado pelo <xref:System.Activities.OverloadGroupAttribute> . A atividade é válida quando apenas um conjunto de argumentos em um grupo de sobrecarga está associado. No exemplo a seguir, uma `CreateLocation` classe é definida.  
  
```csharp  
class CreateLocation: Activity  
{  
    [RequiredArgument]  
    public InArgument<string> Name { get; set; }  
  
    public InArgument<string> Description { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G1")]  
    public InArgument<int> Latitude { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G1")]  
    public InArgument<int> Longitude { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    [OverloadGroup("G3")]  
    public InArgument<string> Street { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    public InArgument<string> City { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G2")]  
    public InArgument<string> State { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("G3")]  
    public InArgument<int> Zip { get; set; }
}  
```  
  
 O objetivo desta atividade é especificar um local nos EUA]). Para fazer isso, o usuário da atividade pode especificar o local usando um dos três grupos de argumentos. Para especificar as combinações de argumentos, válidos três grupos de sobrecarga são definidos. `G1` contém os argumentos de `Latitude` e de `Longitude` . `G2` contém `Street`, `City`, e `State`. `G3` contém `Street` e `Zip`. `Name` é também um argumento necessário, mas não é parte de um grupo de sobrecarga. Para que esta atividade é válida, `Name` terá que ser associado junto com todos os argumentos de um e somente um grupo de sobrecarga.  
  
 No exemplo a seguir, extraído do exemplo de [atividades de acesso ao banco de dados](./samples/database-access-activities.md) , há dois grupos de sobrecarga: `ConnectionString` e `ConfigFileSectionName` . Para que esta atividade é válida, ou outro os argumentos de `ProviderName` e de `ConnectionString` devem ser associados, ou o argumento de `ConfigName` , mas não ambos.  
  
```csharp  
public class DbUpdate: AsyncCodeActivity  
{  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DefaultValue(null)]  
    public InArgument<string> ProviderName { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConnectionString")]  
    [DependsOn("ProviderName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConnectionString { get; set; }  
  
    [RequiredArgument]  
    [OverloadGroup("ConfigFileSectionName")]  
    [DefaultValue(null)]  
    public InArgument<string> ConfigName { get; set; }  
  
    [DefaultValue(null)]  
    public CommandType CommandType { get; set; }  
  
    [RequiredArgument]  
    public InArgument<string> Sql { get; set; }  
  
    [DependsOn("Sql")]  
    [DefaultValue(null)]  
    public IDictionary<string, Argument> Parameters { get; }  
  
    [DependsOn("Parameters")]  
    public OutArgument<int> AffectedRecords { get; set; }
}  
```  
  
 Ao definir um grupo de sobrecarga:  
  
- Um grupo de sobrecarga não pode ser um subconjunto ou um conjunto equivalente de outro grupo de sobrecarga.  
  
    > [!NOTE]
    > Há uma exceção a essa regra. Se um grupo de sobrecarga é um subconjunto de outro grupo de sobrecarga, e o subconjunto contém somente os argumentos onde `RequiredArgument` é `false`, então o grupo de sobrecarga é válido.  
  
- Grupos de sobrecarga podem sobrepor mas é um erro se a interseção de grupos contém todos os argumentos necessários de um ou ambos os grupos de sobrecarga. No exemplo anterior grupos de sobrecarga de `G2` e de `G3` sobrepors, mas porque a interseção não contém todos os argumentos de um ou ambos os grupos isso era válidos.  
  
 Ao associar argumentos em um grupo de sobrecarga:  
  
- Um grupo de sobrecarga está sendo associado se todos os argumentos de `RequiredArgument` no grupo são associados.  
  
- Se um grupo tem os argumentos de `RequiredArgument` zero e pelo menos um argumento associado, então o grupo está sendo associado.  
  
- É um erro de validação se nenhum grupo de sobrecarga é associado a menos que um grupo de sobrecarga não tem nenhum argumento de `RequiredArgument` nele.  
  
- É um erro para ter mais de um grupo de sobrecarga associada, isto é, todos os argumentos necessários em um grupo de sobrecarga é limitado e qualquer argumento em outro grupo de sobrecarga está associado também.
