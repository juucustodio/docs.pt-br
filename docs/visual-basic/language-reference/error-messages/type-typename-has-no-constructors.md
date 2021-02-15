---
description: "Saiba mais sobre: BC30251: o tipo ' <typename> ' não tem construtores"
title: O tipo '<typename>' não tem construtores
ms.date: 07/20/2015
f1_keywords:
- bc30251
- vbc30251
helpviewer_keywords:
- BC30251
ms.assetid: aff3e1df-abe6-4bc0-9abc-a1e70514c561
ms.openlocfilehash: 32ae854e9f1b037a17d9c378ce7ee4a3f9b43ad2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99641168"
---
# <a name="bc30251-type-typename-has-no-constructors"></a>BC30251: o tipo ' \<typename> ' não tem construtores

Um tipo não suporta uma chamada para `Sub New()`. Uma possível causa é um compilador corrompido ou arquivo binário.

 **ID do erro:** BC30251

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Se o tipo estiver em um projeto diferente ou em um arquivo referenciado, reinstale o projeto ou arquivo.

2. Se o tipo estiver no mesmo projeto, recompile o assembly que contém o tipo.

3. Se o erro se repetir, reinstale o compilador Visual Basic.

4. Se o erro persistir, reúna informações sobre as circunstâncias e notifique o Microsoft Product Support Services.

## <a name="see-also"></a>Consulte também

- [Objetos e classes](../../programming-guide/language-features/objects-and-classes/index.md)
- [Fale conosco](/visualstudio/ide/feedback-options)
