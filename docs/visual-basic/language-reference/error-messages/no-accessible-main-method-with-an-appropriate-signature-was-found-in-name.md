---
description: "Saiba mais sobre: BC30737: nenhum método ' Main ' acessível com uma assinatura apropriada foi encontrado em '<name>"
title: Nenhum método 'Main' acessível com uma assinatura apropriada foi encontrado em '<name>'
ms.date: 07/20/2015
f1_keywords:
- bc30737
- vbc30737
helpviewer_keywords:
- BC30737
ms.assetid: 3f40bacd-3fac-4741-b204-852f693d4340
ms.openlocfilehash: 1865d6baea824c435d276aa9c160bcd282abf4ae
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795645"
---
# <a name="bc30737-no-accessible-main-method-with-an-appropriate-signature-was-found-in-name"></a>BC30737: nenhum método ' Main ' acessível com uma assinatura apropriada foi encontrado em ' \<name> '

Os aplicativos de linha de comando devem ter um `Sub Main` definido. `Main` deve ser declarado como `Public Shared` se fosse definido em uma classe, ou como `Public` se estiver definido em um módulo.

 **ID do erro:** BC30737

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Defina um `Public Sub Main` procedimento para seu projeto. Declare-a como `Shared` If e only se você defini-la dentro de uma classe.

## <a name="see-also"></a>Consulte também

- [Estrutura de um programa Visual Basic](../../programming-guide/program-structure/structure-of-a-visual-basic-program.md)
- [Procedimentos](../../programming-guide/language-features/procedures/index.md)
