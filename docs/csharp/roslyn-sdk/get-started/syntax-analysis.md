---
title: Introdução à análise de sintaxe (APIs Roslyn)
description: Uma introdução pela travessia, consulta e percurso por árvores de sintaxe.
ms.date: 02/05/2018
ms.custom: mvc
ms.openlocfilehash: 8b9dd909a83877755dc1ebafd58aae892e460b93
ms.sourcegitcommit: a8a205034eeffc7c3e1bdd6f506a75b0f7099ebf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2020
ms.locfileid: "91756150"
---
# <a name="get-started-with-syntax-analysis"></a>Introdução à análise de sintaxe

Neste tutorial, você explorará a **API de sintaxe**. A API de sintaxe fornece acesso às estruturas de dados que descrevem um programa C# ou Visual Basic. Essas estruturas de dados têm detalhes suficientes para que possam representar qualquer programa, de qualquer tamanho. Essas estruturas podem descrever programas completos que compilam e executam corretamente. Elas também podem descrever programas incompletos, enquanto você os escreve no editor.

Para habilitar essa expressão avançada, as estruturas de dados e as APIs que compõem a API de sintaxe são necessariamente complexas. Começaremos com a aparência da estrutura de dados para o programa "Olá, Mundo" típico:

```csharp
using System;
using System.Collections.Generic;
using System.Linq;

namespace HelloWorld
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Hello World!");
        }
    }
}
```

Veja o texto do programa anterior. Você reconhece elementos familiares. O texto inteiro representa um único arquivo de origem, ou uma **unidade de compilação**. As três primeiras linhas do arquivo de origem são **diretivas de uso**. A origem restante está contida em uma **declaração de namespace**. A declaração de namespace contém uma **declaração de classe** filha. A declaração de classe contém uma **declaração de método**.

A API de sintaxe cria uma estrutura de árvore com a raiz que representa a unidade de compilação. Nós da árvore representam as diretivas using, a declaração de namespace e todos os outros elementos do programa. A estrutura de árvore continua até os níveis mais baixos: a cadeia de caracteres "Olá, Mundo!" é um **token literal da cadeia de caracteres** que é um descendente de um **argumento**. A API de sintaxe fornece acesso à estrutura do programa. Você pode consultar as práticas recomendadas de código específico, percorrer a árvore inteira para entender o código e criar novas árvores ao modificar a árvore existente.

Essa breve descrição fornece uma visão geral do tipo de informações acessíveis usando a API de sintaxe. A API de sintaxe não é nada mais de uma API formal que descreve os constructos de código familiares que você conhece do C#. As funcionalidades completas incluem informações sobre como o código é formatado, incluindo quebras de linha, espaço em branco e recuo. Usando essas informações, você pode representar totalmente o código como escrito e lido por programadores humanos ou pelo compilador. Usar essa estrutura permite que você interaja com o código-fonte em um nível muito significativo. Não se trata mais de cadeias de caracteres de texto, mas de dados que representam a estrutura de um programa C#.

Para começar, será necessário instalar o **SDK do .NET Compiler Platform**:

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

## <a name="understanding-syntax-trees"></a>Noções básicas sobre árvores de sintaxe

Você pode usar a API de sintaxe para uma análise da estrutura do código C#. A **API de sintaxe** expõe os analisadores, as árvores de sintaxe e os utilitários para analisar e criar árvores de sintaxe. Trata-se do modo como você pesquisa o código em busca de elementos de sintaxe específicos ou lê o código para um programa.

Uma árvore de sintaxe é uma estrutura de dados usada pelos compiladores C# e Visual Basic para entender programas nessas linguagens. Árvores de sintaxe são produzidas pelo mesmo analisador que é executado quando um projeto é compilado ou quando um desenvolvedor pressiona F5. As árvores de sintaxe têm fidelidade total com à linguagem de programação; cada bit de informações em um arquivo de código é representado na árvore. Gravar uma árvore de sintaxe em texto reproduz o texto original exato que foi analisado. As árvores de sintaxe também são **imutáveis**; uma vez criada, uma árvore de sintaxe nunca pode ser alterada. Os consumidores de árvores podem analisar as árvores de vários threads, sem bloqueios ou outras medidas de simultaneidade, sabendo que os dados nunca são alterados. Você pode usar APIs para criar novas árvores que são o resultado da modificação de uma árvore existente.

Os quatro principais blocos de construção de árvores de sintaxe são:

* A classe <xref:Microsoft.CodeAnalysis.SyntaxTree?displayProperty=nameWithType>, uma instância da qual representa uma árvore de análise inteira. <xref:Microsoft.CodeAnalysis.SyntaxTree> é uma classe abstrata que tem derivativos específicos a um idioma. Você usa os métodos Parse da <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxTree?displayProperty=nameWithType> classe (ou <xref:Microsoft.CodeAnalysis.VisualBasic.VisualBasicSyntaxTree?displayProperty=nameWithType> ) para analisar o texto em C# (ou Visual Basic).
* A classe <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType>, instâncias da qual representam constructos sintáticos como declarações, instruções, cláusulas e expressões.
* A estrutura <xref:Microsoft.CodeAnalysis.SyntaxToken?displayProperty=nameWithType>, que representa uma pontuação, operador, identificador ou palavra-chave individual.
* Finalmente, a estrutura <xref:Microsoft.CodeAnalysis.SyntaxTrivia?displayProperty=nameWithType>, que representa os bits de informação sem significância sintática, tais como o espaço em branco entre tokens, diretivas de pré-processamento e comentários.

Trívia, tokens e nós são compostos hierarquicamente para formar uma árvore que representa completamente tudo em um fragmento de código do Visual Basic ou do C#. Você pode ver essa estrutura usando a janela **Visualizador de Sintaxe**. No Visual Studio, escolha **Exibir**  >  **outras**  >  **Syntax Visualizer**do Windows. Por exemplo, o arquivo de origem C# anterior examinado usando o **Visualizador de Sintaxe** se parecerá com a figura a seguir:

**SyntaxNode**: Azul | **SyntaxToken**: Verde | **SyntaxTrivia**: Vermelho ![Arquivo de Código C#](media/walkthrough-csharp-syntax-figure1.png)

Ao navegar nessa estrutura de árvore, você pode encontrar qualquer instrução, expressão, token ou bit de espaço em branco em um arquivo de código.

Embora você possa encontrar tudo em um arquivo de código usando as APIs de sintaxe, a maioria dos cenários envolvem o exame de pequenos snippets de código ou a pesquisa por instruções ou fragmentos específicos. Os dois exemplos a seguir mostram usos típicos para navegar pela estrutura de códigos ou pesquisar por instruções individuais.

## <a name="traversing-trees"></a>Percorrendo árvores

Você pode examinar os nós em uma árvore de sintaxe de duas maneiras. Você pode percorrer a árvore para examinar cada nó, ou então consultar elementos ou nós específicos.

### <a name="manual-traversal"></a>Passagem manual

Você pode ver o código concluído para essa amostra no [nosso repositório do GitHub](https://github.com/dotnet/samples/tree/master/csharp/roslyn-sdk/SyntaxQuickStart).

> [!NOTE]
> Os tipos de árvore de sintaxe usam a herança para descrever os elementos de sintaxe diferentes que são válidos em locais diferentes no programa. Usar essas APIs geralmente significa converter propriedades ou membros da coleção em tipos derivados específicos. Nos exemplos a seguir, a atribuição e as conversões são instruções separadas, usando variáveis explicitamente tipadas. Você pode ler o código para ver os tipos de retorno da API e o tipo de runtime dos objetos retornados. Na prática, é mais comum usar variáveis implicitamente tipadas e depender de nomes de API para descrever o tipo de objeto que está sendo examinado.

Criar um novo projeto de **Ferramenta de Análise de Código Autônoma** do C#:

* No Visual Studio, escolha **arquivo**  >  **novo**  >  **projeto** para exibir a caixa de diálogo novo projeto.
* Em extensibilidade do **Visual C#**  >  **Extensibility**, escolha **ferramenta de análise de código autônoma**.
* Nomeie o projeto "**SyntaxTreeManualTraversal**" e clique em OK.

Você analisará o programa "Olá, Mundo!" básico mostrado anteriormente.
Adicione o texto ao programa Olá, Mundo como uma constante em sua classe `Program`:

[!code-csharp[Declare the program text](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#1 "Declare a constant string for the program text to analyze")]

Em seguida, adicione o código a seguir para criar a **árvore de sintaxe** para o texto do código na constante `programText`.  Adicione a seguinte linha ao seu método `Main`:

[!code-csharp[Create the tree](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#2 "Create the syntax tree")]

Essas duas linhas criam a árvore e recuperam o nó raiz dessa árvore. Agora você pode examinar os nós na árvore. Adicione essas linhas ao seu método `Main` para exibir algumas das propriedades do nó raiz na árvore:

[!code-csharp[Examine the root node](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#3 "Examine the root node")]

Execute o aplicativo para ver o que seu código descobriu sobre o nó raiz nessa árvore.

Normalmente, percorreria a árvore para saber mais sobre o código. Neste exemplo, você está analisando código que você conhece para explorar as APIs. Adicione o código a seguir para examinar o primeiro membro do nó `root`:

[!code-csharp[Find the first member](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#4 "Find the first member")]

Esse membro é um <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NamespaceDeclarationSyntax?displayProperty=nameWithType>. Ele representa tudo no escopo da declaração `namespace HelloWorld`. Adicione o seguinte código para examinar quais nós são declarados dentro do namespace `HelloWorld`:

[!code-csharp[Find the class declaration](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#5 "Find the class declaration")]

Execute o programa para ver o que você aprendeu.

Agora que você sabe que a declaração é um <xref:Microsoft.CodeAnalysis.CSharp.Syntax.ClassDeclarationSyntax?displayProperty=nameWithType>, declare uma nova variável de tipo para examinar a declaração de classe. Essa classe contém somente um membro: o método `Main`. Adicione o código a seguir para localizar o método `Main` e convertê-lo em um <xref:Microsoft.CodeAnalysis.CSharp.Syntax.MethodDeclarationSyntax?displayProperty=nameWithType>.

[!code-csharp[Find the main declaration](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#6 "Find the main declaration")]

O nó de declaração do método contém todas as informações de sintaxe sobre o método. Permite exibir o tipo de retorno do método `Main`, o número e os tipos dos argumentos e o texto do corpo do método. Adicione o seguinte código:

[!code-csharp[Examine the syntax of the main method](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#7 "Display information about the main method")]

Execute o programa para ver todas as informações que você descobriu sobre este programa:

```text
The tree is a CompilationUnit node.
The tree has 1 elements in it.
The tree has 4 using statements. They are:
        System
        System.Collections
        System.Linq
        System.Text
The first member is a NamespaceDeclaration.
There are 1 members declared in this namespace.
The first member is a ClassDeclaration.
There are 1 members declared in the Program class.
The first member is a MethodDeclaration.
The return type of the Main method is void.
The method has 1 parameters.
The type of the args parameter is string[].
The body text of the Main method follows:
        {
            Console.WriteLine("Hello, World!");
        }
```

### <a name="query-methods"></a>Métodos de consulta

Além de percorrer árvores, você também pode explorar a árvore de sintaxe usando os métodos de consulta definidos em <xref:Microsoft.CodeAnalysis.SyntaxNode?displayProperty=nameWithType>. Esses métodos devem ser imediatamente familiares a qualquer pessoa familiarizada com o XPath. Você pode usar esses métodos com o LINQ para localizar itens rapidamente em uma árvore. O <xref:Microsoft.CodeAnalysis.SyntaxNode> tem métodos de consulta como <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A>, <xref:Microsoft.CodeAnalysis.SyntaxNode.AncestorsAndSelf%2A> e <xref:Microsoft.CodeAnalysis.SyntaxNode.ChildNodes%2A>.

Você pode usar esses métodos de consulta para localizar o argumento para o método `Main` como uma alternativa a navegar pela árvore. Adicione o seguinte código à parte inferior do método `Main`:

[!code-csharp[Query the tree for the arguments to Main](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/HelloSyntaxTree/Program.cs#8 "Query the tree for the arguments to Main")]

A primeira instrução usa uma expressão LINQ e o método <xref:Microsoft.CodeAnalysis.SyntaxNode.DescendantNodes%2A> para localizar o mesmo parâmetro do exemplo anterior.

Execute o programa e você poderá ver que a expressão LINQ encontrou o mesmo parâmetro encontrado ao navegar manualmente pela árvore.

O exemplo usa instruções `WriteLine` para exibir informações sobre as árvores de sintaxe conforme elas são percorridas. Você também pode aprender mais executando o programa concluído no depurador. Você pode examinar mais das propriedades e métodos que fazem parte da árvore de sintaxe criada para o programa Olá, Mundo.

## <a name="syntax-walkers"></a>Caminhadores de sintaxe

Muitas vezes, você deseja localizar todos os nós de um tipo específico em uma árvore de sintaxe, por exemplo, cada declaração de propriedade em um arquivo. Ao estender a classe <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker?displayProperty=nameWithType> e substituir o método <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor.VisitPropertyDeclaration(Microsoft.CodeAnalysis.CSharp.Syntax.PropertyDeclarationSyntax)>, você processa cada declaração de propriedade em uma árvore de sintaxe sem conhecer a estrutura dele com antecedência. <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker> é um tipo específico de <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor>, que visita recursivamente um nó e cada um dos filhos desse nó.

Este exemplo implementa um <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker> que examina uma árvore de sintaxe. Ele coleta diretivas `using` que ele constata que não estão importando um namespace `System`.

Crie um novo projeto de **Ferramenta de Análise de Código Autônoma** do C#; nomeie-o "**SyntaxWalker**".

Você pode ver o código concluído para essa amostra no [nosso repositório do GitHub](https://github.com/dotnet/samples/tree/master/csharp/roslyn-sdk/SyntaxQuickStart). A amostra no GitHub contém os dois projetos descritos neste tutorial.

Assim como no exemplo anterior, você pode definir uma constante de cadeia de caracteres para conter o texto do programa que você pretende analisar:

[!code-csharp[Define the code text to analyzer](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/Program.cs#1 "Define the program text to analyze")]

Este texto de origem contém diretivas `using` espalhadas em quatro locais diferentes: o nível de arquivo, no namespace de nível superior e nos dois namespaces aninhados. Este exemplo destaca um cenário principal para usar a classe <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker> para consultar código. Seria complicado visitar cada nó na árvore de sintaxe de raiz para encontrar declarações using. Em vez disso, você pode criar uma classe derivada e substituir o método chamado apenas quando o nó atual na árvore é uma diretiva using. O visitante não realiza nenhum trabalho em nenhum outro tipo de nó. Esse método único examina cada uma das instruções `using` e compila uma coleção de namespaces que não estão no namespace `System`. Você compila um <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker> que examina todas as instruções `using`, mas apenas as instruções `using`.

Agora que você definiu o texto do programa, você precisa criar um `SyntaxTree` e obter a raiz dessa árvore:

[!code-csharp[Create the Syntax tree and access the root](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/Program.cs#2 "Create the Syntax tree and access the root node.")]

Em seguida, crie uma nova classe. No Visual Studio, escolha **projeto**  >  **Adicionar novo item**. Na caixa de diálogo **Adicionar Novo Item**, digite *UsingCollector.cs* como o nome do arquivo.

Você implementa a funcionalidade de visitante `using` na classe `UsingCollector`. Para começar, crie a classe `UsingCollector` derivada de <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker>.

[!code-csharp[Declare the base class for the using collector](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/UsingCollector.cs#3 "Declare the base class for the UsingCollector")]

Você precisa de armazenamento para conter os nós de namespace que você está coletando.  Declare uma propriedade pública somente leitura na classe `UsingCollector`; use essa variável para armazenar os nós <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax> que você encontrar:

[!code-csharp[Declare storage for the using syntax nodes](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/UsingCollector.cs#4 "Declare storage for the using syntax nodes")]

A classe base <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxWalker> implementa a lógica para visitar cada nó na árvore de sintaxe. A classe derivada substitui os métodos chamados para os nós específicos nos quais você está interessado. Nesse caso, você está interessado em qualquer diretiva `using`. Isso significa que você deve substituir o método <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor.VisitUsingDirective(Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax)>. Um argumento para esse método é um objeto <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax?displayProperty=nameWithType>. Essa é uma importante vantagem de se usar os visitantes: eles chamam os métodos substituídos com argumentos que já foram convertidos para o tipo de nó específico. A classe <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax?displayProperty=nameWithType> tem uma propriedade <xref:Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax.Name> que armazena o nome do namespace que está sendo importado. É um <xref:Microsoft.CodeAnalysis.CSharp.Syntax.NameSyntax?displayProperty=nameWithType>. Adicione o código a seguir na substituição <xref:Microsoft.CodeAnalysis.CSharp.CSharpSyntaxVisitor.VisitUsingDirective(Microsoft.CodeAnalysis.CSharp.Syntax.UsingDirectiveSyntax)>:

[!code-csharp[Examine using nodes for the System namespace](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/UsingCollector.cs#5 "Examine all using nodes for the System namespace.")]

Assim como no exemplo anterior, você adicionou uma variedade de instruções `WriteLine` para ajudar na compreensão do método. Você pode ver quando ele é chamado e quais argumentos são passados para ele a cada vez.

Por fim, você precisa adicionar duas linhas de código para criar o `UsingCollector` e fazer com que ele acesse o nó raiz, coletando todas as instruções `using`. Em seguida, adicione um loop `foreach` para exibir todas as instruções `using` encontradas pelo seu coletor:

[!code-csharp[Create the UsingCollector and visit the root node.](../../../../samples/snippets/csharp/roslyn-sdk/SyntaxQuickStart/SyntaxWalker/Program.cs#6 "Create the UsingCollector and visit the root node.")]

Compile e execute o programa. A seguinte saída deve ser exibida:

```console
        VisitUsingDirective called with System.
        VisitUsingDirective called with System.Collections.Generic.
        VisitUsingDirective called with System.Linq.
        VisitUsingDirective called with System.Text.
        VisitUsingDirective called with Microsoft.CodeAnalysis.
                Success. Adding Microsoft.CodeAnalysis.
        VisitUsingDirective called with Microsoft.CodeAnalysis.CSharp.
                Success. Adding Microsoft.CodeAnalysis.CSharp.
        VisitUsingDirective called with Microsoft.
                Success. Adding Microsoft.
        VisitUsingDirective called with System.ComponentModel.
        VisitUsingDirective called with Microsoft.Win32.
                Success. Adding Microsoft.Win32.
        VisitUsingDirective called with System.Runtime.InteropServices.
        VisitUsingDirective called with System.CodeDom.
        VisitUsingDirective called with Microsoft.CSharp.
                Success. Adding Microsoft.CSharp.
Microsoft.CodeAnalysis
Microsoft.CodeAnalysis.CSharp
Microsoft
Microsoft.Win32
Microsoft.CSharp
Press any key to continue . . .
```

Parabéns! Você usou a **API de sintaxe** para localizar tipos específicos de instruções C# e declarações em código-fonte C#.
