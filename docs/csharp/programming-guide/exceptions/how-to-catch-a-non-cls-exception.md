---
title: Como capturar uma exceção não compatível com CLS
description: Saiba como capturar uma exceção não-CLS. Consulte um exemplo de código e exiba recursos adicionais disponíveis.
ms.date: 07/20/2015
helpviewer_keywords:
- exceptions [C#], non-CLS
ms.assetid: db4630b3-5240-471a-b3a7-c7ff6ab31e8d
ms.openlocfilehash: db723cb1e29181e9462c5b423c66cdf8de659259
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91178665"
---
# <a name="how-to-catch-a-non-cls-exception"></a>Como capturar uma exceção não compatível com CLS

Algumas linguagens .NET, incluindo o C++/CLI, permite que os objetos lancem exceções que não derivam de <xref:System.Exception>. Essas exceções são chamadas de *exceções não CLS* ou *não exceções*. Em C#, não é possível gerar exceções que não sejam do CLS, mas você pode capturá-las de duas maneiras:  
  
- Em um bloco `catch (RuntimeWrappedException e)`.
  
     Por padrão, um assembly do Visual C# captura exceções não CLS como exceções encapsuladas. Use este método se você precisar de acesso à exceção original, que pode ser acessada por meio da propriedade <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A?displayProperty=nameWithType>. O procedimento, mais adiante neste tópico, explica como capturar exceções dessa maneira.  
  
- Em um bloco de captura geral (um bloco de captura sem um tipo de exceção especificado), que é colocado após todos os outros blocos `catch`.
  
     Use esse método quando desejar realizar alguma ação (como gravar em um arquivo de log) em resposta a exceções não CLS e você não precisa de acesso às informações de exceção. Por padrão, o Common Language Runtime encapsula todas as exceções. Para desabilitar esse comportamento, adicione esse atributo de nível de assembly em seu código, geralmente no arquivo AssemblyInfo.cs: `[assembly: RuntimeCompatibilityAttribute(WrapNonExceptionThrows = false)]`.  
  
### <a name="to-catch-a-non-cls-exception"></a>Para capturar uma exceção não CLS  
  
Em um bloco `catch(RuntimeWrappedException e)`, acesse a exceção original por meio da propriedade <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A?displayProperty=nameWithType>.  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir mostra como capturar uma exceção que não é do CLS, que foi gerada por uma biblioteca de classes escrita em C++/CLI. Observe que, neste exemplo, o código cliente C# sabe com antecedência que o tipo da exceção que está sendo gerada é um <xref:System.String?displayProperty=nameWithType>. Você pode converter a propriedade <xref:System.Runtime.CompilerServices.RuntimeWrappedException.WrappedException%2A?displayProperty=nameWithType> de volta a seu tipo original, desde que o tipo seja acessível por meio do código.  
  
```csharp
// Class library written in C++/CLI.
var myClass = new ThrowNonCLS.Class1();

try
{
    // throws gcnew System::String(  
    // "I do not derive from System.Exception!");  
    myClass.TestThrow();
}
catch (RuntimeWrappedException e)
{
    String s = e.WrappedException as String;
    if (s != null)
    {
        Console.WriteLine(s);
    }
}
```  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.CompilerServices.RuntimeWrappedException>
- [Exceções e manipulação de exceções](./index.md)
