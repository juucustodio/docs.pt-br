---
title: Interoperabilidade – Guia de Programação em C#
description: A interoperabilidade dá suporte a código não gerenciado ao lado do código que é executado no Common Language Runtime. Use esses recursos para entender as opções de interoperabilidade.
ms.date: 07/20/2015
helpviewer_keywords:
- COM interop
- interoperability
- platform invoke, accessing APIs with C#
- C# language, interoperability
ms.assetid: 238bb95a-e962-4026-bbd5-197055bdb8ee
ms.openlocfilehash: 84cdc16ccda7a5c629a90b0752071a98de81a9b4
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91178470"
---
# <a name="interoperability-c-programming-guide"></a>Interoperabilidade (Guia de Programação em C#)

A interoperabilidade permite que você mantenha e aproveite os investimentos existentes em código não gerenciado. O código que é executado sob o controle do CLR (Common Language Runtime) é chamado de *código gerenciado*, e o código que é executado fora do CLR é chamado de *código não gerenciado*. COM, COM+, componentes do C++, componentes do ActiveX e a API do Microsoft Windows são exemplos de código não gerenciado.  
  
O .NET permite a interoperabilidade com código não gerenciado por meio de serviços de invocação de plataforma, o <xref:System.Runtime.InteropServices> namespace, interoperabilidade de C++ e interoperabilidade com (INTEROP com).  
  
## <a name="in-this-section"></a>Nesta seção  

 [Visão geral sobre interoperabilidade](./interoperability-overview.md)  
 Descreve métodos para fins de interoperabilidade entre código gerenciado em C# e código não gerenciado.  
  
 [Como acessar objetos de interoperabilidade do Office usando recursos do C#](./how-to-access-office-onterop-objects.md)  
 Descreve os recursos que são introduzidos no Visual C# para facilitar a programação do Office.  
  
 [Como usar propriedades indexadas na programação para interoperabilidade COM](./how-to-use-indexed-properties-in-com-interop-rogramming.md)  
 Descreve como usar propriedades indexadas para acesso propriedades COM que têm parâmetros.  
  
 [Como usar invocação de plataforma para executar um arquivo WAV](./how-to-use-platform-invoke-to-play-a-wave-file.md)  
 Descreve como usar os serviços de invocação de plataforma para reproduzir um arquivo de som .wav no sistema operacional Windows.  
  
 [Passo a passo: programação do Office](./walkthrough-office-programming.md)  
 Mostra como criar uma planilha do Excel e um documento do Word com um link para a planilha.  
  
 [Exemplo de classe COM](./example-com-class.md)  
 Demonstra como expor uma classe C# como um objeto COM.  
  
## <a name="c-language-specification"></a>Especificação da Linguagem C#  

Para obter mais informações, veja [Noções básicas](~/_csharplang/spec/unsafe-code.md) na [Especificação da linguagem C#](/dotnet/csharp/language-reference/language-specification/introduction). A especificação da linguagem é a fonte definitiva para a sintaxe e o uso de C#.
  
## <a name="see-also"></a>Veja também

- <xref:System.Runtime.InteropServices.Marshal.ReleaseComObject%2A?displayProperty=nameWithType>
- [Guia de programação C#](../index.md)
- [Interoperação com código não gerenciado](../../../framework/interop/index.md)
- [Passo a passo: programação do Office](./walkthrough-office-programming.md)
