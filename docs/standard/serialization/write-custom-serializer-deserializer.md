---
title: Como escrever serializadores personalizados e desserializadores com o System.Text.Json
description: Saiba como escrever serializadores personalizados e desserializadores para JSON usando o System.Text.Json namespace.
ms.date: 11/30/2020
no-loc:
- System.Text.Json
- Newtonsoft.Json
helpviewer_keywords:
- JSON serialization
- serializing objects
- serialization
- objects, serializing
ms.openlocfilehash: a01d3c8dd18c114ea1c3aabc402bc841a6025ffe
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96439906"
---
# <a name="how-to-write-custom-serializers-and-deserializers-with-no-locsystemtextjson"></a>Como escrever serializadores personalizados e desserializadores com o System.Text.Json

<xref:System.Text.Json.Utf8JsonReader?displayProperty=fullName> é um leitor de alto desempenho, de baixa alocação e somente de encaminhamento para texto JSON codificado em UTF-8, lido de um `ReadOnlySpan<byte>` ou `ReadOnlySequence<byte>` . O `Utf8JsonReader` é um tipo de baixo nível que pode ser usado para criar analisadores e desserializadores personalizados. O <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=nameWithType> método usa `Utf8JsonReader` nos bastidores.

<xref:System.Text.Json.Utf8JsonWriter?displayProperty=fullName> é uma maneira de alto desempenho para escrever texto JSON codificado em UTF-8 de tipos comuns do .NET como `String` , `Int32` e `DateTime` . O gravador é um tipo de baixo nível que pode ser usado para criar serializadores personalizados. O <xref:System.Text.Json.JsonSerializer.Serialize%2A?displayProperty=nameWithType> método usa `Utf8JsonWriter` nos bastidores.

<xref:System.Text.Json.JsonDocument?displayProperty=fullName> fornece a capacidade de criar um Modelo de Objeto do Documento somente leitura (DOM) usando o `Utf8JsonReader` . O DOM fornece acesso aleatório aos dados em uma carga JSON. Os elementos JSON que compõem a carga podem ser acessados por meio do <xref:System.Text.Json.JsonElement> tipo. O `JsonElement` tipo fornece enumeradores de matriz e de objeto juntamente com APIs para converter texto JSON em tipos .net comuns. `JsonDocument` expõe uma <xref:System.Text.Json.JsonDocument.RootElement> propriedade.

As seções a seguir mostram como usar essas ferramentas para ler e gravar o JSON.

## <a name="use-jsondocument-for-access-to-data"></a>Usar o JsonDocument para acessar dados

O exemplo a seguir mostra como usar a <xref:System.Text.Json.JsonDocument> classe para acesso aleatório a dados em uma cadeia de caracteres JSON:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs" id="AverageGrades1":::

O código anterior:

* Assume que o JSON a ser analisado está em uma cadeia de caracteres chamada `jsonString` .
* Calcula uma classificação média para objetos em uma `Students` matriz que tem uma `Grade` propriedade.
* Atribui uma classificação padrão de 70 para alunos que não têm uma classificação.
* Conta os alunos incrementando uma `count` variável com cada iteração. Uma alternativa é chamar <xref:System.Text.Json.JsonElement.GetArrayLength%2A> , conforme mostrado no exemplo a seguir:

  :::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentDataAccess.cs" id="AverageGrades2":::

Veja um exemplo do JSON que esse código processa:

:::code language="json" source="snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json":::

## <a name="use-jsondocument-to-write-json"></a>Usar JsonDocument para gravar JSON

O exemplo a seguir mostra como gravar JSON de um <xref:System.Text.Json.JsonDocument> :

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/JsonDocumentWriteJson.cs" id="Serialize":::

O código anterior:

* Lê um arquivo JSON, carrega os dados em um `JsonDocument` e grava JSON formatado (bem-impresso) em um arquivo.
* Usa <xref:System.Text.Json.JsonDocumentOptions> para especificar que os comentários no JSON de entrada são permitidos, mas ignorados.
* Quando terminar, chama <xref:System.Text.Json.Utf8JsonWriter.Flush%2A> o gravador. Uma alternativa é deixar a liberação automática do gravador quando ela é descartada.

Aqui está um exemplo de entrada JSON a ser processada pelo código de exemplo:

:::code language="json" source="snippets/system-text-json-how-to/csharp/Grades.json":::

O resultado é a seguinte saída JSON bem impressa:

:::code language="json" source="snippets/system-text-json-how-to/csharp/GradesPrettyPrint.json":::

## <a name="use-utf8jsonwriter"></a>Usar Utf8JsonWriter

O exemplo a seguir mostra como usar a <xref:System.Text.Json.Utf8JsonWriter> classe:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8WriterToStream.cs" id="Serialize":::

## <a name="use-utf8jsonreader"></a>Usar Utf8JsonReader

O exemplo a seguir mostra como usar a <xref:System.Text.Json.Utf8JsonReader> classe:

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderFromBytes.cs" id="Deserialize":::

O código anterior pressupõe que a `jsonUtf8` variável é uma matriz de bytes que contém um JSON válido, codificado como UTF-8.

### <a name="filter-data-using-utf8jsonreader"></a>Filtrar dados usando Utf8JsonReader

O exemplo a seguir mostra como ler de forma síncrona um arquivo e procurar um valor.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderFromFile.cs":::

Para obter uma versão assíncrona deste exemplo, consulte [.net Samples JSON Project](https://github.com/dotnet/samples/blob/18e31a5f1abd4f347bf96bfdc3e40e2cfb36e319/core/json/Program.cs).

O código anterior:

* Assume que o JSON contém uma matriz de objetos e cada objeto pode conter uma propriedade "Name" do tipo cadeia de caracteres.
* Conta objetos e valores de propriedade "Name" que terminam com "University".
* Pressupõe que o arquivo é codificado como UTF-16 e o codifica em UTF-8. Um arquivo codificado como UTF-8 pode ser lido diretamente em um `ReadOnlySpan<byte>` , usando o seguinte código:

  ```csharp
  ReadOnlySpan<byte> jsonReadOnlySpan = File.ReadAllBytes(fileName);
  ```

  Se o arquivo contiver uma marca de ordem de byte (BOM) UTF-8, remova-a antes de passar os bytes para o `Utf8JsonReader` , uma vez que o leitor espera o texto. Caso contrário, a BOM será considerada JSON inválido e o leitor lançará uma exceção.

Aqui está um exemplo de JSON que o código anterior pode ler. A mensagem de resumo resultante é "2 de 4 têm nomes que terminam com" University "":

:::code language="json" source="snippets/system-text-json-how-to/csharp/Universities.json":::

### <a name="read-from-a-stream-using-utf8jsonreader"></a>Ler de um fluxo usando Utf8JsonReader

Ao ler um arquivo grande (um gigabyte ou mais, por exemplo), talvez você queira evitar ter que carregar todo o arquivo na memória de uma só vez. Para esse cenário, você pode usar um <xref:System.IO.FileStream> .

Ao usar o `Utf8JsonReader` para ler de um fluxo, as seguintes regras se aplicam:

* O buffer que contém a carga JSON parcial deve ser pelo menos tão grande quanto o maior token JSON dentro dele, de modo que o leitor possa progredir em encaminhar.
* O buffer deve ser pelo menos tão grande quanto a maior sequência de espaços em branco dentro do JSON.
* O leitor não mantém o controle dos dados lidos até que ele leia completamente o próximo <xref:System.Text.Json.Utf8JsonReader.TokenType%2A> na carga JSON. Assim, quando houver bytes restantes no buffer, você precisa passá-los para o leitor novamente. Você pode usar <xref:System.Text.Json.Utf8JsonReader.BytesConsumed%2A> para determinar quantos bytes serão deixados.

O código a seguir ilustra como ler de um fluxo. O exemplo mostra um <xref:System.IO.MemoryStream> . O código semelhante funcionará com um <xref:System.IO.FileStream> , exceto quando o `FileStream` contiver uma bom UTF-8 no início. Nesse caso, você precisa remover esses três bytes do buffer antes de passar os bytes restantes para o `Utf8JsonReader` . Caso contrário, o leitor lançaria uma exceção, uma vez que a BOM não é considerada uma parte válida do JSON.

O código de exemplo começa com um buffer de 4 KB e dobra o tamanho do buffer sempre que ele descobre que o tamanho não é grande o suficiente para se ajustar a um token JSON completo, que é necessário para que o leitor faça o progresso no conteúdo JSON. O exemplo de JSON fornecido no trecho de código dispara um aumento de tamanho de buffer somente se você definir um tamanho de buffer inicial muito pequeno, por exemplo, 10 bytes. Se você definir o tamanho do buffer inicial como 10, as `Console.WriteLine` instruções ilustrarão a causa e o efeito do tamanho do buffer aumentará. No tamanho do buffer inicial de 4 KB, o JSON de exemplo inteiro é mostrado por cada um `Console.WriteLine` , e o tamanho do buffer nunca precisa ser aumentado.

:::code language="csharp" source="snippets/system-text-json-how-to/csharp/Utf8ReaderPartialRead.cs":::

O exemplo anterior não define nenhum limite quanto ao tamanho do buffer pode crescer. Se o tamanho do token for muito grande, o código poderá falhar com uma <xref:System.OutOfMemoryException> exceção. Isso pode acontecer se o JSON contiver um token com cerca de 1 GB ou mais de tamanho, porque dobrar o tamanho de 1 GB resulta em um tamanho muito grande para caber em um `int32` buffer.

## <a name="see-also"></a>Confira também

* [System.Text.Json sobre](system-text-json-overview.md)
* [Como personalizar a codificação de caracteres](system-text-json-character-encoding.md)
* [Como escrever conversores personalizados para serialização JSON](system-text-json-converters-how-to.md)
* [System.Text.Json Referência de API](xref:System.Text.Json)
