---
title: Artigos de instruções (Guia de C#)
description: Uma coleção de dicas rápidas e exemplos de código curtos e focados
ms.date: 12/20/2017
ms.openlocfilehash: 26d3931ff3b4ecfcc052c3ace25a09801f84c505
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537399"
---
# <a name="how-to-c"></a>Instruções (C#)

Na seção como do guia do C#, você pode encontrar respostas rápidas para perguntas comuns. Em alguns casos, os artigos podem ser listados em várias seções. Queremos facilitar que sejam localizados por vários caminhos de pesquisa.

## <a name="general-c-concepts"></a>Conceitos gerais de C#

Há várias dicas e truques que são práticas de desenvolvedor C# comuns:

- [Inicializar objetos usando um inicializador de objeto](../programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer.md).
- [Aprenda as diferenças entre passar um struct e uma classe para um método](../programming-guide/classes-and-structs/how-to-know-the-difference-passing-a-struct-and-passing-a-class-to-a-method.md).
- [Use a sobrecarga de operador](../language-reference/operators/operator-overloading.md).
- [Implemente e chame um método de extensão personalizado](../programming-guide/classes-and-structs/how-to-implement-and-call-a-custom-extension-method.md).
- Até mesmo os programadores C# podem querer [usar o `My` namespace de Visual Basic](../programming-guide/namespaces/how-to-use-the-my-namespace.md).
- [Crie um novo método para um tipo `enum` usando métodos de extensão](../programming-guide/classes-and-structs/how-to-create-a-new-method-for-an-enumeration.md).

### <a name="class-and-struct-members"></a>Membros de classe e struct

As classes e os structs são criados para implementar seu programa. Essas técnicas são comumente usadas durante a gravação de classes ou structs.

- [Declare propriedades implementadas automaticamente](../programming-guide/classes-and-structs/how-to-implement-a-lightweight-class-with-auto-implemented-properties.md).
- [Declare e use propriedades de leitura/gravação](../programming-guide/classes-and-structs/how-to-declare-and-use-read-write-properties.md).
- [Defina constantes](../programming-guide/classes-and-structs/how-to-define-constants.md).
- [Substitua o método `ToString` para fornecer saída de cadeia de caracteres](../programming-guide/classes-and-structs/how-to-override-the-tostring-method.md).
- [Definir propriedades abstratas](../programming-guide/classes-and-structs/how-to-define-abstract-properties.md).
- [Use os recursos de documentação para documentar seu código](../programming-guide/xmldoc/how-to-use-the-xml-documentation-features.md).
- [Implemente membros de interface explicitamente](../programming-guide/interfaces/how-to-explicitly-implement-interface-members.md) para manter a interface pública concisa.
- [Implemente explicitamente membros de duas interfaces](../programming-guide/interfaces/how-to-explicitly-implement-members-of-two-interfaces.md).

### <a name="working-with-collections"></a>Trabalhando com coleções

Esses artigos ajudam você a trabalhar com coleções de dados.

- [Inicializar um dicionário com um inicializador de coleção](../programming-guide/classes-and-structs/how-to-initialize-a-dictionary-with-a-collection-initializer.md).

## <a name="working-with-strings"></a>Trabalhando com cadeias de caracteres

As cadeias de caracteres são o tipo de dados fundamental usado para exibir ou manipular texto. Esses artigos demonstram práticas comuns com cadeias de caracteres.

- [Comparar cadeias de caracteres](compare-strings.md).
- [Modifique o conteúdo da cadeia de caracteres](modify-string-contents.md).
- [Determine se uma cadeia de caracteres representa um número](../programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md).
- [Use `String.Split` para separar as cadeias de caracteres](parse-strings-using-split.md).
- [Junte várias cadeias de caracteres em uma](concatenate-multiple-strings.md).
- [Pesquise texto em uma cadeia de caracteres](search-strings.md).

## <a name="convert-between-types"></a>Conversão entre tipos

Talvez seja necessário converter um objeto em um tipo diferente.

- [Determine se uma cadeia de caracteres representa um número](../programming-guide/strings/how-to-determine-whether-a-string-represents-a-numeric-value.md).
- [Converta entre cadeias de caracteres que representam números hexadecimais e o número](../programming-guide/types/how-to-convert-between-hexadecimal-strings-and-numeric-types.md).
- [Converta uma cadeia de caracteres para um `DateTime`](../../standard/base-types/parsing-datetime.md).
- [Converta uma matriz de bytes em um int](../programming-guide/types/how-to-convert-a-byte-array-to-an-int.md).
- [Converta uma cadeia de caracteres em um número](../programming-guide/types/how-to-convert-a-string-to-a-number.md).
- [Use a correspondência de padrões, os operadores `as` e `is` para converter para um tipo diferente com segurança](safely-cast-using-pattern-matching-is-and-as-operators.md).
- [Define as conversões de tipo personalizado](../language-reference/operators/user-defined-conversion-operators.md).
- [Determine se um tipo é um tipo de valor anulável](../language-reference/builtin-types/nullable-value-types.md#how-to-identify-a-nullable-value-type).
- [Converta entre tipos de valor anuláveis e não anuláveis](../language-reference/builtin-types/nullable-value-types.md#conversion-from-a-nullable-value-type-to-an-underlying-type).

## <a name="equality-and-ordering-comparisons"></a>Comparações de ordem e igualdade

É possível criar tipos que definem suas próprias regras de igualdade ou definem uma ordem natural entre os objetos desse tipo.

- [Testar a igualdade com base em referência](../programming-guide/statements-expressions-operators/how-to-test-for-reference-equality-identity.md).
- [Defina a igualdade com base em valor para um tipo](../programming-guide/statements-expressions-operators/how-to-define-value-equality-for-a-type.md).

## <a name="exception-handling"></a>Tratamento de exceções

Programas .NET relatam que os métodos não concluíram seu trabalho com sucesso ao lançar exceções. Nesses artigos, você aprenderá a trabalhar com exceções.

- [Trate exceções usando `try` e `catch`](../programming-guide/exceptions/how-to-handle-an-exception-using-try-catch.md).
- [Limpe recursos usando as `finally` cláusulas](../programming-guide/exceptions/how-to-execute-cleanup-code-using-finally.md).
- [Recupere com base em exceções não CLS (Common Language Specification)](../programming-guide/exceptions/how-to-catch-a-non-cls-exception.md).

## <a name="delegates-and-events"></a>Representantes e eventos

Representantes e eventos fornecem uma capacidade para estratégias que envolve blocos de código acoplados livremente.

- [Declare, crie uma instância e use delegados](../programming-guide/delegates/how-to-declare-instantiate-and-use-a-delegate.md).
- [Combine delegados multicast](../programming-guide/delegates/how-to-combine-delegates-multicast-delegates.md).

Os eventos fornecem um mecanismo para publicar ou assinar notificações.

- [Assine e cancele a assinatura de eventos](../programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).
- [Implemente eventos declarados nas interfaces](../programming-guide/events/how-to-implement-interface-events.md).
- [Conformidade com as diretrizes do .net quando seu código publica eventos](../programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md).
- [Gere eventos definidos nas classes de base de classes derivadas](../programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md).
- [Implemente acessadores de eventos personalizados](../programming-guide/events/how-to-implement-custom-event-accessors.md).

## <a name="linq-practices"></a>Práticas do LINQ

O LINQ permite que você grave códigos para consultar qualquer fonte de dados compatível com o padrão de expressão de consulta do LINQ. Esses artigos o ajudarão a entender o padrão e trabalhar com diferentes fontes de dados.

- [Consulte uma coleção](../programming-guide/concepts/linq/how-to-query-an-arraylist-with-linq.md).
- [Use expressões lambda em uma consulta](../programming-guide/statements-expressions-operators/how-to-use-lambda-expressions-in-a-query.md).
- [Use `var` nas expressões de consulta](../programming-guide/classes-and-structs/how-to-use-implicitly-typed-local-variables-and-arrays-in-a-query-expression.md).
- [Retorne subconjuntos de propriedades de elementos em uma consulta](../programming-guide/classes-and-structs/how-to-return-subsets-of-element-properties-in-a-query.md).
- [Grave consultas com filtragem complexa](../../standard/linq/write-queries-complex-filtering.md).
- [Classifique os elementos de uma fonte de dados](../../standard/linq/sort-elements.md).
- [Classifique os elementos em múltiplas chaves](../../standard/linq/sort-elements-multiple-keys.md).
- [Controle o tipo de uma projeção](../../standard/linq/control-type-projection.md).
- [Conte as ocorrências de um valor em uma sequência de origem](../programming-guide/concepts/linq/how-to-count-occurrences-of-a-word-in-a-string-linq.md).
- [Calcule valores intermediários](../../standard/linq/calculate-intermediate-values.md).
- [Mescle dados de várias fontes](../programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md).
- [Encontre a diferença de conjunto entre duas sequências](../programming-guide/concepts/linq/how-to-find-the-set-difference-between-two-lists-linq.md).
- [Depure resultados de consultas vazios](../../standard/linq/debug-empty-query-results-sets.md).
- [Adicione métodos personalizados a consultas LINQ](../programming-guide/concepts/linq/how-to-add-custom-methods-for-linq-queries.md).

## <a name="multiple-threads-and-async-processing"></a>Threads múltiplos e processamento assíncrono

Programas modernos geralmente usam operações assíncronas. Esses artigos o ajudarão a aprender a usar essas técnicas.

- [Melhore o desempenho assíncrono usando `System.Threading.Tasks.Task.WhenAll`](../programming-guide/concepts/async/index.md).
- [Faça várias solicitações da Web paralelamente usando `async` e `await`](../programming-guide/concepts/async/index.md).
- [Use um pool de thread](../../standard/threading/the-managed-thread-pool.md#using-the-thread-pool).

## <a name="command-line-args-to-your-program"></a>Argumentos da linha de comando para o programa

Geralmente, os programas de C# têm argumentos da linha de comando. Esses artigos o ensinam a acessar e processar esses argumentos da linha de comando.

- [Recupere todos os argumentos da linha de comando com `for`](../programming-guide/main-and-command-args/how-to-display-command-line-arguments.md).
