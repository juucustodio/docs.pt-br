---
description: 'Saiba mais sobre: não foi possível concluir a operação porque o diretório de destino está no diretório de origem'
title: Não foi possível concluir a operação porque o diretório de destino está sob o diretório de origem
ms.date: 07/20/2015
f1_keywords:
- vbrIO_CyclicOperation
ms.assetid: 850d3a24-5d51-4ac8-a912-630efcd75278
ms.openlocfilehash: 5fb0bf1d761faf9d3d0c64e8815e28e14841b1fd
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100463514"
---
# <a name="could-not-complete-operation-since-target-directory-is-under-source-directory"></a>Não foi possível concluir a operação porque o diretório de destino está sob o diretório de origem

Falha em uma operação cíclica. Ciclo de operações cíclicas e, portanto, não pode ser concluído. Por exemplo, o objeto A pode tentar herdar do objeto B, que por sua vez é herdado do objeto A.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Ao herdar, verifique se não há referências cíclicas.  
  
## <a name="see-also"></a>Consulte também

- [Tipos de erro](../programming-guide/language-features/error-types.md)
- [Usar pontos de interrupção no depurador do Visual Studio](/visualstudio/debugger/using-breakpoints)
