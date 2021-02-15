---
title: Novidades no C# 7.0 – Guia do C#
description: Obtenha uma visão geral dos novos recursos na versão 7.0 da linguagem C#.
ms.date: 10/02/2020
ms.assetid: fd41596d-d0c2-4816-b94d-c4d00a5d0243
ms.openlocfilehash: c238439b0f435e579d932b3b1eb13e9b0061fa5f
ms.sourcegitcommit: 4b79862c5b41fbd86cf38f926f6a49516059f6f2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/18/2020
ms.locfileid: "97678229"
---
# <a name="whats-new-in-c-70-through-c-73"></a>O que há de novo no C# 7,0 até C# 7,3

O c# 7,0 até o C# 7,3 trouxe vários recursos e aprimoramentos incrementais em sua experiência de desenvolvimento com o C#. Este artigo fornece uma visão geral dos novos recursos de linguagem e opções de compilador. As descrições descrevem o comportamento do C# 7,3, que é a versão mais recente com suporte para aplicativos baseados em .NET Framework.

O elemento de configuração de [seleção de versão de idioma](../language-reference/configure-language-version.md) foi adicionado com C# 7,1, que permite que você especifique a versão do idioma do compilador no arquivo do projeto.

O c# 7.0-7.3 adiciona esses recursos e temas à linguagem C#:

- [Tuplas e Descartes](#tuples-and-discards)
  - Você pode criar tipos simples e sem nome que contêm vários campos públicos. Compiladores e ferramentas IDE entendem a semântica desses tipos.
  - Descartes são variáveis temporárias de somente gravação usadas em atribuições quando o valor atribuído não tem importância. Eles são mais úteis ao desconstruir tuplas e tipos definidos pelo usuário, bem como ao chamar métodos com parâmetros `out`.
- [Correspondência de padrões](#pattern-matching)
  - Você pode criar a lógica de ramificação com base em tipos e valores arbitrários dos membros desses tipos.
- [`async``Main`método](#async-main)
  - O ponto de entrada para um aplicativo pode ter o modificador `async`.
- [Funções locais](#local-functions)
  - Você pode aninhar funções dentro de outras funções para limitar seu escopo e visibilidade.
- [Mais membros aptos para expressão](#more-expression-bodied-members)
  - A lista de membros que podem ser criados usando expressões cresceu.
- [`throw` Expressões](#throw-expressions)
  - Gere exceções em constructos de código que anteriormente não eram permitidos devido ao fato de `throw` ser uma instrução.
- [`default` expressões literais](#default-literal-expressions)
  - Use expressões literais padrão em expressões de valor padrão quando o tipo de destino pode ser inferido.
- [Aprimoramentos da sintaxe de literais numéricos](#numeric-literal-syntax-improvements)
  - Novos tokens aprimoram a legibilidade para constantes numéricas.
- [`out` as](#out-variables)
  - Declare valores `out` embutidos como argumentos para o método em que eles são usados.
- [Argumentos nomeados que não estejam à direita](#non-trailing-named-arguments)
  - Os argumentos nomeados podem ser seguidos por argumentos posicionais.
- [`private protected` modificador de acesso](#private-protected-access-modifier)
  - O modificador de acesso `private protected` permite o acesso a classes derivadas no mesmo assembly.
- [Resolução de sobrecarga aprimorada](#improved-overload-candidates)
  - Novas regras para resolver ambiguidade na resolução de sobrecarga.
- [Técnicas para escrever código eficiente seguro](#enabling-more-efficient-safe-code)
  - Uma combinação de aprimoramentos de sintaxe que permitem trabalhar com tipos de valor usando a semântica de referência.

Por fim, o compilador tem novas opções:

- `-refout` e `-refonly` essa [geração de assembly de referência](#reference-assembly-generation)de controle.
- `-publicsign` para habilitar a assinatura de Software de código aberto (OSS) de assemblies.
- `-pathmap` para fornecer um mapeamento para diretórios de origem.

O restante deste artigo fornece uma visão geral de cada recurso. Para cada recurso, você aprenderá o raciocínio por trás dele e a sintaxe. Você pode explorar esses recursos em seu ambiente usando a ferramenta global `dotnet try`:

1. Instale a ferramenta global [dotnet-try](https://github.com/dotnet/try/blob/master/README.md#setup).
1. Clone o repositório [dotnet/try-samples](https://github.com/dotnet/try-samples).
1. Definir o diretório atual do subdiretório *csharp7* para o repositório *try-samples*.
1. Execute `dotnet try`.

## <a name="tuples-and-discards"></a>Tuplas e Descartes

O C# fornece uma sintaxe avançada para classes e structs que são usados para explicar a intenção do design. Mas, às vezes, essa sintaxe avançada requer trabalho adicional com poucas vantagens. Geralmente, você pode escrever métodos que precisam de uma estrutura simples que contém mais de um elemento de dados. Para dar suporte a esses cenários foram adicionadas *tuplas* ao C#. As tuplas são estruturas de dados leves que contêm vários campos para representar os membros de dados. Os campos não são validados e você não pode definir seus próprios métodos. Os tipos de tupla C# dão suporte a `==` e `!=` . Para obter mais informações.

> [!NOTE]
> As tuplas estavam disponíveis antes do C# 7.0, mas elas eram ineficientes e não tinham nenhum suporte de linguagem. Isso significava que os elementos de tupla só podiam ser referenciados como `Item1`, `Item2` e assim por diante. O C# 7.0 introduz o suporte de linguagem para tuplas, que permite nomes semânticos para os campos de uma tupla, usando tipos de tupla novos e mais eficientes.

Você pode criar uma tupla atribuindo um valor a cada membro e, opcionalmente, fornecendo nomes semânticos para cada um dos membros da tupla:

[!code-csharp[NamedTuple](~/samples/snippets/csharp/new-in-7/program.cs#NamedTuple "Named tuple")]

A tupla `namedLetters` contém campos denominados `Alpha` e `Beta`. Esses nomes existem somente no momento da compilação e não são preservados, por exemplo, ao inspecionar a tupla usando reflexão em tempo de execução.

Em uma atribuição de tupla, você também pode especificar os nomes dos campos no lado direito da atribuição:

[!code-csharp[ImplicitNamedTuple](~/samples/snippets/csharp/new-in-7/program.cs#ImplicitNamedTuple "Implicitly named tuple")]

Pode haver ocasiões em que você deseja descompactar os membros de uma tupla que foram retornados de um método.  Você pode fazer isso declarando variáveis separadas para cada um dos valores na tupla. Essa descompactação é chamada *desconstrução* da tupla:

[!code-csharp[CallingWithDeconstructor](~/samples/snippets/csharp/new-in-7/program.cs#CallingWithDeconstructor "Deconstructing a tuple")]

Você também pode fornecer uma desconstrução semelhante para qualquer tipo no .NET. Escreva um método `Deconstruct` como um membro da classe. esse método `Deconstruct` fornece um conjunto de argumentos `out` para cada uma das propriedades que você deseja extrair. Considere essa classe `Point` que fornece um método desconstrutor que extrai as coordenadas `X` e `Y`:

[!code-csharp[PointWithDeconstruction](~/samples/snippets/csharp/new-in-7/point.cs#PointWithDeconstruction "Point with deconstruction method")]

Extraia os campos individuais atribuindo um `Point` a uma tupla:

[!code-csharp[DeconstructPoint](~/samples/snippets/csharp/new-in-7/program.cs#DeconstructPoint "Deconstruct a point")]

Muitas vezes, quando você Inicializa uma tupla, as variáveis usadas para o lado direito da atribuição são as mesmas que os nomes desejados para os elementos de tupla: os nomes dos elementos de tupla podem ser inferidos das variáveis usadas para inicializar a tupla:

```csharp
int count = 5;
string label = "Colors used in the map";
var pair = (count, label); // element names are "count" and "label"
```

Você pode saber mais sobre esse recurso no artigo [tipos de tupla](../language-reference/builtin-types/value-tuples.md) .

Geralmente, ao desconstruir uma tupla ou chamar um método com parâmetros `out`, você é forçado a definir uma variável cujo valor não é importante e você não pretende usar. O C# adiciona suporte para *descartes* para lidar com esse cenário. Um descarte é uma variável de somente gravação cujo nome é `_` (o caractere de sublinhado); você pode atribuir todos os valores que você pretende descartar à variável única. Um descarte é como uma variável não atribuída. Além da instrução de atribuição, o descarte não pode ser usado no código.

Os descartes são compatíveis com os seguintes cenários:

- Ao desconstruir tuplas ou tipos definidos pelo usuário.
- Ao chamar métodos com parâmetros [out](../language-reference/keywords/out-parameter-modifier.md).
- Em uma operação de correspondência de padrões com as instruções [is](../language-reference/keywords/is.md) e [switch](../language-reference/keywords/switch.md).
- Como um identificador autônomo quando você deseja identificar explicitamente o valor de uma atribuição como um descarte.

O exemplo a seguir define um método `QueryCityDataForYears` que retorna uma tupla de 6 que contém dados de dois anos diferentes para uma cidade. A chamada do método no exemplo é relacionada somente com os dois valores de população retornados pelo método e, por isso, trata os valores restantes na tupla como descartes ao desconstruir a tupla.

[!code-csharp[Tuple-discard](~/samples/snippets/csharp/programming-guide/deconstructing-tuples/discard-tuple1.cs)]

Para obter mais informações, consulte [Descartes](../discards.md).

## <a name="pattern-matching"></a>Correspondência de padrões

*Correspondência de padrões* é um conjunto de recursos que permitem novas maneiras de expressar o fluxo de controle em seu código. Você pode testar variáveis para seus tipos, valores ou os valores de suas propriedades. Essas técnicas criam um fluxo de código mais legível.

A correspondência de padrões tem suporte a expressões `is` e `switch`. Cada uma delas permite inspecionar um objeto e suas propriedades para determinar se esse objeto satisfaz o padrão procurado. Você usa a palavra-chave `when` para especificar regras adicionais para o padrão.

A `is` expressão de padrão estende o [ `is` operador](../language-reference/keywords/is.md#pattern-matching-with-is) familiar para consultar um objeto sobre seu tipo e atribuir o resultado em uma instrução. O seguinte código verifica se uma variável é um `int` e, nesse caso, adiciona-a à soma atual:

```csharp
if (input is int count)
    sum += count;
```

O pequeno exemplo anterior demonstra as melhorias na expressão `is`. Você pode realizar o teste nos tipos de valor, bem como nos tipos de referência, e atribuir o resultado com êxito a uma nova variável do tipo correto.

A expressão de correspondência switch tem uma sintaxe conhecida, baseada na instrução `switch` que já faz parte da linguagem C#. A instrução switch atualizada tem vários novos constructos:

- O tipo controlador de uma expressão `switch` não está mais restrito a tipos integrais, tipos `Enum`, `string` ou a um tipo que permite valor nulo correspondente a um desses tipos. Qualquer tipo pode ser usado.
- Teste o tipo da expressão `switch` em cada rótulo `case`. Assim como ocorre com a expressão `is`, você pode atribuir uma nova variável a esse tipo.
- Adicione uma cláusula `when` para testar mais condições de teste nessa variável.
- A ordem dos rótulos `case` agora é importante. O primeiro branch para correspondência é executado; os outros são ignorados.

O seguinte código demonstra esses novos recursos:

```csharp
public static int SumPositiveNumbers(IEnumerable<object> sequence)
{
    int sum = 0;
    foreach (var i in sequence)
    {
        switch (i)
        {
            case 0:
                break;
            case IEnumerable<int> childSequence:
            {
                foreach(var item in childSequence)
                    sum += (item > 0) ? item : 0;
                break;
            }
            case int n when n > 0:
                sum += n;
                break;
            case null:
                throw new NullReferenceException("Null found in sequence");
            default:
                throw new InvalidOperationException("Unrecognized type");
        }
    }
    return sum;
}
```

- `case 0:` é o padrão de constante conhecido.
- `case IEnumerable<int> childSequence:` é um padrão de tipo.
- `case int n when n > 0:` é um padrão de tipo com uma condição `when` adicional.
- `case null:` é o padrão de nulo.
- `default:` é o caso padrão conhecido.

A partir do C# 7.1, a expressão de padrão para o padrão de tipo `is` e `switch` pode ter o tipo de um parâmetro de tipo genérico. Isso pode ser mais útil ao verificar tipos que podem ser do tipo `struct` ou `class` e você deseja evitar conversão boxing.

Saiba mais sobre a correspondência de padrões em [Correspondência de padrões em C#](../pattern-matching.md).

## <a name="async-main"></a>Async main

Um método *async main* permite que você use `await` no método `Main`. Anteriormente, você precisava escrever:

```csharp
static int Main()
{
    return DoAsyncWork().GetAwaiter().GetResult();
}
```

Agora, você pode escrever:

```csharp
static async Task<int> Main()
{
    // This could also be replaced with the body
    // DoAsyncWork, including its await expressions:
    return await DoAsyncWork();
}
```

Se o programa não retorna um código de saída, declare um método `Main` que retorna um <xref:System.Threading.Tasks.Task>:

```csharp
static async Task Main()
{
    await SomeAsyncMethod();
}
```

Leia mais sobre os detalhes no tópico [async main](../programming-guide/main-and-command-args/index.md) no guia de programação.

## <a name="local-functions"></a>Funções locais

Muitos designs para classes incluem métodos que são chamados de apenas um local. Esses métodos privados adicionais mantêm cada método pequeno e focado. As *funções locais* permitem que você declare métodos dentro do contexto de outro método. Funções locais tornam mais fácil para os leitores da classe verem que o método local é chamado apenas do contexto em que é declarado.

Há dois casos de uso muito comuns para funções locais: métodos iteradores públicos e métodos assíncronos públicos. Ambos os tipos de métodos de geram código que relata os erros mais tarde do que os programadores podem esperar. Em métodos iteradores, as exceções são observadas apenas ao chamar o código que enumera a sequência retornada. Em métodos assíncronos, as exceções são observadas apenas quando a `Task` retornada é aguardada. O seguinte exemplo demonstra a validação de parâmetro de separação da implementação do iterador usando uma função local:

[!code-csharp[22_IteratorMethodLocal](~/samples/snippets/csharp/new-in-7/Iterator.cs#IteratorMethodLocal "Iterator method with local function")]

A mesma técnica pode ser empregada com métodos `async` para garantir que as exceções decorrentes da validação de argumento sejam lançadas antes de o trabalho assíncrono começar:

[!code-csharp[TaskExample](~/samples/snippets/csharp/new-in-7/AsyncWork.cs#TaskExample "Task returning method with local function")]

Agora há suporte para esta sintaxe:

```csharp
[field: SomeThingAboutFieldAttribute]
public int SomeProperty { get; set; }
```

O atributo `SomeThingAboutFieldAttribute` é aplicado ao campo de suporte gerado pelo compilador para `SomeProperty`. Para saber mais, confira [atributos](../programming-guide/concepts/attributes/index.md) no guia de programação em C#.

> [!NOTE]
> Alguns dos designs com suporte das funções locais também podem ser realizados usando *expressões lambda*. Para obter mais informações, consulte [funções locais versus expressões lambda](../programming-guide/classes-and-structs/local-functions.md#local-functions-vs-lambda-expressions).

## <a name="more-expression-bodied-members"></a>Mais membros aptos para expressão

O C# 6 introduziu Membros Expression-apto para para funções membro e propriedades somente leitura. O C# 7.0 expande os membros permitidos que podem ser implementados como expressões. No C# 7.0, você pode implementar *construtores*, *finalizadores* e acessadores `get` e `set` em *propriedades* e *indexadores*. O código a seguir mostra exemplos de cada um:

[!code-csharp[ExpressionBodiedMembers](~/samples/snippets/csharp/new-in-7/expressionmembers.cs#ExpressionBodiedEverything "new expression-bodied members")]

> [!NOTE]
> Este exemplo não precisa de um finalizador, mas ele é mostrado para demonstrar a sintaxe. Você não deve implementar um finalizador em sua classe a menos que seja necessário para liberar recursos não gerenciados. Você também deve considerar o uso da classe <xref:System.Runtime.InteropServices.SafeHandle> em vez de gerenciar recursos não gerenciados diretamente.

Esses novos locais para membros aptos para expressão representam uma etapa importante para a linguagem C#: esses recursos foram implementados por membros da comunidade trabalhando no projeto [Roslyn](https://github.com/dotnet/Roslyn) de software livre.

A alteração de um método para um membro de corpo da expressão é uma [alteração compatível com binário](version-update-considerations.md#binary-compatible-changes).

## <a name="throw-expressions"></a>Expressões throw

No C#, `throw` sempre foi uma instrução. Como `throw` é uma instrução, não uma expressão, havia constructos do C# em que não era possível usá-la. Eles incluíam expressões condicionais, expressões de união nulas e algumas expressões lambda. A adição de membros aptos para expressão inclui mais locais em que as expressões `throw` seriam úteis. Para que você possa escrever qualquer um desses construtos, o C# 7.0 apresenta [*expressões throw*](../language-reference/keywords/throw.md#the-throw-expression).

Essa adição facilita a escrita de um código mais baseado em expressão. Você não precisa de instruções adicionais para a verificação de erros.

## <a name="default-literal-expressions"></a>Expressões literais padrão

Expressões literais padrão são uma melhoria das expressões de valor padrão. Essas expressões inicializam uma variável com o valor padrão. Nos casos em que você anteriormente escrevia:

```csharp
Func<string, bool> whereClause = default(Func<string, bool>);
```

Agora você pode omitir o tipo no lado direito da inicialização:

```csharp
Func<string, bool> whereClause = default;
```

Para saber mais, confira a seção [Literais padrão](../language-reference/operators/default.md#default-literal) do artigo do [operador padrão](../language-reference/operators/default.md).

## <a name="numeric-literal-syntax-improvements"></a>Aprimoramentos da sintaxe de literais numéricos

A leitura incorreta das constantes numéricas pode fazer com que seja difícil entender o código ao lê-lo pela primeira vez. Bitmasks ou outros valores simbólicos são propensos a equívocos. O C# 7.0 inclui dois novos recursos para a escrita de números da maneira mais legível possível para o uso pretendido: *literais binários* e *separadores de dígito*.

Para ocasiões em que você estiver criando bitmasks ou sempre que uma representação binária de um número tornar o código mais legível, escreva esse número em binário:

[!code-csharp[ThousandSeparators](~/samples/snippets/csharp/new-in-7/Program.cs#ThousandSeparators "Thousands separators")]

O `0b` no início da constante indica que o número é escrito como um número binário. Os números binários podem chegar longos e, em geral, é mais fácil ver os padrões de bit introduzindo o `_` como um separador de dígito, conforme mostrado na constante binária no exemplo anterior. O separador de dígitos pode aparecer em qualquer lugar na constante. Para números de base 10, é comum usá-lo como separador de milhar. Os literais numéricos hexadecimais e binários podem começar com um `_` :

[!code-csharp[LargeIntegers](~/samples/snippets/csharp/new-in-7/Program.cs#LargeIntegers "Large integer")]

O separador de dígito pode ser usado com os tipos `decimal`, `float` e `double` também:

[!code-csharp[OtherConstants](~/samples/snippets/csharp/new-in-7/Program.cs#OtherConstants "non-integral constants")]

Juntos, você pode declarar constantes numéricas com muito mais facilidade de leitura.

## <a name="out-variables"></a>Variáveis `out`

A sintaxe existente que dá suporte a `out` parâmetros foi aprimorada no C# 7. Agora você pode declarar variáveis `out` na lista de argumentos de uma chamada de método, em vez de escrever uma instrução de declaração separada:

[!code-csharp[OutVariableDeclarations](~/samples/snippets/csharp/new-in-7/program.cs#OutVariableDeclarations "Out variable declarations")]

Talvez você queira especificar o tipo da `out` variável para fins de clareza, conforme mostrado no exemplo anterior. No entanto, a linguagem dá suporte ao uso de variável local de tipo implícito:

[!code-csharp[OutVarVariableDeclarations](~/samples/snippets/csharp/new-in-7/program.cs#OutVarVariableDeclarations "Implicitly typed Out variable")]

- O código é mais fácil de ler.
  - Você declara a variável out onde você a usa, não em uma linha de código anterior.
- Não é necessário atribuir um valor inicial.
  - Ao declarar a variável `out` no local em que ela é usada em uma chamada de método, você não pode usá-la acidentalmente antes de ela ser atribuída.

A sintaxe adicionada no C# 7.0 para permitir declarações de variável `out` foi estendida para incluir inicializadores de campo, inicializadores de propriedade, inicializadores de construtor e cláusulas de consulta. Ela permite código como no seguinte exemplo:

```csharp
public class B
{
   public B(int i, out int j)
   {
      j = i;
   }
}

public class D : B
{
   public D(int i) : base(i, out var j)
   {
      Console.WriteLine($"The value of 'j' is {j}");
   }
}
```

## <a name="non-trailing-named-arguments"></a>Argumentos nomeados que não estejam à direita

Agora as chamadas de método podem usar argumentos nomeados que precedem argumentos posicionais quando esses argumentos nomeados estão nas posições corretas. Para obter mais informações, consulte [argumentos nomeados e opcionais](../programming-guide/classes-and-structs/named-and-optional-arguments.md).

## <a name="private-protected-access-modifier"></a>modificador de acesso *protegido privado*

Um novo modificador de acesso composto: `private protected` indica que um membro pode ser acessado pela classe que o contém ou por classes derivadas que são declaradas no mesmo assembly. Enquanto que `protected internal` permite o acesso por classes derivadas ou classes que estejam no mesmo assembly, o `private protected` limita o acesso a tipos derivados declarados no mesmo assembly.

Para obter mais informações, consulte [modificadores de acesso](../language-reference/keywords/access-modifiers.md) na referência de linguagem.

## <a name="improved-overload-candidates"></a>Candidatos de sobrecarga aprimorados

Em cada versão, as regras de resolução de sobrecarga são atualizadas para resolver situações em que as chamadas de método ambíguas têm uma opção "óbvia". Esta versão adiciona três novas regras para ajudar o compilador a escolher a opção óbvia:

1. Quando um grupo de métodos contém membros de instância e estáticos, o compilador descartará os membros da instância se o método tiver sido chamado sem um receptor ou contexto de instância. O compilador descartará os membros estáticos se o método tiver sido chamado com um receptor de instância. Quando não há receptor, o compilador inclui apenas membros estáticos em um contexto estático, caso contrário, membros estáticos e de instância. Quando o receptor é ambiguamente uma instância ou um tipo, o compilador inclui ambos. Um contexto estático, em que não é possível usar um receptor de instância `this` implícito, inclui o corpo de membros em que nenhum `this` é definido, como membros estáticos, bem como locais onde `this` não pode ser usado, como inicializadores de campo e inicializadores de construtor.
1. Quando um grupo de métodos contém alguns métodos genéricos cujos argumentos de tipo não satisfazem suas restrições, esses membros são removidos do conjunto de candidatos.
1. Para uma conversão de grupo de métodos, os métodos candidatos cujo tipo de retorno não corresponda ao tipo de retorno do delegado são removidos do conjunto.

Você notará essa mudança somente porque encontrará menos erros de compilador para sobrecargas de métodos ambíguos quando tiver certeza de qual método é melhor.

## <a name="enabling-more-efficient-safe-code"></a>Como habilitar código seguro mais eficiente

Você deve ser capaz de escrever um código C# de forma segurança que seja executado tão bem quanto o código não seguro. O código seguro evita classes de erros, como estouros de buffer, ponteiros perdidos e outros erros de acesso à memória. Esses novos recursos expandem as capacidades do código seguro verificável. Tente escrever mais partes do seu código usando construções seguras. Esses recursos tornam isso mais fácil.

Os novos recursos a seguir são compatíveis com o tema de melhor desempenho para código seguro:

- Você pode acessar campos fixos sem fixação.
- Você pode reatribuir variáveis locais `ref`.
- Você pode usar inicializadores em matrizes `stackalloc`.
- Você pode usar instruções `fixed` com qualquer tipo compatível com um padrão.
- Você pode usar restrições genéricas adicionais.
- O modificador `in` em parâmetros, para especificar que um argumento é passado por referência, mas não modificado pelo método chamado. Adicionar o modificador `in` a um argumento é uma [alteração compatível com a origem](version-update-considerations.md#source-compatible-changes).
- O modificador `ref readonly` nos retornos de método, para indicar que um método retorna seu valor por referência, mas não permite gravações nesse objeto. Adicionar o modificador `ref readonly` é uma [alteração compatível com a origem](version-update-considerations.md#source-compatible-changes) se o retorno é atribuído a um valor. Adicionar o modificador `readonly` a uma instrução de retorno `ref` existente é uma [alteração incompatível](version-update-considerations.md#incompatible-changes). Ela requer que os chamadores atualizem a declaração de `ref` variáveis locais para incluir o modificador `readonly`.
- A declaração `readonly struct`, para indicar que uma struct é imutável e deve ser passado como um parâmetro `in` para seus métodos de membro. Adicionar o modificador `readonly` a uma declaração struct existente é uma [alteração compatível com binário](version-update-considerations.md#binary-compatible-changes).
- A declaração `ref struct`, para indicar que um tipo de struct acessa a memória gerenciada diretamente e deve sempre ser alocado por pilha. Adicionar o modificador `ref` a uma declaração `struct` existente é uma [alteração incompatível](version-update-considerations.md#incompatible-changes). Um `ref struct` não pode ser um membro de uma classe ou usado em outros locais em que ele pode ser alocado no heap.

Você pode ler mais sobre todas essas alterações em [Escrever código eficiente seguro](../write-safe-efficient-code.md).

### <a name="ref-locals-and-returns"></a>Locais e retornos de ref

Esse recurso permite que os algoritmos que usam e retornam referências para as variáveis definidas em outro lugar. Um exemplo é trabalhar com matrizes grandes e localizar um único local com determinadas características. O seguinte método retorna uma **referência** a esse armazenamento na matriz:

[!code-csharp[FindReturningRef](~/samples/snippets/csharp/new-in-7/MatrixSearch.cs#FindReturningRef "Find returning by reference")]

Você pode declarar o valor retornado como uma `ref` e modificar esse valor na matriz, conforme mostrado no seguinte código:

[!code-csharp[AssignRefReturn](~/samples/snippets/csharp/new-in-7/Program.cs#AssignRefReturn "Assign ref return")]

A linguagem C# tem várias regras que protegem contra o uso indevido de locais e retornos de `ref`:

- É necessário adicionar a palavra-chave `ref` à assinatura do método e a todas as instruções `return` em um método.
  - Isso torna claro que o método é retornado por referência em todo o método.
- Um `ref return` pode ser atribuído a uma variável de valor ou a uma variável `ref`.
  - O chamador controla se o valor retornado é copiado ou não. A omissão do modificador `ref` ao atribuir o valor retornado indica que o chamador deseja obter uma cópia do valor, não uma referência ao armazenamento.
- Não é possível atribuir um valor retornado do método padrão a uma variável local de `ref`.
  - Isso proíbe que instruções como `ref int i = sequence.Count();`
- Não é possível retornar um `ref` para uma variável cujo tempo de vida não se estende para além da execução do método.
  - Isso significa que não é possível retornar uma referência a uma variável local ou a uma variável com um escopo semelhante.
- O locais e retornos de `ref` não podem ser usados com métodos assíncronos.
  - O compilador não consegue saber se a variável referenciada foi definida com o valor final quando o método assíncrono retorna.

A adição de locais e retornos de ref permite algoritmos que são mais eficientes evitando a cópia de valores ou a execução múltipla de operações de desreferenciamento.

Adicionar `ref` ao valor retornado é uma [alteração compatível com a origem](version-update-considerations.md#source-compatible-changes). O código existente é compilado, mas o valor retornado ref é copiado quando atribuído. Os chamadores devem atualizar o armazenamento para o valor retornado para uma variável local `ref` para armazenar o retorno como uma referência.

Agora, as variáveis locais `ref` podem ser reatribuídas para se referir a diferentes instâncias depois de serem inicializadas. O comando a seguir agora compila:

```csharp
ref VeryLargeStruct refLocal = ref veryLargeStruct; // initialization
refLocal = ref anotherVeryLargeStruct; // reassigned, refLocal refers to different storage.
```

Para obter mais informações, consulte o artigo sobre [ `ref` retornos e `ref` locais](../programming-guide/classes-and-structs/ref-returns.md)e o artigo sobre [`foreach`](../language-reference/keywords/foreach-in.md) .

Para saber mais, confira o artigo [Palavra-chave ref](../language-reference/keywords/ref.md).

### <a name="conditional-ref-expressions"></a>Expressões `ref` condicionais

Por fim, a expressão condicional pode produzir um resultado ref em vez de um resultado de valor. Por exemplo, você gravaria o seguinte para recuperar uma referência ao primeiro elemento em uma de duas matrizes:

```csharp
ref var r = ref (arr != null ? ref arr[0] : ref otherArr[0]);
```

A variável `r` é uma referência ao primeiro valor em `arr` ou `otherArr`.

Para saber mais, confira [Operador condicional (?:)](../language-reference/operators/conditional-operator.md) na referência da linguagem.

### <a name="in-parameter-modifier"></a>`in` modificador de parâmetro

A `in` palavra-chave complementa as palavras-chaves ref e out existentes para passar argumentos por referência. A palavra-chave `in` especifica a passagem do argumento por referência, mas o método chamado não modifica o valor.

Você pode declarar sobrecargas que passam por valor ou por referência ReadOnly, conforme mostrado no código a seguir:

```csharp
static void M(S arg);
static void M(in S arg);
```

A sobrecarga por valor (primeiro no exemplo anterior) é melhor do que a versão de referência ReadOnly. Para chamar a versão com o argumento de referência somente leitura, inclua o modificador `in` ao chamar o método.

Para obter mais informações, consulte o artigo sobre o [ `in` modificador de parâmetro](../language-reference/keywords/in-parameter-modifier.md).

### <a name="more-types-support-the-fixed-statement"></a>Mais tipos são compatíveis com a instrução `fixed`

A instrução `fixed` era compatível com um conjunto limitado de tipos. A partir do C# 7.3, qualquer tipo que contenha um método `GetPinnableReference()` que retorna `ref T` ou `ref readonly T` pode ser `fixed`. A adição desse recurso significa que `fixed` pode ser usado com <xref:System.Span%601?displayProperty=nameWithType> e tipos relacionados.

Para obter mais informações, consulte o artigo da [ `fixed` instrução](../language-reference/keywords/fixed-statement.md) na referência de linguagem.

### <a name="indexing-fixed-fields-does-not-require-pinning"></a>A indexação de campos `fixed` não requer fixação

Considere este struct:

```csharp
unsafe struct S
{
    public fixed int myFixedField[10];
}
```

Em versões anteriores do C#, era preciso fixar uma variável para acessar um dos números inteiros que fazem parte de `myFixedField`. Agora, o código a seguir compila sem fixar a variável `p` dentro de uma instrução `fixed` separada:

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        int p = s.myFixedField[5];
    }
}
```

A variável `p` acessa um elemento em `myFixedField`. Não é necessário declarar uma variável `int*` separada. Você ainda precisa de um `unsafe` contexto. Em versões anteriores do C#, é necessário declarar um segundo ponteiro fixo:

```csharp
class C
{
    static S s = new S();

    unsafe public void M()
    {
        fixed (int* ptr = s.myFixedField)
        {
            int p = ptr[5];
        }
    }
}
```

Para obter mais informações, consulte o artigo na [ `fixed` instrução](../language-reference/keywords/fixed-statement.md).

### <a name="stackalloc-arrays-support-initializers"></a>Matrizes `stackalloc` são compatíveis com inicializadores

Você conseguiu especificar os valores dos elementos em uma matriz ao inicializá-la:

```csharp
var arr = new int[3] {1, 2, 3};
var arr2 = new int[] {1, 2, 3};
```

Agora, essa mesma sintaxe pode ser aplicada a matrizes declaradas com `stackalloc`:

```csharp
int* pArr = stackalloc int[3] {1, 2, 3};
int* pArr2 = stackalloc int[] {1, 2, 3};
Span<int> arr = stackalloc [] {1, 2, 3};
```

Para obter mais informações, consulte o artigo do [ `stackalloc` operador](../language-reference/operators/stackalloc.md) .

### <a name="enhanced-generic-constraints"></a>Restrições genéricas aprimoradas

Agora é possível especificar o tipo <xref:System.Enum?displayProperty=nameWithType> ou <xref:System.Delegate?displayProperty=nameWithType> como restrições de classe base para um parâmetro de tipo.

Você também pode usar a nova `unmanaged` restrição para especificar que um parâmetro de tipo deve ser um tipo não- [gerenciado](../language-reference/builtin-types/unmanaged-types.md)não anulável.

Para obter mais informações, consulte os artigos sobre [ `where` restrições genéricas](../language-reference/keywords/where-generic-type-constraint.md) e [restrições em parâmetros de tipo](../programming-guide/generics/constraints-on-type-parameters.md).

Adicionar essas restrições a tipos existentes é uma [alteração incompatível](version-update-considerations.md#incompatible-changes). Tipos genéricos fechados podem não atender mais a essas novas restrições.

### <a name="generalized-async-return-types"></a>Tipos de retorno assíncrono generalizado

Retornar um objeto `Task` de métodos assíncronos pode introduzir gargalos de desempenho em determinados caminhos. `Task` é um tipo de referência, portanto, usá-lo significa alocar um objeto. Em casos em que um método declarado com o modificador `async` retorna um resultado armazenado em cache ou é concluído de forma síncrona, as alocações extras podem se tornar um custo de tempo significativo em seções críticas de desempenho de código. Isso pode se tornar caro se essas alocações ocorrem em loops rígidos.

O novo recurso de linguagem significa que os tipos de retorno do método assíncrono não se limitam a `Task`, `Task<T>` e `void`. O tipo retornado ainda deve satisfazer o padrão assíncrono, o que significa que um método `GetAwaiter` deve ser acessível. Como um exemplo concreto, o `ValueTask` tipo foi adicionado ao .net para fazer uso desse novo recurso de linguagem:

[!code-csharp[UsingValueTask](~/samples/snippets/csharp/new-in-7/AsyncWork.cs#UsingValueTask "Using ValueTask")]

> [!NOTE]
> Você precisa adicionar o pacote NuGet [`System.Threading.Tasks.Extensions`](https://www.nuget.org/packages/System.Threading.Tasks.Extensions/) > para usar o <xref:System.Threading.Tasks.ValueTask%601> tipo.

Essa melhoria é mais útil para autores de biblioteca impedirem a alocação de uma `Task` em um código crítico para o desempenho.

## <a name="new-compiler-options"></a>Novas opções do compilador

Novas opções do compilador são compatíveis com novos cenários de build e DevOps para programas C#.

### <a name="reference-assembly-generation"></a>Geração de assembly de referência

Há duas novas opções de compilador que geram *assemblies somente de referência*: [-refout](../language-reference/compiler-options/refout-compiler-option.md) e [-refonly](../language-reference/compiler-options/refonly-compiler-option.md).
Os artigos vinculados explicam essas opções e os assemblies de referência mais detalhadamente.

### <a name="public-or-open-source-signing"></a>Assinatura pública ou de código aberto

A opção de compilador `-publicsign` instrui o compilador a assinar o assembly usando uma chave pública. O assembly é marcado como assinado, mas a assinatura é obtida da chave pública. Essa opção permite criar crie assemblies assinados a partir de projetos de código aberto usando uma chave pública.

Para saber mais, confira o artigo [Opção do compilador -publicsign](../language-reference/compiler-options/publicsign-compiler-option.md).

### <a name="pathmap"></a>pathmap

A opção de compilador `-pathmap` instrui o compilador a substituir os caminhos de origem do ambiente de build com caminhos de origem mapeados. A opção `-pathmap` controla o caminho de origem gravado pelo compilador para arquivos PDB ou para o <xref:System.Runtime.CompilerServices.CallerFilePathAttribute>.

Para saber mais, confira o artigo [Opção do compilador -pathmap](../language-reference/compiler-options/pathmap-compiler-option.md).
