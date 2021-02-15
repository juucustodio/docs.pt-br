---
description: "Saiba mais sobre: BC30002: o tipo ' <typename> ' não está definido"
title: O tipo '<typename>' não está definido
ms.date: 07/20/2015
f1_keywords:
- vbc30002
- bc30002
helpviewer_keywords:
- BC30002
ms.assetid: b0faf204-57fd-44de-8c05-9db027eea663
ms.openlocfilehash: 48ee0c38492769aea8c1be2e9d54eaa537e35766
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99641116"
---
# <a name="bc30002-type-typename-is-not-defined"></a>BC30002: tipo " \<typename> " não está definido

A instrução fez referência a um tipo que não foi definido. Você pode definir um tipo em uma instrução de declaração, como `Enum` ,, `Structure` `Class` ou `Interface` .

 **ID do erro:** BC30002

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Verifique se a definição de tipo e sua referência usam a mesma grafia.

- Certifique-se de que a definição de tipo seja acessível para a referência. Por exemplo, se o tipo estiver em outro módulo e tiver sido declarado `Private` , mova a definição de tipo para o módulo de referência ou declare-a `Public` .

- Certifique-se de que o namespace do tipo não seja redefinido no seu projeto. Se for, use a `Global` palavra-chave para qualificar totalmente o nome do tipo. Por exemplo, se um projeto definir um namespace chamado `System` , o <xref:System.Object?displayProperty=nameWithType> tipo não poderá ser acessado, a menos que seja totalmente qualificado com a `Global` palavra-chave: `Global.System.Object` .

- Se o tipo for definido, mas a biblioteca de objetos ou biblioteca de tipos na qual ele está definido não estiver registrada em Visual Basic, clique em **Adicionar referência** no menu **projeto** e selecione a biblioteca de objetos ou a biblioteca de tipos apropriada.

- Verifique se o tipo está em um assembly que faz parte do perfil de .NET Framework de destino. Para obter mais informações, consulte [Solução de problemas de erros de definição de destino do .NET Framework](/visualstudio/msbuild/troubleshooting-dotnet-framework-targeting-errors).

## <a name="see-also"></a>Consulte também

- [Namespaces no Visual Basic](../../programming-guide/program-structure/namespaces.md)
- [Instrução Enum](../statements/enum-statement.md)
- [Instrução Structure](../statements/structure-statement.md)
- [Instrução Class](../statements/class-statement.md)
- [Instrução Interface](../statements/interface-statement.md)
- [Gerenciando referências em um projeto](/visualstudio/ide/managing-references-in-a-project)
