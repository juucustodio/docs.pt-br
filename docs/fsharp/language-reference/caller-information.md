---
title: Informações do chamador
description: Descreve como usar atributos de argumento de informações do chamador para obter informações do chamador de um método.
ms.date: 11/04/2019
ms.openlocfilehash: 700cde26fbe4e6c48155f88bfc63af59af86cfe2
ms.sourcegitcommit: ecd9e9bb2225eb76f819722ea8b24988fe46f34c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/05/2020
ms.locfileid: "96739770"
---
# <a name="caller-information"></a>Informações do chamador

Ao usar atributos de informações do chamador, você pode obter informações sobre o chamador de um método. Você pode obter o caminho do arquivo do código-fonte, o número da linha no código-fonte e o nome do membro do chamador. Essas informações são úteis para fins de rastreamento, depuração e criação de ferramentas de diagnóstico.

Para obter essas informações, você deve usar os atributos que são aplicadas aos parâmetros opcionais, cada qual com um valor padrão. A tabela a seguir lista os atributos de informações do chamador que são definidos no namespace [System. Runtime. CompilerServices](/dotnet/api/system.runtime.compilerservices) :

|Atributo|Descrição|Type|
|---------|-----------|----|
|[CallerFilePath](/dotnet/api/system.runtime.compilerservices.callerfilepathattribute)|O caminho completo do arquivo de origem que contém o chamador. Esse é o caminho do arquivo no momento da compilação.|`String`
|[CallerLineNumber](/dotnet/api/system.runtime.compilerservices.callerlinenumberattribute)|Número da linha no arquivo fonte no qual o método é chamado.|`Integer`|
|[CallerMemberName](/dotnet/api/system.runtime.compilerservices.callermembernameattribute)|Nome do método ou da propriedade do chamador. Consulte a seção nomes de membro mais adiante neste tópico.|`String`|

## <a name="example"></a>Exemplo

O exemplo a seguir mostra como você pode usar esses atributos para rastrear um chamador.

```fsharp
open System.Diagnostics
open System.Runtime.CompilerServices
open System.Runtime.InteropServices

type Tracer() =
    member _.DoTrace(message: string,
                      [<CallerMemberName; Optional; DefaultParameterValue("")>] memberName: string,
                      [<CallerFilePath; Optional; DefaultParameterValue("")>] path: string,
                      [<CallerLineNumber; Optional; DefaultParameterValue(0)>] line: int) =
        Trace.WriteLine(sprintf $"Message: {message}")
        Trace.WriteLine(sprintf $"Member name: {memberName}")
        Trace.WriteLine(sprintf $"Source file path: {path}")
        Trace.WriteLine(sprintf $"Source line number: {line}")
```

## <a name="remarks"></a>Comentários

Os atributos de informações do chamador só podem ser aplicados a parâmetros opcionais. Os atributos de informações do chamador fazem com que o compilador grave o valor adequado para cada parâmetro opcional decorado com um atributo de informações do chamador.

Os valores de informações do chamador são emitidos como literais em linguagem intermediária (IL) em tempo de compilação. Ao contrário dos resultados da propriedade [StackTrace](/dotnet/api/system.diagnostics.stacktrace) para exceções, os resultados não são afetados pela ofuscação.

Você pode fornecer explicitamente os argumentos opcionais para controlar as informações do chamador ou ocultá-las.

## <a name="member-names"></a>Nomes dos membros

Você pode usar o [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) atributo para evitar a especificação do nome do membro como um `String` argumento para o método chamado. Ao usar essa técnica, você evita o problema de que a Refatoração de Renomeação não altera os valores de `String`. Esse benefício é especialmente útil para as seguintes tarefas:

- Usar rotinas de rastreamento e diagnóstico.
- Implementando a interface [INotifyPropertyChanged](/dotnet/api/system.componentmodel.inotifypropertychanged) ao associar dados. Essa interface permite que a propriedade de um objeto notifique um controle associado sobre a alteração da propriedade de modo que o controle possa exibir as informações atualizadas. Sem o [`CallerMemberName`](/dotnet/api/system.runtime.compilerservices.callermembernameattribute) atributo, você deve especificar o nome da propriedade como um literal.

O gráfico a seguir mostra os nomes de membro que são retornados quando você usa o atributo CallerMemberName.

|As chamadas ocorrem em|Resultado de nome de membro|
|-------------------|------------------|
|Método, propriedade ou evento|O nome do método, da propriedade ou do evento em que a chamada foi originada.|
|Construtor|A cadeia de caracteres “.ctor”|
|Construtor estático|A cadeia de caracteres “.cctor”|
|Destruidor|A cadeia de caracteres "Finalize"|
|Operadores usuário ou conversões definidos pelo usuário|O nome gerado para o membro, por exemplo, “op_Addition”.|
|Construtor de atributos|O nome do membro ao qual o atributo se aplica. Se o atributo é qualquer elemento dentro de um membro (como um parâmetro, um valor de retorno, ou um parâmetro de tipo genérico), esse resultado é o nome do membro associado a esse elemento.|
|Nenhum membro contentor (por exemplo, nível de assembly ou atributos que são aplicadas aos tipos)|O valor padrão do parâmetro opcional.|

## <a name="see-also"></a>Confira também

- [Atributos](attributes.md)
- [Argumentos nomeados](parameters-and-arguments.md#named-arguments)
- [Parâmetros opcionais](parameters-and-arguments.md#optional-parameters)
