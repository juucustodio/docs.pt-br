---
description: "Saiba mais sobre: BC30149: <type1> ' <typename> ' deve implementar ' <methodname> ' para interface '<interfacename>"
title: <type1>'<typename>' deve implementar '<methodname>' para interface '<interfacename>'
ms.date: 07/20/2015
f1_keywords:
- vbc30149
- bc30149
helpviewer_keywords:
- BC30149
ms.assetid: 29d1b7f4-dca7-478c-bbe7-c657f342c183
ms.openlocfilehash: 34635cbe5b8736d273d5972a1bb83aa3d975490b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675007"
---
# <a name="bc30149-type1typename-must-implement-methodname-for-interface-interfacename"></a>BC30149: \<type1> ' \<typename> ' deve implementar ' \<methodname> ' para a interface ' \<interfacename> '

Uma classe ou estrutura alega implementar uma interface, mas não implementa um procedimento definido pela interface. Todos os membros da interface devem ser implementados.

 **ID do erro:** BC30149

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Declare um procedimento com o mesmo nome e assinatura, conforme definido na interface. Certifique-se de incluir pelo menos `End Function` a `End Sub` instrução ou.

2. Adicione uma `Implements` cláusula ao final da `Function` `Sub` instrução ou. Por exemplo:

    ```vb
    Public Sub DoSomething() Implements IBaseInterface.DoSomething
    ```

## <a name="see-also"></a>Confira também

- [Instrução Implements](../statements/implements-statement.md)
- [Interfaces](../../programming-guide/language-features/interfaces/index.md)
