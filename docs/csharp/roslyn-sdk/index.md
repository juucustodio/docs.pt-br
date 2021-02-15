---
title: O SDK do .NET Compiler Platform (APIs do Roslyn)
description: Aprenda a usar o SDK do .NET Compiler Platform (também chamado de APIs do Roslyn) para entender o código .NET, identificar os erros e corrigi-los.
ms.date: 10/10/2017
ms.custom: mvc
ms.openlocfilehash: cd81551234a1bc955323e392f473cd01180f6dc5
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98899237"
---
# <a name="the-net-compiler-platform-sdk"></a>O SDK do .NET Compiler Platform

Os compiladores criam um modelo detalhado do código do aplicativo conforme validam a sintaxe e a semântica do código. O uso desse modelo para criar a saída executável do código-fonte. O SDK do .NET Compiler Platform fornece acesso a esse modelo. Cada vez mais, contamos com recursos do IDE (ambiente de desenvolvimento integrado), como IntelliSense, refatoração, renomeação inteligente, "Localizar todas as referências" e "Ir para definição" para aumentar nossa produtividade. Contamos com ferramentas de análise de código para melhorar a qualidade e com geradores de código para ajudar na criação do aplicativo. À medida que essas ferramentas ficam mais inteligentes, elas precisam de acesso a cada vez mais do modelo que somente os compiladores podem criar conforme processam o código do aplicativo. Essa é a missão principal das APIs do Roslyn: abrir as caixas opacas e permitir que as ferramentas e os usuários finais compartilhem na riqueza de compiladores de informações sobre nosso código.
Em vez de ser meros conversores de código-fonte e objeto-código-saída, por meio do Roslyn, os compiladores se tornam plataformas: as APIs que você pode usar para as tarefas relacionadas ao código em seus aplicativos e ferramentas.

## <a name="net-compiler-platform-sdk-concepts"></a>Conceitos do SDK do .NET Compiler Platform

O SDK do .NET Compiler Platform diminui drasticamente a barreira de entrada para a criação de aplicativos e ferramentas voltadas para o código. Ele cria muitas oportunidades de inovação em áreas como metaprogramação, geração de código e transformação, uso interativo das linguagens C# e Visual Basic e incorporação de C# e Visual Basic em linguagens específicas de domínio.

O SDK do .NET Compiler Platform permite compilar ***analisadores** _ e _*_correções de código_*_ que localizam e corrigem erros de codificação. Os _*_analisadores_*_ entendem a sintaxe (estrutura de código) e a semântica para detectar práticas que devem ser corrigidas. As _*_correções de código_*_ fornecem uma ou mais correções sugeridas para lidar com erros de codificação encontrados por analisadores ou diagnóstico de compilador. Normalmente, um analisador e as correções de código associadas são empacotados em um único projeto.

Os analisadores e as correções de código usam a análise estática para entender o código. Eles não executam o código ou fornecem outros benefícios de teste. No entanto, eles podem destacar práticas que geralmente levam a bugs, código não sustentável ou violação de diretriz padrão.

Além de analisadores e correções de código, o SDK do .NET Compiler Platform também permite que você crie _*_refatorações de código_*_.
Ele também fornece um conjunto único de APIs que permitem que você examine e entenda uma base de código C# ou Visual Basic. Uma vez que você pode usar essa base de código única, é possível escrever analisadores e correções de código com mais facilidade aproveitando as APIs de análise de sintaxe e de semântica fornecidas pelo SDK do .NET Compiler Platform. Liberado da enorme tarefa de replicar a análise feita pelo compilador, você pode se concentrar na tarefa de localizar e corrigir os erros de codificação comuns no projeto ou na biblioteca.

Um benefício menor é que os analisadores e as correções de código são menores e usam muito menos memória quando carregados no Visual Studio do que usariam se você tivesse escrito sua própria base de código para entender o código em um projeto. Aproveitando as mesmas classes usadas pelo compilador e o Visual Studio, você pode criar suas próprias ferramentas de análise estática. Isso significa que sua equipe poderá usar os analisadores e as correções de código sem um impacto significativo no desempenho do IDE.

Há três cenários principais para escrever analisadores e correções de código:

1. [Padrões de codificação de _Enforce equipe *](#enforce-team-coding-standards)
1. [*Fornecer diretrizes com pacotes de biblioteca*](#provide-guidance-with-library-packages)
1. [*Fornecer diretrizes gerais*](#provide-general-guidance)

## <a name="enforce-team-coding-standards"></a>Impor padrões de codificação à equipe

Muitas equipes têm padrões de codificação aplicados por meio de revisões de código feitas com outros membros da equipe. Os analisadores e as correções de código podem tornar esse processo muito mais eficiente. As revisões de código ocorrem quando um desenvolvedor compartilha seu trabalho com outras pessoas da equipe. O desenvolvedor terá investido todo o tempo necessário para concluir um novo recurso antes de obter algum comentário. Semanas podem passar enquanto o desenvolvedor reforça hábitos que não correspondem às práticas da equipe.

Os analisadores são executados à medida que um desenvolvedor escreve o código. O desenvolvedor obtém comentários imediatos que o incentiva a seguir as diretrizes no mesmo instante. O desenvolvedor cria hábitos para gravar códigos compatíveis assim que começa a criar protótipos. Quando o recurso está pronto para que outras pessoas o examinem, todas as diretrizes padrão já terão sido impostas.

As equipes podem criar analisadores e correções de código que procurem as práticas mais comuns que violem as práticas de codificação em equipe. Eles podem ser instalados nos computadores de cada desenvolvedor para impor os padrões.

> [!TIP]
> Antes de criar seu próprio analisador, confira os internos. Para obter mais informações, consulte [regras de estilo de código](../../fundamentals/code-analysis/overview.md#code-style-analysis).

## <a name="provide-guidance-with-library-packages"></a>Fornecer diretrizes com pacotes de biblioteca

Há uma infinidade de bibliotecas disponíveis para desenvolvedores do .NET no NuGet.
Algumas dessas provenientes da Microsoft, algumas de terceiros e outras de membros e de voluntários da comunidade. Essas bibliotecas obtêm mais adoção e análises mais positivas quando os desenvolvedores são bem-sucedidos com elas.

Além de fornecer a documentação, você pode fornecer analisadores e correções de código que encontram e corrigem os usos inadequados comuns da sua biblioteca. Essas correções imediatas ajudarão os desenvolvedores a obter êxito mais rapidamente.

Você pode empacotar analisadores e correções de código com sua biblioteca no NuGet. Nesse cenário, cada desenvolvedor que instalar o pacote do NuGet também instalará o pacote do analisador. Todos os desenvolvedores que estiverem usando a biblioteca obterão imediatamente as diretrizes da sua equipe na forma de comentários imediatos sobre erros e correções sugeridas.

## <a name="provide-general-guidance"></a>Fornecer diretrizes gerais

A comunidade de desenvolvedores do .NET descobriu, por meio de experiência, padrões que funcionam bem e padrões que são mais bem evitados. Vários membros da comunidade criaram analisadores que impõem esses padrões recomendados. À medida que aprendemos mais, sempre haverá espaço para novas ideias.

Esses analisadores podem ser carregados no [Visual Studio Marketplace](https://marketplace.visualstudio.com/vs) e baixados por desenvolvedores que usam o Visual Studio. Quem ainda não tem experiência na linguagem e na plataforma aprende rapidamente as práticas aceitas e se torna produtivo mais cedo em sua jornada no .NET. Quando as práticas se tornam amplamente usadas, a comunidade as adota.

## <a name="next-steps"></a>Próximas etapas

O SDK do .NET Compiler Platform inclui os modelos de objeto de linguagem mais recentes para geração de código, análise e refatoração. Esta seção fornece uma visão geral conceitual do SDK do .NET Compiler Platform. Mais detalhes podem ser encontrados nas seções guias de início rápido, exemplos e tutoriais.

Você pode saber mais sobre os conceitos no SDK do .NET Compiler Platform nestes cinco tópicos:

- [Explorar código com o visualizador de sintaxe](syntax-visualizer.md)
- [Entender o modelo de API do compilador](compiler-api-model.md)
- [Trabalhar com sintaxe](work-with-syntax.md)
- [Trabalhar com semântica](work-with-semantics.md)
- [Trabalhar com um workspace](work-with-workspace.md)

Para começar, será necessário instalar o **SDK do .NET Compiler Platform**:

[!INCLUDE[interactive-note](~/includes/roslyn-installation.md)]

<!--

Turn this on as more of the conceptual content is in place:
- Try the [Quickstarts](quickstart/index.md) to create your first tutorial.
- Experiment with one of the [Tutorials](tutorials/index.md).
- Explore the [Samples](samples/index.md) to see some simple analyzers.
- Read the [Concepts](concepts/index.md) to understand the ideas behind analyzers and code fixes.

-->
