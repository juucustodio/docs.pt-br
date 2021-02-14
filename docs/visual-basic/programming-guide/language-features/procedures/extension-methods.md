---
description: 'Saiba mais sobre: métodos de extensão (Visual Basic)'
title: Métodos de Extensão
ms.date: 07/20/2015
f1_keywords:
- vb.ExtensionMethods
helpviewer_keywords:
- extending data types [Visual Basic]
- extension methods [Visual Basic]
ms.assetid: b8020aae-374d-46a9-bcb7-8cc2390b93b6
ms.openlocfilehash: 5a1482502b144524c0be90e1c83a38f49b4a4d26
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100434349"
---
# <a name="extension-methods-visual-basic"></a>Métodos de extensão (Visual Basic)

Os métodos de extensão permitem que os desenvolvedores adicionem funcionalidade personalizada a tipos de dados que já estão definidos sem a criação de um novo tipo derivado. Os métodos de extensão possibilitam escrever um método que pode ser chamado como se fosse um método de instância do tipo existente.

## <a name="remarks"></a>Comentários

Um método de extensão pode ser apenas um `Sub` procedimento ou um `Function` procedimento. Você não pode definir uma propriedade de extensão, um campo ou um evento. Todos os métodos de extensão devem ser marcados com o atributo `<Extension>` de extensão do <xref:System.Runtime.CompilerServices?displayProperty=nameWithType> namespace e devem ser definidos em um [módulo](../../../language-reference/statements/module-statement.md). Se um método de extensão for definido fora de um módulo, o compilador Visual Basic gerará o erro [BC36551](../../../misc/bc36551.md), "os métodos de extensão podem ser definidos somente em módulos".

O primeiro parâmetro em uma definição de método de extensão especifica o tipo de dados que o método estende. Quando o método é executado, o primeiro parâmetro é associado à instância do tipo de dados que invoca o método.

O `Extension` atributo só pode ser aplicado a um Visual Basic [`Module`](../../../language-reference/statements/module-statement.md) , [`Sub`](../../../language-reference/statements/sub-statement.md) ou [`Function`](../../../language-reference/statements/function-statement.md) . Se você aplicá-lo a um `Class` ou a `Structure` , o compilador Visual Basic gerará o erro [BC36550](../../../language-reference/error-messages/extension-attribute-can-be-applied-only-to-module-sub-or-function-declarations.md), o atributo "extensão" poderá ser aplicado somente às declarações "módulo", "sub" ou "função".

## <a name="example"></a>Exemplo

O exemplo a seguir define uma `Print` extensão para o <xref:System.String> tipo de dados. O método usa `Console.WriteLine` para exibir uma cadeia de caracteres. O parâmetro do `Print` método, `aString` , estabelece que o método estende a <xref:System.String> classe.

[!code-vb[VbVbalrExtensionMethods#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/StringExtensions.vb#1)]

Observe que a definição do método de extensão está marcada com o atributo de extensão `<Extension()>` . Marcar o módulo no qual o método é definido é opcional, mas cada método de extensão deve ser marcado. <xref:System.Runtime.CompilerServices> deve ser importado para acessar o atributo de extensão.

Os métodos de extensão podem ser declarados somente dentro de módulos. Normalmente, o módulo no qual um método de extensão é definido não é o mesmo módulo que aquele em que ele é chamado. Em vez disso, o módulo que contém o método de extensão é importado, se precisar, para colocá-lo no escopo. Depois que o módulo que contém `Print` está no escopo, o método pode ser chamado como se fosse um método de instância comum que não usa argumentos, como `ToUpper` :

[!code-vb[VbVbalrExtensionMethods#2](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class1.vb#2)]

O exemplo a seguir, `PrintAndPunctuate` , também é uma extensão para <xref:System.String> , desta vez definido com dois parâmetros. O primeiro parâmetro, `aString` , estabelece que o método de extensão se estende <xref:System.String> . O segundo parâmetro, `punc` , deve ser uma cadeia de caracteres de sinais de pontuação que é passada como um argumento quando o método é chamado. O método exibe a cadeia de caracteres seguida pelas marcas de pontuação.

[!code-vb[VbVbalrExtensionMethods#3](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class2.vb#3)]

O método é chamado enviando em um argumento de cadeia de caracteres para `punc` : `example.PrintAndPunctuate(".")`

O exemplo a seguir mostra `Print` e é `PrintAndPunctuate` definido e chamado. <xref:System.Runtime.CompilerServices> é importado no módulo de definição para habilitar o acesso ao atributo de extensão.

```vb
Imports System.Runtime.CompilerServices

Module StringExtensions

    <Extension()>
    Public Sub Print(aString As String)
        Console.WriteLine(aString)
    End Sub

    <Extension()>
    Public Sub PrintAndPunctuate(aString As String, punc As String)
        Console.WriteLine(aString & punc)
    End Sub
End Module
```

Em seguida, os métodos de extensão são trazidos para o escopo e chamados:

```vb
Imports ConsoleApplication2.StringExtensions

Module Module1

    Sub Main()
        Dim example As String = "Example string"
        example.Print()

        example = "Hello"
        example.PrintAndPunctuate(".")
        example.PrintAndPunctuate("!!!!")
    End Sub
End Module
```

Tudo o que é necessário para poder executar esses ou métodos de extensão semelhantes é que eles estão no escopo. Se o módulo que contém um método de extensão estiver no escopo, ele ficará visível no IntelliSense e poderá ser chamado como se fosse um método de instância comum.

Observe que, quando os métodos são invocados, nenhum argumento é enviado para o primeiro parâmetro. `aString`O parâmetro nas definições de método anteriores está associado a `example` , a instância do que as `String` chama. O compilador usará `example` como o argumento enviado ao primeiro parâmetro.

Se um método de extensão for chamado para um objeto definido como `Nothing` , o método de extensão será executado. Isso não se aplica a métodos de instância comuns. Você pode verificar explicitamente `Nothing` no método de extensão.

## <a name="types-that-can-be-extended"></a>Tipos que podem ser estendidos

Você pode definir um método de extensão na maioria dos tipos que podem ser representados em uma Visual Basic lista de parâmetros, incluindo o seguinte:

- Classes (tipos de referência)
- Estruturas (tipos de valor)
- Interfaces
- Delegados
- Argumentos ByRef e ByVal
- Parâmetros de método genérico
- Matrizes

Como o primeiro parâmetro especifica o tipo de dados que o método de extensão estende, ele é necessário e não pode ser opcional. Por esse motivo, `Optional` parâmetros e parâmetros `ParamArray` não podem ser o primeiro parâmetro na lista de parâmetros.

Os métodos de extensão não são considerados na associação tardia. No exemplo a seguir, a instrução `anObject.PrintMe()` gera uma <xref:System.MissingMemberException> exceção, a mesma exceção que você veria se a definição do segundo `PrintMe` método de extensão fosse excluída.

[!code-vb[VbVbalrExtensionMethods#9](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class6.vb#9)]

## <a name="best-practices"></a>Práticas recomendadas

Os métodos de extensão fornecem uma maneira conveniente e eficiente de estender um tipo existente. No entanto, para usá-los com êxito, há alguns pontos a serem considerados. Essas considerações se aplicam principalmente a autores de bibliotecas de classes, mas podem afetar qualquer aplicativo que use métodos de extensão.

Geralmente, os métodos de extensão que você adiciona aos tipos que não são de sua propriedade são mais vulneráveis do que os métodos de extensão adicionados aos tipos que você controla. Várias coisas podem ocorrer em classes que não são de sua propriedade que podem interferir nos métodos de extensão.

- Se existir algum membro de instância acessível que tenha uma assinatura compatível com os argumentos na instrução de chamada, sem conversões redutoras necessárias do argumento para o parâmetro, o método de instância será usado em preferência para qualquer método de extensão. Portanto, se um método de instância apropriado for adicionado a uma classe em algum momento, um membro de extensão existente que você depende poderá se tornar inacessível.

- O autor de um método de extensão não pode impedir que outros programadores gravem métodos de extensão conflitantes que possam ter precedência sobre a extensão original.

- Você pode melhorar a robustez colocando métodos de extensão em seu próprio namespace. Os consumidores da sua biblioteca podem, então, incluir um namespace ou excluí-lo ou selecionar entre namespaces, separadamente do restante da biblioteca.

- Pode ser mais seguro estender interfaces do que estender classes, especialmente se você não possuir a interface ou classe. Uma alteração em uma interface afeta cada classe que a implementa. Portanto, talvez seja menos provável que o autor adicione ou altere métodos em uma interface. No entanto, se uma classe implementar duas interfaces que têm métodos de extensão com a mesma assinatura, nenhum método de extensão será visível.

- Estenda o tipo mais específico que você pode. Em uma hierarquia de tipos, se você selecionar um tipo do qual muitos outros tipos são derivados, haverá camadas de possibilidades para a introdução de métodos de instância ou outros métodos de extensão que possam interferir com o seu.

## <a name="extension-methods-instance-methods-and-properties"></a>Métodos de extensão, métodos de instância e propriedades

Quando um método de instância no escopo tem uma assinatura que é compatível com os argumentos de uma instrução de chamada, o método de instância é escolhido de preferência para qualquer método de extensão. O método de instância tem precedência mesmo se o método de extensão for uma correspondência melhor. No exemplo a seguir, `ExampleClass` contém um método de instância chamado `ExampleMethod` que tem um parâmetro do tipo `Integer` . O método `ExampleMethod` de extensão estende `ExampleClass` e tem um parâmetro do tipo `Long` .

[!code-vb[VbVbalrExtensionMethods#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class4.vb#4)]

A primeira chamada para `ExampleMethod` no código a seguir chama o método de extensão, porque `arg1` é `Long` e é compatível apenas com o `Long` parâmetro no método de extensão. A segunda chamada para `ExampleMethod` tem um `Integer` argumento, `arg2` e ele chama o método de instância.

[!code-vb[VbVbalrExtensionMethods#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class4.vb#5)]

Agora inverta os tipos de dados dos parâmetros nos dois métodos:

[!code-vb[VbVbalrExtensionMethods#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class5.vb#6)]

Desta vez, o código em `Main` chama o método de instância duas vezes. Isso ocorre porque ambos `arg1` e `arg2` têm uma conversão de ampliação para `Long` , e o método de instância tem precedência sobre o método de extensão em ambos os casos.

[!code-vb[VbVbalrExtensionMethods#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Class5.vb#7)]

Portanto, um método de extensão não pode substituir um método de instância existente. No entanto, quando um método de extensão tem o mesmo nome que um método de instância, mas as assinaturas não entram em conflito, ambos os métodos podem ser acessados. Por exemplo, se `ExampleClass` a classe contiver um método chamado `ExampleMethod` que não usa argumentos, os métodos de extensão com o mesmo nome, mas assinaturas diferentes, serão permitidos, conforme mostrado no código a seguir.

[!code-vb[VbVbalrExtensionMethods#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrExtensionMethods/VB/Module3.vb#8)]

A saída desse código é a seguinte:

```console
Extension method
Instance method
```

A situação é mais simples com propriedades: se um método de extensão tiver o mesmo nome que uma propriedade da classe que estende, o método de extensão não será visível e não poderá ser acessado.

## <a name="extension-method-precedence"></a>Precedência do método de extensão

Quando dois métodos de extensão que têm assinaturas idênticas estiverem no escopo e acessíveis, aquele com maior precedência será invocado. A precedência de um método de extensão é baseada no mecanismo usado para colocar o método no escopo. A lista a seguir mostra a hierarquia de precedência, da mais alta para a mais baixa.

1. Métodos de extensão definidos dentro do módulo atual.

2. Métodos de extensão definidos dentro de tipos de dados no namespace atual ou qualquer um de seus pais, com namespaces filho com precedência maior do que namespaces pai.

3. Métodos de extensão definidos dentro de qualquer tipo importado no arquivo atual.

4. Métodos de extensão definidos dentro de qualquer importação de namespace no arquivo atual.

5. Métodos de extensão definidos dentro de qualquer importação de tipo de nível de projeto.

6. Métodos de extensão definidos dentro de qualquer importação de namespace em nível de projeto.

Se a precedência não resolver a ambiguidade, você poderá usar o nome totalmente qualificado para especificar o método que está chamando. Se o `Print` método no exemplo anterior for definido em um módulo chamado `StringExtensions` , o nome totalmente qualificado será `StringExtensions.Print(example)` em vez de `example.Print()` .

## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.CompilerServices>
- <xref:System.Runtime.CompilerServices.ExtensionAttribute>
- [Métodos de Extensão](../../../../csharp/programming-guide/classes-and-structs/extension-methods.md)
- [Instrução Module](../../../language-reference/statements/module-statement.md)
- [Parâmetros e Argumentos de Procedimento](procedure-parameters-and-arguments.md)
- [Parâmetros Opcionais](optional-parameters.md)
- [Matrizes de parâmetros](parameter-arrays.md)
- [Visão geral de atributos](../../concepts/attributes/index.md)
- [Escopo no Visual Basic](../declared-elements/scope.md)
