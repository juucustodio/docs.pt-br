---
title: O que há de novo no C# 9,0 – Guia C#
description: Obtenha uma visão geral dos novos recursos disponíveis no C# 9,0.
ms.date: 09/04/2020
ms.openlocfilehash: ddffe4aaaed6c9079999b2ab29ca61ab5753f15a
ms.sourcegitcommit: 43d5aca3fda42bad8843f6c4e72f6bd52daa55f1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/09/2020
ms.locfileid: "89598137"
---
# <a name="whats-new-in-c-90"></a>Novidades do C# 9.0

O c# 9,0 adiciona os seguintes recursos e aprimoramentos à linguagem C#:

- Registros
- Setters somente init
- Instruções de nível superior
- Melhorias na correspondência de padrões
- Inteiros de tamanho nativo
- Ponteiros de função
- Suprimir emissão do sinalizador localsinit
- Expressões new com tipo de destino
- funções anônimas estáticas
- Expressões condicionais de tipo de destino
- Tipos de retorno covariantes
- `GetEnumerator`Suporte de extensão para `foreach` loops
- Parâmetros discard de lambda
- Atributos em funções locais
- Inicializadores de módulo
- Novos recursos para métodos parciais

O C# 9,0 tem suporte no **.NET 5**. Para obter mais informações, consulte [controle de versão da linguagem C#](../language-reference/configure-language-version.md).

## <a name="record-types"></a>Tipos de registro

O C# 9,0 apresenta ***tipos de registro***, que são um tipo de referência que fornece métodos sintetizados para fornecer a semântica de valor para igualdade. Os registros são imutáveis por padrão.

Os tipos de registro facilitam a criação de tipos de referência imutáveis no .NET. Historicamente, os tipos .NET são classificados em grande parte como tipos de referência (incluindo classes e tipos anônimos) e tipos de valor (incluindo structs e tuplas). Embora tipos de valor imutáveis sejam recomendados, os tipos de valores mutáveis geralmente não introduzem erros. As variáveis de tipo de valor contêm os valores para que as alterações sejam feitas em uma cópia dos dados originais quando os tipos de valor são passados para métodos.

Também há muitas vantagens em tipos de referência imutáveis. Essas vantagens são mais pronunciadas em programas simultâneos com dados compartilhados. Infelizmente, o C# forçou você a escrever um pouco de código extra para criar tipos de referência imutáveis. Os registros fornecem uma declaração de tipo para um tipo de referência imutável que usa semântica de valor para igualdade. Os métodos sintetizados para códigos de igualdade e hash consideram dois registros iguais se suas propriedades forem iguais. Considere esta definição:

:::code language="csharp" source="snippets/whats-new-csharp9/RecordsExamples.cs" ID="RecordDefinition":::

A definição de registro cria um `Person` tipo que contém duas propriedades ReadOnly: `FirstName` e `LastName` . O `Person` tipo é um tipo de referência. Se você examinou o IL, ele é uma classe. É imutável, pois nenhuma das propriedades pode ser modificada depois de ser criada. Quando você define um tipo de registro, o compilador sintetiza vários outros métodos para você:

- Métodos para comparações de igualdade com base em valor
- Substituir para <xref:System.Object.GetHashCode>
- Copiar e clonar Membros
- `PrintMembers` e <xref:System.Object.ToString>
- Método `Deconstruct`

Registra o suporte à herança. Você pode declarar um novo registro derivado do da `Person` seguinte maneira:

:::code language="csharp" source="snippets/whats-new-csharp9/RecordsExamples.cs" ID="InheritedRecord":::

Você também pode lacrar registros para evitar uma maior derivação:

:::code language="csharp" source="snippets/whats-new-csharp9/RecordsExamples.cs" ID="SealedRecord":::

O compilador sintetiza versões diferentes dos métodos acima. As assinaturas de método dependem de se o tipo de registro é lacrado e se a classe base direta é Object. Os registros devem ter os seguintes recursos:

- A igualdade é baseada em valor e inclui uma verificação de que os tipos correspondem. Por exemplo, um `Student` não pode ser igual a a `Person` , mesmo que os dois registros compartilhem o mesmo nome.
- Os registros têm uma representação de cadeia de caracteres consistente gerada para você.
- Os registros dão suporte à construção de cópia. A construção correta da cópia deve incluir hierarquias de herança e propriedades adicionadas por desenvolvedores.
- Os registros podem ser copiados com modificações. Essas operações de cópia e modificação oferecem suporte a mutação não destrutiva.
- Todos os registros dão suporte à desconstrução.

Além das `Equals` sobrecargas conhecidas, `operator ==` e `operator !=` , o compilador sintetiza uma nova `EqualityContract` propriedade. A propriedade retorna um `Type` objeto que corresponde ao tipo do registro. Se o tipo base for `object` , a propriedade será `virtual` . Se o tipo base for outro tipo de registro, a propriedade será um `override` . Se o tipo de registro for `sealed` , a propriedade será `sealed` . O sintetizado `GetHashCode` usa o `GetHashCode` de todas as propriedades e campos declarados no tipo base e no tipo de registro. Esses métodos sintetizados impõem a igualdade baseada em valor em uma hierarquia de herança. Isso significa que um `Student` nunca será considerado igual a um `Person` com o mesmo nome. Os tipos dos dois registros devem corresponder e todas as propriedades compartilhadas entre os tipos de registro são iguais.

Os registros também têm um Construtor sintetizado e um método de "clonagem" para a criação de cópias. O Construtor sintetizado tem um argumento do tipo de registro. Ele produz um novo registro com os mesmos valores para todas as propriedades do registro. Esse construtor é privado se o registro estiver lacrado, caso contrário, será protegido. O método "clone" sintetizado dá suporte à construção de cópia para hierarquias de registro. O termo "clone" está entre aspas porque o nome real é gerado pelo compilador. Você não pode criar um método chamado `Clone` em um tipo de registro. O método "clone" sintetizado retorna o tipo de registro que está sendo copiado usando a expedição virtual. O compilador adiciona diferentes modificadores para o método "clone" dependendo dos modificadores de acesso no `record` :

- Se o tipo de registro for `abstract` , o método "clone" também será `abstract` . Se o tipo base não for `object` , o método também será `override` .
- Para tipos de registro que não são `abstract` quando o tipo base é `object` :
  - Se o registro for `sealed` , nenhum modificador adicional será adicionado ao método "clone" (o que significa que ele não é `virtual` ).
  - Se o registro não for `sealed` , o método "clone" será `virtual` .
- Para tipos de registro que não são `abstract` quando o tipo base não é `object` :
  - Se o registro for `sealed` , o método "clone" também será `sealed` .
  - Se o registro não for `sealed` , o método "clone" será `override` .

O resultado de todas essas regras é que a igualdade é implementada consistentemente em qualquer hierarquia de tipos de registro. Dois registros são iguais entre si se suas propriedades forem iguais e seus tipos forem os mesmos, conforme mostrado no exemplo a seguir:

:::code language="csharp" source="snippets/whats-new-csharp9/RecordsExamples.cs" ID="RecordsEquality":::

O compilador sintetiza dois métodos que dão suporte à saída impressa: uma <xref:System.Object.ToString> substituição e `PrintMembers` . O `PrintMembers` usa <xref:System.Text.StringBuilder?displayProperty=nameWithType> como argumento. Ele acrescenta uma lista separada por vírgulas de nomes de propriedade e valores para todas as propriedades no tipo de registro. `PrintMembers` chama a implementação de base para todos os registros derivados de outros registros. A <xref:System.Object.ToString> substituição retorna a cadeia de caracteres produzida por `PrintMembers` , cercada por `{` e `}` . Por exemplo, o <xref:System.Object.ToString> método para `Student` retorna um `string` semelhante ao seguinte código:

```csharp
"Student { LastName = Wagner, FirstName = Bill, Level = 11 }"
```

Os exemplos mostrados até agora usam a sintaxe tradicional para declarar Propriedades. Há uma forma mais concisa chamada ***registros posicionais***.  Aqui estão os três tipos de registro definidos anteriormente como registros posicionais:

:::code language="csharp" source="snippets/whats-new-csharp9/PositionalRecords.cs" ID="PositionalRecords":::

Essas declarações criam a mesma funcionalidade da versão anterior (com alguns recursos extras abordados na seção a seguir). Essas declarações terminam com um ponto e vírgula em vez de colchetes porque esses registros não adicionam outros métodos. Você pode adicionar um corpo e também incluir outros métodos:

:::code language="csharp" source="snippets/whats-new-csharp9/PositionalRecords.cs" ID="RecordsWithMethods":::

O compilador produz um `Deconstruct` método para registros posicionais. O `Deconstruct` método tem parâmetros que correspondem aos nomes de todas as propriedades públicas no tipo de registro. O `Deconstruct` método pode ser usado para desconstruir o registro em suas propriedades de componente:

:::code language="csharp" source="snippets/whats-new-csharp9/PositionalRecords.cs" ID="DeconstructRecord":::

Por fim, os registros têm suporte ***com expressões-Expressions***. Uma ***expressão with*** instrui o compilador a criar uma cópia de um registro, mas *com* as propriedades especificadas modificadas:

:::code language="csharp" source="snippets/whats-new-csharp9/PositionalRecords.cs" ID="Wither":::

A linha acima cria um novo `Person` registro no qual a `LastName` propriedade é uma cópia de `person` e o `FirstName` é "Paul". Você pode definir qualquer número de propriedades em uma expressão with.  Qualquer um dos membros sintetizados, exceto o método "clone", pode ser escrito por você. Se um tipo de registro tiver um método que corresponda à assinatura de qualquer método sintetizado, o compilador não sintetizará esse método. O `Dog` exemplo de registro anterior contém um método codificado <xref:System.String.ToString> por mão como um exemplo.

## <a name="init-only-setters"></a>Setters somente init

Os ***setters somente init*** fornecem sintaxe consistente para inicializar membros de um objeto. Os inicializadores de propriedade fornecem claro qual valor está definindo qual propriedade. A desvantagem é que essas propriedades devem ser configurável. A partir do C# 9,0, você pode criar `init` acessadores em vez de `set` acessadores para propriedades e indexadores. Os chamadores podem usar a sintaxe do inicializador de propriedade para definir esses valores em expressões de criação, mas essas propriedades são ReadOnly quando a construção é concluída. Os setters somente init fornecem uma janela para alterar o estado. Essa janela fecha quando a fase de construção termina. A fase de construção termina com eficiência após toda a inicialização, incluindo inicializadores de propriedade e with-Expressions concluídos.

O exemplo anterior para registros posicionais demonstra o uso de um setter somente init para definir uma propriedade usando uma expressão with. Você pode declarar somente setters init em qualquer tipo que você escreve. Por exemplo, a seguinte estrutura define uma estrutura de observação do clima:

:::code language="csharp" source="snippets/whats-new-csharp9/WeatherObservation.cs" ID="DeclareWeatherObservation":::

Os chamadores podem usar a sintaxe do inicializador de propriedade para definir os valores, enquanto ainda preservam a imutabilidade:

:::code language="csharp" source="snippets/whats-new-csharp9/WeatherObservation.cs" ID="UseWeatherObservation":::

Mas, a alteração de uma observação após a inicialização é um erro ao atribuir a uma propriedade somente init fora da inicialização:

```csharp
// Error! CS8852.
now.TempetureInCelsius = 18;
```

Os setters somente init podem ser úteis para definir propriedades de classe base de classes derivadas. Eles também podem definir propriedades derivadas por meio de auxiliares em uma classe base. Registros posicionais declaram propriedades usando somente init setters. Esses setters são usados em with-Expressions. Você pode declarar setters somente init para qualquer um `class` ou `struct` definir.

## <a name="top-level-statements"></a>Instruções de nível superior

As ***instruções de nível superior*** removem a cerimônia desnecessária de muitos aplicativos. Considere o canônico "Olá, Mundo!" Program

```csharp
using System;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

Há apenas uma linha de código que faz qualquer coisa. Com as instruções de nível superior, você pode substituir todo o texto clichê pela `using` instrução e a única linha que faz o trabalho:

:::code language="csharp" source="snippets/whats-new-csharp9/Program.cs" ID="TopLevelStatements":::

Se você quisesse um programa de uma linha, poderia remover a `using` diretiva e usar o nome do tipo totalmente qualificado:

```csharp
System.Console.WriteLine("Hello World!");
```

Somente um arquivo em seu aplicativo pode usar instruções de nível superior. Se o compilador encontrar instruções de nível superior em vários arquivos de origem, será um erro. Também será um erro se você combinar instruções de nível superior com um método de ponto de entrada de programa declarado, normalmente um `Main` método. De certa forma, você pode imaginar que um arquivo contém as instruções que normalmente estaria no `Main` método de uma `Program` classe.  

Um dos usos mais comuns para esse recurso é a criação de materiais de ensino. Desenvolvedores de C# iniciantes podem escrever o "Olá, Mundo!" canônico em uma ou duas linhas de código. Nenhuma das cerimônias extras é necessária. No entanto, os desenvolvedores experientes também encontrarão muitos usos para esse recurso. As instruções de nível superior permitem uma experiência semelhante a um script para experimentação semelhante ao que os notebooks Jupyter fornecem. As instruções de nível superior são ótimas para pequenos programas de console e utilitários. O Azure Functions é um caso de uso ideal para instruções de nível superior.

O mais importante é que as instruções de nível superior não limitam o escopo ou a complexidade do aplicativo. Essas instruções podem acessar ou usar qualquer classe .NET. Eles também não limitam o uso de argumentos de linha de comando ou valores de retorno. Instruções de nível superior podem acessar uma matriz de cadeias de caracteres denominadas args. Se as instruções de nível superior retornarem um valor inteiro, esse valor se tornará o código de retorno de inteiro de um método sintetizado `Main` . As instruções de nível superior podem conter expressões assíncronas. Nesse caso, o ponto de entrada sintetizado retorna um `Task` , ou `Task<int>` .

## <a name="pattern-matching-enhancements"></a>Melhorias na correspondência de padrões

O C# 9 inclui novas melhorias de correspondência de padrões:

- ***Padrões de tipo*** correspondem a uma variável é um tipo
- ***Padrões entre parênteses*** impõem ou enfatizam a precedência de combinações de padrões
- *** `and` Padrões de conjuntiva*** exigem os dois padrões para corresponder
- *** `or` Padrões de disjunctive*** exigem qualquer padrão para corresponder
- *** `not` Padrões negados*** exigem que um padrão não corresponda
- Os ***padrões relacionais*** exigem que a entrada seja menor que, maior que, menor ou igual ou maior ou igual a uma determinada constante.

Esses padrões enriquecem a sintaxe para padrões. Considere estes exemplos:

:::code language="csharp" source="snippets/whats-new-csharp9/PatternUtilities.cs" ID="IsLetterPattern":::

Como alternativa, com parênteses opcionais para deixá-lo claro que `and` tem precedência maior do que `or` :

:::code language="csharp" source="snippets/whats-new-csharp9/PatternUtilities.cs" ID="IsLetterOrSeparatorPattern":::

Um dos usos mais comuns é uma nova sintaxe para uma verificação nula:

```csharp
if (e is not null)
{
    // ...
}
```

Qualquer um desses padrões pode ser usado em qualquer contexto em que os padrões são permitidos: `is` expressões `switch` de padrão, expressões, padrões aninhados e o padrão do rótulo de uma `switch` instrução `case` .

## <a name="performance-and-interop"></a>Desempenho e interoperabilidade

Três novos recursos melhoram o suporte para a interoperabilidade nativa e bibliotecas de nível baixo que exigem alto desempenho: inteiros de tamanho nativo, ponteiros de função e omissão do `localsinit` sinalizador.

Inteiros de tamanho nativo `nint` e `nuint` , são tipos inteiros. Eles são expressos pelos tipos subjacentes <xref:System.IntPtr?displayProperty=nameWithType> e <xref:System.UIntPtr?displayProperty=nameWithType> . O compilador superfícies de conversões e operações adicionais para esses tipos como ints nativas. Os ints de tamanho nativo não têm constantes para `MaxValue` ou `MinValue` , exceto para `nuint.MinValue` , que tem um `MinValue` de `0` . Outros valores não podem ser expressos como constantes porque depende do tamanho nativo de um inteiro no computador de destino. Você pode usar valores constantes para `nint` no intervalo [ `int.MinValue` .. `int.MaxValue`]. Você pode usar valores constantes para `nuint` no intervalo [ `uint.MinValue` .. `uint.MaxValue`]. O compilador executa o dobramento constante para todos os operadores unários e binários usando os <xref:System.Int32?displayProperty=nameWithType> <xref:System.UInt32?displayProperty=nameWithType> tipos e. Se o resultado não couber em 32 bits, a operação será executada em tempo de execução e não será considerada uma constante. Os inteiros de tamanho nativo podem aumentar o desempenho em cenários em que a matemática de inteiros é usada extensivamente e precisa ter o desempenho mais rápido possível.

Ponteiros de função fornecem uma sintaxe fácil para acessar os opcodes de IL `ldftn` e `calli` . Você pode declarar ponteiros de função usando a nova `delegate*` sintaxe. Um `delegate*` tipo é um tipo de ponteiro. Invocar o `delegate*` tipo usa `calli` , em contraste com um delegado que usa `callvirt` no `Invoke()` método. Sintaticamente, as invocações são idênticas. Invocação de ponteiro de função usa a `managed` Convenção de chamada. Você adiciona a `unmanaged` palavra-chave após a `delegate*` sintaxe para declarar que deseja a `unmanaged` Convenção de chamada. Outras convenções de chamada podem ser especificadas usando atributos na `delegate*` declaração.

Por fim, você pode adicionar o <xref:System.Runtime.CompilerServices.SkipLocalsInitAttribute?displayProperty=nameWithType> para instruir o compilador a não emitir o `localsinit` sinalizador. Esse sinalizador instrui o CLR a inicializar zero todas as variáveis locais. O `localsinit` sinalizador tem sido o comportamento padrão para C# desde 1,0. No entanto, a inicialização zero extra pode ter um impacto mensurável no desempenho em alguns cenários. Em particular, quando você usa o `stackalloc` . Nesses casos, você pode adicionar o <xref:System.Runtime.CompilerServices.SkipLocalsInitAttribute> . Você pode adicioná-lo a um único método ou propriedade, ou a um `class` ,, `struct` `interface` ou até mesmo a um módulo. Esse atributo não afeta `abstract` os métodos; ele afeta o código gerado para a implementação.

Esses recursos podem melhorar o desempenho em alguns cenários. Eles devem ser usados somente após um parâmetro de comparação cuidadoso antes e depois da adoção. O código que envolve inteiros de tamanho nativo deve ser testado em várias plataformas de destino com tamanhos de inteiro diferentes. Os outros recursos exigem código não seguro.

## <a name="fit-and-finish-features"></a>Recursos de ajuste e término

Muitos dos outros recursos ajudam a escrever código com mais eficiência. No C# 9,0, você pode omitir o tipo em uma nova expressão quando o tipo do objeto criado já é conhecido. O uso mais comum está em declarações de campo:

:::code language="csharp" source="snippets/whats-new-csharp9/FitAndFinish.cs" ID="WeatherStationField":::

O tipo de destino New também pode ser usado quando você precisa criar um novo objeto para passar como um parâmetro para um método. Considere um `ForecastFor()` método com a seguinte assinatura:

:::code language="csharp" source="snippets/whats-new-csharp9/FitAndFinish.cs" ID="ForecastSignature":::

Você pode chamá-lo da seguinte maneira:

:::code language="csharp" source="snippets/whats-new-csharp9/FitAndFinish.cs" ID="TargetTypeNewArgument":::

Outro bom uso para esse recurso é combiná-lo com propriedades init somente para inicializar um novo objeto:

:::code language="csharp" source="snippets/whats-new-csharp9/FitAndFinish.cs" ID="InitWeatherStation":::

Você pode retornar uma instância criada pelo construtor padrão usando uma `return new();` expressão.

Um recurso semelhante melhora a resolução de tipo de destino de expressões condicionais. Com essa alteração, as duas expressões não precisam ter uma conversão implícita de uma para a outra, mas podem ter conversões implícitas em um tipo comum. Você provavelmente não perceberá essa alteração. O que você observará é que algumas expressões condicionais que antes exigiam conversões ou que não compilaram agora só funcionam.

A partir do C# 9,0, você pode adicionar o `static` modificador a expressões lambda ou a métodos anônimos. As expressões lambda estáticas são análogas às `static` funções locais: uma função lambda ou anônima estática não pode capturar variáveis locais ou estado de instância. O `static` modificador impede a captura acidental de outras variáveis.

Os tipos de retorno covariantes fornecem flexibilidade para os tipos de retorno de funções substituídas. Uma função virtual substituída pode retornar um tipo derivado do tipo de retorno declarado no método de classe base. Isso pode ser útil para registros e para outros tipos que dão suporte a métodos de clonagem ou de alocador virtual.

Além disso, o `foreach` loop reconhecerá e usará um método de extensão `GetEnumerator` que, de outra forma, atende ao `foreach` padrão. Essa alteração significa `foreach` ser consistente com outras construções baseadas em padrão, como o padrão assíncrono e a desconstrução baseada em padrões. Na prática, essa alteração significa que você pode adicionar `foreach` suporte a qualquer tipo. Você deve limitar seu uso ao ao enumerar um objeto faz sentido em seu design.

Em seguida, você pode usar os descartes como parâmetros para expressões lambda. Essa conveniência permite que você evite nomear o argumento, e o compilador pode evitar usá-lo. Você usa o `_` para qualquer argumento.

Por fim, agora você pode aplicar atributos a funções locais. Por exemplo, você pode aplicar anotações de atributo anulável a funções locais.

## <a name="support-for-code-generators"></a>Suporte para geradores de código

Dois recursos finais dão suporte a geradores de código C#. Os geradores de código C# são um componente que você pode escrever que é semelhante a um analisador de Roslyn ou a uma correção de código. A diferença é que os geradores de código analisam o código e gravam novos arquivos de código-fonte como parte do processo de compilação. Um gerador de código típico pesquisa código em busca de atributos ou outras convenções.

Um gerador de código lê atributos ou outros elementos de código usando as APIs de análise de Roslyn. A partir dessas informações, ele adiciona um novo código à compilação. Os geradores de origem só podem adicionar código; Eles não têm permissão para modificar nenhum código existente na compilação.

Os dois recursos adicionados para geradores de código são extensões para ***sintaxe de método parcial***e ***inicializadores de módulo***. Primeiro, as alterações em métodos parciais. Antes do C# 9,0, os métodos parciais são `private` , mas não podem especificar um modificador de acesso, ter um `void` retorno e não podem ter `out` parâmetros. Essas restrições destinam-se que, se nenhuma implementação de método for fornecida, o compilador removerá todas as chamadas para o método parcial. O C# 9,0 remove essas restrições, mas requer que as declarações de método parciais tenham uma implementação. Os geradores de código podem fornecer essa implementação. Para evitar a introdução de uma alteração significativa, o compilador considera qualquer método parcial sem um modificador de acesso para seguir as regras antigas. Se o método parcial incluir o `private` modificador de acesso, as novas regras regem esse método parcial.

O segundo novo recurso para geradores de código é ***inicializadores de módulo***. Inicializadores de módulo são métodos que têm o <xref:System.Runtime.CompilerServices.ModuleInitializerAttribute> atributo anexado a eles. Esses métodos serão chamados pelo tempo de execução quando o assembly for carregado. Um método inicializador de módulo:

- Deve ser estático
- Não deve ter parâmetros
- Deve retornar void
- Não deve ser um método genérico
- Não deve estar contido em uma classe genérica
- Deve ser acessível do módulo que a contém

Esse último ponto de marcador efetivamente significa que o método e sua classe recipiente devem ser internos ou públicos. O método não pode ser uma função local.
