---
description: 'Saiba mais sobre: o uso da instância padrão de uma classe no construtor de classe pode levar à chamada recursiva infinita'
title: O uso de instância padrão de uma classe no construtor de classe pode levar a chamada recursiva infinita
ms.date: 07/20/2015
ms.assetid: 9645b47f-7de5-46d0-bb45-d5fdaa8aaa2a
ms.openlocfilehash: f65956c92f7d391aa77734d7afd5adf3bea1f906
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100475676"
---
# <a name="use-of-default-instance-of-a-class-in-the-class-constructor-could-lead-to-infinite-recursive-call"></a>O uso de instância padrão de uma classe no construtor de classe pode levar a chamada recursiva infinita

Uma instância padrão de uma classe foi usada no construtor da classe. Isso pode levar a uma chamada recursiva infinita, também conhecida como um loop infinito.  
  
## <a name="to-correct-this-error"></a>Para corrigir este erro  
  
- Remova a instância padrão do construtor de classe.  
  
## <a name="see-also"></a>Consulte também

- [Construtores](../programming-guide/concepts/object-oriented-programming.md#constructors)
