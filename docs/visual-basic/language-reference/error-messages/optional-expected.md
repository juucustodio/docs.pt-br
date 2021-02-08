---
description: "Saiba mais sobre: BC30202: ' optional ' esperado"
title: "'Optional' esperado"
ms.date: 07/20/2015
f1_keywords:
- bc30202
- vbc30202
helpviewer_keywords:
- BC30202
ms.assetid: 6f75060c-2db4-4a79-b5d1-5780c09a74cd
ms.openlocfilehash: 543dbf6226d4d298d46764ee506b55e770c91604
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795541"
---
# <a name="bc30202-optional-expected"></a>BC30202: ' optional ' esperado

Um argumento opcional em uma declaração de procedimento é seguido por um argumento necessário. Todos os argumentos após um argumento opcional também devem ser opcionais.

 **ID do erro:** BC30202

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Se o argumento se destinar a ser necessário, mova-o para preceder o primeiro argumento opcional na lista de argumentos.

- Se o argumento se destinar a ser opcional, use a `Optional` palavra-chave.

## <a name="see-also"></a>Consulte também

- [Parâmetros Opcionais](../../programming-guide/language-features/procedures/optional-parameters.md)
