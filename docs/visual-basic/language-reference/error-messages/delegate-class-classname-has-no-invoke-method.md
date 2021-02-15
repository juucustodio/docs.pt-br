---
description: "Saiba mais sobre: BC30220: a classe delegate ' <classname> ' não tem um método Invoke, portanto, uma expressão desse tipo não pode ser o destino de uma chamada de método"
title: Classe Delegate '<classname>' não tem nenhum método Invoke. Portanto, uma expressão desse tipo não pode ser o destino de uma chamada de método
ms.date: 07/20/2015
f1_keywords:
- vbc30220
- bc30220
helpviewer_keywords:
- BC30220
ms.assetid: 6be0d61c-f2f9-4f9b-ab90-8871a0d7206d
ms.openlocfilehash: c0d3f6e352a98e194b2c2ddca04bfa7254ec37a7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796620"
---
# <a name="bc30220-delegate-class-classname-has-no-invoke-method-so-an-expression-of-this-type-cannot-be-the-target-of-a-method-call"></a>BC30220: a classe delegate ' \<classname> ' não tem um método Invoke, portanto, uma expressão desse tipo não pode ser o destino de uma chamada de método

Uma chamada para `Invoke` por meio de um delegado falhou porque `Invoke` não está implementada na classe delegate.

 **ID do erro:** BC30220

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Certifique-se de que uma instância da classe delegate tenha sido criada com uma `Dim` instrução e que um procedimento tenha sido atribuído à instância delegada com o `AddressOf` operador.

2. Localize o código que implementa a classe delegada e verifique se ele implementa o `Invoke` procedimento.

## <a name="see-also"></a>Consulte também

- [Representantes](../../programming-guide/language-features/delegates/index.md)
- [Instrução Delegate](../statements/delegate-statement.md)
- [Operador AddressOf](../operators/addressof-operator.md)
- [Instrução Dim](../statements/dim-statement.md)
