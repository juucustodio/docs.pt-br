---
description: 'Saiba mais sobre: BC30188: declaração esperada'
title: Declaração esperada
ms.date: 07/20/2015
f1_keywords:
- vbc30188
- bc30188
helpviewer_keywords:
- BC30188
ms.assetid: da6b1df3-fe6b-4415-88e6-0977e5189e0b
ms.openlocfilehash: b86c182fb9dc8ab7d624833136f0e87b072aed92
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99796659"
---
# <a name="bc30188-declaration-expected"></a>BC30188: declaração esperada

Uma instrução não declarativa, como uma instrução de atribuição ou loop, ocorre fora de qualquer procedimento. Somente declarações são permitidas para procedimentos externos.

 Como alternativa, um elemento de programação é declarado sem uma palavra-chave de declaração, como `Dim` ou `Const` .

 **ID do erro:** BC30188

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Mova a instrução Declaration para o corpo de um procedimento.

- Inicie a declaração com uma palavra-chave de declaração apropriada.

- Certifique-se de que uma palavra-chave de declaração não tenha sido digitada incorretamente.

## <a name="see-also"></a>Consulte também

- [Procedimentos](../../programming-guide/language-features/procedures/index.md)
- [Instrução Dim](../statements/dim-statement.md)
