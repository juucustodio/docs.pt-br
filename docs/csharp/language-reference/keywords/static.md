---
description: Modificador static – Referência de C#
title: Modificador static – Referência de C#
ms.date: 09/25/2020
f1_keywords:
- static
- static_CSharpKeyword
helpviewer_keywords:
- static keyword [C#]
ms.assetid: 5509e215-2183-4da3-bab4-6b7e607a4fdf
ms.openlocfilehash: 239163fc2f91ccbfe8b1c111a358db87d36a8308
ms.sourcegitcommit: 4d45bda8cd9558ea8af4be591e3d5a29360c1ece
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2020
ms.locfileid: "91654633"
---
# <a name="static-c-reference"></a>static (Referência de C#)

Esta página aborda a `static` palavra-chave do modificador. A `static` palavra-chave também faz parte da [`using static`](using-static.md) diretiva.

Use o modificador `static` para declarar um membro estático que pertença ao próprio tipo, em vez de um objeto específico. O `static` modificador pode ser usado para declarar `static` classes. Em classes, interfaces e structs, você pode adicionar o `static` modificador a campos, métodos, propriedades, operadores, eventos e construtores. O `static` modificador não pode ser usado com indexadores ou finalizadores. Para obter mais informações, consulte [classes estáticas e membros de classe estática](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md).

A partir do C# 8,0, você pode adicionar o `static` modificador a uma [função local](../../programming-guide/classes-and-structs/local-functions.md). Uma função local estática não pode capturar variáveis locais ou estado de instância.

A partir do C# 9,0, você pode adicionar o `static` modificador a uma [expressão lambda](../operators/lambda-expressions.md) ou a um [método anônimo](../operators/delegate-operator.md). Um método lambda ou anônimo estático não pode capturar variáveis locais ou estado de instância.

## <a name="example---static-class"></a>Exemplo-classe estática

A seguinte classe é declarada como `static` e contém apenas métodos `static`:

[!code-csharp[csrefKeywordsModifiers#18](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#18)]

Uma constante ou declaração de tipo é implicitamente um `static` membro. Um `static` membro não pode ser referenciado por meio de uma instância. Em vez disso, ele é referenciado por meio do nome do tipo. Por exemplo, considere a seguinte classe:

[!code-csharp[csrefKeywordsModifiers#19](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#19)]

Para fazer referência ao `static` membro `x` , use o nome totalmente qualificado, `MyBaseC.MyStruct.x` , a menos que o membro seja acessível do mesmo escopo:

```csharp
Console.WriteLine(MyBaseC.MyStruct.x);
```

Embora uma instância de uma classe contenha uma cópia separada de todos os campos de instância da classe, há apenas uma cópia de cada `static` campo.

Não é possível usar [`this`](this.md) para referenciar `static` métodos ou acessadores de propriedade.

Se a `static` palavra-chave for aplicada a uma classe, todos os membros da classe deverão ser `static` .

Classes, interfaces e `static` classes podem ter `static` construtores. Um `static` Construtor é chamado em algum ponto entre quando o programa é iniciado e a classe é instanciada.

> [!NOTE]
> A palavra-chave `static` tem utilizações mais limitadas do que no C++. Para comparar com a palavra-chave do C++, consulte [Storage classes (C++)](/cpp/cpp/storage-classes-cpp#static) (Classes de armazenamento (C++)).

Para demonstrar `static` os membros, considere uma classe que representa um funcionário da empresa. Suponha que a classe contém um método para contar funcionários e um campo para armazenar o número de funcionários. O método e o campo não pertencem a uma instância de funcionário. Em vez disso, eles pertencem à classe de funcionários como um todo. Eles devem ser declarados como `static` membros da classe.

## <a name="example---static-field-and-method"></a>Exemplo-campo e método estáticos

Este exemplo lê o nome e a ID de um novo funcionário, incrementa o contador de funcionário em um e exibe as informações do novo funcionário e do novo número de funcionários. Este programa lê o número atual de funcionários do teclado.

[!code-csharp[csrefKeywordsModifiers#20](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#20)]  

## <a name="example---static-initialization"></a>Exemplo – inicialização estática

Este exemplo mostra que você pode inicializar um `static` campo usando outro `static` campo que ainda não está declarado. Os resultados serão indefinidos até que você atribua explicitamente um valor ao `static` campo.

[!code-csharp[csrefKeywordsModifiers#21](~/samples/snippets/csharp/VS_Snippets_VBCSharp/csrefKeywordsModifiers/CS/csrefKeywordsModifiers.cs#21)]  

## <a name="c-language-specification"></a>Especificação da linguagem C#

[!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]

## <a name="see-also"></a>Consulte também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Palavras-chave do C#](index.md)
- [Modificadores](index.md)
- [usando diretiva estática](using-static.md)
- [Classes static e membros de classes static](../../programming-guide/classes-and-structs/static-classes-and-static-class-members.md)
