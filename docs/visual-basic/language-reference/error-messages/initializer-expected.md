---
description: 'Saiba mais sobre: BC30996: inicializador esperado'
title: Inicializador esperado
ms.date: 07/20/2015
f1_keywords:
- vbc30996
- bc30996
helpviewer_keywords:
- BC30996
ms.assetid: 6e183fe0-8888-43ed-a062-01571079455f
ms.openlocfilehash: a9859dc319ec53cb42785d71b21447a097ce30f6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796048"
---
# <a name="bc30996-initializer-expected"></a>BC30996: inicializador esperado

Você tentou declarar uma instância de uma classe usando um inicializador de objeto no qual a lista de inicialização está vazia, conforme mostrado no exemplo a seguir.

 `' Not valid.`

 `' Dim aStudent As New Student With {}`

 Pelo menos um campo ou propriedade deve ser inicializado na lista de inicializadores, conforme mostrado no exemplo a seguir.

 `Dim aStudent As New Student With {.year = "Senior"}`

 **ID do erro:** BC30996

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Inicialize pelo menos um campo ou propriedade no inicializador ou não use um inicializador de objeto.

## <a name="see-also"></a>Consulte também

- [Inicializadores de objeto: tipos nomeados e anônimos](../../programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)
- [Como declarar um objeto usando um inicializador de objeto](../../programming-guide/language-features/objects-and-classes/how-to-declare-an-object-by-using-an-object-initializer.md)
