---
title: Tour do .NET
description: Um tour guiado por alguns dos recursos mais importantes do .NET.
author: cartermp
ms.author: wiwagn
ms.date: 05/22/2017
ms.technology: dotnet-standard
ms.assetid: bbfe6465-329d-4982-869d-472e7ef85d93
ms.openlocfilehash: a44c3692dc9ed9b3de37955191edfb279403f152
ms.sourcegitcommit: 0c3ce6d2e7586d925a30f231f32046b7b3934acb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89516015"
---
# <a name="tour-of-net"></a>Tour do .NET

O .NET é uma plataforma de desenvolvimento de uso geral. Ele tem vários recursos importantes, como suporte a várias linguagens de programação, modelos de programação assíncronos e simultâneos, além de interoperabilidade nativa, o que possibilita uma ampla variedade de cenários em várias plataformas.

Este artigo oferece um tour guiado por alguns dos principais recursos do .NET. Consulte o tópico [Componentes de arquitetura do .NET](components.md) para saber mais sobre as partes de arquitetura do .NET e para que elas são usadas.

## <a name="how-to-run-the-code-samples"></a>Como executar os exemplos de código

Para saber como configurar um ambiente de desenvolvimento para executar os exemplos de código, consulte o tópico [Introdução](get-started.md). Copie e cole os exemplos de código desta página no seu ambiente para executá-los.

## <a name="programming-languages"></a>Linguagens de programação

O .NET dá suporte a várias linguagens de programação. As implementações do .NET implementam o [CLI (Common Language Infrastructure)](https://visualstudio.microsoft.com/license-terms/ecma-c-common-language-infrastructure-standards/), que, entre outras coisas, especifica um runtime independente de linguagem e interoperabilidade de linguagem. Isso significa que você escolhe qualquer linguagem .NET para criar aplicativos e serviços no .NET.

A Microsoft desenvolve e dá suporte ativamente a três linguagens .NET: C#, F # e Visual Basic.

* A C# é simples, poderosa, fortemente tipada e orientada a objeto, mantendo a expressividade e elegância das linguagens de estilo C. Qualquer pessoa familiarizada com C e linguagens semelhantes encontra poucos problemas para adaptar-se à C#. Confira o [Guia de C#](../csharp/index.yml) para saber mais sobre o C#.

* F# é uma linguagem de programação de plataforma cruzada com prioridade para a parte funcional e que também dá suporte à programação imperativa e orientada a objeto tradicional. Confira o [Guia de F#](../fsharp/index.yml) para saber mais sobre o F#.

* A Visual Basic é uma linguagem fácil de aprender, que você usa para criar uma variedade de aplicativos executados no .NET. Entre as linguagens .NET, a sintaxe do Visual Basic é mais próxima da linguagem humana comum, geralmente facilitando o desenvolvimento de software por pessoas novas.

## <a name="automatic-memory-management"></a>Gerenciamento automático de memória

O .NET usa a [(GC) coleta de lixo](garbage-collection/index.md) para fornecer gerenciamento automático de memória para os programas. A GC opera em uma abordagem lenta no gerenciamento de memória, dando prioridade à taxa de transferência do aplicativo em relação à coleta imediata da memória. Para saber mais sobre o GC do .NET, confira [Noções básicas da coleta de lixo (GC)](garbage-collection/fundamentals.md).

As duas linhas a seguir alocam memória:

[!code-csharp[MemoryManagement](../../samples/snippets/csharp/snippets/tour/MemoryManagement.csx#L1-L2)]

Não há nenhuma palavra-chave análoga para desalocar memória, pois a desalocação ocorre automaticamente quando o coletor de lixo recupera a memória por meio de sua execução agendada.

O coletor de lixo é um dos serviços que ajudam a garantir a *segurança da memória*. Um programa é considerado de memória segura se ele acessa somente a memória alocada. Por exemplo, o runtime garante que um aplicativo não acesse memória não alocada além dos limites de uma matriz.

No exemplo a seguir, o runtime aciona uma exceção <xref:System.IndexOutOfRangeException> para impor segurança da memória:

[!code-csharp[MemoryManagement](../../samples/snippets/csharp/snippets/tour/MemoryManagement.csx#L4-L5)]

## <a name="working-with-unmanaged-resources"></a>Trabalhando com recursos não gerenciados

Alguns objetos fazem referência a *recursos não gerenciados*. Os recursos não gerenciados são recursos que não são mantidos automaticamente pelo runtime do .NET. Por exemplo, um identificador de arquivo é um recurso não gerenciado. Um objeto <xref:System.IO.FileStream> é um objeto gerenciado, mas ele faz referência a um identificador de arquivo, que não é gerenciado. Quando você termina de usar o <xref:System.IO.FileStream>, é necessário liberar o identificador de arquivo.

No .NET, objetos que fazem referência a recursos não gerenciados implementam a interface <xref:System.IDisposable>. Quando você termina de usar o objeto, você chama o método <xref:System.IDisposable.Dispose> do objeto, responsável por liberar quaisquer recursos não gerenciados. As linguagens .NET fornecem uma [ `using` instrução](../csharp/language-reference/keywords/using.md) conveniente para tais objetos, conforme mostrado no exemplo a seguir:

[!code-csharp[UnmanagedResources](../../samples/snippets/csharp/snippets/tour/UnmanagedResources.csx#L1-L6)]

Uma vez que o bloco `using` é concluído, o runtime do .NET automaticamente chama o método <xref:System.IDisposable.Dispose> do objeto `stream`, que libera o identificador de arquivo. O runtime também faz isso se uma exceção faz com que o controle deixe o bloco.

Para obter mais detalhes, consulte os seguintes tópicos:

* Para C#, consulte o tópico [Instrução Using (referência de C#)](../csharp/language-reference/keywords/using-statement.md).
* Para F#, consulte [Gerenciamento de recursos: a palavra-chave Use](../fsharp/language-reference/resource-management-the-use-keyword.md).
* Para Visual Basic, consulte o tópico [usando a instrução (Visual Basic)](../visual-basic/language-reference/statements/using-statement.md) .

## <a name="type-safety"></a>Segurança de tipos

Um objeto é uma instância de um tipo específico. As únicas operações permitidas para um determinado objeto são aquelas do seu tipo. Um tipo `Dog` pode ter os métodos `Jump` e `WagTail`, mas não um método `SumTotal`. Um programa só chama os métodos que pertencem a um determinado tipo. Todas as outras chamadas resultam em um erro em tempo de compilação ou uma exceção de tempo de execução (no caso de usar recursos dinâmicos ou `object`).

As linguagens do .NET são orientadas a objeto, com hierarquias de classes base e classes derivadas. O runtime do .NET só permite conversões de objeto e chamadas alinhadas à hierarquia do objeto. Lembre-se de que todos os tipos definidos em qualquer linguagem .NET derivam do tipo base <xref:System.Object>.

[!code-csharp[TypeSafety](../../samples/snippets/csharp/snippets/tour/TypeSafety.csx#L19-L23)]

A segurança de tipos também é usada para ajudar a forçar o encapsulamento, garantindo a fidelidade das palavras-chave acessadoras. Palavras-chave acessadoras são artefatos que controlam o acesso a membros de um determinado tipo por outro código. Elas geralmente são usadas para vários tipos de dados dentro de um tipo que são usados para gerenciar seu comportamento.

[!code-csharp[TypeSafety](../../samples/snippets/csharp/snippets/tour/TypeSafety.csx#L3-L3)]

C#, Visual Basic e F# dão suporte à *inferência de tipo* de variável local. Inferência de tipos significa que o compilador deduz o tipo da expressão no lado esquerdo da expressão com base na expressão do lado direito. Isso não significa que a segurança de tipos é interrompida ou evitada. O tipo resultante realmente tem um tipo forte com tudo o que a expressão implica. No exemplo anterior, `dog` é reescrito para introduzir a inferência de tipos e o restante do exemplo permanece inalterado:

[!code-csharp[TypeSafety](../../samples/snippets/csharp/snippets/tour/TypeSafety.csx#L28-L34)]

F # tem ainda mais recursos de inferência de tipos do que a inferência de tipo de método local encontrada em C# e Visual Basic. Para obter mais informações, consulte [Inferência de tipos](../fsharp/language-reference/type-inference.md).

## <a name="delegates-and-lambdas"></a>Delegados e lambdas

Um delegado é representado por uma assinatura de método. Qualquer método com essa assinatura pode ser atribuído ao delegado e é executado quando o delegado é invocado.

Os delegados são como ponteiros de função do C++, exceto pelo fato de que eles são fortemente tipados. Eles são um tipo de método desconectado dentro do sistema de tipos CLR. Os métodos regulares são anexados a uma classe e só podem ser chamados diretamente por meio de convenções de chamada estáticas ou de instância.

No .NET, os delegados são comumente usados em manipuladores de eventos, na definição de operações assíncronas e em expressões lambda, que são a base da LINQ. Saiba mais no tópico [Delegados e lambdas](delegates-lambdas.md).

## <a name="generics"></a>Genéricos

Os genéricos permitem que o programador introduza um *parâmetro de tipo* ao criar suas classes, o que permite que o código do cliente (os usuários do tipo) especifiquem o tipo exato a ser usado no lugar do parâmetro de tipo.

Os genéricos foram adicionados para ajudar os programadores a implementar estruturas de dados genéricos. Antes da chegada, para que um tipo como o `List` tipo seja genérico, ele teria que trabalhar com elementos que eram do tipo `object` . Isso tinha vários problemas de desempenho e semânticos, juntamente com possíveis erros sutis de tempo de execução. Um erro de tempo de execução comum é quando uma estrutura de dados contém, por exemplo, inteiros e cadeias de caracteres, e um <xref:System.InvalidCastException> é lançado durante o processamento dos membros da lista.

O exemplo a seguir mostra a execução de um programa básico usando uma instância de tipos <xref:System.Collections.Generic.List%601>:

[!code-csharp[GenericsShort](../../samples/snippets/csharp/snippets/tour/GenericsShort.csx)]

Para obter mais informações, veja o tópico [Visão geral de tipos genéricos (Genéricos)](generics.md).

## <a name="async-programming"></a>Programação assíncrona

Programação assíncrona é um conceito de primeira classe no .NET, com suporte assíncrono no runtime, bibliotecas de estrutura e constructos da linguagem do .NET. Internamente, elas são baseadas em objetos (como `Task`) que aproveitam o sistema operacional para realizar trabalhos associados a E/S de modo tão eficiente quanto possível.

Para saber mais sobre programação assíncrona no .NET, comece com o tópico [Visão geral da assincronia](async.md).

## <a name="language-integrated-query-linq"></a>LINQ (Consulta Integrada à Linguagem)

O LINQ é um conjunto poderoso de recursos para C# e Visual Basic que permitem que você escreva um código declarativo simples para operar em dados. Os dados podem ser de várias formas (como objetos na memória, um banco de dados SQL ou um documento XML), mas o código LINQ que você escreve não difere para cada fonte de dados.

Para saber mais e ver alguns exemplos, consulte o artigo [visão geral do LINQ (consulta integrada à linguagem)](./linq/index.md) .

## <a name="native-interoperability"></a>Interoperabilidade nativa

Todos os sistemas operacionais incluem uma API (interface de programação de aplicativo) que fornece serviços de sistema. O .NET fornece várias maneiras de chamar essas APIs.

A principal maneira de fazer interoperabilidade nativa é via "invocação de plataforma" ou P/Invoke, de forma abreviada, que tem suporte em plataformas Linux e Windows. A maneira somente para Windows de se fazer interoperabilidade nativa é conhecida como "interoperabilidade COM", que é usada para trabalhar com [componentes COM](/cpp/atl/introduction-to-com) em código gerenciado. Ela foi desenvolvida com base na infraestrutura de P/Invoke, mas funciona de maneiras levemente diferentes.

A maioria do suporte de interoperabilidade do Mono (e, portanto, do Xamarin) para Java e Objective-C é criado da mesma forma, ou seja, eles usam os mesmos princípios.

Para obter mais informações sobre a interoperabilidade nativa, confira o artigo [Native interoperability](native-interop/index.md) (Interoperabilidade nativa).

## <a name="unsafe-code"></a>Código não seguro

Dependendo do suporte da linguagem, o CLR permite acessar a memória nativa e realizar aritmética de ponteiro por meio de código `unsafe`. Essas operações são necessárias para certos algoritmos e interoperabilidade do sistema. Embora poderoso, o uso de código não seguro não é recomendado a menos que seja necessário para fornecer interoperabilidade com APIs do sistema ou implementar um algoritmo mais eficiente. O código não seguro pode não ser executado da mesma maneira em ambientes diferentes e também perde os benefícios de um coletor de lixo e da segurança de tipos. Recomenda-se restringir e centralizar ao máximo o código não seguro, além de testar esse código detalhadamente.

O exemplo a seguir é uma versão modificada do `ToString()` método da classe `StringBuilder`. Ele ilustra como o uso do código `unsafe` pode implementar um algoritmo com eficiência movendo blocos de memória diretamente:

[!code-csharp[Unsafe](../../samples/snippets/csharp/snippets/tour/Unsafe.csx)]

## <a name="next-steps"></a>Próximas etapas

Se você estiver interessado em um tour pelos recursos do C#, confira [Tour do C#](../csharp/tour-of-csharp/index.md).

Se você estiver interessado em um tour pelos recursos do F#, veja o [Tour do F#](../fsharp/tour.md).

Se você deseja começar a escrever seu próprio código, viste [Introdução](get-started.md).

Para saber mais sobre componentes importantes do .NET, confira [Componentes de Arquitetura do .NET](components.md).
