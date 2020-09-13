---
title: Documentando seu código com comentários em XML
description: Saiba como documentar seu código com comentários de documentação XML e gerar um arquivo de documentação XML em tempo de compilação.
ms.date: 01/21/2020
ms.technology: csharp-fundamentals
ms.assetid: 8e75e317-4a55-45f2-a866-e76124171838
ms.openlocfilehash: 91de11c610ea17999dabff6d0552de9440f532e6
ms.sourcegitcommit: e7acba36517134238065e4d50bb4a1cfe47ebd06
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/04/2020
ms.locfileid: "89465293"
---
# <a name="document-your-code-with-xml-comments"></a>Documente seu código com comentários XML

Comentários em documentação XML são um tipo especial de comentário, adicionados acima da definição de qualquer membro ou tipo definido pelo usuário.
Eles são especiais porque podem ser processados pelo compilador para gerar um arquivo de documentação XML em tempo de compilação.
O arquivo XML gerado pelo compilador pode ser distribuído junto com seu assembly .NET para que o Visual Studio e outros IDEs possam usar o IntelliSense para mostrar informações rápidas sobre tipos ou membros. Além disso, o arquivo XML pode ser executado por ferramentas como [DocFX](https://dotnet.github.io/docfx/) e [Sandcastle](https://github.com/EWSoftware/SHFB) para gerar sites de referência de API.

Comentários de documentação XML, como todos os outros comentários, são ignorados pelo compilador.

É possível gerar o arquivo XML em tempo de compilação seguindo um destes procedimentos:

- Se você estiver desenvolvendo um aplicativo com o .NET Core na linha de comando, poderá adicionar um `GenerateDocumentationFile` elemento à `<PropertyGroup>` seção do seu arquivo de projeto. csproj. Você também pode especificar o caminho para o arquivo de documentação diretamente usando o [ `DocumentationFile` elemento](/visualstudio/msbuild/common-msbuild-project-properties). O seguinte exemplo gera um arquivo XML no diretório do projeto com o mesmo nome de arquivo raiz do assembly:

   ```xml
   <GenerateDocumentationFile>true</GenerateDocumentationFile>
   ```

   Isso é equivalente ao seguinte:

   ```xml
   <DocumentationFile>bin\$(Configuration)\$(TargetFramework)\$(AssemblyName).xml</DocumentationFile>
   ```

- Se estiver desenvolvendo um aplicativo usando o Visual Studio, clique com botão direito do mouse no projeto e selecione **Propriedades**. Na caixa de diálogo Propriedades, selecione a guia **Build** e marque **Arquivo de documentação XML**. Também é possível alterar o local em que o compilador grava o arquivo.

- Se você estiver Compilando um aplicativo .NET na linha de comando, adicione a [opção-doc do compilador](language-reference/compiler-options/doc-compiler-option.md) ao compilar.  

Comentários de documentação XML usam três barras (`///`) e o corpo do comentário formatado em XML. Por exemplo:

[!code-csharp[XML Documentation Comment](../../samples/snippets/csharp/concepts/codedoc/xml-comment.cs)]

## <a name="walkthrough"></a>Passo a passo

Vamos examinar a documentação de uma biblioteca matemática muito básica para facilitar que os novos desenvolvedores compreendam/contribuam e que os desenvolvedores de terceiros usem.

Este é o código para a biblioteca de matemática simples:

[!code-csharp[Sample Library](../../samples/snippets/csharp/concepts/codedoc/sample-library.cs)]

A biblioteca de exemplo dá suporte a quatro operações aritméticas principais ( `add` , `subtract` , `multiply` e `divide` ) em `int` e `double` tipos de dados.

Agora você deseja poder criar um documento de referência de API do seu código para desenvolvedores de terceiros que usam sua biblioteca, mas não têm acesso ao código-fonte.
Como já foi mencionado, as marcas da documentação XML podem ser usadas para isso. Agora, você será apresentado às marcas XML padrão que têm suporte do compilador de C#.

## \<summary>

A marca `<summary>` adiciona informações sucintas sobre um tipo ou membro.
Vou demonstrar seu uso adicionando-a à definição de classe `Math` e ao primeiro método `Add`. Fique à vontade para aplicá-la ao restante de seu código.

[!code-csharp[Summary Tag](~/samples/snippets/csharp/concepts/codedoc/summary-tag.cs)]

A `<summary>` marca é importante e é recomendável incluí-la porque seu conteúdo é a fonte primária do tipo ou informações de membro no IntelliSense ou em um documento de referência de API.

## \<remarks>

A marca `<remarks>` complementa as informações sobre tipos ou membros que a marca `<summary>` fornece. Neste exemplo, você apenas a adiciona à classe.

[!code-csharp[Remarks Tag](~/samples/snippets/csharp/concepts/codedoc/remarks-tag.cs)]

## \<returns>

A marca `<returns>` descreve o valor retornado de uma declaração de método.
Assim como antes, o exemplo a seguir ilustra a marca `<returns>` no primeiro método `Add`. É possível fazer o mesmo em outros métodos.

[!code-csharp[Returns Tag](~/samples/snippets/csharp/concepts/codedoc/returns-tag.cs)]

## \<value>

A marca `<value>` é semelhante à marca `<returns>`, exceto pelo fato de você usá-la para propriedades.
Supondo que sua biblioteca `Math` tivesse uma propriedade estática chamada `PI`, você usaria essa marca desta forma:

[!code-csharp[Value Tag](~/samples/snippets/csharp/concepts/codedoc/value-tag.cs)]

## \<example>

Você usa a marca `<example>` para incluir um exemplo em sua documentação XML.
Isso envolve o uso da marca `<code>` filho.

[!code-csharp[Example Tag](~/samples/snippets/csharp/concepts/codedoc/example-tag.cs)]

A marca `code` preserva quebras de linha e recuos para exemplos mais longos.

## \<para>

Você usa a marca `<para>` para formatar o conteúdo dentro de sua marca pai. Normalmente, `<para>` é usado dentro de uma marcação, como `<remarks>` ou `<returns>`, para dividir o texto em parágrafos.
Você pode formatar o conteúdo da marcação `<remarks>` para a definição de classe.

[!code-csharp[Para Tag](~/samples/snippets/csharp/concepts/codedoc/para-tag.cs)]

## \<c>

Ainda com relação à formatação, use a marca `<c>` para marcar parte do texto como código.
Ela é semelhante à marca `<code>`, mas embutida. Ela é útil quando você deseja mostrar um exemplo de código rápido como parte do conteúdo da marca.
Vamos atualizar a documentação para a classe `Math`.

[!code-csharp[C Tag](~/samples/snippets/csharp/concepts/codedoc/c-tag.cs)]

## \<exception>

Usando a marca `<exception>`, você informa os desenvolvedores de que um método pode lançar exceções específicas.
Observando sua biblioteca `Math`, você pode ver que ambos os métodos `Add` lançarão uma exceção se uma determinada condição for atendida. Algo menos óbvio, porém, é que o método inteiro `Divide` também será lançado se o parâmetro `b` for zero. Agora, adicione a documentação de exceção a esse método.

[!code-csharp[Exception Tag](~/samples/snippets/csharp/concepts/codedoc/exception-tag.cs)]

O atributo `cref` representa uma referência a uma exceção que está disponível no ambiente de compilação atual.
Pode ser qualquer tipo definido no projeto ou um assembly referenciado. O compilador emitirá um aviso se o valor não puder ser resolvido.

## \<see>

A marca `<see>` permite criar um link clicável para uma página de documentação para outro elemento de código. Em nosso próximo exemplo, criaremos um link clicável entre os dois métodos `Add`.

[!code-csharp[See Tag](~/samples/snippets/csharp/concepts/codedoc/see-tag.cs)]

O `cref` é um atributo **obrigatório** que representa uma referência para um tipo ou seu membro que está disponível no ambiente de compilação atual.
Pode ser qualquer tipo definido no projeto ou um assembly referenciado.

## \<seealso>

Você usa a marca `<seealso>` da mesma forma que usaria a marca `<see>`. A única diferença é que seu conteúdo normalmente é colocado em uma seção "Consulte também". Aqui, adicionaremos uma marca `seealso` ao método inteiro `Add` para fazer referência a outros métodos na classe que aceitam parâmetros inteiros:

[!code-csharp[Seealso Tag](~/samples/snippets/csharp/concepts/codedoc/seealso-tag.cs)]

O atributo `cref` representa uma referência para um tipo ou seu membro que está disponível no ambiente de compilação atual.
Pode ser qualquer tipo definido no projeto ou um assembly referenciado.

## \<param>

Você usa a marca `<param>` para descrever os parâmetros de um método. Veja um exemplo do `Add` Método Double: o parâmetro que a marca descreve é especificado no atributo **Required** `name` .

[!code-csharp[Param Tag](~/samples/snippets/csharp/concepts/codedoc/param-tag.cs)]

## \<typeparam>

Use a marca `<typeparam>` exatamente como a marca `<param>`, mas para declarações de método ou de tipo genérico para descrever um parâmetro genérico.
Adicione um método genérico rápido à sua classe `Math` para verificar se uma quantidade é maior que outra.

[!code-csharp[Typeparam Tag](~/samples/snippets/csharp/concepts/codedoc/typeparam-tag.cs)]

## \<paramref>

Às vezes, você pode estar descrevendo o que um método faz, no que poderia ser uma marcação `<summary>` e talvez queira fazer uma referência a um parâmetro. A marcação `<paramref>` é excelente para exatamente isso. Vamos atualizar o resumo de nosso método `Add` de base dupla. Assim como a `<param>` marca, o nome do parâmetro é especificado no atributo **Required** `name` .

[!code-csharp[Paramref Tag](~/samples/snippets/csharp/concepts/codedoc/paramref-tag.cs)]

## \<typeparamref>

Use a marca `<typeparamref>` exatamente como a marca `<paramref>`, mas para declarações de método ou de tipo genérico para descrever um parâmetro genérico.
É possível usar o mesmo método genérico criado anteriormente.

[!code-csharp[Typeparamref Tag](~/samples/snippets/csharp/concepts/codedoc/typeparamref-tag.cs)]

## \<list>

Você usa a `<list>` marca para formatar informações de documentação como uma lista ordenada, uma lista não ordenada ou uma tabela. Crie uma lista não ordenada de cada operação matemática a que sua biblioteca `Math` dá suporte.

[!code-csharp[List Tag](~/samples/snippets/csharp/concepts/codedoc/list-tag.cs)]

É possível fazer uma lista ordenada ou tabela alterando o atributo `type` para `number` ou `table`, respectivamente.

## \<inheritdoc>

Você pode usar a `<inheritdoc>` marca para herdar comentários XML de classes base, interfaces e métodos semelhantes. Isso elimina a cópia indesejada e a colagem de comentários XML duplicados e mantém automaticamente os comentários XML sincronizados.

[!code-csharp-interactive[InheritDoc Tag](~/samples/snippets/csharp/concepts/codedoc/inheritdoc-tag.cs)]

### <a name="put-it-all-together"></a>Colocar tudo isso junto

Se você seguiu o tutorial e aplicou as marcas ao seu código quando necessário, seu código deve ser semelhante ao seguinte:

[!code-csharp[Tagged Library](~/samples/snippets/csharp/concepts/codedoc/tagged-library.cs)]

No seu código, você pode gerar um site de documentação detalhada completo com referências cruzadas clicáveis. Mas você se depara com outro problema: o código tornou-se difícil de ler.
Há tanta informação para ser analisada que será um pesadelo para qualquer desenvolvedor que desejar contribuir para esse código.
Felizmente, há uma marca XML que pode ajudá-lo a lidar com isso:

## \<include>

A marcação `<include>` permite fazer referência a comentários em um arquivo XML separado que descrevem os tipos e membros em seu código-fonte, em vez de colocar comentários de documentação diretamente em seu arquivo de código-fonte.

Agora, você moverá todas as suas marcas XML para um arquivo XML separado chamado `docs.xml`. Fique à vontade para nomear o arquivo como desejar.

[!code-xml[Sample XML](~/samples/snippets/csharp/concepts/codedoc/include.xml)]

No XML acima, os comentários de documentação de cada membro aparecem diretamente dentro de uma marca cujo nome corresponde ao que eles fazem. Você pode escolher sua própria estratégia.
Agora que você tem seus comentários XML em um arquivo separado, vamos ver como seu código pode ficar mais legível usando a marca `<include>`:

[!code-csharp[Include Tag](~/samples/snippets/csharp/concepts/codedoc/include-tag.cs)]

E aqui está: nosso código voltou a ser legível e nenhuma informação de documentação foi perdida.

O atributo `file` representa o nome do arquivo XML que contém a documentação.

O atributo `path` representa uma consulta [XPath](../standard/data/xml/xpath-queries-and-namespaces.md) para o `tag name` presente no `file` especificado.

O atributo `name` representa o especificador de nome na marca que precede os comentários.

O `id` atributo, que pode ser usado no lugar de `name` , representa a ID da marca que precede os comentários.

### <a name="user-defined-tags"></a>Marcas definidas pelo usuário

Todas as marcas descritas acima representam as marcas que são reconhecidas pelo compilador C#. No entanto, o usuário é livre para definir suas próprias marcas.
Ferramentas como Sandcastle oferecem suporte para marcas extras [\<event>](https://ewsoftware.github.io/XMLCommentsGuide/html/81bf7ad3-45dc-452f-90d5-87ce2494a182.htm) , como e [\<note>](https://ewsoftware.github.io/XMLCommentsGuide/html/4302a60f-e4f4-4b8d-a451-5f453c4ebd46.htm) , e até mesmo dão suporte a [namespaces de documentação](https://ewsoftware.github.io/XMLCommentsGuide/html/BD91FAD4-188D-4697-A654-7C07FD47EF31.htm).
Ferramentas de geração de documentação internas ou personalizadas também podem ser usadas com as marcas padrão e vários formatos de saída, de HTML a PDF, podem ter suporte.

## <a name="recommendations"></a>Recomendações

Documentar o código é recomendável por vários motivos. A seguir, temos algumas práticas recomendadas, cenários de caso de uso gerais e coisas que você precisa saber ao usar marcas de documentação XML em seu código C#.

- Para fins de consistência, todos os tipos visíveis publicamente e seus membros devem ser documentados. Se você precisar fazer isso, faça tudo.
- Membros particulares também podem ser documentados usando comentários XML. No entanto, isso expõe o funcionamento interno (potencialmente confidencial) de sua biblioteca.
- No mínimo, os tipos e seus membros devem ter uma marca `<summary>`, porque seu conteúdo é necessário para o IntelliSense.
- O texto da documentação deve ser escrito usando frases terminadas com ponto final.
- Classes parciais têm suporte total e informações da documentação serão concatenadas em uma única entrada para esse tipo.
- O compilador verifica a sintaxe das `<exception>` marcas,,,, `<include>` `<param>` `<see>` `<seealso>` e `<typeparam>` .
- O compilador valida os parâmetros que contêm caminhos de arquivo e referências para outras partes do código.

## <a name="see-also"></a>Veja também

- [Comentários de documentação XML (guia de programação C#)](programming-guide/xmldoc/index.md)
- [Marcas recomendadas para comentários de documentação (Guia de Programação em C#)](programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)
