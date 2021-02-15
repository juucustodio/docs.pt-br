---
title: Introdução ao C# – familiarize-se com as ferramentas de desenvolvimento
description: Este artigo fornece uma introdução básica às ferramentas que você usará para desenvolver aplicativos C# e .NET no seu computador.
ms.date: 02/02/2021
ms.openlocfilehash: d5fbd23679fc11f4e4c207c59858a71ab753c038
ms.sourcegitcommit: 65af0f0ad316858882845391d60ef7e303b756e8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/05/2021
ms.locfileid: "99585319"
---
# <a name="set-up-your-local-environment"></a>Configurar o ambiente local

A primeira etapa para executar um tutorial em seu computador é configurar um ambiente de desenvolvimento. Escolha uma das seguintes alternativas:

* Para usar a CLI do .NET e sua escolha de texto ou editor de código, consulte o tutorial do .NET [Olá, mundo em 10 minutos](https://dotnet.microsoft.com/learn/dotnet/hello-world-tutorial/intro). O tutorial tem instruções para configurar um ambiente de desenvolvimento no Windows, Linux ou macOS.
* Para usar a CLI do .NET e Visual Studio Code, instale o [SDK do .net](https://dotnet.microsoft.com/download) e o [Visual Studio Code](https://code.visualstudio.com/).
* Para usar o Visual Studio 2019 no Windows, consulte [tutorial: criar um aplicativo de console C# simples no Visual Studio](/visualstudio/get-started/csharp/tutorial-console).

## <a name="basic-application-development-flow"></a>Fluxo de desenvolvimento de aplicativos básico

As instruções nesses tutoriais pressupõem que você esteja usando a CLI do .NET para criar, compilar e executar aplicativos. Você usará os seguintes comandos:

* [`dotnet new`](../../../core/tools/dotnet-new.md) Cria um aplicativo. Este comando gera os arquivos e ativos necessários para o seu aplicativo. Todos os tutoriais de introdução ao C# usam o tipo de aplicativo `console`. Depois de conhecer as noções básicas, você poderá expandir para outros tipos de aplicativo.
* [`dotnet build`](../../../core/tools/dotnet-build.md) compila o executável.
* [`dotnet run`](../../../core/tools/dotnet-run.md) executa o executável.

Se você usar o Visual Studio 2019 para esses tutoriais, escolherá uma seleção de menu do Visual Studio quando um tutorial o direcionar a executar um destes comandos da CLI:

* Do **arquivo**  >  **Novo**  >  O **projeto** cria um aplicativo.
* **Criar**  >   A **solução de compilação** compila o executável.
* **Depurar**  >  **Iniciar sem depuração** executa o executável.

## <a name="pick-your-tutorial"></a>Escolha seu tutorial

Você pode iniciar com qualquer um dos seguintes tutoriais:

## <a name="numbers-in-c"></a>Números em C\#

No tutorial [Números em C#](numbers-in-csharp-local.md), você aprenderá como os computadores armazenam números e como executar cálculos com diferentes tipos de número. Você aprenderá os conceitos básicos de arredondamento e como executar cálculos matemáticos usando C#.

Esse tutorial pressupõe a conclusão da lição [Olá, Mundo](hello-world.yml).

## <a name="branches-and-loops"></a>Loops e branches

O tutorial [Branches e loops](branches-and-loops-local.md) ensina os conceitos básicos da seleção de diferentes caminhos de execução de código com base nos valores armazenados em variáveis. Você aprenderá os conceitos básicos do fluxo de controle, que são os fundamentos de como os programas tomam decisões e escolhem ações diferentes.

Esse tutorial pressupõe a conclusão das lições [Olá, Mundo](hello-world.yml) e [Números em C#](numbers-in-csharp-local.md).

## <a name="list-collection"></a>Coleções de lista

A lição [Coleções de lista](arrays-and-collections.md) fornece um tour pelo tipo Coleções de lista que armazena as sequências de dados. Você aprenderá a adicionar e remover itens, pesquisar itens e classificar listas. Você explorará os diferentes tipos de listas.

Esse tutorial pressupõe a conclusão das lições listadas acima.

## <a name="introduction-to-classes"></a>Introdução às classes

Na [introdução às classes](introduction-to-classes.md), você criará um aplicativo de console e verá os recursos básicos orientados a objeto que fazem parte da linguagem C#. Este é o tutorial final da introdução ao C#. Ele só está disponível para execução em seu computador, usando seu próprio ambiente de desenvolvimento local e .NET.
