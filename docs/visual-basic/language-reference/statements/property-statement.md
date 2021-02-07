---
description: 'Saiba mais sobre: instrução de propriedade'
title: Instrução Property
ms.date: 05/12/2018
f1_keywords:
- vb.PropertySet
- vb.Property
- vb.PropertyGet
helpviewer_keywords:
- Property statement [Visual Basic]
- default modifier
- property procedures [Visual Basic], Property statements
- Property keyword [Visual Basic]
ms.assetid: 3155edaf-8ebd-45c6-9cef-11d5d2dc8d38
ms.openlocfilehash: 95f2ac1f993fc8698d2033dfe50d925cd55a7dc4
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741387"
---
# <a name="property-statement"></a>Instrução Property

Declara o nome de uma propriedade e os procedimentos de propriedade usados para armazenar e recuperar o valor da propriedade.

## <a name="syntax"></a>Syntax

```vb
[ <attributelist> ] [ Default ] [ accessmodifier ]
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ] [ Iterator ]
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]
    [ <attributelist> ] [ accessmodifier ] Get
        [ statements ]
    End Get
    [ <attributelist> ] [ accessmodifier ] Set ( ByVal value As returntype [, parameterlist ] )
        [ statements ]
    End Set
End Property
- or -
[ <attributelist> ] [ Default ] [ accessmodifier ]
[ propertymodifiers ] [ Shared ] [ Shadows ] [ ReadOnly | WriteOnly ]
Property name ( [ parameterlist ] ) [ As returntype ] [ Implements implementslist ]
```

## <a name="parts"></a>Partes

- `attributelist`

  Opcional. Lista de atributos que se aplicam a esta propriedade ou `Get` `Set` procedimento. Consulte a [lista de atributos](attribute-list.md).

- `Default`

  Opcional. Especifica que essa propriedade é a propriedade padrão para a classe ou estrutura na qual ela está definida. As propriedades padrão devem aceitar parâmetros e podem ser definidas e recuperadas sem especificar o nome da propriedade. Se você declarar a propriedade como `Default` , não poderá usar `Private` na propriedade ou em qualquer um de seus procedimentos de propriedade.

- `accessmodifier`

  Opcional na `Property` instrução e em no máximo uma das `Get` `Set` instruções e. Pode ser um dos seguintes:

  - [Público](../modifiers/public.md)

  - [Protected](../modifiers/protected.md)

  - [Friend](../modifiers/friend.md)

  - [Privado](../modifiers/private.md)

  - [Amigo Protegido](../modifiers/protected-friend.md)

  - [Particular protegido](../modifiers/private-protected.md)

  Consulte [níveis de acesso em Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md).

- `propertymodifiers`

  Opcional. Pode ser um dos seguintes:

  - [Sobrecargas](../modifiers/overloads.md)

  - [Substituições](../modifiers/overrides.md)

  - [Substituível](../modifiers/overridable.md)

  - [NotOverridable](../modifiers/notoverridable.md)

  - [MustOverride](../modifiers/mustoverride.md)

  - `MustOverride Overrides`

  - `NotOverridable Overrides`

- `Shared`

  Opcional. Consulte [compartilhado](../modifiers/shared.md).

- `Shadows`

  Opcional. Consulte [Shadows](../modifiers/shadows.md).

- `ReadOnly`

  Opcional. Consulte [ReadOnly](../modifiers/readonly.md).

- `WriteOnly`

  Opcional. Consulte [WriteOnly](../modifiers/writeonly.md).

- `Iterator`

  Opcional. Consulte [iterador](../modifiers/iterator.md).

- `name`

  Obrigatório. Nome da propriedade. Consulte [nomes de elementos declarados](../../programming-guide/language-features/declared-elements/declared-element-names.md).

- `parameterlist`

  Opcional. Lista de nomes de variáveis locais que representam os parâmetros dessa propriedade e possíveis parâmetros adicionais do `Set` procedimento. Consulte a [lista de parâmetros](parameter-list.md).

- `returntype`

  Obrigatório se `Option Strict` for `On` . Tipo de dados do valor retornado por essa propriedade.

- `Implements`

  Opcional. Indica que essa propriedade implementa uma ou mais propriedades, cada uma definida em uma interface implementada por essa propriedade que contém a classe ou a estrutura. Consulte a [instrução Implements](implements-statement.md).

- `implementslist`

  Necessário se `Implements` for fornecido. Lista de propriedades que estão sendo implementadas.

  `implementedproperty [ , implementedproperty ... ]`

  Cada `implementedproperty` uma tem a seguinte sintaxe e partes:

  `interface.definedname`

  |Parte|Descrição|
  |---|---|
  |`interface`|Obrigatórios. Nome de uma interface implementada por essa propriedade que contém a classe ou a estrutura.|
  |`definedname`|Obrigatório. Nome pelo qual a propriedade é definida `interface` .|

- `Get`

  Opcional. Obrigatório se a propriedade estiver marcada `ReadOnly` . Inicia um `Get` procedimento de propriedade que é usado para retornar o valor da propriedade.  A `Get` instrução não é usada com [Propriedades implementadas automaticamente](../../programming-guide/language-features/procedures/auto-implemented-properties.md).

- `statements`

  Opcional. Bloco de instruções a serem executadas dentro `Get` do `Set` procedimento ou.

- `End Get`

  Encerra o `Get` procedimento de propriedade.

- `Set`

  Opcional. Obrigatório se a propriedade estiver marcada `WriteOnly` . Inicia um `Set` procedimento de propriedade que é usado para armazenar o valor da propriedade.  A `Set` instrução não é usada com [Propriedades implementadas automaticamente](../../programming-guide/language-features/procedures/auto-implemented-properties.md).

- `End Set`

  Encerra o `Set` procedimento de propriedade.

- `End Property`

  Encerra a definição desta propriedade.

## <a name="remarks"></a>Comentários

A `Property` instrução apresenta a declaração de uma propriedade. Uma propriedade pode ter um `Get` procedimento (somente leitura), um `Set` procedimento (somente gravação) ou ambos (leitura-gravação). Você pode omitir `Get` o `Set` procedimento e ao usar uma propriedade implementada automaticamente. Para obter mais informações, consulte [Propriedades autoimplementadas](../../programming-guide/language-features/procedures/auto-implemented-properties.md).

Você pode usar `Property` somente no nível de classe. Isso significa que o *contexto de declaração* para uma propriedade deve ser uma classe, estrutura, módulo ou interface e não pode ser um arquivo de origem, namespace, procedimento ou bloco. Para obter mais informações, consulte [Contextos de declaração e níveis de acesso padrão](declaration-contexts-and-default-access-levels.md).

Por padrão, as propriedades usam acesso público. Você pode ajustar o nível de acesso de uma propriedade com um modificador de acesso na `Property` instrução e, opcionalmente, pode ajustar um de seus procedimentos de propriedade para um nível de acesso mais restritivo.

Visual Basic passa um parâmetro para o `Set` procedimento durante as atribuições de propriedade. Se você não fornecer um parâmetro para `Set` , o IDE (ambiente de desenvolvimento integrado) usará um parâmetro implícito chamado `value` . Esse parâmetro contém o valor a ser atribuído à propriedade. Normalmente, você armazena esse valor em uma variável local privada e retorna-o sempre que o `Get` procedimento é chamado.

## <a name="rules"></a>Regras

- **Níveis de acesso misto.** Se você estiver definindo uma propriedade de leitura/gravação, poderá opcionalmente especificar um nível de acesso diferente para o `Get` ou o `Set` procedimento, mas não ambos. Se você fizer isso, o nível de acesso do procedimento deverá ser mais restritivo do que o nível de acesso da propriedade. Por exemplo, se a propriedade for declarada `Friend` , você poderá declarar o `Set` procedimento `Private` , mas não `Public` .

  Se você estiver definindo uma `ReadOnly` `WriteOnly` propriedade ou, o procedimento de propriedade única ( `Get` ou `Set` , respectivamente) representará toda a propriedade. Você não pode declarar um nível de acesso diferente para tal procedimento, pois isso definiria dois níveis de acesso para a propriedade.

- **Tipo de retorno.** A `Property` instrução pode declarar o tipo de dados do valor que ele retorna. Você pode especificar qualquer tipo de dados ou o nome de uma enumeração, estrutura, classe ou interface.

  Se você não especificar `returntype` , a propriedade retornará `Object` .

- **Implementação.** Se essa propriedade usar a `Implements` palavra-chave, a classe ou estrutura que a contém deverá ter uma `Implements` instrução imediatamente após sua `Class` `Structure` instrução or. A `Implements` instrução deve incluir cada interface especificada em `implementslist` . No entanto, o nome pelo qual uma interface define o `Property` (in `definedname` ) não precisa ser igual ao nome dessa propriedade (em `name` ).

## <a name="behavior"></a>Comportamento

- **Retornando de um procedimento de propriedade.** Quando o `Get` `Set` procedimento ou retorna ao código de chamada, a execução continua com a instrução após a instrução que a invocou.

  As `Exit Property` `Return` instruções e causam uma saída imediata de um procedimento de propriedade. Qualquer número de `Exit Property` `Return` instruções and pode aparecer em qualquer lugar no procedimento, e você pode misturar `Exit Property` e `Return` demonstrativos.

- **Valor de retorno.** Para retornar um valor de um `Get` procedimento, você pode atribuir o valor ao nome da propriedade ou incluí-lo em uma `Return` instrução. O exemplo a seguir atribui o valor de retorno ao nome da propriedade `quoteForTheDay` e, em seguida, usa a `Exit Property` instrução a ser retornada.

  [!code-vb[VbVbalrStatements#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#27)]

  [!code-vb[VbVbalrStatements#28](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#28)]

  Se você usar `Exit Property` sem atribuir um valor ao `name` , o `Get` procedimento retornará o valor padrão para o tipo de dados da propriedade.

  A `Return` instrução ao mesmo tempo atribui o `Get` valor de retorno do procedimento e sai do procedimento. O exemplo a seguir mostra a isso.

  [!code-vb[VbVbalrStatements#27](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#27)]

  [!code-vb[VbVbalrStatements#29](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#29)]

## <a name="example"></a>Exemplo

O exemplo a seguir declara uma propriedade em uma classe.

[!code-vb[VbVbalrStatements#51](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#51)]

## <a name="see-also"></a>Consulte também

- [Propriedades autoimplementadas](../../programming-guide/language-features/procedures/auto-implemented-properties.md)
- [Objetos e classes](../../programming-guide/language-features/objects-and-classes/index.md)
- [Instrução Get](get-statement.md)
- [Instrução SET](set-statement.md)
- [Lista de parâmetros](parameter-list.md)
- [Default](../modifiers/default.md)
