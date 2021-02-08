---
description: 'Saiba mais sobre: Friend (Visual Basic)'
title: Friend
ms.date: 07/20/2015
f1_keywords:
- vb.Friend
helpviewer_keywords:
- Friend keyword [Visual Basic]
- Friend access modifier
- Friend keyword [Visual Basic], syntax
- Protected Friend keyword combination
- Friend keyword [Visual Basic], and Protected
ms.assetid: b664605e-1c79-4728-b996-aa59c50846bc
ms.openlocfilehash: ef2444555c05d6a4b24048316e282d269d4b7f1b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99774584"
---
# <a name="friend-visual-basic"></a>Friend (Visual Basic)

Especifica que um ou mais elementos de programação declarados são acessíveis somente de dentro do assembly que contém sua declaração.  
  
## <a name="remarks"></a>Comentários  

 Em muitos casos, você deseja que elementos de programação, como classes e estruturas, sejam usados pelo assembly inteiro, não apenas pelo componente que os declara. No entanto, talvez você não queira que eles fiquem acessíveis pelo código fora do assembly (por exemplo, se o aplicativo for proprietário). Se você quiser limitar o acesso a um elemento dessa forma, você pode declará-lo usando o `Friend` modificador.  
  
 O código em outras classes, estruturas e módulos que são compilados para o mesmo assembly pode acessar todos os `Friend` elementos nesse assembly.  
  
 `Friend` o acesso é geralmente o nível preferencial para os elementos de programação de um aplicativo e `Friend` é o nível de acesso padrão de uma interface, um módulo, uma classe ou uma estrutura.  
  
 Você pode usar `Friend` somente no nível do módulo, da interface ou do namespace. Portanto, o contexto de declaração de um `Friend` elemento deve ser um arquivo de origem, um namespace, uma interface, um módulo, uma classe ou uma estrutura; ele não pode ser um procedimento.  

> [!NOTE]
> Você também pode usar o modificador de acesso [Friend protegido](protected-friend.md) , que torna um membro de classe acessível de dentro dessa classe, de classes derivadas e do mesmo assembly no qual a classe é definida. Para restringir o acesso a um membro de dentro de sua classe e de classes derivadas no mesmo assembly, use o modificador de acesso [protegido privado](private-protected.md) .

 Para obter uma comparação entre `Friend` o e os outros modificadores de acesso, consulte [níveis de acesso em Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md).  
  
> [!NOTE]
> Você pode especificar que outro assembly é um assembly Friend, que permite que ele acesse todos os tipos e membros marcados como `Friend` . Para obter mais informações, consulte [Assemblies amigáveis](../../../standard/assembly/friend.md).

## <a name="example"></a>Exemplo  

 A classe a seguir usa o `Friend` modificador para permitir que outros elementos de programação dentro do mesmo assembly acessem determinados membros.  
  
 [!code-vb[VbVbalrAccessModifiers#1](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/vbvbalraccessmodifiers/vb/class1.vb#1)]  
  
## <a name="usage"></a>Uso  

 Você pode usar o `Friend` modificador nestes contextos:  
  
 [Instrução Class](../statements/class-statement.md)  
  
 [Instrução Const](../statements/const-statement.md)  
  
 [Instrução Declare](../statements/declare-statement.md)  
  
 [Instrução Delegate](../statements/delegate-statement.md)  
  
 [Instrução Dim](../statements/dim-statement.md)  
  
 [Instrução Enum](../statements/enum-statement.md)  
  
 [Instrução Event](../statements/event-statement.md)  
  
 [Instrução Function](../statements/function-statement.md)  
  
 [Instrução Interface](../statements/interface-statement.md)  
  
 [Instrução Module](../statements/module-statement.md)  
  
 [Instrução Property](../statements/property-statement.md)  
  
 [Instrução Structure](../statements/structure-statement.md)  
  
 [Instrução Sub](../statements/sub-statement.md)  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Runtime.CompilerServices.InternalsVisibleToAttribute>
- [Público](public.md)
- [Protected](protected.md)
- [Privado](private.md)
- [Particular protegido](./private-protected.md)
- [Amigo Protegido](./protected-friend.md)
- [Níveis de acesso no Visual Basic](../../programming-guide/language-features/declared-elements/access-levels.md)
- [Procedimentos](../../programming-guide/language-features/procedures/index.md)
- [Estruturas](../../programming-guide/language-features/data-types/structures.md)
- [Objetos e classes](../../programming-guide/language-features/objects-and-classes/index.md)
