---
title: Exemplos de invocação de plataforma
description: Consulte um exemplo de invocação de plataforma que demonstra como definir e chamar a função MessageBox no User32.dll.
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- examples [.NET Framework], platform invoke
- unmanaged functions
- COM interop, platform invoke
- platform invoke, examples
- interoperation with unmanaged code, platform invoke
- DLL functions
ms.assetid: 15926806-f0b7-487e-93a6-4e9367ec689f
ms.openlocfilehash: 3b626061a579e089f92f2bf7de7f83f7db5bd184
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96268879"
---
# <a name="platform-invoke-examples"></a>Exemplos de invocação de plataforma

Os exemplos a seguir demonstram como definir e chamar a função **MessageBox** na User32.dll, passando uma cadeia de caracteres simples como um argumento. Nos exemplos, o campo <xref:System.Runtime.InteropServices.DllImportAttribute.CharSet?displayProperty=nameWithType> é definido como **Auto** para permitir que a plataforma de destino determine a largura de caractere e o marshaling da cadeia de caracteres.  
  
 [!code-cpp[Conceptual.Interop.PInvoke#1](../../../samples/snippets/cpp/VS_Snippets_CLR/Conceptual.Interop.PInvoke/cpp/Example.cpp#1)]
 [!code-csharp[Conceptual.Interop.PInvoke#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.Interop.PInvoke/cs/Example1.cs#1)]
 [!code-vb[Conceptual.Interop.PInvoke#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.Interop.PInvoke/vb/Example1.vb#1)]  
  
 Para obter exemplos adicionais, consulte [Marshaling de dados com invocação de plataforma](marshaling-data-with-platform-invoke.md).  
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.InteropServices.DllImportAttribute>
- [Criando protótipos em código gerenciado](creating-prototypes-in-managed-code.md)
- [Especificando um conjunto de caracteres](specifying-a-character-set.md)
