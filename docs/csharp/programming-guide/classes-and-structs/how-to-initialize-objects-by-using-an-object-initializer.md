---
title: Como inicializar objetos usando um inicializador de objeto-guia de programação C#
description: Saiba como usar inicializadores de objeto para inicializar objetos de tipo em C# sem invocar um construtor. Use um inicializador de objeto para definir um tipo anônimo.
ms.date: 12/20/2018
helpviewer_keywords:
- object initializers [C#], how to use
- objects [C#], initializing
ms.topic: how-to
ms.custom: contperf-fy21q2
ms.assetid: 4b75ebb2-2e29-43de-929c-d736a8f27ce6
ms.openlocfilehash: 0c2d38713a1fdefd922234a02e23518c0f00add5
ms.sourcegitcommit: d0990c1c1ab2f81908360f47eafa8db9aa165137
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/15/2020
ms.locfileid: "97512776"
---
# <a name="how-to-initialize-objects-by-using-an-object-initializer-c-programming-guide"></a>Como inicializar objetos usando um inicializador de objeto (guia de programação C#)

Você pode usar os inicializadores de objeto para inicializar objetos de tipo de maneira declarativa, sem invocar explicitamente um construtor para o tipo.  
  
Os exemplos a seguir mostram como usar os inicializadores de objeto com objetos nomeados. O compilador processa inicializadores de objeto acessando primeiro o construtor de instância sem parâmetros e, em seguida, processando as inicializações de membro. Portanto, se o construtor sem parâmetros for declarado como `private` na classe, os inicializadores de objeto que exigem acesso público falharão.
  
Se você estiver definindo um tipo anônimo, é necessário usar um inicializador de objeto. Para obter mais informações, consulte [como retornar subconjuntos de propriedades de elemento em uma consulta](how-to-return-subsets-of-element-properties-in-a-query.md).  
  
## <a name="example"></a>Exemplo  

O exemplo a seguir mostra como inicializar um novo tipo `StudentName`, usando inicializadores de objeto. Este exemplo define as propriedades de `StudentName` tipo:
  
[!code-csharp[InitializerObjectExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/HowToObjectInitializers.cs#HowToObjectInitializers)]  

Os inicializadores de objeto podem ser usados para definir indexadores em um objeto. O exemplo a seguir define uma classe `BaseballTeam` que usa um indexador para obter e definir jogadores em posições diferentes. O inicializador pode atribuir jogadores com base na abreviação da posição ou no número usado para cada scorecard de beisebol de posição:

[!code-csharp[InitializerIndexerExample](../../../../samples/snippets/csharp/programming-guide/classes-and-structs/object-collection-initializers/HowToIndexInitializer.cs#HowToIndexInitializer)]  

## <a name="see-also"></a>Consulte também

- [Guia de programação C#](../index.md)
- [Inicializadores de objeto e coleção](object-and-collection-initializers.md)
