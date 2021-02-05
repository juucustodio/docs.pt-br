---
title: Instruções de nível superior – tutorial em C#
description: Este tutorial mostra como você pode usar as instruções de nível superior para testar e provar os conceitos enquanto explora suas ideias
ms.date: 10/28/2020
ms.openlocfilehash: c56a40e7a9715ff0265a897c494b457a32e52df2
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585618"
---
# <a name="tutorial-explore-ideas-using-top-level-statements-to-build-code-as-you-learn"></a>Tutorial: explorar ideias usando instruções de nível superior para criar código conforme você aprende

Neste tutorial, você aprenderá como:

> [!div class="checklist"]
>
> - Conheça as regras que regem o uso de instruções de nível superior.
> - Use as instruções de nível superior para explorar os algoritmos.
> - Refatorar explorações em componentes reutilizáveis.

## <a name="prerequisites"></a>Pré-requisitos

Você precisará configurar seu computador para executar o .NET 5, que inclui o compilador C# 9. O compilador do C# 9 está disponível a partir do [Visual Studio 2019 versão 16,9 Preview 1](https://visualstudio.microsoft.com/vs/preview/) ou do [SDK do .NET 5,0](https://dot.net/get-dotnet5).

Este tutorial pressupõe que você esteja familiarizado com o C# e .NET, incluindo o Visual Studio ou a CLI do .NET Core.

## <a name="start-exploring"></a>Comece a explorar

As instruções de nível superior permitem evitar a cerimônia extra necessária colocando o ponto de entrada do programa em um método estático em uma classe. O ponto de partida típico para um novo aplicativo de console é semelhante ao seguinte código:

```csharp
using System;

namespace Application
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

O código anterior é o resultado da execução do `dotnet new console` comando e da criação de um novo aplicativo de console. Essas 11 linhas contêm apenas uma linha de código executável. Você pode simplificar esse programa com o novo recurso de instruções de nível superior. Isso permite remover tudo, exceto duas das linhas deste programa:

```csharp
using System;

Console.WriteLine("Hello World!");
```

Essa ação simplifica o que é necessário para começar a explorar novas ideias. Você pode usar instruções de nível superior para cenários de script ou para explorar. Depois de trabalhar com as noções básicas, você pode começar a refatorar o código e criar métodos, classes ou outros assemblies para componentes reutilizáveis que você criou. As instruções de nível superior permitem a rápida experimentação e tutoriais iniciantes. Eles também fornecem um caminho suave de experimentação para programas completos.

As instruções de nível superior são executadas na ordem em que aparecem no arquivo. Instruções de nível superior só podem ser usadas em um arquivo de origem em seu aplicativo. O compilador gerará um erro se você usá-los em mais de um arquivo.

## <a name="build-a-magic-net-answer-machine"></a>Criar uma máquina de resposta do .NET mágico

Para este tutorial, vamos criar um aplicativo de console que responde a uma pergunta "Sim" ou "não" com uma resposta aleatória. Você criará a funcionalidade passo a passo. Você pode se concentrar em sua tarefa em vez de na cerimônia necessária para a estrutura de um programa típico. Em seguida, quando estiver satisfeito com a funcionalidade, você poderá refatorar o aplicativo como desejar.

Um bom ponto de partida é escrever a pergunta de volta ao console. Você pode começar escrevendo o código a seguir:

```csharp
using System;

Console.WriteLine(args);
```

Você não declara uma `args` variável. Para o arquivo de origem único que contém as instruções de nível superior, o compilador reconhece `args` para significar os argumentos de linha de comando. O tipo de args é a `string[]` , como em todos os programas em C#.

Você pode testar seu código executando o seguinte `dotnet run` comando:

```dotnetcli
dotnet run -- Should I use top level statements in all my programs?
```

Os argumentos após o `--` na linha de comando são passados para o programa. Você pode ver o tipo da `args` variável, pois isso é o que é impresso no console:

```console
System.String[]
```

Para gravar a pergunta no console, você precisará enumerar os argumentos e separá-los com um espaço. Substitua a `WriteLine` chamada pelo código a seguir:

:::code language="csharp" source="snippets/top-level-statements/ProgramSnippets.cs" ID="EchoInput":::

Agora, quando você executar o programa, ele exibirá corretamente a pergunta como uma cadeia de caracteres de argumentos.

## <a name="respond-with-a-random-answer"></a>Responder com uma resposta aleatória

Depois de ecoar a pergunta, você pode adicionar o código para gerar a resposta aleatória. Comece adicionando uma matriz de possíveis respostas:

:::code language="csharp" source="snippets/top-level-statements/ProgramSnippets.cs" ID="Answers":::

Essa matriz tem 12 respostas que são afirmativo, seis que não são confirmadas e seis que são negativas. Em seguida, adicione o seguinte código para gerar e exibir uma resposta aleatória da matriz:

:::code language="csharp" source="snippets/top-level-statements/ProgramSnippets.cs" ID="GenerateAnswer":::

Você pode executar o aplicativo novamente para ver os resultados. Você deverá ver algo semelhante à seguinte saída:

```dotnetcli
dotnet run -- Should I use top level statements in all my programs?

Should I use top level statements in all my programs?
Better not tell you now.
```

Esse código responde às perguntas, mas vamos adicionar mais um recurso. Você gostaria que seu aplicativo de pergunta simulasse pensar sobre a resposta. Você pode fazer isso adicionando um pouco de animação ASCII e pausando enquanto trabalha.  Adicione o seguinte código após a linha que ecoa a pergunta:

:::code language="csharp" source="snippets/top-level-statements/UtilitiesPassOne.cs" ID="AnimationFirstPass":::

Você também precisará adicionar uma `using` instrução à parte superior do arquivo de origem:

```csharp
using System.Threading.Tasks;
```

As `using` instruções devem ser anteriores a qualquer outra instrução no arquivo. Caso contrário, é um erro do compilador. Você pode executar o programa novamente e ver a animação. Isso faz uma melhor experiência. Experimente o comprimento do atraso para corresponder ao seu gosto.

O código anterior cria um conjunto de linhas giratórias separadas por um espaço. A adição da `await` palavra-chave instrui o compilador a gerar o ponto de entrada do programa como um método que tem o `async` modificador e retorna um <xref:System.Threading.Tasks.Task?displayProperty=nameWithType> . Este programa não retorna um valor, portanto, o ponto de entrada do programa retorna um `Task` . Se o seu programa retornar um valor inteiro, você adicionaria uma instrução return ao final de suas instruções de nível superior. Essa instrução de retorno especificaria o valor inteiro a ser retornado. Se as instruções de nível superior incluírem uma `await` expressão, o tipo de retorno se tornará <xref:System.Threading.Tasks.Task%601?displayProperty=nameWithType> .

## <a name="refactoring-for-the-future"></a>Refatoração para o futuro

Seu programa deve ser semelhante ao seguinte código:

```csharp
using System;
using System.Threading.Tasks;

Console.WriteLine();
foreach(var s in args)
{
    Console.Write(s);
    Console.Write(' ');
}
Console.WriteLine();

for (int i = 0; i < 20; i++)
{
    Console.Write("| -");
    await Task.Delay(50);
    Console.Write("\b\b\b");
    Console.Write("/ \\");
    await Task.Delay(50);
    Console.Write("\b\b\b");
    Console.Write("- |");
    await Task.Delay(50);
    Console.Write("\b\b\b");
    Console.Write("\\ /");
    await Task.Delay(50);
    Console.Write("\b\b\b");
}
Console.WriteLine();

string[] answers =
{
    "It is certain.",       "Reply hazy, try again.",     "Don’t count on it.",
    "It is decidedly so.",  "Ask again later.",           "My reply is no.",
    "Without a doubt.",     "Better not tell you now.",   "My sources say no.",
    "Yes – definitely.",    "Cannot predict now.",        "Outlook not so good.",
    "You may rely on it.",  "Concentrate and ask again.", "Very doubtful.",
    "As I see it, yes.",
    "Most likely.",
    "Outlook good.",
    "Yes.",
    "Signs point to yes.",
};

var index = new Random().Next(answers.Length - 1);
Console.WriteLine(answers[index]);
```

O código anterior é razoável. Funciona. Mas não é reutilizável. Agora que o aplicativo está funcionando, é hora de retirar as partes reutilizáveis.

Um candidato é o código que exibe a animação em espera. Esse trecho de código pode se tornar um método:

Você pode começar criando uma função local em seu arquivo. Substitua a animação atual pelo código a seguir:

```csharp
await ShowConsoleAnimation();

static async Task ShowConsoleAnimation()
{
    for (int i = 0; i < 20; i++)
    {
        Console.Write("| -");
        await Task.Delay(50);
        Console.Write("\b\b\b");
        Console.Write("/ \\");
        await Task.Delay(50);
        Console.Write("\b\b\b");
        Console.Write("- |");
        await Task.Delay(50);
        Console.Write("\b\b\b");
        Console.Write("\\ /");
        await Task.Delay(50);
        Console.Write("\b\b\b");
    }
    Console.WriteLine();
}
```

O código anterior cria uma função local dentro do método Main. Isso ainda não pode ser reutilizado. Portanto, extraia esse código em uma classe. Crie um novo arquivo chamado *Utilities.cs* e adicione o seguinte código:

:::code language="csharp" source="snippets/top-level-statements/UtilitiesPassOne.cs" ID="SnippetUtilities":::

As instruções de nível superior só podem estar em um arquivo, e esse arquivo não pode conter namespaces ou tipos.

Por fim, você pode limpar o código de animação para remover alguma duplicação:

:::code language="csharp" source="snippets/top-level-statements/Utilities.cs" ID="Animation":::

Agora você tem um aplicativo completo e refatorou as partes reutilizáveis para uso posterior. Você pode chamar o novo método de utilitário de suas instruções de nível superior, conforme mostrado abaixo na versão concluída do programa principal:

:::code language="csharp" source="snippets/top-level-statements/Program.cs":::

Isso adiciona a chamada para `Utilities.ShowConsoleAnimation` e adiciona uma instrução adicional `using` .

## <a name="summary"></a>Resumo

As instruções de nível superior facilitam a criação de programas simples para serem usados para explorar novos algoritmos. Você pode experimentar algoritmos experimentando trechos de código diferentes. Depois de aprender o que funciona, você pode refatorar o código para ser mais passível de manutenção.

Instruções de nível superior simplificam programas baseados em aplicativos de console. Isso inclui o Azure functions, ações do GitHub e outros utilitários pequenos.
