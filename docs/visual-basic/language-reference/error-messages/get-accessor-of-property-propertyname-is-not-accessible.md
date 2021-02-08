---
description: "Saiba mais sobre: BC31103: o acessador ' Get ' da propriedade ' <propertyname> ' não está acessível"
title: O acessador 'Get' da propriedade '<propertyname>' não está acessível
ms.date: 07/20/2015
f1_keywords:
- vbc31103
- bc31103
helpviewer_keywords:
- BC31103
ms.assetid: 3c346c32-7669-4b04-841d-7a9df9cb703e
ms.openlocfilehash: 3517bc7ec512ec99909539eb4d7cf3fafe9016fa
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796126"
---
# <a name="bc31103-get-accessor-of-property-propertyname-is-not-accessible"></a>BC31103: o acessador ' Get ' da propriedade ' \<propertyname> ' não está acessível

Uma instrução tenta recuperar o valor de uma propriedade quando ela não tem acesso ao procedimento da propriedade `Get` .

 Se a [instrução Get](../statements/get-statement.md) for marcada com um nível de acesso mais restritivo do que sua [instrução Property](../statements/property-statement.md), uma tentativa de ler o valor da propriedade poderá falhar nos seguintes casos:

- A `Get` instrução é marcada como [particular](../modifiers/private.md) e o código de chamada está fora da classe ou estrutura na qual a propriedade é definida.

- A `Get` instrução é marcada como [protegida](../modifiers/protected.md) e o código de chamada não está na classe ou estrutura na qual a propriedade é definida, nem em uma classe derivada.

- A `Get` instrução é marcada como [Friend](../modifiers/friend.md) e o código de chamada não está no mesmo assembly no qual a propriedade é definida.

 **ID do erro:** BC31103

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Se você tiver controle do código-fonte que define a propriedade, considere declarar o `Get` procedimento com o mesmo nível de acesso que a própria propriedade.

- Se você não tem controle do código-fonte que define a propriedade ou deve restringir o nível de `Get` acesso do procedimento mais do que a propriedade em si, tente mover a instrução que lê o valor da propriedade para uma região de código que tenha melhor acesso à propriedade.

## <a name="see-also"></a>Consulte também

- [Procedimentos de propriedade](../../programming-guide/language-features/procedures/property-procedures.md)
- [Como declarar uma propriedade com níveis de acesso mistos](../../programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)
