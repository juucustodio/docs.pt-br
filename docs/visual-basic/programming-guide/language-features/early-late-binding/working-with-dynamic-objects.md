---
description: 'Saiba mais sobre: trabalhando com objetos dinâmicos (Visual Basic)'
title: Trabalhar com Objetos Dinâmicos
ms.date: 07/20/2015
helpviewer_keywords:
- dynamic objects [Visual Basic]
ms.assetid: bdee2a00-07ff-46f9-86dd-fdac9b99cc97
ms.openlocfilehash: 4991ae3deca908fc0b96760f50c85514df92714f
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100434388"
---
# <a name="working-with-dynamic-objects-visual-basic"></a>Trabalhando com objetos dinâmicos (Visual Basic)

Os objetos dinâmicos fornecem outra maneira, além do `Object` tipo, para associar tardiamente a um objeto em tempo de execução. Um objeto dinâmico expõe Membros como propriedades e métodos em tempo de execução usando interfaces dinâmicas que são definidas no <xref:System.Dynamic> namespace. Você pode usar as classes no <xref:System.Dynamic> namespace para criar objetos que funcionam com estruturas de dados que não correspondem a um tipo ou formato estático. Você também pode usar os objetos dinâmicos que são definidos em linguagens dinâmicas, como IronPython e IronRuby. Para obter exemplos que mostram como criar objetos dinâmicos ou usar um objeto dinâmico definido em uma linguagem dinâmica, consulte [Walkthrough: Criando e usando objetos dinâmicos](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md), <xref:System.Dynamic.DynamicObject> ou <xref:System.Dynamic.ExpandoObject> .  
  
 O Visual Basic é associado a objetos do tempo de execução de linguagem dinâmica e linguagens dinâmicas, como IronPython e IronRuby, usando a <xref:System.Dynamic.IDynamicMetaObjectProvider> interface. Exemplos de classes que implementam a `IDynamicMetaObjectProvider` interface são <xref:System.Dynamic.DynamicObject> as <xref:System.Dynamic.ExpandoObject> classes e.  
  
 Se uma chamada de ligação tardia for feita em um objeto que implementa a `IDynamicMetaObjectProvider` interface, o Visual Basic será associado ao objeto dinâmico usando essa interface. Se uma chamada de ligação tardia for feita em um objeto que não implementa a `IDynamicMetaObjectProvider` interface, ou se a chamada à `IDynamicMetaObjectProvider` interface falhar, o Visual Basic será associado ao objeto usando os recursos de associação tardia do tempo de execução de Visual Basic.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Dynamic.DynamicObject>
- <xref:System.Dynamic.ExpandoObject>
- [Walkthrough: Criando e usando objetos dinâmicos](../../../../csharp/programming-guide/types/walkthrough-creating-and-using-dynamic-objects.md)
- [Associação antecipada e tardia](index.md)
