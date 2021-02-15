---
description: "Saiba mais sobre: BC30269: ' <methodname> ' tem várias definições com assinaturas idênticas"
title: "'<methodname>' tem várias definições com assinaturas idênticas"
ms.date: 07/20/2015
f1_keywords:
- vbc30269
- bc30269
helpviewer_keywords:
- BC30269
ms.assetid: 39489621-6617-4e5c-9b24-c2faf8273891
ms.openlocfilehash: 7364ee7a308fab96afce268ff0c92cd45717f1bd
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795801"
---
# <a name="bc30269-methodname-has-multiple-definitions-with-identical-signatures"></a>BC30269: ' \<methodname> ' tem várias definições com assinaturas idênticas

Uma `Function` `Sub` declaração de procedimento or usa o nome de procedimento idêntico e a lista de argumentos como uma declaração anterior. Uma causa possível é uma tentativa de sobrecarregar o procedimento original. Os procedimentos sobrecarregados devem ter diferentes listas de argumentos.

 **ID do erro:** BC30269

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Altere o nome do procedimento ou a lista de argumentos ou remova a declaração duplicada.

## <a name="see-also"></a>Consulte também

- [Referências a elementos declarados](../../programming-guide/language-features/declared-elements/references-to-declared-elements.md)
- [Considerações sobre procedimentos de sobrecarga](../../programming-guide/language-features/procedures/considerations-in-overloading-procedures.md)
