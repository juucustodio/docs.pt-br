---
description: "Saiba mais sobre: BC32005: a instrução não pode encerrar um bloco fora de uma instrução ' If ' de linha"
title: A instrução não pode finalizar um bloco fora de uma instrução 'If' de linha
ms.date: 07/20/2015
f1_keywords:
- vbc32005
- bc32005
helpviewer_keywords:
- BC32005
ms.assetid: 4039f51b-e0ee-4789-a89b-45d06de06b5d
ms.openlocfilehash: afe856b2c2ea3fa1db029d35c5b876f5d67da411
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99731097"
---
# <a name="bc32005-statement-cannot-end-a-block-outside-of-a-line-if-statement"></a>BC32005: a instrução não pode encerrar um bloco fora de uma instrução ' If ' de linha

Uma `If` instrução de linha única contém várias instruções separadas por dois-pontos (:), uma das quais é uma `End` instrução para um bloco de controle fora da linha única `If` . `If`Instruções de linha única não usam a `End If` instrução.

 **ID do erro:** BC32005

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Mova a instrução de linha única para `If` fora do bloco de controle que contém a `End If` instrução.

## <a name="see-also"></a>Consulte também

- [Instrução If...Then...Else](../statements/if-then-else-statement.md)
