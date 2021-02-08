---
description: 'Saiba mais sobre: como ler de arquivos FEXT com vários formatos no Visual Basic'
title: 'Como: ler de arquivos de texto com vários formatos'
ms.date: 07/20/2015
helpviewer_keywords:
- TextFieldParser object, reading from a file
- TextFieldType enumeration
- My.Computer.FileSystem.WriteAllText method, parsing structured text files
- WriteAllText method [Visual Basic], parsing structured text files
- PeekChars method [Visual Basic], determining format of text
- reading text files [Visual Basic], multiple formats
- I/O [Visual Basic], reading text files
- text files [Visual Basic], reading
ms.assetid: 8d185eb2-79ca-42cd-95a7-d3ff44a5a0f8
ms.openlocfilehash: 90d981ad051fb395d57604434cf9ba6b74603e7d
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99797439"
---
# <a name="how-to-read-from-fext-files-with-multiple-formats-in-visual-basic"></a>Como: ler de arquivos FEXT com vários formatos no Visual Basic

O objeto <xref:Microsoft.VisualBasic.FileIO.TextFieldParser> fornece uma maneira fácil e eficiente de analisar arquivos de texto estruturados, como logs. É possível processar um arquivo com vários formatos usando o método `PeekChars` para determinar o formato de cada linha conforme você analisa por meio do arquivo.
  
### <a name="to-parse-a-text-file-with-multiple-formats"></a>Para analisar um arquivo de texto com vários formatos

1. Adicione um arquivo de texto chamado *testfile.txt* ao seu projeto. Adicione o seguinte conteúdo ao arquivo de texto:

    ```text
    Err  1001 Cannot access resource.
    Err  2014 Resource not found.
    Acc  10/03/2009User1      Administrator.
    Err  0323 Warning: Invalid access attempt.
    Acc  10/03/2009User2      Standard user.
    Acc  10/04/2009User2      Standard user.
    ```

2. Defina o formato esperado e o formato usado quando um erro é relatado. A última entrada em cada matriz é -1, portanto, supõe-se que o último campo tenha largura variável. Isso ocorre quando a última entrada na matriz é menor ou igual a 0.

     [!code-vb[VbFileIORead#4](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#4)]

3. Crie um novo objeto <xref:Microsoft.VisualBasic.FileIO.TextFieldParser>, definindo a largura e o formato.

     [!code-vb[VbFileIORead#5](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#5)]

4. Percorra as linhas, testando seus formatos antes da leitura.

     [!code-vb[VbFileIORead#6](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#6)]

5. Grave os erros no console.

     [!code-vb[VbFileIORead#7](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#7)]

## <a name="example"></a>Exemplo

Veja a seguir o exemplo completo que lê a partir do arquivo `testfile.txt` :

 [!code-vb[VbFileIORead#8](~/samples/snippets/visualbasic/VS_Snippets_VBCSharp/VbFileIORead/VB/Class1.vb#8)]

## <a name="robust-programming"></a>Programação robusta

As seguintes condições podem causar uma exceção:  
  
- Não é possível analisar uma linha usando o formato especificado (<xref:Microsoft.VisualBasic.FileIO.MalformedLineException>). A mensagem de exceção especifica a linha que está causando a exceção, enquanto a propriedade <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.ErrorLine%2A> é atribuída ao texto contido na linha.
- O arquivo especificado não existe (<xref:System.IO.FileNotFoundException>).
- Uma situação de confiança parcial na qual o usuário não tem permissões suficientes para acessar o arquivo. (<xref:System.Security.SecurityException>).
- O caminho é muito longo (<xref:System.IO.PathTooLongException>).
- O usuário não tem permissões suficientes para acessar o arquivo (<xref:System.UnauthorizedAccessException>).

## <a name="see-also"></a>Consulte também

- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser?displayProperty=nameWithType>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.PeekChars%2A>
- <xref:Microsoft.VisualBasic.FileIO.MalformedLineException>
- <xref:Microsoft.VisualBasic.FileIO.FileSystem.WriteAllText%2A>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.EndOfData%2A>
- <xref:Microsoft.VisualBasic.FileIO.TextFieldParser.TextFieldType%2A>
- [Como: ler de arquivos de texto separados por vírgula](how-to-read-from-comma-delimited-text-files.md)
- [Como: ler de arquivos de texto de largura fixa](how-to-read-from-fixed-width-text-files.md)
- [Analisando arquivos de texto com o objeto TextFieldParser](parsing-text-files-with-the-textfieldparser-object.md)
