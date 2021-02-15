---
title: Explorar código com o visualizador de sintaxe Roslyn no Visual Studio
description: O visualizador de sintaxe fornece uma ferramenta visual para explorar os modelos que o SDK do .NET Compiler Platform gera para o código.
ms.date: 03/07/2018
ms.custom: mvc, vs-dotnet
ms.openlocfilehash: a911a99e78ad5a5f4c6771b91a3c541b1812d67c
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91167568"
---
# <a name="explore-code-with-the-roslyn-syntax-visualizer-in-visual-studio"></a>Explorar código com o visualizador de sintaxe Roslyn no Visual Studio

Este artigo oferece uma visão geral sobre a ferramenta de Visualizador de sintaxe que é fornecida como parte do SDK do .NET Compiler Platform ("Roslyn"). O Visualizador de sintaxe é uma janela de ferramentas que ajuda a inspecionar e explorar árvores de sintaxe. É uma ferramenta essencial para compreender os modelos do código que você deseja analisar. Também é um auxílio para depuração ao desenvolver seus próprios aplicativos usando o SDK do.NET Compiler Platform ("Roslyn"). Abra essa ferramenta ao criar seus primeiros analisadores. O visualizador ajuda você a entender os modelos usados pelas APIs. Você também pode usar ferramentas como [SharpLab](https://sharplab.io) ou [LINQPad](https://www.linqpad.net/) para inspecionar o código e entender as árvores de sintaxe.

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

Familiarize-se com os conceitos usados no SDK do.NET Compiler Platform lendo o artigo de [visão geral](compiler-api-model.md). Ele fornece uma introdução a árvores de sintaxe, nós, tokens e trívia.

## <a name="syntax-visualizer"></a>Visualizador de sintaxe

O **Syntax Visualizer** habilita a inspeção da árvore de sintaxe para o arquivo de código C# ou Visual Basic na janela atual do editor ativo dentro do IDE do Visual Studio. O Visualizador pode ser iniciado clicando em **Exibir**  >  **outras**  >  **Syntax Visualizer**do Windows.  Você também pode usar a barra de ferramentas de **Início Rápido** no canto superior direito. Digite "sintaxe" e o comando para abrir o **Visualizador de sintaxe** deverá aparecer.

Este comando abre o Visualizador de sintaxe como uma janela de ferramentas flutuante. Se você não tiver uma janela de editor de código aberta, a exibição ficará em branco, conforme mostrado na figura a seguir.

![A janela de ferramentas do Visualizador de sintaxe](media/syntax-visualizer/syntax-visualizer.png)

Encaixe esta janela de ferramentas em um local conveniente dentro do Visual Studio, como o lado esquerdo. O Visualizador mostra informações sobre o arquivo de código atual.

Crie um novo projeto usando o comando **File**  >  **New Project** . Você pode criar um projeto Visual Basic ou C#. Quando o Visual Studio abre o arquivo de código principal deste projeto, o visualizador exibe a árvore de sintaxe dele. Você pode abrir qualquer arquivo C#/Visual Basic existente nessa instância do Visual Studio e o visualizador exibe a árvore de sintaxe do arquivo. Se você tiver vários arquivos de código abertos no Visual Studio, o visualizador exibirá a árvore de sintaxe do arquivo de código atualmente ativo, (o arquivo de código que tem o foco do teclado).

<!-- markdownlint-disable MD025 -->

# <a name="c"></a>[C#](#tab/csharp)

![Visualizando uma árvore de sintaxe de C#](media/syntax-visualizer/visualize-csharp.png)

# <a name="visual-basic"></a>[Visual Basic](#tab/vb)

![Visualizando uma árvore de sintaxe de Visual Basic](media/syntax-visualizer/visualize-visual-basic.png)

---

Conforme mostrado nas imagens acima, a janela de ferramentas do visualizador exibe a árvore de sintaxe na parte superior e uma grade de propriedade na parte inferior. A grade de propriedade exibe as propriedades do item atualmente selecionado na árvore, incluindo *Type* e *Kind* (SyntaxKind) do .NET do item.

As árvores de sintaxe incluem três tipos de itens: *nós*, *tokens* e *trívia*. Você pode ler mais sobre esses tipos no artigo [Trabalhar com sintaxe](work-with-syntax.md). Os itens de cada tipo estão representados com cores diferentes. Clique no botão "Legenda" para uma visão geral das cores usadas.

Cada item da árvore também exibe sua própria **extensão**. A **extensão** é composta pelos índices (a posição inicial e final) do nó no arquivo de texto.  No exemplo de C# anterior, o token “UsingKeyword [0..5)” selecionado tem uma **abrangência** de cinco caracteres de largura, [0..5). A notação "[..)" significa que o índice inicial faz parte da extensão, mas o índice final não.

Há duas maneiras de navegar na árvore:

* Expandir ou clicar em itens na árvore. O visualizador seleciona automaticamente o texto correspondente à extensão do item no editor de código.
* Clicar ou selecionar texto no editor de código. No exemplo de Visual Basic anterior, se você selecionar a linha que contém "Module Module1" no editor de código, o visualizador navegará automaticamente para o nó ModuleStatement correspondente na árvore.

O visualizador realça o item da árvore cuja extensão melhor corresponda com a extensão do texto selecionado no editor.

O visualizador atualiza a árvore para corresponder às modificações no arquivo de código ativo. Adicione uma chamada a `Console.WriteLine()` dentro de `Main()`. Conforme você digita, o visualizador atualiza a árvore.

Pare de digitar quando já tiver digitado `Console.`. A árvore tem alguns itens coloridos em rosa. Neste ponto, há erros (também conhecidos como "Diagnóstico") no código digitado. Esses erros são anexados a nós, tokens e trívia na árvore de sintaxe. O visualizador mostra quais itens têm erros anexados a eles, realçando a tela de fundo em rosa. Você pode inspecionar os erros em qualquer item colorido em rosa passando o mouse sobre o item. O visualizador exibe somente erros sintáticos (os erros relacionados à sintaxe do código digitado); erros semânticos não são exibidos.

## <a name="syntax-graphs"></a>Gráficos de sintaxe

Clique com o botão direito do mouse em qualquer item da árvore e clique em **Exibir gráfico de sintaxe direcionado**.

# <a name="c"></a>[C#](#tab/csharp)

O visualizador exibe uma representação gráfica da subárvore com raiz no item selecionado. Repita essas etapas para o nó **MethodDeclaration** correspondente ao método `Main()` no exemplo de C#. O visualizador exibe um gráfico de sintaxe que tem a seguinte aparência:

![Exibindo um gráfico de sintaxe de C#](media/syntax-visualizer/csharp-syntax-graph.png)

# <a name="visual-basic"></a>[Visual Basic](#tab/vb)

Tente o mesmo para o nó de **subbloco** correspondente ao `Main()` método no exemplo de Visual Basic anterior. O visualizador exibe um gráfico de sintaxe que tem a seguinte aparência:

![Exibindo um grafo de sintaxe de Visual Basic](media/syntax-visualizer/visual-basic-syntax-graph.png)

---

A sintaxe do Graph Viewer tem uma opção para exibir uma legenda para seu esquema de cores. Você também pode passar o mouse sobre itens específicos no gráfico de sintaxe para exibir as respectivas propriedades.

Você pode exibir gráficos de sintaxe de itens diferentes da árvore repetidamente e os gráficos serão sempre exibidos na mesma janela no Visual Studio. Você pode encaixar essa janela em um local conveniente no Visual Studio para não precisar alternar entre as guias para exibir um novo gráfico de sintaxe. A parte inferior, abaixo das janelas do editor de código, geralmente é conveniente.

Veja o layout de encaixe para usar com a janela de ferramentas do visualizador e a janela do gráfico de sintaxe:

![Um layout de encaixe para a janela de gráfico de sintaxe e o visualizador](media/syntax-visualizer/docking-layout.png)

Outra opção é colocar a janela de gráfico de sintaxe em um segundo monitor, em uma configuração de dois monitores.

## <a name="inspecting-semantics"></a>Inspecionando semântica

O Visualizador de sintaxe possibilita uma inspeção rudimentar de símbolos e informações semânticas. Digite `double x = 1 + 1;` dentro de Main() no exemplo de C#. Em seguida, selecione a expressão `1 + 1` na janela do editor de código. O visualizador realça o nó **AddExpression** no visualizador. Clique com o botão direito do mouse nesse **AddExpression** e clique em **Exibir Symbol (se houver)**. Observe que a maioria dos itens de menu tem o qualificador "se houver". O Visualizador de sintaxe inspeciona as propriedades de um Nó, incluindo propriedades que podem não estar presentes em todos os nós.

A grade de propriedade do visualizador é atualizada conforme mostrado na figura a seguir: o símbolo da expressão é um **SynthesizedIntrinsicOperatorSymbol** com **Kind = Method**.

![Propriedades Symbol](media/syntax-visualizer/symbol-properties.png)

Experimente **Exibir TypeSymbol (se houver)** para o mesmo nó **AddExpression**. A grade de propriedade no visualizador é atualizada, conforme mostrado na figura a seguir, indicando que o tipo da expressão selecionada é `Int32`.

![Propriedades TypeSymbol](media/syntax-visualizer/type-symbol-properties.png)

Experimente **Exibir TypeSymbol Convertido (se houver)** para o mesmo nó **AddExpression**. A grade de propriedade é atualizada, indicando que, embora o tipo da expressão seja `Int32`, o tipo convertido da expressão é `Double`, conforme mostrado na figura a seguir. Esse nó inclui informações de símbolo de tipo convertido porque a expressão `Int32` ocorre em um contexto em que deve ser convertida em um `Double`. Essa conversão satisfaz o tipo `Double` especificado para a variável `x` no lado esquerdo do operador de atribuição.

![Propriedades TypeSymbol convertidas](media/syntax-visualizer/converted-type-symbol-properties.png)

Por fim, experimente **Exibir Valor Constante (se houver)** para o mesmo nó **AddExpression**. A grade de propriedade mostra que o valor da expressão é uma constante de tempo de compilação com o valor `2`.

![Um valor constante](media/syntax-visualizer/constant-value.png)

O exemplo anterior também pode ser replicado no Visual Basic. Digite `Dim x As Double = 1 + 1` um arquivo de Visual Basic. Selecione a expressão `1 + 1` na janela do editor de código. O visualizador realça o nó **AddExpression** correspondente no visualizador. Repita as etapas anteriores para esta **AddExpression** e você verá resultados idênticos.

Examine mais códigos em Visual Basic. Atualize o arquivo de Visual Basic principal com o seguinte código:

```vb
Imports C = System.Console

Module Program
    Sub Main(args As String())
        C.WriteLine()
    End Sub
End Module
```

Esse código introduz um alias chamado `C` que mapeia para o tipo `System.Console` na parte superior do arquivo e usa esse alias em `Main()`. Selecione o uso desse alias, o `C` em `C.WriteLine()`, dentro do método `Main()`. O visualizador seleciona o nó **IdentifierName** correspondente no visualizador. Clique com botão direito do mouse nesse nó e clique em **Exibir Symbol (se houver)**. A grade de propriedade mostra que esse identificador é associado com o tipo `System.Console`, conforme mostrado na figura a seguir:

![Propriedades Symbol](media/syntax-visualizer/symbol-visual-basic.png)

Experimente **Exibir AliasSymbol (se houver)** para o mesmo nó **IdentifierName**. A grade de propriedade mostra que o identificador é um alias com nome `C`, que é associado com o destino `System.Console`. Em outras palavras, a grade de propriedade fornece informações sobre o **AliasSymbol** correspondente ao identificador `C`.

![Propriedades AliasSymbol](media/syntax-visualizer/alias-symbol.png)

Inspecione o símbolo correspondente a qualquer tipo, método e propriedade declarados. Selecione o nó correspondente no visualizador e clique em **Exibir Symbol (se houver)**. Selecione o método `Sub Main()`, incluindo o corpo do método. Clique em **Exibir Symbol (se houver)** para o nó **SubBlock** correspondente no visualizador. A grade de propriedade mostra que o **MethodSymbol** deste **SubBlock** tem nome `Main` com o tipo de retorno `Void`.

![Exibindo o símbolo de uma declaração de método](media/syntax-visualizer/method-symbol.png)

Os exemplos de Visual Basic acima podem ser facilmente replicados em C#. Digite `using C = System.Console;` no lugar de `Imports C = System.Console` para o alias. As etapas anteriores em C# geram resultados idênticos na janela do visualizador.

As operações de inspeção semântica estão disponíveis somente em nós. Elas não estão disponíveis em tokens nem trívia. Nem todos os nós têm informações semânticas interessantes para inspecionar. Quando um nó não tem informações semânticas interessantes, clicar em **Exibir \* Symbol (se houver)** mostrará uma grade de propriedade em branco.

Você pode ler mais sobre as APIs para executar análise semântica no documento de visão geral [Trabalhar com semântica](work-with-semantics.md).

## <a name="closing-the-syntax-visualizer"></a>Fechando o visualizador de sintaxe

Você pode fechar a janela do visualizador quando não a estiver usando para examinar o código-fonte. O Visualizador de sintaxe atualiza sua exibição à medida que você navega pelo código, editando e alterando a origem. Ele poderá se tornar uma distração quando você não estiver usando.
