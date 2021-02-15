---
title: Encaminhamento de tipo no Common Language Runtime
description: O encaminhamento de tipo permite que você mova um tipo para outro assembly .NET sem precisar recompilar os aplicativos que usam o assembly original.
ms.date: 08/20/2019
helpviewer_keywords:
- assemblies [.NET], type forwarding
- type forwarding
ms.assetid: 51f8ffa3-c253-4201-a3d3-c4fad85ae097
dev_langs:
- csharp
- cpp
ms.openlocfilehash: cd166068993fb5d1a5164615de3926a06dda8098
ms.sourcegitcommit: 279fb6e8d515df51676528a7424a1df2f0917116
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92687667"
---
# <a name="type-forwarding-in-the-common-language-runtime"></a>Encaminhamento de tipo no Common Language Runtime

O encaminhamento de tipo permite que você mova um tipo para outro assembly sem ter que recompilar os aplicativos que usam o assembly original.  
  
 Por exemplo, suponha que um aplicativo use a `Example` classe em um assembly chamado *Utility.dll* . Os desenvolvedores de *Utility.dll* podem decidir refatorar o assembly e, no processo, eles podem mover a `Example` classe para outro assembly. Se a versão antiga do *Utility.dll* for substituída pela nova versão do *Utility.dll* e seu assembly complementar, o aplicativo que usa a `Example` classe falhará porque não consegue localizar a `Example` classe na nova versão do *Utility.dll* .  
  
 Os desenvolvedores de *Utility.dll* podem evitar isso Encaminhando solicitações para a `Example` classe, usando o <xref:System.Runtime.CompilerServices.TypeForwardedToAttribute> atributo. Se o atributo tiver sido aplicado à nova versão do *Utility.dll* , as solicitações para a `Example` classe serão encaminhadas para o assembly que agora contém a classe. O aplicativo existente continua a funcionar normalmente, sem recompilação.

## <a name="forward-a-type"></a>Encaminhar um tipo

 Há quatro etapas para encaminhar um tipo:  
  
1. Mova o código-fonte para o tipo do assembly original para o conjunto de destino.  

2. No assembly em que o tipo é usado para ser localizado, adicione um <xref:System.Runtime.CompilerServices.TypeForwardedToAttribute> para o tipo que foi movido. O código a seguir mostra o atributo para um tipo chamado `Example` que foi movido.  

   ```cpp  
    [assembly:TypeForwardedToAttribute(Example::typeid)]  
   ```

   ```csharp  
    [assembly:TypeForwardedToAttribute(typeof(Example))]  
   ```  

3. Compile o assembly que agora contém o tipo.  

4. Recompile o assembly onde o tipo estava localizado, com uma referência ao assembly que agora contém o tipo. Por exemplo, se você estiver Compilando um arquivo C# na linha de comando, use a opção [-Reference (opções do compilador C#)](../../csharp/language-reference/compiler-options/reference-compiler-option.md) para especificar o assembly que contém o tipo. Em C++, use a diretiva [#using](/cpp/preprocessor/hash-using-directive-cpp) no arquivo de origem para especificar o assembly que contém o tipo.  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.CompilerServices.TypeForwardedToAttribute>
- [Encaminhamento de tipo (C++/CLI)](/cpp/windows/type-forwarding-cpp-cli)
- [#using diretiva](/cpp/preprocessor/hash-using-directive-cpp)
