---
description: '##define – Referência de C#'
title: '##define – Referência de C#'
ms.date: 06/30/2018
f1_keywords:
- '#define'
helpviewer_keywords:
- '#define directive [C#]'
ms.assetid: 23638b8f-779c-450e-b600-d55682de7d01
ms.openlocfilehash: 961c20c091a4a6d7da421d94500abd41d2d60a5b
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91160496"
---
# <a name="define-c-reference"></a>#define (Referência de C#)

Use `#define` para definir um símbolo. Quando você usa o símbolo como a expressão passada para a diretiva [#if](./preprocessor-if.md), a expressão será avaliada como `true`, conforme mostra o exemplo a seguir:  

 ```csharp
 #define DEBUG
 ```
  
## <a name="remarks"></a>Comentários  
  
> [!NOTE]
> A diretiva `#define` não pode ser usada para declarar valores constantes como normalmente é feito em C e C++. As constantes em C# são mais bem definidas como membros estáticos de uma classe ou struct. Se você tiver várias dessas constantes, considere criar uma classe "Constantes" separada para guardá-las.  
  
 Os símbolos podem ser usados para especificar condições para compilação. É possível testar o símbolo com [#if](./preprocessor-if.md) ou [#elif](./preprocessor-elif.md). Você também pode usar o <xref:System.Diagnostics.ConditionalAttribute> para executar uma compilação condicional.  
  
 É possível definir um símbolo, mas não é possível atribuir um valor a um símbolo. A diretiva `#define` deve ser exibida no arquivo antes de usar as instruções que também não são diretivas de pré-processador.  
  
 Você também pode definir um símbolo com a opção [-definir](../compiler-options/define-compiler-option.md) compilador. É possível excluir um símbolo com [#undef](./preprocessor-undef.md).  
  
 Um símbolo definido com `-define` ou com `#define` não entra em conflito com uma variável do mesmo nome. Ou seja, um nome de variável não deve ser passado para uma diretiva de pré-processador e um símbolo apenas pode ser avaliado por uma diretiva de pré-processador.  
  
 O escopo de um símbolo criado usando `#define` é o arquivo no qual o símbolo foi definido.  
  
 Como mostra o exemplo a seguir, é necessário colocar as diretivas `#define` na parte superior do arquivo.  
  
```csharp  
#define DEBUG  
//#define TRACE  
#undef TRACE  
  
using System;  
  
public class TestDefine  
{  
    static void Main()  
    {  
#if (DEBUG)  
        Console.WriteLine("Debugging is enabled.");  
#endif  
  
#if (TRACE)  
     Console.WriteLine("Tracing is enabled.");  
#endif  
    }  
}  
// Output:  
// Debugging is enabled.  
```  
  
 Para obter um exemplo de como excluir um símbolo, consulte [#undef](./preprocessor-undef.md).  
  
## <a name="see-also"></a>Confira também

- [Referência do C#](../index.md)
- [Guia de programação C#](../../programming-guide/index.md)
- [Diretivas de pré-processador do C#](./index.md)
- [const](../keywords/const.md)
- [Como: compilar condicionalmente com Trace e Debug](../../../framework/debug-trace-profile/how-to-compile-conditionally-with-trace-and-debug.md)
- [#undef](./preprocessor-undef.md)
- [#if](./preprocessor-if.md)
