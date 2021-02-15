---
title: Como gravar em um arquivo de texto – guia de programação C#
description: Saiba como escrever um arquivo de texto com C#. Consulte vários exemplos de código e exiba recursos adicionais disponíveis.
ms.date: 02/11/2021
f1_keywords:
- TextWriter.WriteLine
- StreamWriter.Close
helpviewer_keywords:
- files [C#], text files
- text, writing to files [C#]
ms.assetid: 2e99f184-d88b-4719-a7f1-d9ec482aa809
ms.topic: how-to
ms.custom: contperf-fy21q3
ms.openlocfilehash: ecc3ba73161d4f4571bbc6ae0c9aaa3337586ef7
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100475611"
---
# <a name="how-to-write-to-a-text-file-c-programming-guide"></a>Como gravar em um arquivo de texto (guia de programação C#)

Neste artigo, há vários exemplos que mostram várias maneiras de gravar texto em um arquivo. Os dois primeiros exemplos usam métodos de conveniência estáticos na <xref:System.IO.File?displayProperty=nameWithType> classe para gravar cada elemento de qualquer `IEnumerable<string>` e um `string` em um arquivo de texto. O terceiro exemplo mostra como adicionar texto a um arquivo quando você precisa processar cada linha individualmente ao gravar no arquivo. Nos três primeiros exemplos, você substitui todo o conteúdo existente no arquivo. O exemplo final mostra como acrescentar texto a um arquivo existente.

 Todos esses exemplos gravam literais de cadeia de caracteres em arquivos. Se você quiser formatar o texto gravado em um arquivo, use o método <xref:System.String.Format%2A> ou o recurso de [interpolação de cadeia de caracteres](../../language-reference/tokens/interpolated.md) do C#.

## <a name="write-a-collection-of-strings-to-a-file"></a>Gravar uma coleção de cadeias de caracteres em um arquivo

:::code language="csharp" source="snippets/write-text/WriteAllLines.cs":::

O exemplo de código-fonte anterior:

- Cria uma instância de uma matriz de cadeia de caracteres com três valores.
- Aguarda uma chamada para <xref:System.IO.File.WriteAllLinesAsync%2A?displayProperty=nameWithType> qual:

  - Cria de forma assíncrona um nome de arquivo *WriteLines.txt*. Se o arquivo já existir, ele será substituído.
  - Grava as linhas determinadas no arquivo.
  - Fecha o arquivo, liberando e descartando automaticamente conforme necessário.

## <a name="write-one-string-to-a-file"></a>Gravar uma cadeia de caracteres em um arquivo

:::code language="csharp" source="snippets/write-text/WriteAllText.cs":::

O exemplo de código-fonte anterior:

- Instancia uma cadeia de caracteres de acordo com o literal de cadeia de caracteres atribuído.
- Aguarda uma chamada para <xref:System.IO.File.WriteAllTextAsync%2A?displayProperty=nameWithType> qual:

  - Cria de forma assíncrona um nome de arquivo *WriteText.txt*. Se o arquivo já existir, ele será substituído.
  - Grava o texto fornecido no arquivo.
  - Fecha o arquivo, liberando e descartando automaticamente conforme necessário.

## <a name="write-selected-strings-from-an-array-to-a-file"></a>Gravar cadeias de caracteres selecionadas de uma matriz em um arquivo

:::code language="csharp" source="snippets/write-text/StreamWriterOne.cs":::

O exemplo de código-fonte anterior:

- Cria uma instância de uma matriz de cadeia de caracteres com três valores.
- Instancia um <xref:System.IO.StreamWriter> com um caminho de arquivo de *WriteLines2.txt* como uma [declaração de uso](../../whats-new/csharp-8.md#using-declarations).
- Itera em todas as linhas.
- Aguarda condicionalmente uma chamada para <xref:System.IO.StreamWriter.WriteLineAsync(System.String)?displayProperty=nameWithType> , que grava a linha no arquivo quando a linha não contém `"Second"` .

## <a name="append-text-to-an-existing-file"></a>Acrescentar texto a um arquivo existente

:::code language="csharp" source="snippets/write-text/StreamWriterTwo.cs":::

O exemplo de código-fonte anterior:

- Cria uma instância de uma matriz de cadeia de caracteres com três valores.
- Instancia um <xref:System.IO.StreamWriter> com um caminho de arquivo de *WriteLines2.txt* como uma [declaração using](../../whats-new/csharp-8.md#using-declarations), passando `true` para Append.
- Aguarda uma chamada para <xref:System.IO.StreamWriter.WriteLineAsync(System.String)?displayProperty=nameWithType> , que grava a cadeia de caracteres no arquivo como uma linha acrescentada.

## <a name="exceptions"></a>Exceções

As seguintes condições podem causar uma exceção:

- <xref:System.InvalidOperationException>: O arquivo existe e é somente leitura.
- <xref:System.IO.PathTooLongException>: O nome do caminho pode ser muito longo.
- <xref:System.IO.IOException>: O disco pode estar cheio.

Há condições adicionais que podem causar exceções ao trabalhar com o sistema de arquivos, é melhor programar de forma defensiva.

## <a name="see-also"></a>Consulte também

- [Guia de programação C#](../index.md)
- [Sistema de arquivos e o Registro (Guia de Programação em C#)](./index.md)
- [Exemplo: salvar uma coleção no armazenamento de aplicativos](https://code.msdn.microsoft.com/CSWinStoreAppSaveCollection-bed5d6e6)
