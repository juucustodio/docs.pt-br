---
description: 'Saiba mais sobre: instrução Dim (Visual Basic)'
title: instrução Dim
ms.date: 05/12/2018
f1_keywords:
- vb.Dim
- Dim
helpviewer_keywords:
- Public keyword [Visual Basic], in Dim statement
- Dim statement [Visual Basic]
- fixed-length strings [Visual Basic], declaring
- variables [Visual Basic], declaring
- WithEvents keyword [Visual Basic], Dim statement
- dynamic arrays [Visual Basic], Dim statement
- variables [Visual Basic], initializing
- '{} braces'
- fields [Visual Basic], as member variables
- declarations [Visual Basic], dynamic arrays
- member variables [Visual Basic]
- default values [Visual Basic]
- data types [Visual Basic], assigning
- braces {}
- As keyword [Visual Basic], in Dim statement
- arrays [Visual Basic], declaring
- New keyword [Visual Basic], Dim statement
- To keyword [Visual Basic], in Dim statement
- storage [Visual Basic], allocating
- local variables [Visual Basic]
- declaration statements [Visual Basic]
- Dim statement [Visual Basic], syntax
- variables [Visual Basic], member and local
ms.assetid: fae3eca1-f0b2-4400-994b-7aa58a848448
ms.openlocfilehash: b950ae95af01be4e064ac9177300f144e0cc08b7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795190"
---
# <a name="dim-statement-visual-basic"></a>Instrução Dim (Visual Basic)

Declara e aloca espaço de armazenamento para uma ou mais variáveis.

## <a name="syntax"></a>Syntax

```vb
[ <attributelist> ] [ accessmodifier ] [[ Shared ] [ Shadows ] | [ Static ]] [ ReadOnly ]
Dim [ WithEvents ] variablelist
```

## <a name="parts"></a>Partes

- `attributelist`

  Opcional. Consulte a [lista de atributos](attribute-list.md).

- `accessmodifier`

  Opcional. Pode ser um dos seguintes:

  - [Público](../modifiers/public.md)

  - [Protected](../modifiers/protected.md)

  - [Friend](../modifiers/friend.md)

  - [Privado](../modifiers/private.md)

  - [Amigo Protegido](../modifiers/protected-friend.md)

  - [Particular protegido](../modifiers/private-protected.md)

  Consulte [níveis de acesso em Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md).

- `Shared`

  Opcional. Consulte [compartilhado](../modifiers/shared.md).

- `Shadows`

  Opcional. Consulte [Shadows](../modifiers/shadows.md).

- `Static`

  Opcional. Consulte [estático](../modifiers/static.md).

- `ReadOnly`

  Opcional. Consulte [ReadOnly](../modifiers/readonly.md).

- `WithEvents`

  Opcional. Especifica que essas são variáveis de objeto que se referem a instâncias de uma classe que pode gerar eventos. Consulte [WithEvents](../modifiers/withevents.md).

- `variablelist`

  Obrigatório. Lista de variáveis que estão sendo declaradas nesta instrução.

  `variable [ , variable ... ]`

  Cada `variable` uma tem a seguinte sintaxe e partes:

  `variablename [ ( [ boundslist ] ) ] [ As [ New ] datatype [ With`{`[ .propertyname = propinitializer [ , ... ] ] } ] ] [ = initializer ]`

  |Parte|Descrição|
  |---|---|
  |`variablename`|Obrigatórios. Nome da variável. Consulte [nomes de elementos declarados](../../programming-guide/language-features/declared-elements/declared-element-names.md).|
  |`boundslist`|Opcional. Lista de limites de cada dimensão de uma variável de matriz.|
  |`New`|Opcional. Cria uma nova instância da classe quando a `Dim` instrução é executada.|
  |`datatype`|Opcional. Tipo de dados da variável.|
  |`With`|Opcional. Apresenta a lista de inicializadores de objeto.|
  |`propertyname`|Opcional. O nome de uma propriedade na classe da qual você está fazendo uma instância.|
  |`propinitializer`|Necessário após `propertyname` =. A expressão que é avaliada e atribuída ao nome da propriedade.|
  |`initializer`|Opcional se `New` não for especificado. Expressão que é avaliada e atribuída à variável quando ela é criada.|

## <a name="remarks"></a>Comentários

O compilador Visual Basic usa a `Dim` instrução para determinar o tipo de dados da variável e outras informações, como qual código pode acessar a variável. O exemplo a seguir declara uma variável para conter um `Integer` valor.

```vb
Dim numberOfStudents As Integer
```

Você pode especificar qualquer tipo de dados ou o nome de uma enumeração, estrutura, classe ou interface.

```vb
Dim finished As Boolean
Dim monitorBox As System.Windows.Forms.Form
```

Para um tipo de referência, você usa a `New` palavra-chave para criar uma nova instância da classe ou estrutura especificada pelo tipo de dados. Se você usar `New` , você não usará uma expressão de inicializador. Em vez disso, você fornece argumentos, se eles forem necessários, para o construtor da classe da qual você está criando a variável.

```vb
Dim bottomLabel As New System.Windows.Forms.Label
```

Você pode declarar uma variável em um procedimento, em um bloco, em uma classe, em uma estrutura ou em um módulo. Você não pode declarar uma variável em um arquivo de origem, namespace ou interface. Para obter mais informações, consulte [Contextos de declaração e níveis de acesso padrão](declaration-contexts-and-default-access-levels.md).

Uma variável que é declarada no nível do módulo, fora de qualquer procedimento, é uma variável ou *campo* de *membro* . As variáveis de membro estão no escopo em toda a classe, estrutura ou módulo. Uma variável que é declarada no nível de procedimento é uma *variável local*. As variáveis locais estão no escopo somente dentro de seu procedimento ou bloco.

Os seguintes modificadores de acesso são usados para declarar variáveis fora de um procedimento:,,, `Public` `Protected` `Friend` `Protected Friend` e `Private` . Para obter mais informações, consulte [níveis de acesso em Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md).

A `Dim` palavra-chave é opcional e geralmente omitida se você especificar qualquer um dos seguintes modificadores:,,,,,,,, `Public` `Protected` `Friend` `Protected Friend` `Private` `Shared` `Shadows` `Static` `ReadOnly` ou `WithEvents` .

```vb
Public maximumAllowed As Double
Protected Friend currentUserName As String
Private salary As Decimal
Static runningTotal As Integer
```

Se `Option Explicit` for on (o padrão), o compilador exigirá uma declaração para cada variável que você usar. Para obter mais informações, consulte [instrução Option Explicit](option-explicit-statement.md).

## <a name="specifying-an-initial-value"></a>Especificando um valor inicial

Você pode atribuir um valor a uma variável quando ele é criado. Para um tipo de valor, você usa um *inicializador* para fornecer uma expressão a ser atribuída à variável. A expressão deve ser avaliada como uma constante que pode ser calculada no momento da compilação.

```vb
Dim quantity As Integer = 10
Dim message As String = "Just started"
```

Se um inicializador for especificado e um tipo de dados não for especificado em uma `As` cláusula, a *inferência de tipos* será usada para inferir o tipo de dados do inicializador. No exemplo a seguir, `num1` e `num2` são fortemente tipadas como inteiros. Na segunda declaração, a inferência de tipos infere o tipo do valor 3.

```vb
' Use explicit typing.
Dim num1 As Integer = 3

' Use local type inference.
Dim num2 = 3
```

A inferência de tipos aplica-se ao nível de procedimento. Ele não se aplica fora de um procedimento em uma classe, estrutura, módulo ou interface. Para obter mais informações sobre a inferência de tipos, consulte [instrução Option Infer](option-infer-statement.md) e [inferência de tipo local](../../programming-guide/language-features/variables/local-type-inference.md).

Para obter informações sobre o que acontece quando um tipo de dados ou inicializador não é especificado, consulte [tipos de dados e valores padrão](dim-statement.md#default) posteriormente neste tópico.

Você pode usar um *inicializador de objeto* para declarar instâncias de tipos nomeados e anônimos. O código a seguir cria uma instância de uma `Student` classe e usa um inicializador de objeto para inicializar propriedades.

```vb
Dim student1 As New Student With {.First = "Michael",
                                  .Last = "Tucker"}
```

Para obter mais informações sobre inicializadores de objeto, consulte [como: declarar um objeto usando um inicializador de objeto](../../programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md), [inicializadores de objeto: tipos nomeados e anônimos](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)e [tipos anônimos](../../programming-guide/language-features/objects-and-classes/anonymous-types.md).

## <a name="declaring-multiple-variables"></a>Declarando várias variáveis

Você pode declarar várias variáveis em uma instrução de declaração, especificando o nome da variável para cada uma delas e seguindo cada nome de matriz com parênteses. Várias variáveis são separadas por vírgulas.

```vb
Dim lastTime, nextTime, allTimes() As Date
```

Se você declarar mais de uma variável com uma `As` cláusula, não poderá fornecer um inicializador para esse grupo de variáveis.

Você pode especificar tipos de dados diferentes para variáveis diferentes usando uma `As` cláusula separada para cada variável que declarar. Cada variável usa o tipo de dados especificado na primeira `As` cláusula encontrada após sua `variablename` parte.

```vb
Dim a, b, c As Single, x, y As Double, i As Integer
' a, b, and c are all Single; x and y are both Double
```

## <a name="arrays"></a>Matrizes

Você pode declarar uma variável para conter uma *matriz*, que pode conter vários valores. Para especificar que uma variável contém uma matriz, siga-a `variablename` imediatamente com parênteses. Para obter mais informações sobre matrizes, confira [Matrizes](../../programming-guide/language-features/arrays/index.md).

Você pode especificar o limite inferior e superior de cada dimensão de uma matriz. Para fazer isso, inclua um `boundslist` dentro dos parênteses. Para cada dimensão, `boundslist` especifica o limite superior e, opcionalmente, o limite inferior. O limite inferior é sempre zero, independentemente de você especificá-lo ou não. Cada índice pode variar de zero por seu valor de limite superior.

As duas instruções a seguir são equivalentes. Cada instrução declara uma matriz de 21 `Integer` elementos. Quando você acessa a matriz, o índice pode variar de 0 a 20.

```vb
Dim totals(20) As Integer
Dim totals(0 To 20) As Integer
```

A instrução a seguir declara uma matriz bidimensional do tipo `Double` . A matriz tem 4 linhas (3 + 1) de 6 colunas (5 + 1) cada. Observe que um limite superior representa o maior valor possível para o índice, não o comprimento da dimensão. O comprimento da dimensão é o limite superior mais um.

```vb
Dim matrix2(3, 5) As Double
```

Uma matriz pode ter de 1 a 32 dimensões.

Você pode deixar todos os limites em branco em uma declaração de matriz. Se você fizer isso, a matriz terá o número de dimensões que você especificar, mas ela não será inicializada. Ele tem um valor de `Nothing` até que você inicialize pelo menos alguns de seus elementos. A `Dim` instrução deve especificar limites para todas as dimensões ou para nenhuma dimensão.

```vb
' Declare an array with blank array bounds.
Dim messages() As String
' Initialize the array.
ReDim messages(4)
```

Se a matriz tiver mais de uma dimensão, você deverá incluir vírgulas entre parênteses para indicar o número de dimensões.

```vb
Dim oneDimension(), twoDimensions(,), threeDimensions(,,) As Byte
```

Você pode declarar uma *matriz de comprimento zero* declarando uma das dimensões da matriz como-1. Uma variável que mantém uma matriz de comprimento zero não tem o valor `Nothing` . Matrizes de comprimento zero são exigidas por determinadas funções de Common Language Runtime. Se você tentar acessar essa matriz, ocorrerá uma exceção de tempo de execução. Saiba mais em [Matrizes](../../programming-guide/language-features/arrays/index.md).

Você pode inicializar os valores de uma matriz usando um literal de matriz. Para fazer isso, coloque os valores de inicialização com chaves ( `{}` ).

```vb
Dim longArray() As Long = {0, 1, 2, 3}
```

Para matrizes multidimensionais, a inicialização para cada dimensão separada é colocada entre chaves na dimensão externa. Os elementos são especificados em ordem de linha principal.

```vb
Dim twoDimensions(,) As Integer = {{0, 1, 2}, {10, 11, 12}}
```

Para obter mais informações sobre literais de matriz, consulte [matrizes](../../programming-guide/language-features/arrays/index.md).

## <a name="default-data-types-and-values"></a><a name="default"></a> Valores e tipos de dados padrão

A tabela a seguir descreve os resultados de várias combinações de especificar o tipo de dados e o inicializador em uma instrução `Dim`.

|Tipo de dados especificado?|Inicializador especificado?|Exemplo|Result|
|---|---|---|---|
|Não|Não|`Dim qty`|Se [Option Strict](option-strict-statement.md) for OFF (o padrão), a variável será definida como `Nothing` .<br /><br /> Se `Option Strict` estiver ativado, ocorre um erro de tempo de compilação.|
|Não|Sim|`Dim qty = 5`|Se [Option Infer](option-infer-statement.md) estiver on (o padrão), a variável usará o tipo de dados do inicializador. Consulte [inferência de tipo local](../../programming-guide/language-features/variables/local-type-inference.md).<br /><br /> Se `Option Infer` estiver desativado e `Option Strict` estiver desativado, a variável usa o tipo de dados do `Object`.<br /><br /> Se `Option Infer` estiver desativado e `Option Strict` estiver ativado, ocorre um erro de tempo de compilação.|
|Sim|Não|`Dim qty As Integer`|A variável é inicializada para o valor padrão para o tipo de dados. Consulte a tabela mais adiante nesta seção.|
|Sim|Sim|`Dim qty  As Integer = 5`|Se o tipo de dados do inicializador não for conversível para o tipo de dados especificado, ocorrerá um erro de tempo de compilação.|

Se você especificar um tipo de dados, mas não especificar um inicializador, Visual Basic inicializa a variável para o valor padrão para seu tipo de dados. A tabela a seguir mostra os valores de inicialização padrão.

|Tipo de dados|Valor padrão|
|---|---|
|Todos os tipos numéricos (incluindo `Byte` e `SByte` )|0|
|`Char`|Binário 0|
|Todos os tipos de referência (incluindo `Object` , `String` e todas as matrizes)|`Nothing`|
|`Boolean`|`False`|
|`Date`|12:00 A.M. de 1º de Janeiro do ano 1 (01/01/0001 12:00:00 AM)|

Cada elemento de uma estrutura é inicializado como se fosse uma variável separada. Se você declarar o comprimento de uma matriz, mas não inicializar seus elementos, cada elemento será inicializado como se fosse uma variável separada.

## <a name="static-local-variable-lifetime"></a>Tempo de vida da variável local estática

Uma `Static` variável local tem um tempo de vida maior do que a do procedimento no qual ela é declarada. Os limites do tempo de vida da variável dependem de onde o procedimento é declarado e se ele é `Shared` .

|Declaração de procedimento|Variável inicializada|Variável para existente|
|---|---|---|
|Em um módulo|Na primeira vez que o procedimento é chamado|Quando o programa parar a execução|
|Em uma classe ou estrutura, o procedimento é `Shared`|Na primeira vez que o procedimento é chamado em uma instância específica ou na própria classe ou estrutura|Quando o programa parar a execução|
|Em uma classe ou estrutura, o procedimento não é `Shared`|Na primeira vez que o procedimento é chamado em uma instância específica|Quando a instância é liberada para coleta de lixo (GC)|

## <a name="attributes-and-modifiers"></a>Atributos e modificadores

Você pode aplicar atributos somente a variáveis de membro, não a variáveis locais. Um atributo contribui com informações para os metadados do assembly, o que não é significativo para armazenamento temporário, como variáveis locais.

No nível de módulo, você não pode usar o `Static` modificador para declarar variáveis de membro. No nível de procedimento, você não pode usar `Shared` ,, `Shadows` `ReadOnly` , `WithEvents` ou qualquer modificador de acesso para declarar variáveis locais.

Você pode especificar qual código pode acessar uma variável fornecendo um `accessmodifier` . As variáveis de membro de módulo e classe (fora de qualquer procedimento) são padrão para acesso privado e as variáveis de membro de estrutura padrão para acesso público. Você pode ajustar seus níveis de acesso com os modificadores de acesso. Você não pode usar modificadores de acesso em variáveis locais (dentro de um procedimento).

Você pode especificar `WithEvents` somente as variáveis de membro, não as variáveis locais dentro de um procedimento. Se você especificar `WithEvents` , o tipo de dados da variável deverá ser um tipo de classe específico, não `Object` . Não é possível declarar uma matriz com `WithEvents` . Para obter mais informações sobre eventos, consulte [eventos](../../programming-guide/language-features/events/index.md).

> [!NOTE]
> O código fora de uma classe, estrutura ou módulo deve qualificar o nome de uma variável de membro com o nome dessa classe, estrutura ou módulo. O código fora de um procedimento ou bloco não pode se referir a nenhuma variável local dentro desse procedimento ou bloco.

## <a name="releasing-managed-resources"></a>Liberando recursos gerenciados

O coletor de lixo .NET Framework descarta recursos gerenciados sem qualquer codificação adicional de sua parte. No entanto, você pode forçar a eliminação de um recurso gerenciado em vez de aguardar o coletor de lixo.

Se uma classe se mantiver em um recurso especialmente valioso e escasso (como uma conexão de banco de dados ou identificador de arquivo), talvez você não queira esperar até que a próxima coleta de lixo limpe uma instância de classe que não esteja mais em uso. Uma classe pode implementar a <xref:System.IDisposable> interface para fornecer uma maneira de liberar recursos antes de uma coleta de lixo. Uma classe que implementa essa interface expõe um `Dispose` método que pode ser chamado para forçar a liberação imediata de recursos valiosos.

A `Using` instrução automatiza o processo de aquisição de um recurso, a execução de um conjunto de instruções e a descarta do recurso. No entanto, o recurso deve implementar a <xref:System.IDisposable> interface. Para obter mais informações, consulte [usando a instrução](using-statement.md).

## <a name="example"></a>Exemplo

O exemplo a seguir declara variáveis usando a `Dim` instrução com várias opções.

[!code-vb[VbVbalrStatements#141](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class11.vb#141)]

## <a name="example"></a>Exemplo

O exemplo a seguir lista os números primos entre 1 e 30. O escopo de variáveis locais é descrito em comentários de código.

[!code-vb[VbVbalrStatements#142](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class11.vb#142)]

## <a name="example"></a>Exemplo

No exemplo a seguir, a `speedValue` variável é declarada no nível de classe. A `Private` palavra-chave é usada para declarar a variável. A variável pode ser acessada por qualquer procedimento na `Car` classe.

[!code-vb[VbVbalrStatements#144](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class11.vb#144)]

[!code-vb[VbVbalrStatements#145](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/class11.vb#145)]

## <a name="see-also"></a>Consulte também

- [Instrução Const](const-statement.md)
- [Instrução ReDim](redim-statement.md)
- [Instrução Option Explicit](option-explicit-statement.md)
- [Instrução Option Infer](option-infer-statement.md)
- [Instrução Option Strict](option-strict-statement.md)
- [Página de Compilação, Designer de Projeto (Visual Basic)](/visualstudio/ide/reference/compile-page-project-designer-visual-basic)
- [Declaração de Variável](../../programming-guide/language-features/variables/variable-declaration.md)
- [matrizes](../../programming-guide/language-features/arrays/index.md)
- [Inicializadores de objeto: tipos nomeados e anônimos](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [Tipos anônimos](../../programming-guide/language-features/objects-and-classes/anonymous-types.md)
- [Inicializadores de objeto: tipos nomeados e anônimos](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [Como declarar um objeto usando um inicializador de objeto](../../programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
- [Inferência de Tipo de Variável Local](../../programming-guide/language-features/variables/local-type-inference.md)
