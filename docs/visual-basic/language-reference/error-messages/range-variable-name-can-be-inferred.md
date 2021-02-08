---
description: 'Saiba mais sobre: BC36599: o nome da variável de intervalo pode ser inferido somente de um nome simples ou qualificado sem argumentos'
title: O nome da variável de intervalo só pode ser inferido a partir de um nome simples ou qualificado sem argumentos
ms.date: 07/20/2015
f1_keywords:
- vbc36599
- bc36599
helpviewer_keywords:
- BC36599
ms.assetid: 17763dbe-f74f-4ccb-8086-cb7e45ec4d12
ms.openlocfilehash: b729b6786f9b7803a794b9a4e786d94fa41a57ec
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792057"
---
# <a name="bc36599-range-variable-name-can-be-inferred-only-from-a-simple-or-qualified-name-with-no-arguments"></a>BC36599: o nome da variável de intervalo pode ser deduzido somente de um nome simples ou qualificado sem argumentos

Um elemento de programação que usa um ou mais argumentos é incluído em uma consulta LINQ. O compilador não pode inferir uma variável de intervalo desse elemento de programação.

**ID do erro:** BC36599

## <a name="to-correct-this-error"></a>Para corrigir este erro

Forneça um nome de variável explícito para o elemento de programação, conforme mostrado no código a seguir:

```vb
Dim query = From var1 In collection1
            Select VariableAlias= SampleFunction(var1), var1
```

## <a name="see-also"></a>Consulte também

- [Introdução a LINQ no Visual Basic](../../programming-guide/language-features/linq/introduction-to-linq.md)
- [Cláusula SELECT](../queries/select-clause.md)
