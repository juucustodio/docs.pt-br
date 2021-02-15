---
title: Correspondência de padrões – Guia de C#
description: Saiba mais sobre expressões de correspondência de padrões em C#
ms.date: 04/10/2019
ms.technology: csharp-fundamentals
ms.assetid: 1e575c32-2e2b-4425-9dca-7d118f3ed15b
ms.openlocfilehash: aabd8afe9a94022557275adb313ca3bf95da7548
ms.sourcegitcommit: b4a46f6d7ebf44c0035627d00924164bcae2db30
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/29/2020
ms.locfileid: "91438018"
---
# <a name="pattern-matching"></a>Correspondência padrão

Os padrões testam um valor que tem uma determinada *forma* e podem *extrair* informações do valor quando ele tem a forma correspondente. A correspondência de padrões fornece uma sintaxe mais concisa para algoritmos que você já usa atualmente. Você já cria algoritmos de correspondência de padrões usando a sintaxe existente. Você escreve instruções `if` ou `switch` que testam os valores. Então, quando essas instruções correspondem, você extrai e usa informações desse valor. Os novos elementos de sintaxe são extensões para as instruções com as quais você já está familiarizado: `is` e `switch`. Essas novas extensões combinam o teste de um valor e a extração dessas informações.

Neste artigo, vamos examinar a nova sintaxe para mostrar a você como ela possibilita um código conciso e legível. A correspondência de padrões habilita expressões em que os dados e o código são separados, diferente dos designs orientados a objeto em que os dados e os métodos que os manipulam estão intimamente ligados.

Para ilustrar essas novas expressões, vamos trabalhar com estruturas que representam formas geométricas usando instruções de correspondência de padrões. Provavelmente você está familiarizado com a criação de hierarquias de classe com a criação de [métodos virtuais e métodos substituídos](methods.md#inherited) para personalizar o comportamento do objeto com base no tipo de runtime do objeto.

Essas técnicas não são possíveis para dados não estruturados em uma hierarquia de classe. Quando os dados e métodos são separados, você precisa de outras ferramentas. Os novos constructos de *correspondência de padrões* permitem uma sintaxe mais clara para examinar dados e manipular o fluxo de controle com base em qualquer condição desses dados. Você já escreve instruções `if` e `switch` que testam o valor da variável. Você escreve instruções `is` que testam o tipo da variável. A *correspondência de padrões* adiciona novos recursos a essas instruções.

Neste artigo, você criará um método que calcula a área de diferentes formas geométricas. Mas fará isso sem recorrer às técnicas orientadas a objeto e sem criar uma hierarquia de classe para as diferentes formas.
Em vez disso, você usará *correspondência de padrões*.
Conforme percorrer esse exemplo, contraste esse código com como ele seria estruturado em uma hierarquia de objeto. Quando os dados que você deve consultar e manipular não são uma hierarquia de classe, a correspondência de padrões permite designs elegantes.

Em vez de iniciar com uma definição de forma abstrata e adicionar classes de forma específicas diferentes, vamos começar com os dados simples, apenas definições de dados para cada uma das formas geométricas:

[!code-csharp[ShapeDefinitions](../../samples/snippets/csharp/PatternMatching/Shapes.cs#01_ShapeDefinitions "Shape definitions")]

Dessas estruturas, vamos escrever um método que calcula a área de uma forma.

## <a name="the-is-type-pattern-expression"></a>A expressão padrão de tipo `is`

Antes do C# 7.0, você precisaria testar cada tipo de uma série de instruções `if` e `is`:

[!code-csharp[ClassicIsExpression](../../samples/snippets/csharp/PatternMatching/GeometricUtilities.cs#02_ClassicIsExpression "Classic type pattern using is")]

O código acima é uma expressão clássica do *padrão de tipo*: você está testando uma variável para determinar seu tipo e adotando uma ação diferente com base no tipo.

Esse código se torna mais simples usando extensões para a expressão `is` para atribuir uma variável se o teste tiver êxito:

[!code-csharp[IsPatternExpression](../../samples/snippets/csharp/PatternMatching/GeometricUtilities.cs#03_IsPatternExpression "is pattern expression")]

Nesta versão atualizadas, a expressão `is` testa a variável e a atribui a uma nova variável do tipo adequado. Além disso, observe que essa versão inclui o tipo `Rectangle`, que é um `struct`. A nova expressão `is` funciona com tipos de valor, bem como com tipos de referência.

As regras da linguagem para expressões de correspondência de padrões ajudam a evitar usar incorretamente os resultados de uma expressão de correspondência. No exemplo acima, as variáveis `s`, `c` e `r` estão somente no escopo e são atribuídas definitivamente quando as expressões de correspondência de padrão têm resultados `true`. Se você tentar usar qualquer variável em outro local, seu código gerará erros de compilador.

Vamos examinar ambas as regras detalhadamente, começando com o escopo. A variável `c` está no escopo somente no branch `else` da primeira instrução `if`. A variável `s` está no escopo no método `ComputeAreaModernIs`. Isso ocorre porque cada branch de uma instrução `if` estabelece um escopo separado para as variáveis. No entanto, a instrução `if` em si não. Isso significa que as variáveis declaradas na `if` instrução estão no mesmo escopo que a `if` instrução (o método, nesse caso). Esse comportamento não é específico para correspondência de padrões, mas é o comportamento definido para escopos de variável e instruções `if` e `else`.

As variáveis `c` e `s` são atribuídas quando as respectivas instruções `if` são verdadeiras por causa do mecanismo atribuído definitivamente quando elas são verdadeiras.

> [!TIP]
> Os exemplos neste tópico usam o constructo recomendado quando uma expressão `is` de correspondência de padrão atribui definitivamente a variável correspondente no branch `true` da instrução `if`.
> Você poderia reverter a lógica dizendo que `if (!(shape is Square s))` e a variável `s` seriam definitivamente atribuídas apenas no branch `false`. Embora isso seja válido no C#, não é recomendável porque é mais confuso para acompanhar a lógica.

Essas regras significam que é improvável que você acesse acidentalmente o resultado de uma expressão de correspondência de padrão quando esse padrão não foi atendido.

## <a name="using-pattern-matching-switch-statements"></a>Usando instruções `switch` de correspondência de padrões

Com o tempo, talvez seja necessário dar suporte a outros tipos de forma. Conforme o número de condições sendo testadas aumenta, você descobrirá que usar as expressões de correspondência de padrões `is` pode se tornar complicado. Além de exigirem instruções `if` em cada tipo que você deseja verificar, as expressões `is` são limitadas a testar se a entrada corresponder a um único tipo. Nesse caso, você descobrirá que as expressões de correspondência de padrões `switch` se tornam uma opção melhor.

A instrução `switch` tradicional era uma expressão padrão: ela dava suporte ao padrão de constante.
Você poderia comparar uma variável a qualquer constante usada em uma instrução `case`:

[!code-csharp[ClassicSwitch](../../samples/snippets/csharp/PatternMatching/GeometricUtilities.cs#04_ClassicSwitch "Classic switch statement")]

O único padrão com suporte pela instrução `switch` era o padrão de constante. Ele era ainda mais limitado a tipos numéricos e ao tipo `string`.
Essas restrições foram removidas e agora você pode escrever uma instrução `switch` usando o padrão de tipo:

[!code-csharp[Switch Type Pattern](../../samples/snippets/csharp/PatternMatching/GeometricUtilities.cs#05_SwitchTypePattern "Compute with `switch` expression")]

A instrução `switch` da correspondência de padrões usa a sintaxe familiar para os desenvolvedores que usaram a instrução `switch` de estilo C tradicional. Cada `case` é avaliada e o código sob a condição que corresponde a variável de entrada é executado. A execução de código não pode "passar" de uma expressão case para a seguinte, a sintaxe da instrução `case` requer que cada `case` termine com um `break`, `return` ou `goto`.

> [!NOTE]
> As instruções `goto` para pular para outro rótulo são válidas somente para o padrão de constante, a instrução switch clássica.

Há novas regras importantes regendo a instrução `switch`. As restrições no tipo da variável na expressão `switch` foram removidas.
Qualquer tipo, como `object` neste exemplo, pode ser usado. As expressões case não são mais limitadas a valores de constantes. Remover essa limitação significa que reordenar seções `switch` pode alterar o comportamento do programa.

Quando limitado a valores de constantes, no máximo um rótulo `case` poderia corresponder ao valor da expressão `switch`. Combine isso com a regra de que cada seção `switch` não deve passar para a próxima seção e isso resulta em que as seções `switch` poderiam ser reorganizadas em qualquer ordem sem afetar o comportamento.
Agora, com expressões `switch` mais generalizadas, a ordem de cada seção é importante. As expressões `switch` são avaliadas na ordem textual. A execução transfere o primeiro rótulo `switch` que corresponde à expressão `switch`.  
O case `default` será executado somente se nenhum outro rótulo case corresponder. O case `default` é avaliado por último, independentemente de sua ordem textual. Se não houver nenhum case `default` e nenhuma das outras instruções `case` corresponder, a execução continuará na instrução após a instrução `switch`. Nenhum dos códigos de rótulos `case` será executado.

## <a name="when-clauses-in-case-expressions"></a>Cláusulas `when` em expressões `case`

Você pode criar cases especiais para essas formas que têm área 0 usando uma cláusula `when` no rótulo `case`. Um quadrado com um comprimento do lado 0 ou um círculo com um raio 0 tem uma área 0. Você especifica essa condição usando uma cláusula `when` no rótulo `case`:  

[!code-csharp[ComputeDegenerateShapes](../../samples/snippets/csharp/PatternMatching/GeometricUtilities.cs#07_ComputeDegenerateShapes "Compute shapes with 0 area")]

Essa alteração demonstra alguns pontos importantes sobre a nova sintaxe. Primeiro, vários rótulos `case` podem ser aplicados a uma seção `switch`. O bloco de instrução é executado quando qualquer um desses rótulos é `true`. Neste exemplo, se a expressão `switch` é um círculo ou um quadrado com área 0, o método retorna a constante 0.

Este exemplo apresenta duas variáveis diferentes nos dois rótulos `case` para o primeiro bloco `switch`. Observe que as instruções neste bloco `switch` não usam as variáveis `c` (para o círculo) ou `s` (para o quadrado).
Nenhuma dessas variáveis é atribuída definitivamente nesse bloco `switch`.
Se algum desses casos corresponder, claramente uma das variáveis foi atribuída.
No entanto, é impossível dizer *qual* foi atribuída em tempo de compilação, porque ambos os casos poderiam corresponder em runtime. Por esse motivo, na maioria das vezes que você usar vários rótulos `case` para o mesmo bloco, não introduzirá uma nova variável na instrução `case` ou apenas usará a variável na cláusula `when`.

Depois de adicionar essas formas com a área 0, vamos adicionar mais alguns tipos de forma: um retângulo e um triângulo:

[!code-csharp[AddRectangleAndTriangle](../../samples/snippets/csharp/PatternMatching/GeometricUtilities.cs#09_AddRectangleAndTriangle "Add rectangle and triangle")]

 Esse conjunto de alterações adiciona rótulos `case` para o caso de degeneração e rótulos e blocos para cada uma das novas formas.

Por fim, você pode adicionar um case `null` para garantir que o argumento não seja `null`:

[!code-csharp[NullCase](../../samples/snippets/csharp/PatternMatching/GeometricUtilities.cs#10_NullCase "Add null case")]

O comportamento especial do `null` padrão é interessante porque a constante `null` no padrão não tem um tipo, mas pode ser convertida em qualquer tipo de referência ou tipo de valor anulável. Em vez de converter um `null` em qualquer tipo, a linguagem define que um `null` valor não será correspondente ao padrão de qualquer tipo, independentemente do tipo de tempo de compilação da variável. Esse comportamento torna o novo padrão de tipo baseado em `switch` consistente com a instrução `is`: instruções `is` sempre retornam `false` quando o valor sendo verificado é `null`. Isso também é mais simples: depois de verificar o tipo, não é necessário fazer uma verificação adicional de nulos. Você pode ver isso pelo fato de que não há nenhuma verificação de nulos em nenhum dos blocos de casos dos exemplos acima: elas não são necessárias, já que a correspondência do padrão de tipo assegura um valor não nulo.

## <a name="var-declarations-in-case-expressions"></a>`var` declarações em expressões `case`

A introdução de `var` como uma das expressões de correspondência introduz novas regras à correspondência de padrão.

A primeira regra é de que a declaração `var` segue as regras de inferência de tipos normais: o tipo é inferido como tipo estático da expressão switch. Com base nessa regra, o tipo sempre é correspondente.

A segunda regra é que uma declaração `var` não tem a verificação de nulos que outras expressões do tipo padrão incluem. Isso significa que a variável pode ser nula e uma verificação de nulos é necessária nesse caso.

Essas duas regras significam que, em muitos casos, uma declaração `var` em uma expressão `case` corresponde às mesmas condições que uma expressão `default`.
Como um case não padrão é preferencial ao case `default`, o case `default` nunca será executado.

> [!NOTE]
> O compilador não emite um aviso nos casos em que um case `default` foi gravado, mas nunca será executado. Isso é coerente com a atual comportamento da instrução `switch`, em que todos os casos possíveis foram listados.

A terceira regra introduz usos em que um case `var` pode ser útil. Imagine que você esteja fazendo uma correspondência de padrão em que a entrada é uma cadeia de caracteres e você está pesquisando valores de comando conhecidos. Você pode escrever algo parecido com:

[!code-csharp[VarCaseExpression](../../samples/snippets/csharp/PatternMatching/Program.cs#VarCaseExpression "use a var case expression to filter white space")]

O case `var` corresponde a `null`, a cadeia de caracteres vazia ou qualquer cadeia de caracteres que contém somente espaços em branco. Observe que o código anterior usa o operador `?.` para garantir que ele não gere um <xref:System.NullReferenceException>acidentalmente. O case `default` lida com outros valores de cadeia de caracteres que não são entendidos pelo analisador de comando.

Este é um exemplo em que talvez você queira considerar uma expressão case `var` diferente de uma expressão `default`.

## <a name="conclusions"></a>Conclusões

Os *constructos de correspondência de padrões* permitem que você gerencie facilmente o fluxo de controle entre diferentes tipos e variáveis que não são relacionadas por uma hierarquia de herança. Você também pode controlar a lógica para usar qualquer condição testada na variável. Ela habilita os padrões e expressões que você precisará com mais frequência conforme cria aplicativos mais distribuídos, no qual os dados e os métodos que manipulam esses dados são separados. Você observará que os structs de forma usados nesse exemplo não contêm nenhum método, apenas propriedades somente leitura.
A correspondência de padrões funciona com qualquer tipo de dados. Você escreve expressões que examinam o objeto e toma decisões de fluxo de controle com base nessas condições.

Compare o código deste exemplo com o design que viria após a criação de uma hierarquia de classe para um resumo de `Shape` e formas derivadas específicas, cada uma com sua própria implementação de um método virtual para calcular a área. Muitas vezes você descobrirá que as expressões de correspondência de padrões podem ser uma ferramenta muito útil quando estiver trabalhando com os dados e desejar separar as preocupações de armazenamento de dados das preocupações de comportamento.

## <a name="see-also"></a>Confira também

- [Tutorial: usar a correspondência de padrões para criar algoritmos orientados a dados e baseados em tipos](tutorials/pattern-matching.md)
