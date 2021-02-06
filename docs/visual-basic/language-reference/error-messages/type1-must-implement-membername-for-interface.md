---
description: "Saiba mais sobre: BC30154: <type1> ' <typename> ' deve implementar ' <membername> ' para interface '<interfacename>"
title: <type1>'<typename>' deve implementar '<membername>' para interface '<interfacename>'
ms.date: 07/20/2015
f1_keywords:
- vbc30154
- bc30154
helpviewer_keywords:
- BC30154
ms.assetid: 259afdfa-3608-4760-adcb-88ec0da5020d
ms.openlocfilehash: fc47aaef0477638e0e1a566bca23e9c35cf514f9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99641135"
---
# <a name="bc30154-type1typename-must-implement-membername-for-interface-interfacename"></a>BC30154: \<type1> ' \<typename> ' deve implementar ' \<membername> ' para a interface ' \<interfacename> '

' \<typename> ' deve implementar ' \<membername> ' para a interface ' \<interfacename> '. A implementação da propriedade deve ter especificadores ' ReadOnly '/' WriteOnly ' correspondentes.

 Declarações de classe ou estrutura para implementar uma interface, mas não implementa um procedimento, propriedade ou evento definido pela interface. Todos os membros da interface devem ser implementados.

 **ID do erro:** BC30154

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Declare um membro com o mesmo nome e assinatura, conforme definido na interface. Certifique-se de incluir pelo menos `End Function` a `End Sub` instrução, ou `End Property` .

2. Adicione uma `Implements` cláusula ao final da `Function` instrução,, `Sub` `Property` ou `Event` . Por exemplo:

    ```vb
    Public Event ItHappened() Implements IBaseInterface.ItHappened
    ```

3. Ao implementar uma propriedade, verifique se o `ReadOnly` ou o `WriteOnly` é usado da mesma maneira que na definição da interface.

4. Ao implementar uma propriedade, declare `Get` e `Set` procedimentos, conforme apropriado.

## <a name="see-also"></a>Consulte também

- [Instrução Implements](../statements/implements-statement.md)
- [Interfaces](../../programming-guide/language-features/interfaces/index.md)
