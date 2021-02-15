---
description: 'Saiba mais sobre: instrução de estrutura'
title: Instrução Structure
ms.date: 05/12/2018
f1_keywords:
- vb.Structure
- Structure
helpviewer_keywords:
- user-defined types [Visual Basic], Structure statement
- compound data types [Visual Basic]
- Structure keyword [Visual Basic]
- Structure statement [Visual Basic]
- UDT (user-defined types)
- types [Visual Basic], user-defined
ms.assetid: 9bd1deea-2a89-4cdc-812c-6dcbb947c391
ms.openlocfilehash: 338abe359491f02c25bdb33d996fb639f58f8b35
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99741062"
---
# <a name="structure-statement"></a>Instrução Structure

Declara o nome de uma estrutura e apresenta a definição das variáveis, propriedades, eventos e procedimentos que a estrutura compreende.

## <a name="syntax"></a>Syntax

```vb
[ <attributelist> ] [ accessmodifier ] [ Shadows ] [ Partial ] _
Structure name [ ( Of typelist ) ]
    [ Implements interfacenames ]
    [ datamemberdeclarations ]
    [ methodmemberdeclarations ]
End Structure
```

## <a name="parts"></a>Partes

|Termo|Definição|
|---|---|
|`attributelist`|Opcional. Consulte a [lista de atributos](attribute-list.md).|
|`accessmodifier`|Opcional. Pode ser um dos seguintes:<br /><br /> -   [Publicada](../modifiers/public.md)<br />-   [Protected](../modifiers/protected.md)<br />-   [Público](../modifiers/friend.md)<br />-   [Pessoal](../modifiers/private.md)<br />- [Amigo protegido](../modifiers/protected-friend.md)<br/>- [Particular protegido](../modifiers/private-protected.md) <br /><br /> Consulte [níveis de acesso em Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md).|
|`Shadows`|Opcional. Consulte [Shadows](../modifiers/shadows.md).|
|`Partial`|Opcional. Indica uma definição parcial da estrutura. Consulte [parcial](../modifiers/partial.md).|
|`name`|Obrigatório. Nome desta estrutura. Consulte [nomes de elementos declarados](../../programming-guide/language-features/declared-elements/declared-element-names.md).|
|`Of`|Opcional. Especifica que esta é uma estrutura genérica.|
|`typelist`|Necessário se você usar a palavra-chave [of](of-clause.md) . Lista de parâmetros de tipo para esta estrutura. Consulte [lista de tipos](type-list.md).|
|`Implements`|Opcional. Indica que essa estrutura implementa os membros de uma ou mais interfaces. Consulte a [instrução Implements](implements-statement.md).|
|`interfacenames`|Necessário se você usar a `Implements` instrução. Os nomes das interfaces que essa estrutura implementa.|
|`datamemberdeclarations`|Obrigatório. Zero ou mais `Const` instruções,, `Dim` `Enum` ou `Event` declarando *membros de dados* da estrutura.|
|`methodmemberdeclarations`|Opcional. Zero ou mais declarações de `Function` `Operator` procedimentos,, `Property` ou `Sub` , que servem como *membros de método* da estrutura.|
|`End Structure`|Obrigatório. Encerra a `Structure` definição.|

## <a name="remarks"></a>Comentários

A `Structure` instrução define um tipo de valor composto que você pode personalizar. Uma *estrutura* é uma generalização do tipo definido pelo usuário (UDT) de versões anteriores do Visual Basic. Para obter mais informações, consulte [estruturas](../../programming-guide/language-features/data-types/structures.md).

As estruturas dão suporte a muitos dos mesmos recursos que as classes. Por exemplo, estruturas podem ter propriedades e procedimentos, elas podem implementar interfaces e podem ter construtores com parâmetros. No entanto, há diferenças significativas entre estruturas e classes em áreas como herança, declarações e uso. Além disso, as classes são tipos de referência e estruturas são tipos de valor. Para obter mais informações, consulte [estruturas e classes](../../programming-guide/language-features/data-types/structures-and-classes.md).

Você pode usar `Structure` somente no nível de namespace ou de módulo. Isso significa que o *contexto de declaração* para uma estrutura deve ser um arquivo de origem, namespace, classe, estrutura, módulo ou interface e não pode ser um procedimento ou bloco. Para obter mais informações, consulte [Contextos de declaração e níveis de acesso padrão](declaration-contexts-and-default-access-levels.md).

As estruturas assumem como padrão o acesso [Friend](../modifiers/friend.md) . Você pode ajustar seus níveis de acesso com os modificadores de acesso. Para obter mais informações, consulte [níveis de acesso em Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md).

## <a name="rules"></a>Regras

- **Aninhamento.** Você pode definir uma estrutura dentro de outra. A estrutura externa é chamada de *estrutura de contenção* e a estrutura interna é chamada de *estrutura aninhada*. No entanto, você não pode acessar os membros de uma estrutura aninhada por meio da estrutura que a contém. Em vez disso, você deve declarar uma variável do tipo de dados da estrutura aninhada.

- **Declaração de membro.** Você deve declarar todos os membros de uma estrutura. Um membro de estrutura não pode ser [protegido](../modifiers/protected.md) ou `Protected Friend` porque nada pode herdar de uma estrutura. No entanto, a estrutura em si pode ser `Protected` ou `Protected Friend` .
  
     Você pode declarar zero ou mais variáveis não compartilhadas ou eventos não compartilhados e não-personalizados em uma estrutura. Você não pode ter apenas constantes, propriedades e procedimentos, mesmo que algumas delas não sejam compartilhadas.

- **Inicialização.** Você não pode inicializar o valor de nenhum membro de dados não compartilhado de uma estrutura como parte de sua declaração. Você deve inicializar um membro de dados desse tipo por meio de um construtor com parâmetros na estrutura ou atribuir um valor ao membro depois de ter criado uma instância da estrutura.

- **Herda.** Uma estrutura não pode herdar de nenhum tipo diferente de <xref:System.ValueType> , do qual todas as estruturas herdam. Em particular, uma estrutura não pode herdar de outra.

     Você não pode usar a [instrução Inherits](inherits-statement.md) em uma definição de estrutura, até mesmo para especificar <xref:System.ValueType> .

- **Implementação.** Se a estrutura usar a [instrução Implements](implements-statement.md), você deverá implementar todos os membros definidos por cada interface especificada no `interfacenames` .

- **Propriedade padrão.** Uma estrutura pode especificar, no máximo, uma propriedade como sua *propriedade padrão*, usando o modificador [padrão](../modifiers/default.md) . Para obter mais informações, consulte [padrão](../modifiers/default.md).

## <a name="behavior"></a>Comportamento

- **Nível de acesso.** Dentro de uma estrutura, você pode declarar cada membro com seu próprio nível de acesso. Todos os membros da estrutura assumem como padrão o acesso [público](../modifiers/public.md) . Observe que, se a estrutura em si tiver um nível de acesso mais restrito, isso restringe automaticamente o acesso a seus membros, mesmo se você ajustar seus níveis de acesso com os modificadores de acesso.

- **Com.** Uma estrutura está no escopo em todo o namespace, classe, estrutura ou módulo que o contém.

     O escopo de cada membro da estrutura é a estrutura inteira.

- **Existência.** Uma estrutura não tem, em si, um tempo de vida. Em vez disso, cada instância dessa estrutura tem um tempo de vida independente de todas as outras instâncias.

     O tempo de vida de uma instância começa quando é criado por uma [nova cláusula Operator](../operators/new-operator.md) . Ele termina quando o tempo de vida da variável que a mantém termina.

     Não é possível estender o tempo de vida de uma instância de estrutura. Uma aproximação da funcionalidade de estrutura estática é fornecida por um módulo. Para obter mais informações, consulte [instrução de módulo](module-statement.md).

     Os membros da estrutura têm tempos de vida, dependendo de como e onde eles são declarados. Para obter mais informações, consulte "Lifetime" na [declaração de classe](class-statement.md).

- **Aprovação.** O código fora de uma estrutura deve qualificar o nome de um membro com o nome dessa estrutura.

     Se o código dentro de uma estrutura aninhada fizer uma referência não qualificada a um elemento de programação, Visual Basic pesquisará o elemento primeiro na estrutura aninhada e, em seguida, na estrutura que a contém, e assim por diante, para o elemento contendo mais externo. Para obter mais informações, consulte [referências a elementos declarados](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md).

- **Consumo de memória.** Assim como acontece com todos os tipos de dados compostos, você não pode calcular com segurança o consumo total de memória de uma estrutura adicionando as alocações de armazenamento nominal de seus membros. Além disso, você não pode supor com segurança que a ordem de armazenamento na memória é igual à sua ordem de declaração. Se você precisar controlar o layout de armazenamento de uma estrutura, poderá aplicar o <xref:System.Runtime.InteropServices.StructLayoutAttribute> atributo à `Structure` instrução.

## <a name="example"></a>Exemplo

O exemplo a seguir usa a `Structure` instrução para definir um conjunto de dados relacionados para um funcionário. Ele mostra o uso de `Public` , `Friend` e `Private` Membros para refletir a sensibilidade dos itens de dados. Ele também mostra os membros de evento, propriedade e procedimento.

[!code-vb[VbVbalrStatements#57](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbalrStatements/VB/Class1.vb#57)]

Para obter mais informações sobre como usar `Structure` s, consulte [variável de estrutura](../../programming-guide/language-features/data-types/structure-variables.md).

## <a name="see-also"></a>Consulte também

- [Instrução Class](class-statement.md)
- [Instrução Interface](interface-statement.md)
- [Instrução Module](module-statement.md)
- [Instrução Dim](dim-statement.md)
- [Instrução Const](const-statement.md)
- [Instrução Enum](enum-statement.md)
- [Instrução Event](event-statement.md)
- [Instrução Operator](operator-statement.md)
- [Instrução Property](property-statement.md)
- [Estruturas e classes](../../programming-guide/language-features/data-types/structures-and-classes.md)
