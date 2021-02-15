---
title: Tipos de exceção
description: 'Saiba como definir e usar tipos de exceção F #.'
ms.date: 05/16/2016
ms.openlocfilehash: 8b4ceec31a2d68abbcd025812ffeeefc0c090efb
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90557223"
---
# <a name="exception-types"></a>Tipos de exceção

Há duas categorias de exceções em F #: tipos de exceção do .NET e tipos de exceção F #. Este tópico descreve como definir e usar tipos de exceção F #.

## <a name="syntax"></a>Sintaxe

```fsharp
exception exception-type of argument-type
```

## <a name="remarks"></a>Comentários

Na sintaxe anterior, o *tipo* de exceção é o nome de um novo tipo de exceção F #, e o *tipo de argumento* representa o tipo de um argumento que pode ser fornecido quando você gera uma exceção desse tipo. Você pode especificar vários argumentos usando um tipo de tupla para o *tipo de argumento*.

Uma definição típica para uma exceção F # é semelhante à seguinte.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5501.fs)]

Você pode gerar uma exceção desse tipo usando a `raise` função, da seguinte maneira.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5502.fs)]

Você pode usar um tipo de exceção F # diretamente nos filtros em uma `try...with` expressão, conforme mostrado no exemplo a seguir.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet5503.fs)]

O tipo de exceção que você define com a `exception` palavra-chave em F # é um novo tipo que herda de `System.Exception` .

## <a name="see-also"></a>Confira também

- [Tratamento de Exceção](index.md)
- [Exceções: a função `raise`](the-raise-function.md)
- [Hierarquia de exceções](../../../standard/exceptions/index.md)
