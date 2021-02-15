---
description: "Saiba mais sobre: BC30617: instruções ' module ' só podem ocorrer em nível de arquivo ou de namespace"
title: Instruções 'Module' só podem ocorrer no nível de namespace ou arquivo
ms.date: 07/20/2015
f1_keywords:
- bc30617
- vbc30617
helpviewer_keywords:
- BC30617
ms.assetid: 5e9de8e5-d26b-4fb2-9e28-814413fe9cef
ms.openlocfilehash: f5c3ea0cd1c08fb0243043ae50e707e2c59b00f2
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99795775"
---
# <a name="bc30617-module-statements-can-occur-only-at-file-or-namespace-level"></a>BC30617: instruções ' module ' só podem ocorrer em nível de arquivo ou de namespace

`Module` as instruções devem aparecer na parte superior do arquivo de origem imediatamente após `Option` e `Imports` instruções, atributos globais e declarações de namespace, mas antes de todas as outras declarações.

 **ID do erro:** BC30617

## <a name="to-correct-this-error"></a>Para corrigir este erro

- Mova a `Module` instrução para a parte superior da sua declaração de namespace ou arquivo de origem.

## <a name="see-also"></a>Consulte também

- [Instrução Module](../statements/module-statement.md)
