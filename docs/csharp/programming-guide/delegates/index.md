---
title: Delegados – Guia de Programação em C#
description: Um delegado em C# é um tipo que se refere a métodos com uma lista de parâmetros e um tipo de retorno. Delegados são usados para passar métodos como argumentos a outros métodos.
ms.date: 02/02/2021
helpviewer_keywords:
- C# language, delegates
- delegates [C#]
ms.assetid: 97de039b-c76b-4b9c-a27d-8c1e1c8d93da
ms.openlocfilehash: 86f7908501c075881786d16caffdd765b8aaf6b5
ms.sourcegitcommit: 4df8e005c074ceb1f978f007b222fe253be2baf3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/04/2021
ms.locfileid: "99548065"
---
# <a name="delegates-c-programming-guide"></a>Delegados (Guia de Programação em C#)

Um [delegado](../../language-reference/builtin-types/reference-types.md) é um tipo que representa referências aos métodos com lista de parâmetros e tipo de retorno específicos. Ao instanciar um delegado, você pode associar sua instância a qualquer método com assinatura e tipo de retorno compatíveis. Você pode invocar (ou chamar) o método através da instância de delegado.

Delegados são usados para passar métodos como argumentos a outros métodos. Os manipuladores de eventos nada mais são do que métodos chamados por meio de delegados. Ao criar um método personalizado, uma classe como um controle do Windows poderá chamá-lo quando um determinado evento ocorrer. O seguinte exemplo mostra uma declaração de delegado:

[!code-csharp[csProgGuideDelegates#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csProgGuideDelegates/CS/Delegates.cs#20)]

Qualquer método de qualquer classe ou struct acessível que corresponda ao tipo delegado pode ser atribuído ao delegado. O método pode ser estático ou de instância. Essa flexibilidade significa que você pode alterar programaticamente as chamadas de método ou conectar o novo código a classes existentes.

> [!NOTE]
> No contexto da sobrecarga de método, a assinatura de um método não inclui o valor retornado. No entanto, no contexto de delegados, a assinatura inclui o valor retornado. Em outras palavras, um método deve ter o mesmo tipo de retorno que o delegado.

Essa capacidade de se referir a um método como um parâmetro torna delegados ideais para definir métodos de retorno de chamada. Você pode escrever um método que Compare dois objetos em seu aplicativo. Esse método pode ser usado em um delegado para um algoritym de classificação. Como o código de comparação é separado da biblioteca, o método Sort pode ser mais geral.

[Ponteiros de função](~/_csharplang/proposals/csharp-9.0/function-pointers.md) foram adicionados ao C# 9 para cenários semelhantes, onde você precisa de mais controle sobre a Convenção de chamada. O código associado a um delegado é invocado usando um método virtual adicionado a um tipo delegate. Usando ponteiros de função, você pode especificar diferentes convenções.

## <a name="delegates-overview"></a>Visão geral de delegados

Os delegados possuem as seguintes propriedades:

- Representantes são semelhantes a ponteiros de função do C++, mas delegados são totalmente orientados a objeto e, ao contrário dos ponteiros de C++ para funções de membro, os delegados encapsulam uma instância do objeto e um método.
- Os delegados permitem que métodos sejam passados como parâmetros.
- Os delegados podem ser usados para definir métodos de retorno de chamada.
- Os delegados podem ser encadeados juntos; por exemplo, vários métodos podem ser chamados um único evento.
- Os métodos não precisam corresponder exatamente ao tipo delegado. Para obter mais informações, confira [Usando a variação delegados](../concepts/covariance-contravariance/using-variance-in-delegates.md).
- As expressões lambda são uma maneira mais concisa de escrever blocos de código embutidos. As expressões lambda (em determinados contextos) são compiladas para tipos delegados. Para saber mais sobre expressões lambda, confira o artigo sobre [expressões lambda](../../language-reference/operators/lambda-expressions.md).

## <a name="in-this-section"></a>Nesta seção

- [Usando delegados](./using-delegates.md)
- [Quando usar delegados em vez de interfaces (Guia de Programação em C#)](/previous-versions/visualstudio/visual-studio-2010/ms173173(v=vs.100))
- [Delegados com Métodos Nomeados vs. Métodos anônimos](./delegates-with-named-vs-anonymous-methods.md)
- [Usando variação em delegados](../concepts/covariance-contravariance/using-variance-in-delegates.md)
- [Como combinar delegados (delegados de multicast)](./how-to-combine-delegates-multicast-delegates.md)
- [Como declarar e usar um delegado e criar uma instância dele](./how-to-declare-instantiate-and-use-a-delegate.md)

## <a name="c-language-specification"></a>Especificação da Linguagem C#

Para obter mais informações, veja [Delegados](~/_csharplang/spec/delegates.md) na [Especificação da linguagem C#](/dotnet/csharp/language-reference/language-specification/introduction). A especificação da linguagem é a fonte definitiva para a sintaxe e o uso de C#.

## <a name="featured-book-chapters"></a>Capítulos do Livro em Destaque

- [Expressões lambda, eventos e delegados](/previous-versions/visualstudio/visual-studio-2008/ff518994(v=orm.10)) em [C# 3.0 Cookbook, Third Edition: More than 250 solutions for C# 3.0 programmers](/previous-versions/visualstudio/visual-studio-2008/ff518995(v=orm.10))
- [Delegados e eventos](/previous-versions/visualstudio/visual-studio-2008/ff652490(v=orm.10)) em [Learning C# 3.0: Master the fundamentals of C# 3.0](/previous-versions/visualstudio/visual-studio-2008/ff652493(v=orm.10))

## <a name="see-also"></a>Confira também

- <xref:System.Delegate>
- [Guia de programação C#](../index.md)
- [Eventos](../events/index.md)
