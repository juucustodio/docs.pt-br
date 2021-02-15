---
description: '#region – Referência de C#'
title: '#region – Referência de C#'
ms.date: 07/20/2015
f1_keywords:
- '#region'
helpviewer_keywords:
- '#region directive [C#]'
ms.assetid: 672c87d1-9771-4f64-ab3f-0ad3d4ffb2b4
ms.openlocfilehash: dcb806a213bea9d7c782eeddc712f1eb76257e80
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91186400"
---
# <a name="region-c-reference"></a>#region (Referência de C#)

`#region` permite especificar um bloco de código que você pode expandir ou recolher ao usar o recurso de [estrutura de tópicos](/visualstudio/ide/outlining) do editor de códigos. Em arquivos de código mais longos, é conveniente recolher ou ocultar uma ou mais regiões para que você possa se concentrar na parte do arquivo que está trabalhando no momento. O exemplo a seguir mostra como definir uma região:  
  
```csharp
#region MyClass definition  
public class MyClass
{  
    static void Main()
    {  
    }  
}  
#endregion  
```  
  
## <a name="remarks"></a>Comentários  

 Um bloco `#region` deverá ser encerrado com uma diretiva [#endregion](./preprocessor-endregion.md).  
  
 Um bloco `#region` não pode sobrepor um bloco [#if](./preprocessor-if.md). No entanto, um bloco `#region` pode ser aninhado em um bloco `#if` e um bloco `#if` pode ser aninhado em um bloco `#region`.  
  
## <a name="see-also"></a>Veja também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
