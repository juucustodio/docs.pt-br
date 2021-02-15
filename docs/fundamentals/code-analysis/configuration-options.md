---
title: Configurar regras de análise de código
description: Saiba como configurar regras de análise de código em um arquivo de configuração do Analyzer.
ms.date: 09/24/2020
ms.topic: conceptual
no-loc:
- EditorConfig
ms.openlocfilehash: 9c09fc381a161a9deea012d98d06ab57f2f7345e
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100480538"
---
# <a name="configuration-options-for-code-analysis"></a>Opções de configuração para análise de código

As regras de análise de código têm várias opções de configuração. Essas opções são especificadas como pares chave-valor em um [arquivo de configuração do analisador](configuration-files.md) usando a sintaxe `<option key> = <option value>` .

A opção mais comum que você configurará é a severidade de uma [regra](#severity-level). Você pode configurar o nível de severidade para todas as regras do analisador, incluindo [regras de qualidade de código](quality-rules/index.md) e regras de estilo de [código](style-rules/index.md). Por exemplo, para habilitar uma regra como um aviso, você pode adicionar o seguinte par chave-valor a um EditorConfig arquivo.

`dotnet_diagnostic.<rule ID>.severity = warning`

Você também pode configurar opções adicionais para personalizar o comportamento da regra:

- As regras de qualidade de código têm [Opções adicionais](code-quality-rule-options.md) para configurar o comportamento, como a quais nomes de método uma regra deve ser aplicada.
- As regras de estilo de código têm [Opções de estilo de código personalizadas](code-style-rule-options.md).
- As regras de analisador de terceiros podem definir suas próprias opções de configuração, com nomes de chave personalizados e formatos de valor.

A sintaxe para configurar a severidade de uma regra específica em um [arquivo de configuração do analisador](configuration-files.md) é a seguinte:

```ini
dotnet_diagnostic.<rule ID>.severity = <severity>
```

## <a name="general-options"></a>Opções gerais

Essas opções se aplicam à análise de código como um todo. Eles não podem ser aplicados somente a uma única regra ou conjunto de regras.

### <a name="exclude-generated-code"></a>Excluir código gerado

Você pode configurar arquivos e pastas adicionais para serem tratados como código gerado adicionando uma `generated_code = true | false` entrada ao arquivo de [configuração](configuration-files.md). Os avisos do analisador de código .NET não são úteis em arquivos de código gerados, como arquivos gerados pelo designer, que os usuários não podem editar para corrigir quaisquer violações. Na maioria dos casos, os analisadores de código ignoram os arquivos de código gerados e não relatam violações nesses arquivos.

Por padrão, os arquivos com determinadas extensões de arquivo ou cabeçalhos de arquivo gerados automaticamente são tratados como arquivos de código gerados. Por exemplo, um nome de arquivo que termina com `.designer.cs` ou `.generated.cs` é considerado código gerado. Essa opção de configuração permite que você especifique padrões de nomenclatura adicionais.

Por exemplo, para tratar todos os arquivos cujo nome termina com `.MyGenerated.cs` o código gerado, adicione a seguinte entrada:

```ini
[*.MyGenerated.cs]
generated_code = true
```

## <a name="rule-specific-options"></a>Opções específicas de regra

As opções específicas de regra podem ser aplicadas a uma única regra, a um conjunto de regras ou a todas as regras. As opções específicas de regra incluem:

- [Nível de severidade da regra](#severity-level)
- [Opções específicas para regras de *qualidade de código*](code-quality-rule-options.md)

### <a name="severity-level"></a>Nível de severidade

A tabela a seguir mostra as diferentes severidades de regra que você pode configurar para todas as regras do analisador, incluindo a [qualidade de código](quality-rules/index.md) e as regras de [estilo de código](style-rules/index.md) .

| Valor de configuração de severidade | Comportamento de tempo de compilação |
|-|-|
| `error` | As violações aparecem como *erros* de compilação e causam a falha das compilações.|
| `warning` | As violações aparecem como *avisos* de compilação, mas não causam a falha das compilações (a menos que você tenha uma opção definida para tratar avisos como erros). |
| `suggestion` | As violações aparecem como *mensagens* de Build e como sugestões no IDE do Visual Studio. |
| `silent` | As violações não são visíveis para o usuário. |
| `none` | A regra foi completamente suprimida. |
| `default` | A severidade padrão da regra é usada. As severidades padrão para cada versão do .NET são listadas no [repositório Roslyn-Analyzers](https://github.com/dotnet/roslyn-analyzers/blob/master/src/NetAnalyzers/Core/AnalyzerReleases.Shipped.md). Nessa tabela, "Disabled" corresponde a `none` , "Hidden" corresponde a `silent` e "info" corresponde a `suggestion` . |

> [!TIP]
> Para obter informações sobre como a superfície de severidades de regra no Visual Studio, consulte [níveis de severidade](/visualstudio/ide/editorconfig-language-conventions#severity-levels).

#### <a name="scope"></a>Escopo

Para definir a severidade da regra para uma única regra, use a sintaxe a seguir.

```ini
dotnet_diagnostic.<rule ID>.severity = <severity value>
```

Para definir a severidade da regra padrão para uma [categoria de regras](categories.md), use a sintaxe a seguir. A categoria de cada regra é fornecida nas páginas de referência de regra individuais, por exemplo, [CA1000](quality-rules/ca1000.md).

```ini
dotnet_analyzer_diagnostic.category-<rule category>.severity = <severity value>
```

Para definir a severidade da regra padrão para todas as regras do analisador, use a sintaxe a seguir.

```ini
dotnet_analyzer_diagnostic.severity = <severity value>
```

> [!IMPORTANT]
> Quando você configura o nível de severidade para várias regras com uma única entrada, seja para uma *categoria* de regras ou para *todas* as regras, a gravidade se aplica somente às regras [habilitadas por padrão](https://github.com/dotnet/roslyn-analyzers/blob/master/src/NetAnalyzers/Core/AnalyzerReleases.Shipped.md). Para habilitar as regras que estão desabilitadas por padrão, você deve:
>
> - Adicione uma `dotnet_diagnostic.<rule ID>.severity = <severity>` entrada de configuração explícita para cada regra.
> - Habilite *todas* as regras definindo [\<AnalysisMode>](../../core/project-sdk/msbuild-props.md#analysismode) como `AllEnabledByDefault` .

#### <a name="precedence"></a>Precedência

Se você tiver várias entradas de configuração de severidade que podem ser aplicadas à mesma ID de regra, a precedência será escolhida na seguinte ordem:

- Uma entrada para uma regra individual por ID tem precedência sobre uma entrada para uma categoria.
- Uma entrada para uma categoria tem precedência sobre uma entrada para todas as regras do analisador.

Considere o exemplo a seguir, em que [CA1822](/visualstudio/code-quality/ca1822) tem a categoria "performance":

```ini
[*.cs]
dotnet_diagnostic.CA1822.severity = error
dotnet_analyzer_diagnostic.category-performance.severity = warning
dotnet_analyzer_diagnostic.severity = suggestion
```

No exemplo anterior, todas as três entradas de severidade são aplicáveis a CA1822. No entanto, usando as regras de precedência especificadas, a primeira entrada baseada na ID da regra vence nas próximas entradas. Neste exemplo, o CA1822 terá uma severidade efetiva de `error` . Todas as outras regras dentro da categoria "desempenho" terão uma severidade de `warning` .

Para obter informações sobre como a precedência entre arquivos é decidida, consulte a [seção precedência do artigo arquivos de configuração](configuration-files.md#precedence).
