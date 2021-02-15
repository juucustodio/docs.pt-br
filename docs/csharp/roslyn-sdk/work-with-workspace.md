---
title: Trabalhar com o modelo de workspace do SDK do .NET Compiler Platform
description: Esta visão geral fornece uma compreensão do tipo usado para consultar e manipular o workspace e os projetos para o código.
ms.date: 10/15/2017
ms.custom: mvc
ms.openlocfilehash: b613c85c01cc054dea9dd4bb9cf0062ffedb08bf
ms.sourcegitcommit: 8299abfbd5c49b596d61f1e4d09bc6b8ba055b36
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/27/2021
ms.locfileid: "98899107"
---
# <a name="work-with-a-workspace"></a>Trabalhar com um workspace

A camada **Workspaces** é o ponto inicial para fazer a análise de código e refatoração em soluções inteiras. Nessa camada, a API do Workspace ajudará você a organizar todas as informações sobre os projetos de uma solução em um único modelo de objeto, oferecendo acesso direto aos modelos de objeto da camada do compilador como texto de origem, árvores de sintaxe, modelos semânticos e compilações, sem a necessidade de analisar arquivos, configurar opções ou gerenciar dependências entre projetos.

Ambientes de host, como um IDE, fornecem um workspace para você correspondente à solução aberta. Também é possível usar esse modelo fora de um IDE apenas carregando um arquivo de solução.

## <a name="workspace"></a>Workspace

Um workspace é uma representação ativa da solução como uma coleção de projetos, cada uma com uma coleção de documentos. Um workspace normalmente é vinculado a um ambiente de host que está sendo modificado constantemente conforme um usuário digita ou manipula propriedades.

O <xref:Microsoft.CodeAnalysis.Workspace> fornece acesso ao modelo atual da solução. Quando ocorre uma alteração no ambiente de host, o workspace aciona eventos correspondentes e a propriedade <xref:Microsoft.CodeAnalysis.Workspace.CurrentSolution?displayProperty=nameWithType> é atualizada. Por exemplo, quando o usuário digita em um editor de texto algo correspondente a um dos documentos de origem, o workspace usa um evento para sinalizar que o modelo geral da solução foi alterado e qual documento foi modificado. Em seguida, você pode reagir a essas alterações analisando o novo modelo quanto à exatidão, realçando áreas de significância ou fazendo uma sugestão de alteração de código.

Também pode criar workspaces independentes desconectados do ambiente de host ou usados em um aplicativo que não tem nenhum ambiente de host.

## <a name="solutions-projects-and-documents"></a>Soluções, projetos e documentos

Embora um workspace possa ser alterado sempre que uma tecla é pressionada, você pode trabalhar com o modelo da solução de forma isolada.

Uma solução é um modelo imutável dos projetos e documentos. Isso significa que o modelo pode ser compartilhado sem bloqueio nem duplicação. Depois de obter uma instância da solução da propriedade <xref:Microsoft.CodeAnalysis.Workspace.CurrentSolution?displayProperty=nameWithType>, essa instância nunca será alterada. No entanto, assim como árvores de sintaxe e compilações, você pode modificar soluções construindo novas instâncias com base em soluções existentes e alterações específicas. Para fazer com que o workspace reflita as alterações, é necessário aplicar explicitamente a solução alterada novamente ao workspace.

Um projeto é uma parte do modelo de solução imutável geral. Ele representa todos os documentos do código-fonte, opções de análise e compilação e referências de assembly e projeto a projeto. Em um projeto, você pode acessar a compilação correspondente sem a necessidade de determinar as dependências de projeto nem analisar arquivos de origem.

Um documento também é uma parte do modelo de solução imutável geral. Um documento representa um único arquivo de origem do qual você pode acessar o texto do arquivo, a árvore de sintaxe e o modelo semântico.

O diagrama a seguir é uma representação de como o Workspace se relaciona ao ambiente de host, às ferramentas e ao modo como as edições são feitas.

![as relações entre os diferentes elementos de um workspace que contém projetos e arquivos de origem](media/work-with-workspace/workspace-obj-relations.png)

## <a name="summary"></a>Resumo

O Roslyn expõe um conjunto de APIs do compilador e APIs dos Workspaces que fornecem informações detalhadas sobre o código-fonte e que têm fidelidade total com as linguagens C# e Visual Basic.  O SDK do .NET Compiler Platform diminui drasticamente a barreira de entrada para a criação de aplicativos e ferramentas voltadas para o código. Ele cria muitas oportunidades de inovação em áreas como metaprogramação, geração de código e transformação, uso interativo das linguagens C# e Visual Basic e incorporação de C# e Visual Basic em linguagens específicas de domínio.  
