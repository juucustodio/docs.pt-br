---
description: "Saiba mais sobre: BC32025: as instruções ' #Region ' e ' #End Region ' não são válidas nos corpos de método/lambdas de várias linhas"
title: As instruções '#Region' e '#End Region' não são válidas dentro dos corpos/lambdas de várias linhas do método
ms.date: 07/20/2015
f1_keywords:
- bc32025
- vbc32025
helpviewer_keywords:
- BC32025
ms.assetid: 43707bf1-1c6b-4d82-b081-e5a17dca51c1
ms.openlocfilehash: 0746b9caf677699d6fbbf0c5a7063b1b33d86f3a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99792018"
---
# <a name="bc32025-region-and-end-region-statements-are-not-valid-within-method-bodiesmultiline-lambdas"></a>BC32025: as instruções ' #Region ' e ' #End Region ' não são válidas em corpos de método/lambdas de várias linhas

O `#Region` bloco deve ser declarado em um nível de classe, módulo ou namespace. Uma região recolhível pode incluir um ou mais procedimentos, mas não pode começar ou terminar dentro de um procedimento.

 **ID do erro:** BC32025

## <a name="to-correct-this-error"></a>Para corrigir este erro

1. Verifique se o procedimento anterior foi encerrado corretamente com `End Function` uma `End Sub` instrução ou.

2. Verifique se as `#Region` `#End Region` diretivas e estão no mesmo bloco de código.

## <a name="see-also"></a>Consulte também

- [#Region diretiva](../directives/region-directive.md)
