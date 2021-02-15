---
title: Guia de estilo do F#
description: 'Aprenda os cinco princípios de um bom código F #.'
ms.date: 12/10/2018
ms.openlocfilehash: 9f47257626e04b09b546de2ae315d48d791678be
ms.sourcegitcommit: 67ebdb695fd017d79d9f1f7f35d145042d5a37f7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92223655"
---
# <a name="f-style-guide"></a>Guia de estilo do F#

Os artigos a seguir descrevem as diretrizes para formatar o código F # e as diretrizes do tópicas para recursos da linguagem e como eles devem ser usados.

Este guia foi formulado com base no uso de F # em bases de código grandes com um grupo variado de programadores. Essas diretrizes geralmente levam ao uso bem-sucedido de F # e minimizam as frustrações quando os requisitos de programas mudam ao longo do tempo.

## <a name="five-principles-of-good-f-code"></a>Cinco princípios de um bom código F #

Lembre-se dos princípios a seguir sempre que escrever código em F #, especialmente em sistemas que serão alterados ao longo do tempo. Cada parte das diretrizes em artigos adicionais se origina desses cinco pontos.

1. **O bom código F # é sucinto, expressivo e combinável**

    O F # tem muitos recursos que permitem expressar ações em menos linhas de código e reutilizar a funcionalidade genérica. A biblioteca de núcleos F # também contém muitos tipos e funções úteis para trabalhar com coleções comuns de dados. A composição de suas próprias funções e aquelas na biblioteca principal do F # (ou outras bibliotecas) fazem parte da programação de rotina idiomática F #. Como regra geral, se você puder expressar uma solução para um problema em menos linhas de código, outros desenvolvedores (ou seus futuros) serão apreciativo. Também é altamente recomendável que você use uma biblioteca como FSharp. Core, as [grandes bibliotecas .net](../../../api/index.md) em que o F # é executado, ou um pacote de terceiros no [NuGet](https://www.nuget.org/) quando você precisa fazer uma tarefa não trivial.

2. **O bom código F # é interoperável**

    A interoperação pode assumir vários formulários, incluindo o consumo de código em idiomas diferentes. Os limites de seu código que outros chamadores interoperam com são partes críticas para obter o direito, mesmo que os chamadores também estejam em F #. Ao escrever F #, você deve estar sempre pensando em como o outro código chamará o código que você está escrevendo, incluindo se eles fizerem de outra linguagem, como C#. As [diretrizes de design de componente F #](component-design-guidelines.md) descrevem a interoperabilidade em detalhes.

3. **O bom código F # usa a programação de objetos, não a orientação do objeto**

    O F # tem suporte completo para a programação com objetos no .NET, incluindo [classes](../language-reference/classes.md), [interfaces](../language-reference/interfaces.md), [modificadores de acesso](../language-reference/access-control.md), [classes abstratas](../language-reference/abstract-classes.md)e assim por diante. Para um código funcional mais complicado, como funções que devem ser reconhecidas por contexto, os objetos podem encapsular facilmente informações contextuais de maneiras que as funções não podem. Recursos como [parâmetros opcionais](../language-reference/members/methods.md#optional-arguments) e uso cuidadoso de [sobrecarga](../language-reference/members/methods.md#overloaded-methods) podem tornar o consumo dessa funcionalidade mais fácil para os chamadores.

4. **Um bom código F # funciona bem sem expor a mutação**

    Não é secreto que o código de alto desempenho seja escrito, você deve usar mutação. É assim que os computadores funcionam, afinal. Esse código geralmente é propenso a erros e é difícil de ficar certo. Evite expor mutação a chamadores. Em vez disso, [crie uma interface funcional que oculte uma implementação baseada em mutação quando o](conventions.md#performance) desempenho for crítico.

5. **O bom código F # é de ferramenta**

    As ferramentas são inestimávels para trabalhar em grandes bases de código, e você pode escrever códigos F # de modo que possam ser usados com mais eficiência com ferramentas de linguagem F #. Um exemplo é certificar-se de que você não o exagerar com um estilo de programação sem ponto, para que os valores intermediários possam ser inspecionados com um depurador. Outro exemplo é usar [comentários de documentação XML](../language-reference/xml-documentation.md) que descrevem construções de forma que as dicas de ferramentas em editores possam exibir esses comentários no local de chamada. Sempre pense em como seu código será lido, navegado, depurado e manipulado por outros programadores com suas ferramentas.

## <a name="next-steps"></a>Próximas etapas

As [diretrizes de formatação de código F #](formatting.md) fornecem orientação sobre como formatar código para que seja fácil de ler.

As [convenções de codificação f #](conventions.md) fornecem orientação para linguagens de programação f # que ajudarão a manutenção de longo prazo de bases de código f # maiores.

As [diretrizes de design de componentes do f #](component-design-guidelines.md) fornecem diretrizes para a criação de componentes do f #, como bibliotecas.
