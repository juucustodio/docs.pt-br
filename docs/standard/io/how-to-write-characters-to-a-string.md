---
description: 'Saiba mais sobre: como escrever caracteres para uma cadeia de caracteres'
title: 'Como: gravar caracteres em uma cadeia de caracteres'
ms.date: 01/21/2019
dev_langs:
- csharp
- vb
helpviewer_keywords:
- data streams, writing characters to string
- writing characters to strings
- streams, writing characters to strings
- I/O [.NET], writing characters to strings
ms.assetid: 1222cbeb-0760-44bf-9888-914a2a37174b
ms.openlocfilehash: 86b19222d05e720904192d16f2082e8ae53a993f
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99675618"
---
# <a name="how-to-write-characters-to-a-string"></a>Como: gravar caracteres em uma cadeia de caracteres

Os exemplos de código a seguir gravam caracteres de forma síncrona ou assíncrona de uma matriz de caracteres em uma cadeia de caracteres.  
  
## <a name="example-write-characters-synchronously-in-a-console-app"></a>Exemplo: gravar caracteres de forma síncrona em um aplicativo de console  

 O exemplo a seguir usa um <xref:System.IO.StringWriter> para gravar cinco caracteres de forma síncrona em um objeto <xref:System.Text.StringBuilder>.
  
 [!code-csharp[Conceptual.StringBuilder#9](../../../samples/snippets/csharp/VS_Snippets_CLR/Conceptual.StringBuilder/cs/example2.cs#9)]
 [!code-vb[Conceptual.StringBuilder#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Conceptual.StringBuilder/vb/example2.vb#9)]  
  
## <a name="example-write-characters-asynchronously-in-a-wpf-app"></a>Exemplo: gravar caracteres de forma assíncrona em um aplicativo WPF

 O próximo exemplo é o código por trás de um aplicativo WPF. Na carga de janela, o exemplo lê todos os caracteres de forma assíncrona de um controle <xref:System.Windows.Controls.TextBox> e os armazena em uma matriz. Em seguida, ele grava cada letra ou caractere de espaço em branco de forma assíncrona em uma linha separada de um controle <xref:System.Windows.Controls.TextBlock>.  
  
 [!code-csharp[StreamReaderWriter](../../../samples/snippets/csharp/VS_Snippets_Wpf/StringReaderWriter/MainWindow.xaml.cs)]
 [!code-vb[StreamReaderWriter](../../../samples/snippets/visualbasic/VS_Snippets_Wpf/StringReaderWriter/MainWindow.xaml.vb)]  
  
## <a name="see-also"></a>Consulte também

- <xref:System.IO.StringWriter>  
- <xref:System.IO.StringWriter.Write%2A?displayProperty=nameWithType>  
- <xref:System.Text.StringBuilder>  
- [E/S de arquivo e de fluxo](index.md)  
- [E/S de arquivo assíncrona](asynchronous-file-i-o.md)  
- [Como: enumerar diretórios e arquivos](how-to-enumerate-directories-and-files.md)  
- [Como: ler e gravar em um arquivo de dados recém-criado](how-to-read-and-write-to-a-newly-created-data-file.md)  
- [Como: abrir e anexar a um arquivo de log](how-to-open-and-append-to-a-log-file.md)  
- [Como: ler texto de um arquivo](how-to-read-text-from-a-file.md)  
- [Como: gravar texto em um arquivo](how-to-write-text-to-a-file.md)  
- [Como: ler caracteres de uma cadeia de caracteres](how-to-read-characters-from-a-string.md)
