---
title: Introdução ao C# – tutoriais interativos
description: Aprenda C# em seu navegador e comece a trabalhar com seu próprio ambiente de desenvolvimento
ms.date: 02/02/2021
ms.custom: mvc
ms.openlocfilehash: 62856206c30afac04346d150560c458c6795077d
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585644"
---
# <a name="introduction-to-c"></a>Introdução ao C\#

Bem-vindo aos tutoriais de introdução ao C#. Essas lições começam com código interativo que você pode executar em seu navegador. Você pode aprender as noções básicas do C# na [série de vídeos do c# 101](https://aka.ms/dotnet3-csharp) antes de iniciar essas lições interativas.

<!--markdownlint-disable MD034 -->
> [!VIDEO https://channel9.msdn.com/Series/CSharp-101/What-is-C/player]

As primeiras lições explicam os conceitos de C# usando pequenos snippets de código. Você aprenderá os conceitos básicos da sintaxe de C# e como trabalhar com tipos de dados como cadeias de caracteres, números e valores boolianos. É tudo interativo e você começará a gravar e executar o código em questão de minutos. Estas primeiras lições não exigem conhecimento prévio de programação ou da linguagem C#.

Você pode experimentar esses tutoriais em ambientes diferentes. Os conceitos que você aprenderá são os mesmos. A diferença é qual experiência você prefere:

- [No navegador, na plataforma docs](hello-world.yml): essa experiência incorpora uma janela de código do C# executável em páginas de documentos. Você escreve e executa o código C# no navegador.
- [Na experiência de Microsoft Learn](/learn/paths/csharp-first-steps/). Este roteiro de aprendizagem contém vários módulos que ensinam as noções básicas do C#.
- [No Jupyter no fichário](https://mybinder.org/v2/gh/dotnet/try-samples/master?filepath=hello-csharp%2Fhello-world.ipynb). Você pode experimentar o código C# em um notebook Jupyter no fichário.
- [No computador local](numbers-in-csharp-local.md). Depois de explorar online, você pode [baixar](https://dotnet.microsoft.com/download) o SDK do .NET Core e criar programas em seu computador.

Todos os tutoriais de introdução posteriores à lição Olá, Mundo estão disponíveis por meio da experiência de navegador online ou [em seu próprio ambiente de desenvolvimento local](local-environment.md). No final de cada tutorial, você decidirá se deseja continuar com a próxima lição online ou no próprio computador. Há links para ajudar você a configurar seu ambiente e continuar com o próximo tutorial no computador.

## <a name="hello-world"></a>[Olá, mundo](hello-world.yml)

No tutorial [Olá, Mundo](hello-world.yml), você criará o programa C# mais básico. Você explorará o tipo `string` e como trabalhar com texto. Você também pode usar o caminho em [Microsoft Learn](/learn/paths/csharp-first-steps/) ou [Jupyter no fichário](https://mybinder.org/v2/gh/dotnet/try-samples/master?filepath=hello-csharp%2Fhello-world.ipynb).

## <a name="numbers-in-c"></a>[Números em C#](numbers-in-csharp.yml)

No tutorial [Números em C#](numbers-in-csharp.yml), você aprenderá como os computadores armazenam números e como executar cálculos com diferentes tipos de número. Você aprenderá os conceitos básicos de arredondamento e como executar cálculos matemáticos usando C#. Este tutorial também está disponível [para execução local no seu computador](numbers-in-csharp-local.md).

Este tutorial pressupõe que você concluiu a lição [Olá, mundo](hello-world.yml) .

## <a name="branches-and-loops"></a>[Loops e branches](branches-and-loops.yml)

O tutorial [Branches e loops](branches-and-loops.yml) ensina os conceitos básicos da seleção de diferentes caminhos de execução de código com base nos valores armazenados em variáveis. Você aprenderá os conceitos básicos do fluxo de controle, que são os fundamentos de como os programas tomam decisões e escolhem ações diferentes. Este tutorial também está disponível [para execução local no seu computador](branches-and-loops-local.md).

Este tutorial pressupõe que você concluiu o [Olá mundo](hello-world.yml) e os [números em lições do C#](numbers-in-csharp.yml) .

## <a name="list-collection"></a>[Coleções de lista](list-collection.yml)

A lição [Coleções de lista](list-collection.yml) fornece um tour pelo tipo Coleções de lista que armazena as sequências de dados. Você aprenderá a adicionar e remover itens, pesquisar itens e classificar listas. Você explorará os diferentes tipos de listas. Este tutorial também está disponível [para execução local no seu computador](arrays-and-collections.md).

Este tutorial pressupõe que você concluiu as lições listadas acima.

## <a name="introduction-to-classes"></a>[Introdução às classes](introduction-to-classes.md)

Este tutorial só está disponível para ser executado em seu computador, usando seu próprio ambiente de desenvolvimento local e o .NET Core.
Você compilará um aplicativo de console e verá os recursos básicos orientados para objeto que fazem parte da linguagem C#.

Este tutorial pressupõe a conclusão dos tutoriais de introdução online e a instalação do [SDK do .NET Core](https://dotnet.microsoft.com/download) e do [Visual Studio Code](https://code.visualstudio.com/).

## <a name="object-oriented-programming"></a>[Programação orientada a objeto](object-oriented-programming.md)

Este tutorial ensina os conceitos usados na programação orientada a objeto. Você aprenderá os conceitos de *abstração*, *encapsulamento*, *herança* e *polimorfismo* usando exemplos de C#.

Este tutorial pressupõe que você concluiu os tutoriais de introdução online e instalou [SDK do .NET Core](https://dotnet.microsoft.com/download) e [Visual Studio Code](https://code.visualstudio.com/) ou o [Visual Studio](https://visualstudio.com) em seu computador de desenvolvimento.

## <a name="101-linq-samples"></a>[Exemplos de LINQ 101](https://github.com/dotnet/try-samples/tree/master/101-linq-samples)

Este exemplo requer a ferramenta global [dotnet-try](https://github.com/dotnet/try/blob/main/README.md#setup) . Depois de instalar a ferramenta e clonar o repositório [try-Samples](https://github.com/dotnet/try-samples) , você pode aprender LINQ (consulta integrada à linguagem) por meio de um conjunto de exemplos de 101 que podem ser executados interativamente. Você pode explorar diferentes maneiras de consultar, explorar e transformar sequências de dados.
