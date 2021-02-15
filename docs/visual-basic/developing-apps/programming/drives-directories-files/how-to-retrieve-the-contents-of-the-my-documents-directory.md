---
description: 'Saiba mais sobre: como recuperar o conteúdo do diretório meus documentos no Visual Basic'
title: 'Como: recuperar o conteúdo do diretório Meus Documentos'
ms.date: 07/20/2015
helpviewer_keywords:
- My Documents directory
ms.assetid: 26560d01-7dda-4457-8e95-21db23d71aea
ms.openlocfilehash: e9e6ffc202332bd8d1849ef886fd4e7d6cc46a54
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797387"
---
# <a name="how-to-retrieve-the-contents-of-the-my-documents-directory-in-visual-basic"></a>Como recuperar o conteúdo do diretório Meus Documentos no Visual Basic

O objeto <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories> pode ser usado para ler na maioria do diretórios de **Todos os Usuários**, como **Meus Documentos** ou **Área de Trabalho**.  
  
### <a name="to-read-from-the-my-documents-folder"></a>Para ler na pasta Meus Documentos  
  
- Use o método `ReadAllText` para ler o texto de cada arquivo em um diretório específico. O código a seguir especifica um diretório e um arquivo e, em seguida, usa o método `ReadAllText` para lê-los na cadeia de caracteres denominada `patients`.  
  
     [!code-vb[VbVbcnMyFileSystem#15](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbVbcnMyFileSystem/VB/Class1.vb#15)]  
  
## <a name="see-also"></a>Confira também

- <xref:Microsoft.VisualBasic.FileIO.SpecialDirectories>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.ReadAllText%2A>
