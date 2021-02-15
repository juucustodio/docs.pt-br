---
description: Palavras-chave C#
title: Palavras-chave C#
ms.date: 03/07/2017
f1_keywords:
- cs.keywords
helpviewer_keywords:
- keywords [C#]
- C# language, keywords
- Visual C#, keywords
- '@ keyword'
ms.custom: updateeachrelease
ms.assetid: e929b0f2-4b92-4d37-8060-23d323b098ad
ms.openlocfilehash: 3991fc62d75982b395162e085f0adfcc6d3cfb9a
ms.sourcegitcommit: 30a686fd4377fe6472aa04e215c0de711bc1c322
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/10/2020
ms.locfileid: "94439632"
---
# <a name="c-keywords"></a>Palavras-chave C#

As palavras-chave são identificadores reservados predefinidos com significados especiais para o compilador. Elas não podem ser usadas como identificadores em seu programa, a não ser que incluam `@` como prefixo. Por exemplo, `@if` é um identificador válido, mas `if` não é porque `if` é uma palavra-chave.  
  
 A primeira tabela neste tópico lista as palavras-chave que são identificadores reservados em qualquer parte de um programa C#. A segunda tabela neste tópico lista as palavras-chave contextuais em C#. As palavras-chave contextuais têm significado especial somente em um contexto limitado de programa e podem ser usadas como identificadores fora de contexto. Em geral, à medida que novas palavras-chave são adicionadas na linguagem C#, elas são adicionadas como palavras-chave contextuais para evitar a interrupção de programas escritos em versões anteriores.  
  
|||||  
|---|---|---|---|  
|[resume](abstract.md)|[as](../operators/type-testing-and-cast.md#as-operator)|[base](base.md)|[bool](../builtin-types/bool.md)|  
|[break](break.md)|[byte](../builtin-types/integral-numeric-types.md)|[casos](switch.md)|[catch](try-catch.md)|  
|[char](../builtin-types/char.md)|[check](checked.md)|[class](class.md)|[const](const.md)|  
|[continua](continue.md)|[decimal](../builtin-types/floating-point-numeric-types.md)|[default](default.md)|[delegate](../builtin-types/reference-types.md)|  
|[do](do.md)|[double](../builtin-types/floating-point-numeric-types.md)|[senão](if-else.md)|[enumera](../builtin-types/enum.md)|  
|[event](event.md)|[explicita](../operators/user-defined-conversion-operators.md)|[extern](extern.md)|[false](../builtin-types/bool.md)|  
|[disso](try-finally.md)|[fixado](fixed-statement.md)|[float](../builtin-types/floating-point-numeric-types.md)|[for](for.md)|  
|[foreach](foreach-in.md)|[goto](goto.md)|[if](if-else.md)|[localiza](../operators/user-defined-conversion-operators.md)|  
|[Em](in.md)|[int](../builtin-types/integral-numeric-types.md)|[interface](interface.md)|[interno](internal.md)|
|[for](is.md)|[proprietário](lock-statement.md)|[longo](../builtin-types/integral-numeric-types.md)|[namespace](namespace.md)|
|[Novo](../operators/new-operator.md)|[null](null.md)|[object](../builtin-types/reference-types.md)|[operator](../operators/operator-overloading.md)|
|[fora](out.md)|[override](override.md)|[params](params.md)|[pessoal](private.md)|
|[protegidos](protected.md)|[público](public.md)|[leitura](readonly.md)|[ref](ref.md)|
|[exibir](return.md)|[sbyte](../builtin-types/integral-numeric-types.md)|[sealed](sealed.md)|[short](../builtin-types/integral-numeric-types.md)||
[sizeof](../operators/sizeof.md)|[stackalloc](../operators/stackalloc.md)|[static](static.md)|[cadeia de caracteres](../builtin-types/reference-types.md)|
|[struct](../builtin-types/struct.md)|[switch](switch.md)|[this](this.md)|[throw](throw.md)|
|[true](../builtin-types/bool.md)|[Tente](try-catch.md)|[typeof](../operators/type-testing-and-cast.md#typeof-operator)|[uint](../builtin-types/integral-numeric-types.md)|
|[ULONG](../builtin-types/integral-numeric-types.md)|[desmarcada](unchecked.md)|[UNSAFE](unsafe.md)|[ushort](../builtin-types/integral-numeric-types.md)|
|[using](using.md)|[virtuaisLUNs](virtual.md)|[void](../builtin-types/void.md)|[volatile](volatile.md)|
|[mesmo](while.md)|

## <a name="contextual-keywords"></a>Palavras-chave contextuais

 Uma palavra-chave contextual é usada para fornecer um significado específico no código, mas não é uma palavra reservada no C#. Algumas palavras-chave contextuais, como `partial` e `where`, têm significados especiais em dois ou mais contextos.  
  
||||  
|---|---|---|  
|[add](add.md)|[alias](extern-alias.md)|[ascending](ascending.md)|
|[async](async.md)|[await](../operators/await.md)|[by](by.md)|
|[descending](descending.md)|[dinâmico](../builtin-types/reference-types.md)|[equals](equals.md)|
|[from](from-clause.md)|[get](get.md)|[geral](../operators/namespace-alias-qualifier.md)|
|[grupo](group-clause.md)|[into](into.md)|[join](join-clause.md)|
|[permitindo](let-clause.md)|[nameof](../operators/nameof.md)|[notnull](../../programming-guide/generics/constraints-on-type-parameters.md#notnull-constraint)|
|[on](on.md)|[OrderBy](orderby-clause.md)|[Partial (tipo)](partial-type.md)|
|[Partial (método)](partial-method.md)|[remove](remove.md)|[select](select-clause.md)|
|[set](set.md)|[não gerenciado (restrição de tipo genérico)](../../programming-guide/generics/constraints-on-type-parameters.md#unmanaged-constraint)|[value](value.md)|
|[var](var.md)|[when (condição de filtro)](when.md)|[where (restrição de tipo genérico)](where-generic-type-constraint.md)|
|[where (cláusula de consulta)](where-clause.md)|[por](../operators/with-expression.md)|[yield](yield.md)|
  
## <a name="see-also"></a>Confira também

- [Referência de C#](../index.md)
