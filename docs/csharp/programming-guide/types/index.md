---
title: Tipos – Guia de Programação em C#
description: Saiba mais sobre os tipos em programação em C#, como tipos internos, tipos personalizados, tipos de valor e tipos de referência.
ms.date: 11/19/2020
helpviewer_keywords:
- value types [C#]
- reference types [C#]
- types [C#]
- C# language, data types
- common type system [C#]
- data types [C#]
- C# language, types
- strong typing [C#]
ms.assetid: f782d7cc-035e-4500-b1b1-36a9881130ad
ms.openlocfilehash: 6a1a5b230e427a4991162a702245f1a87352784d
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98190241"
---
# <a name="types-c-programming-guide"></a>Tipos (Guia de Programação em C#)

## <a name="types-variables-and-values"></a>Tipos, variáveis e valores

O C# é uma linguagem fortemente tipada. Todas as variáveis e constantes têm um tipo, assim como cada expressão que é avaliada como um valor. Cada declaração de método especifica um nome, número de parâmetros e tipo e espécie (valor, referência ou saída) para cada parâmetro de entrada e para o valor de retorno. A biblioteca de classes .NET define um conjunto de tipos numéricos internos e tipos mais complexos que representam uma ampla variedade de constructos lógicos, como o sistema de arquivos, conexões de rede, coleções e matrizes de objetos e datas. Um programa C# típico usa tipos da biblioteca de classes e dos tipos definidos pelo usuário que modelam os conceitos específicos para o domínio do problema do programa.

As informações armazenadas em um tipo podem incluir os seguintes itens:

- O espaço de armazenamento que uma variável do tipo requer.
- Os valores mínimo e máximo que ele pode representar.
- Os membros (métodos, campos, eventos e etc.) que ele contém.
- O tipo base do qual ele herda.
- As interfaces que ela implementa.
- O local no qual a memória para as variáveis será alocada em tempo de execução.
- Os tipos de operações que são permitidos.

O compilador usa informações de tipo para garantir que todas as operações executadas em seu código sejam de *tipo seguro*. Por exemplo, se você declarar uma variável do tipo [int](../../language-reference/builtin-types/integral-numeric-types.md), o compilador permitirá que você use a variável nas operações de adição e subtração. Se você tentar executar as mesmas operações em uma variável do tipo [bool](../../language-reference/builtin-types/bool.md), o compilador gerará um erro, como mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="TypeSafeExample":::

> [!NOTE]
> Desenvolvedores de C e C++, observem que, em C#, [bool](../../language-reference/builtin-types/bool.md) não é conversível em [int](../../language-reference/builtin-types/integral-numeric-types.md).

O compilador insere as informações de tipo no arquivo executável como metadados. O CLR (Common Language Runtime) usa esses metadados em tempo de execução para assegurar mais segurança de tipos ao alocar e recuperar a memória.

### <a name="specifying-types-in-variable-declarations"></a>Especificando tipos em declarações de variável

Quando declara uma variável ou constante em um programa, você deve especificar o tipo da variável ou usar a palavra-chave [var](../../language-reference/keywords/var.md) para permitir que o compilador infira o tipo. O exemplo a seguir mostra algumas declarações de variáveis que usam tipos numéricos internos e tipos complexos definidos pelo usuário:

:::code language="csharp" source="snippets/index/Program.cs" id="Declarations":::

Os tipos de parâmetros de método e valores de retorno são especificados na declaração do método. A assinatura a seguir mostra um método que requer um [int](../../language-reference/builtin-types/integral-numeric-types.md) como um argumento de entrada e retorna uma cadeia de caracteres:

:::code language="csharp" source="snippets/index/Program.cs" id="GetName":::

Depois de declarar uma variável, você não pode redeclará-la com um novo tipo e não pode atribuir um valor não compatível com seu tipo declarado. Por exemplo, você não pode declarar um [int](../../language-reference/builtin-types/integral-numeric-types.md) e, em seguida, atribuir a ele um valor booliano de `true` . No entanto, os valores podem ser convertidos em outros tipos, por exemplo, quando são atribuídos a novas variáveis ou passados como argumentos de método. Uma *conversão de tipo* que não causa a perda de dados é executada automaticamente pelo compilador. Uma conversão que pode causar perda de dados requer um *cast* no código-fonte.

Para obter mais informações, consulte [Conversões Cast e Conversões de Tipo](./casting-and-type-conversions.md).

## <a name="built-in-types"></a>Tipos internos

O C# fornece um conjunto padrão de tipos internos para representar inteiros, valores de ponto flutuante, expressões booleanas, caracteres de texto, valores decimais e outros tipos de dados. Também há tipos `string` e `object` internos. Esses tipos estão disponíveis para uso em qualquer programa em C#. Para obter a lista completa dos tipos internos, consulte [tipos internos](../../language-reference/builtin-types/built-in-types.md).

## <a name="custom-types"></a>Tipos personalizados

Você usa os constructos [struct](../../language-reference/builtin-types/struct.md), [classe](../../language-reference/keywords/class.md), [interface](../../language-reference/keywords/interface.md) e [enum](../../language-reference/builtin-types/enum.md) para criar seus próprios tipos personalizados. A biblioteca de classes do .NET em si é uma coleção de tipos personalizados fornecida pela Microsoft, que você pode usar em seus próprios aplicativos. Por padrão, os tipos usados com mais frequência na biblioteca de classes estão disponíveis em qualquer programa em C#. Outras se tornam disponíveis somente quando você adiciona explicitamente uma referência de projeto ao assembly no qual elas são definidas. Depois que o compilador tiver uma referência ao assembly, você pode declarar variáveis (e constantes) dos tipos declarados nesse assembly no código-fonte. Para saber mais, confira [Biblioteca de classes do .NET](../../../standard/class-library-overview.md).

## <a name="the-common-type-system"></a>O Common Type System

É importante entender dois pontos fundamentais sobre o sistema de tipos no .NET:

- Ele dá suporte ao conceito de herança. Os tipos podem derivar de outros tipos, chamados *tipos base*. O tipo derivado herda (com algumas restrições) os métodos, as propriedades e outros membros do tipo base. O tipo base, por sua vez, pode derivar de algum outro tipo, nesse caso, o tipo derivado herda os membros de ambos os tipos base na sua hierarquia de herança. Todos os tipos, incluindo tipos numéricos internos, como <xref:System.Int32?displayProperty=nameWithType> (palavra-chave de C#: [int](../../language-reference/builtin-types/integral-numeric-types.md)), derivam, em última análise, de um único tipo base, que é o <xref:System.Object?displayProperty=nameWithType> (palavra-chave de C#: [object](../../language-reference/builtin-types/reference-types.md)). Essa hierarquia unificada de tipos é chamada de CTS [(Common Type System)](../../../standard/base-types/common-type-system.md). Para obter mais informações sobre herança em C#, consulte [Herança](../classes-and-structs/inheritance.md).
- Cada tipo no CTS é definido como um *tipo de valor* ou um *tipo de referência*. Esses tipos incluem todos os tipos personalizados na biblioteca de classes do .NET e também seus próprios tipos definidos pelo usuário. Os tipos que você define usando a palavra-chave [struct](../../language-reference/builtin-types/struct.md) são tipos de valor. Todos os tipos numéricos internos são `structs`. Os tipos que você define usando a palavra-chave [class](../../language-reference/keywords/class.md) são tipos de referência. Os tipos de referência e os tipos de valor têm diferentes regras de tempo de compilação e comportamento de tempo de execução diferente.

A ilustração a seguir mostra a relação entre tipos de referência e tipos de valor no CTS.

![Captura de tela que mostra de tipos de valor CTS e tipos de referência.](./media/index/value-reference-types-common-type-system.png)

> [!NOTE]
> Você pode ver que os tipos mais usados normalmente são todos organizados no namespace <xref:System>. No entanto, o namespace no qual um tipo está contido não tem relação com a possibilidade de ele ser um tipo de valor ou um tipo de referência.

### <a name="value-types"></a>Tipos de valor

Os tipos de valor derivam de <xref:System.ValueType?displayProperty=nameWithType>, que deriva de <xref:System.Object?displayProperty=nameWithType>. Os tipos que derivam de <xref:System.ValueType?displayProperty=nameWithType> apresentam um comportamento especial no CLR. As variáveis de tipo de valor contêm diretamente seus valores, o que significa que a memória é alocada embutida em qualquer contexto em que a variável é declarada. Não há nenhuma alocação de heap separada ou sobrecarga de coleta de lixo para variáveis de tipo de valor.

Há duas categorias de tipos de valor: [struct](../../language-reference/builtin-types/struct.md) e [enum](../../language-reference/builtin-types/enum.md).

Os tipos numéricos internos são structs e têm campos e métodos que você pode acessar:

:::code language="csharp" source="snippets/index/Program.cs" id="ConstantByte":::

Mas você declara e atribui valores a eles como se eles fossem tipos simples não agregados:

:::code language="csharp" source="snippets/index/Program.cs" id="NonAggregateTypes":::

Os tipos de valor são *lacrados*, o que significa que você não pode derivar um tipo de qualquer tipo de valor, por exemplo <xref:System.Int32?displayProperty=nameWithType> . Você não pode definir uma struct para herdar de qualquer classe definida pelo usuário ou struct porque uma struct só pode herdar de <xref:System.ValueType?displayProperty=nameWithType> . No entanto, um struct pode implementar uma ou mais interfaces. Você pode converter um tipo struct em qualquer tipo de interface que ele implementa; Essa conversão faz com que uma operação *Boxing* envolva a struct dentro de um objeto de tipo de referência no heap gerenciado. As operações de conversão boxing ocorrem quando você passa um tipo de valor para um método que usa um <xref:System.Object?displayProperty=nameWithType> ou qualquer tipo de interface como parâmetro de entrada. Para obter mais informações, consulte [Conversões boxing e unboxing](./boxing-and-unboxing.md).

Você usa a palavra-chave [struct](../../language-reference/builtin-types/struct.md) para criar seus próprios tipos de valor personalizados. Normalmente, um struct é usado como um contêiner para um pequeno conjunto de variáveis relacionadas, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="Coords":::

Para obter mais informações sobre structs, consulte [tipos de estrutura](../../language-reference/builtin-types/struct.md). Para obter mais informações sobre tipos de valor, consulte [tipos de valor](../../language-reference/builtin-types/value-types.md).

A outra categoria de tipos de valor é [enum](../../language-reference/builtin-types/enum.md). Uma enum define um conjunto de constantes integrais nomeadas. Por exemplo, a enumeração <xref:System.IO.FileMode?displayProperty=nameWithType> na biblioteca de classes do .NET contém um conjunto de números inteiros constantes nomeados que especificam como um arquivo deve ser aberto. Ele é definido como mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="EnumFileMode":::

A constante `System.IO.FileMode.Create` tem um valor de 2. No entanto, o nome é muito mais significativo para as pessoas que lêem o código-fonte e, por esse motivo, é melhor usar enumerações em vez de números literais constantes. Para obter mais informações, consulte <xref:System.IO.FileMode?displayProperty=nameWithType>.

Todas as enumerações herdam de <xref:System.Enum?displayProperty=nameWithType>, que herda de <xref:System.ValueType?displayProperty=nameWithType>. Todas as regras que se aplicam a structs também se aplicam a enums. Para obter mais informações sobre enums, consulte [tipos de enumeração](../../language-reference/builtin-types/enum.md).

### <a name="reference-types"></a>Tipos de referência

Um tipo que é definido como uma [classe](../../language-reference/keywords/class.md), [delegado](../../language-reference/builtin-types/reference-types.md), matriz ou [interface](../../language-reference/keywords/interface.md) é um *tipo de referência*. No tempo de execução, quando você declara uma variável de um tipo de referência, a variável contém o valor [null](../../language-reference/keywords/null.md) até você criar explicitamente um objeto usando o operador [new](../../language-reference/operators/new-operator.md) ou atribuir a ele um objeto que foi criado em outro lugar com o operador `new`, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="DeclarationAndAssignment":::

Uma interface deve ser inicializada com um objeto da classe que a implementa. Se `MyClass` implementa `IMyInterface`, você cria uma instância de `IMyInterface`, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="InterfaceDeclaration":::

Quando o objeto é criado, a memória é alocada no heap gerenciado e a variável contém apenas uma referência para o local do objeto. Os tipos no heap gerenciado exigem sobrecarga quando são alocados e quando são recuperados pela funcionalidade de gerenciamento automático de memória do CLR, que é conhecida como *coleta de lixo*. No entanto, a coleta de lixo também é altamente otimizada e, na maioria dos cenários, ela não cria um problema de desempenho. Para obter mais informações sobre a coleta de lixo, consulte [Gerenciamento automático de memória](../../../standard/automatic-memory-management.md).

Todas as matrizes são tipos de referência, mesmo se seus elementos forem tipos de valor. As matrizes derivam implicitamente da classe <xref:System.Array?displayProperty=nameWithType>, mas você declara e usa as matrizes com a sintaxe simplificada fornecida pelo C#, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="ArrayDeclaration":::

Os tipos de referência dão suporte completo à herança. Quando você cria uma classe, pode herdar de qualquer outra interface ou classe que não esteja definida como [sealed](../../language-reference/keywords/sealed.md), e outras classes podem herdar de sua classe e substituir seus métodos virtuais. Para obter mais informações sobre como criar suas próprias classes, consulte [Classes e structs](../classes-and-structs/index.md). Para obter mais informações sobre herança e métodos virtuais, consulte [Herança](../classes-and-structs/inheritance.md).

## <a name="types-of-literal-values"></a>Tipos de valores literais

No C#, valores literais recebem um tipo do compilador. Você pode especificar como um literal numérico deve ser digitado anexando uma letra ao final do número. Por exemplo, para especificar que o valor 4,56 deve ser tratado como um float, acrescente um "f" ou "F" após o número: `4.56f`. Se nenhuma letra for anexada, o compilador inferirá um tipo para o literal. Para obter mais informações sobre quais tipos podem ser especificados com sufixos de letra, consulte [tipos numéricos inteiros](../../language-reference/builtin-types/integral-numeric-types.md) e [tipos numéricos de ponto flutuante](../../language-reference/builtin-types/floating-point-numeric-types.md).

Como os literais são digitados e todos os tipos derivam <xref:System.Object?displayProperty=nameWithType> , você pode escrever e compilar um código como o código a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="ConvertTypes":::

## <a name="generic-types"></a>Tipos genéricos

Um tipo pode ser declarado com um ou mais *parâmetros de tipo* que servem como um espaço reservado para o tipo real (o *tipo concreto*) que o código cliente fornecerá ao criar uma instância do tipo. Esses tipos são chamados de *tipos genéricos*. Por exemplo, o tipo .NET <xref:System.Collections.Generic.List%601?displayProperty=nameWithType> tem um parâmetro de tipo que, por convenção, recebe o nome *T*. Ao criar uma instância do tipo, você especifica o tipo dos objetos que a lista conterá, por exemplo, Cadeia de caracteres:

:::code language="csharp" source="snippets/index/Program.cs" id="GenericType":::

O uso do parâmetro de tipo possibilita a reutilização da mesma classe para conter qualquer tipo de elemento sem precisar converter cada elemento em [objeto](../../language-reference/builtin-types/reference-types.md). As classes de coleção genéricas são chamadas de coleções com rigidez de *tipos* , pois o compilador sabe o tipo específico dos elementos da coleção e pode gerar um erro no momento da compilação se, por exemplo, você tentar adicionar um inteiro ao `stringList` objeto no exemplo anterior. Para obter mais informações, consulte [Genéricos](../generics/index.md).

## <a name="implicit-types-anonymous-types-and-nullable-value-types"></a>Tipos implícitos, tipos anônimos e tipos de valor anulável

Conforme mencionado anteriormente, você pode digitar implicitamente uma variável local (mas não os membros de classe) usando a palavra-chave [var](../../language-reference/keywords/var.md). A variável ainda recebe um tipo em tempo de compilação, mas o tipo é fornecido pelo compilador. Para obter mais informações, consulte [Variáveis locais de tipo implícito](../classes-and-structs/implicitly-typed-local-variables.md).

Pode ser inconveniente criar um tipo nomeado para conjuntos simples de valores relacionados que você não pretende armazenar ou passar os limites de método externos. Você pode criar *tipos anônimos* para essa finalidade. Para obter mais informações, consulte [Tipos Anônimos](../classes-and-structs/anonymous-types.md).

Tipos de valor comum não podem ter um valor [nulo](../../language-reference/keywords/null.md). No entanto, você pode criar tipos de valor anuláveis acrescentando um `?` após o tipo. Por exemplo, `int?` é um tipo `int` que também pode ter o valor [nulo](../../language-reference/keywords/null.md). Os tipos de valor anuláveis são instâncias do tipo struct genérico <xref:System.Nullable%601?displayProperty=nameWithType> . Os tipos de valor anulável são especialmente úteis quando você está passando dados de e para bancos de dado nos quais valores numéricos podem ser nulos. Para obter mais informações, consulte [tipos de valor anulável](../../language-reference/builtin-types/nullable-value-types.md).

## <a name="compile-time-type-and-runtime-type"></a>Tipo de hora de compilação e tipo de tempo de execução

Uma variável pode ter tipos diferentes de tempo de compilação e tempo de execução. O *tipo de tempo de compilação* é o tipo declarado ou inferido da variável no código-fonte. O *tipo de tempo de execução* é o tipo da instância referenciada por essa variável. Geralmente, esses dois tipos são os mesmos, como no exemplo a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="CompileTimeType":::

Em outros casos, o tipo de tempo de compilação é diferente, conforme mostrado nos dois exemplos a seguir:

:::code language="csharp" source="snippets/index/Program.cs" id="RuntimeTypes":::

Nos dois exemplos anteriores, o tipo de tempo de execução é um `string` . O tipo de tempo de compilação está `object` na primeira linha e `IEnumerable<char>` no segundo.

Se os dois tipos forem diferentes para uma variável, é importante entender quando o tipo de tempo de compilação e o tipo de tempo de execução se aplicam. O tipo de tempo de compilação determina todas as ações executadas pelo compilador. Essas ações de compilador incluem resolução de chamada de método, resolução de sobrecarga e conversões implícitas e explícitas disponíveis. O tipo de tempo de execução determina todas as ações que são resolvidas em tempo de execução. Essas ações de tempo de execução incluem a expedição de chamadas de método virtual, avaliação `is` e `switch` expressões e outras APIs de teste de tipo. Para entender melhor como seu código interage com tipos, reconheça qual ação se aplica a qual tipo.

## <a name="related-sections"></a>Seções relacionadas

Para obter mais informações, consulte os seguintes artigos:

- [Conversões cast e conversões de tipo](./casting-and-type-conversions.md)
- [Boxing e unboxing](./boxing-and-unboxing.md)
- [Usando o tipo dynamic](./using-type-dynamic.md)
- [Tipos de valor](../../language-reference/builtin-types/value-types.md)
- [Tipos de referência](../../language-reference/keywords/reference-types.md)
- [Classes e structs](../classes-and-structs/index.md)
- [Tipos anônimos](../classes-and-structs/anonymous-types.md)
- [Genéricos](../generics/index.md)

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Confira também

- [Referência do C#](../../language-reference/index.md)
- [Guia de programação C#](../index.md)
- [Conversão de tipos de dados XML](../../../standard/data/xml/conversion-of-xml-data-types.md)
- [Tipos integrais](../../language-reference/builtin-types/integral-numeric-types.md)
