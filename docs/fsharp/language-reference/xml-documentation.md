---
title: Documentação XML
description: 'Saiba mais sobre o suporte no F # para gerar documentação de comentários.'
ms.date: 09/15/2020
ms.openlocfilehash: 2f8788e79ea964143eecfaddbeb039474dd61f8e
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025010"
---
# <a name="document-your-code-with-xml-comments"></a>Documente seu código com comentários XML

Você pode produzir a documentação de comentários de código de barra tripla (///) em F #. Os comentários XML podem preceder declarações nos arquivos de código (. FS) ou de assinatura (. FSI).

Comentários em documentação XML são um tipo especial de comentário, adicionados acima da definição de qualquer membro ou tipo definido pelo usuário.
Eles são especiais porque podem ser processados pelo compilador para gerar um arquivo de documentação XML em tempo de compilação.
O arquivo XML gerado pelo compilador pode ser distribuído junto com seu assembly .NET para que as IDEs possam usar dicas de ferramenta para mostrar informações rápidas sobre tipos ou membros. Além disso, o arquivo XML pode ser executado por meio de ferramentas como [fsdocs](http://fsprojects.github.io/FSharp.Formatting/) para gerar sites de referência de API.

Comentários de documentação XML, como todos os outros comentários, são ignorados pelo compilador, a menos que as opções descritas abaixo estejam habilitadas para verificar a validade e a integridade dos comentários em tempo de compilação.

É possível gerar o arquivo XML em tempo de compilação seguindo um destes procedimentos:

- Você pode adicionar um `GenerateDocumentationFile` elemento à `<PropertyGroup>` seção do arquivo de `.fsproj` projeto, que gera um arquivo XML no diretório do projeto com o mesmo nome de arquivo raiz do assembly. Por exemplo:

   ```xml
   <GenerateDocumentationFile>true</GenerateDocumentationFile>
   ```

- Se estiver desenvolvendo um aplicativo usando o Visual Studio, clique com botão direito do mouse no projeto e selecione **Propriedades**. Na caixa de diálogo Propriedades, selecione a guia **Build** e marque **Arquivo de documentação XML**. Também é possível alterar o local em que o compilador grava o arquivo.

Há duas maneiras de escrever comentários de documentação XML: com e sem marcas XML. Ambos usam comentários de barra tripla.

## <a name="comments-without-xml-tags"></a>Comentários sem marcas XML

Se um `///` comentário não começar com um `<` , todo o texto do comentário será levado como a documentação resumida da construção de código que segue imediatamente. Use esse método quando desejar escrever apenas um breve resumo para cada construção.

O comentário é codificado em XML durante a preparação da documentação, portanto, caracteres como `<` , `>` e `&` não precisam ser ignorados. Se você não especificar uma marca de resumo explicitamente, não deverá especificar outras marcas, como **param** ou **retorna** marcas.

O exemplo a seguir mostra o método alternativo, sem marcas XML. Neste exemplo, o texto inteiro no comentário é considerado um resumo.

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet7102.fs)]

## <a name="comments-with-xml-tags"></a>Comentários com marcas XML

Se um corpo de comentário começa com `<` (normalmente `<summary>` ), ele é tratado como um corpo de comentário XML formatado usando marcas XML. Esse segundo permite que você especifique anotações separadas para um breve resumo, comentários adicionais, documentação para cada parâmetro e parâmetro de tipo e exceções lançadas e uma descrição do valor de retorno.

Este é um comentário de documentação XML típico em um arquivo de assinatura:

[!code-fsharp[Main](~/samples/snippets/fsharp/lang-ref-2/snippet7101.fs)]

## <a name="recommended-tags"></a>Marcas recomendadas

Se você estiver usando marcas XML, a tabela a seguir descreve as marcas externas reconhecidas nos comentários de código XML F #.

| Sintaxe de marca                                  | Descrição |
|---------------------------------------------|-----------|
| `<summary>`**_texto_**`</summary>`           | Especifica que o *texto* é uma breve descrição do elemento Program. A descrição geralmente é uma ou duas frases.|
| `<remarks>`**_texto_**`</remarks>`           | Especifica que o *texto* contém informações suplementares sobre o elemento Program.|
| `<param name="`**_nome_** `">` do **_Descrição_ do**`</param>` | Especifica o nome e a descrição de um parâmetro de função ou método.|
| `<typeparam name="`**_nome_** `">` do **_Descrição_ do**`</typeparam>` | Especifica o nome e a descrição de um parâmetro de tipo.|
| `<returns>`**_texto_**`</returns>`           | Especifica que o *texto* descreve o valor de retorno de uma função ou método.|
| `<exception cref="`**_tipo_** `">` de **_Descrição_ do**`</exception>` |Especifica o tipo de exceção que pode ser gerado e as circunstâncias sob as quais ela é gerada.|
| `<seealso cref="`**_referência_**`"/>`      | Especifica um link consulte também a documentação de outro tipo. A *referência* é o nome que aparece no arquivo de documentação XML. Consulte também os links geralmente aparecem na parte inferior de uma página de documentação.|

A tabela a seguir descreve as marcas para uso nas seções de descrição:

| Sintaxe de marca                                | Descrição |
|-------------------------------------------|-------------|
| `<para>`**_texto_**`</para>`               | Especifica um parágrafo de texto. Isso é usado para separar o texto dentro da marca de **comentários** .|
| `<code>`**_texto_**`</code>`               | Especifica que o *texto* tem várias linhas de código. Essa marca pode ser usada por geradores de documentação para exibir texto em uma fonte apropriada para o código.|
| `<paramref name="`**_nomes_**`"/>`         | Especifica uma referência a um parâmetro no mesmo comentário de documentação.|
| `<typeparamref name="`**_nomes_**`"/>`     | Especifica uma referência a um parâmetro de tipo no mesmo comentário de documentação.|
| `<c>`**_texto_**`</c>`                     | Especifica que o *texto* é um código embutido. Essa marca pode ser usada por geradores de documentação para exibir texto em uma fonte apropriada para o código.|
| `<see cref="`**_referência_** `">` do **_texto_ de**`</see>` | Especifica um link embutido para outro elemento de programa. A *referência* é o nome que aparece no arquivo de documentação XML. O *texto* é o texto mostrado no link.|

### <a name="user-defined-tags"></a>Marcas definidas pelo usuário

As marcas anteriores representam as que são reconhecidas pelo compilador F # e pelas ferramentas típicas do editor F #. No entanto, o usuário é livre para definir suas próprias marcas.
Ferramentas como fsdocs oferecem suporte para marcas adicionais como [\<namespacedoc>](https://github.com/fsharp/fslang-design/blob/master/tooling/FST-1031-xmldoc-extensions.md) .
Ferramentas de geração de documentação internas ou personalizadas também podem ser usadas com as marcas padrão e vários formatos de saída, de HTML a PDF, podem ter suporte.

## <a name="compile-time-checking"></a>Verificação de tempo de compilação

Quando `--warnon:3390` é habilitado, o compilador verifica a sintaxe do XML e os parâmetros referenciados nas `<param>` `<paramref>` marcas e.

## <a name="documenting-f-constructs"></a>Documentando construções F #

Construções F #, como módulos, membros, casos de União e campos de registro, são documentados por um `///` comentário imediatamente antes de sua declaração.
Se necessário, os construtores implícitos de classes são documentados fornecendo um `///` comentário antes da lista de argumentos. Por exemplo:

```fsharp
/// This is the type
type SomeType
      /// This is the implicit constructor
      (a: int, b: int) =

    /// This is the member
    member _.Sum() = a + b
```

## <a name="limitations"></a>Limitações

Não há suporte para alguns recursos da documentação XML em C# e em outras linguagens .NET no F #.

- Em F #, as referências cruzadas devem usar a assinatura XML completa do símbolo correspondente, por exemplo `cref="T:System.Console"` .
  Referências cruzadas simples no estilo C#, como `cref="Console"` não são elaboradas para assinaturas XML completas, e esses elementos não são verificados pelo compilador F #. Algumas ferramentas de documentação podem permitir o uso dessas referências cruzadas por processamento posterior, mas as assinaturas completas devem ser usadas.

- As marcas `<include>` `<inheritdoc>` não são suportadas pelo compilador F #. Nenhum erro será fornecido se forem usados, mas eles serão simplesmente copiados para o arquivo de documentação gerado sem, de outra forma, afetar a documentação gerada.

- Referências cruzadas não são verificadas pelo compilador F #, mesmo quando `-warnon:3390` é usado.

- Os nomes usados nas marcas `<typeparam>` e `<typeparamref>` não são verificados pelo compilador F #, mesmo quando `--warnon:3390` é usado.

- Nenhum aviso será fornecido se a documentação estiver ausente, mesmo quando `--warnon:3390` for usado.

## <a name="recommendations"></a>Recomendações

Documentar o código é recomendável por vários motivos. O que vem a seguir são algumas práticas recomendadas, cenários de caso de uso geral e coisas que você deve saber ao usar marcas de documentação XML em seu código F #.

- Habilite a opção `--warnon:3390` em seu código para ajudar a garantir que a documentação XML seja um XML válido.

- Considere adicionar arquivos de assinatura para separar comentários de documentação XML longos da sua implementação.

- Para fins de consistência, todos os tipos visíveis publicamente e seus membros devem ser documentados. Se você precisar fazer isso, faça tudo.

- No mínimo, os módulos, os tipos e seus membros devem ter um `///` comentário ou marca simples `<summary>` . Isso será exibido em uma janela de dica de ferramenta de preenchimento automático em ferramentas de edição F #.

- O texto da documentação deve ser escrito usando frases terminadas com ponto final.

## <a name="see-also"></a>Veja também

- [Comentários de documentação XML do C# &#40;guia de programação C&#35;&#41;](../../csharp/programming-guide/xmldoc/index.md).
- [Referência de linguagem F #](index.md)
- [Opção de compilador](compiler-options.md)
