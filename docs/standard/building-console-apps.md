---
description: 'Saiba mais sobre: aplicativos de console no .NET'
title: Criar aplicativos de console no .NET
ms.date: 03/30/2017
helpviewer_keywords:
- .NET, creating console applications
- application development [.NET], console
- console applications
ms.assetid: c21fb997-9f0e-40a5-8741-f73bba376bd8
ms.openlocfilehash: 9ebc0fbdc71cf0b6d30a07fc8a375899c5f55d52
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99676203"
---
# <a name="console-apps-in-net"></a>Aplicativos de console no .NET

Os aplicativos .NET podem usar a <xref:System.Console?displayProperty=nameWithType> classe para ler caracteres e gravar caracteres no console. Os dados do console são lidos a partir do fluxo de entrada padrão, os dados para o console são gravados no fluxo de saída padrão e os dados de erro do console são gravados no fluxo de saída de erro padrão. Esses fluxos são automaticamente associados ao console quando o aplicativo é iniciado e são apresentados como as propriedades <xref:System.Console.In%2A>, <xref:System.Console.Out%2A> e <xref:System.Console.Error%2A>, respectivamente.

O valor da propriedade <xref:System.Console.In%2A?displayProperty=nameWithType> é um objeto <xref:System.IO.TextReader?displayProperty=nameWithType>, ao passo que os valores das propriedades <xref:System.Console.Out%2A?displayProperty=nameWithType> e <xref:System.Console.Error%2A?displayProperty=nameWithType> são objetos <xref:System.IO.TextWriter?displayProperty=nameWithType>. Você pode associar essas propriedades com fluxos que não representam o console, tornando possível apontar para o fluxo em um local diferente de entrada ou saída. Por exemplo, você pode redirecionar a saída para um arquivo ao definir a propriedade <xref:System.Console.Out%2A?displayProperty=nameWithType> para um <xref:System.IO.StreamWriter?displayProperty=nameWithType> que encapsula um <xref:System.IO.FileStream?displayProperty=nameWithType> pelo método <xref:System.Console.SetOut%2A?displayProperty=nameWithType>. As propriedades <xref:System.Console.In%2A?displayProperty=nameWithType> e <xref:System.Console.Out%2A?displayProperty=nameWithType> não precisam fazer referência ao mesmo fluxo.

> [!NOTE]
> Para mais informações sobre a compilação de aplicativos de console, incluindo exemplos em C #, Visual Basic e C++, consulte a documentação da classe <xref:System.Console>.

Se o console não existir, por exemplo, em um aplicativo Windows Forms, a saída gravada no fluxo de saída padrão não será visível, pois não há nenhum console no qual gravar as informações. A gravação de informações em um console inacessível não gera uma exceção. (Você sempre pode alterar o tipo de aplicativo para **aplicativo de console**, por exemplo, nas páginas de propriedades do projeto no Visual Studio).

A classe **System.Console** tem métodos que podem ler caracteres individuais ou linhas inteiras do console. Outros métodos convertem dados e cadeias de formato e gravam as cadeias formatadas no console. Para obter mais informações sobre cadeias de caracteres de formatação, consulte [tipos de formatação](base-types/formatting-types.md).

> [!TIP]
> Nos aplicativos de console falta uma bomba de mensagem iniciada por padrão. Portanto, as chamadas do console para os temporizadores do Microsoft Win32 podem falhar.

## <a name="see-also"></a>Consulte também

- <xref:System.Console?displayProperty=nameWithType>
- [Formatar tipos](base-types/formatting-types.md)
