---
title: Arquivos de configuração para regras de análise de código
description: Saiba mais sobre arquivos de configuração diferentes para configurar regras de análise de código.
ms.date: 09/24/2020
ms.topic: conceptual
no-loc:
- EditorConfig
ms.openlocfilehash: b98fdd48f2373bd23fcd3273834860a60c682969
ms.sourcegitcommit: 68c9d9d9a97aab3b59d388914004b5474cf1dbd7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/30/2021
ms.locfileid: "99216376"
---
# <a name="configuration-files-for-code-analysis-rules"></a>Arquivos de configuração para regras de análise de código

As regras de análise de código têm várias [Opções de configuração](configuration-options.md). Você especifica essas opções como pares de chave-valor em um dos seguintes arquivos de configuração do analisador:

- [EditorConfig](#editorconfig) arquivo: opções de configuração baseadas em arquivo ou em pasta.
- Arquivo [AnalyzerConfig global](#global-analyzerconfig) : opções de configuração no nível do projeto. Útil quando alguns arquivos de projeto residem fora da pasta do projeto.

## EditorConfig

[EditorConfig](/visualstudio/ide/create-portable-custom-editor-options) os arquivos são usados para fornecer **opções que se aplicam a arquivos ou pastas de origem específicos**. As opções são colocadas em cabeçalhos de seção para identificar os arquivos e pastas aplicáveis. Adicione uma entrada para cada regra que você deseja configurar e coloque-a na seção extensão de arquivo correspondente, por exemplo, `[*.cs]` .

```ini
[*.cs]
<option_name> = <option_value>
```

No exemplo acima, `[*.cs]` é um cabeçalho de seção editorconfig para selecionar todos os arquivos C# com `.cs` extensão de arquivo na pasta atual, incluindo subpastas. A entrada subsequente, `<option_name> = <option_value>` , é uma opção do analisador que será aplicada a todos os arquivos C#.

Você pode aplicar EditorConfig convenções de arquivo a uma pasta, um projeto ou um repositório inteiro colocando o arquivo no diretório correspondente. Essas opções são aplicadas ao executar a análise no momento da compilação e enquanto você edita o código no Visual Studio.

Se você tiver um arquivo *. editorconfig* existente para as configurações do editor, como o tamanho do recuo ou se deseja cortar o espaço em branco à direita, você poderá posicionar as opções de configuração da análise de código no mesmo arquivo.

> [!TIP]
> O Visual Studio fornece um modelo de item *. editorconfig* que torna fácil adicionar um desses arquivos ao seu projeto. Para obter mais informações, consulte [Adicionar um EditorConfig arquivo a um projeto](/visualstudio/ide/create-portable-custom-editor-options#add-an-editorconfig-file-to-a-project).

### <a name="example"></a>Exemplo

A seguir, um EditorConfig arquivo de exemplo para configurar as opções e a severidade da regra:

```ini
# Remove the line below if you want to inherit .editorconfig settings from higher directories
root = true

# C# files
[*.cs]

#### Core EditorConfig Options ####

# Indentation and spacing
indent_size = 4
indent_style = space
tab_width = 4

#### .NET Coding Conventions ####

# this. and Me. preferences
dotnet_style_qualification_for_method = true

#### Diagnostic configuration ####

# CA1000: Do not declare static members on generic types
dotnet_diagnostic.CA1000.severity = warning
```

## <a name="global-analyzerconfig"></a>AnalyzerConfig global

A partir do SDK do .NET 5 (que tem suporte no Visual Studio 2019 versão 16,8 e posterior), você também pode configurar opções do analisador com arquivos _AnalyzerConfig_ globais. Esses arquivos são usados para fornecer **opções que se aplicam a todos os arquivos de origem em um projeto**, independentemente de seus nomes de arquivo ou caminhos de arquivo.

Ao contrário dos [EditorConfig](#editorconfig) arquivos, os arquivos de configuração global não podem ser usados para definir as configurações de estilo do editor para ides, como recuar tamanho ou se deseja aparar o espaço em branco à direita. Em vez disso, eles são projetados puramente para especificar opções de configuração do analisador de nível de projeto.

### <a name="format"></a>Formatar

Ao contrário dos EditorConfig arquivos, que devem ter cabeçalhos de seção, como `[*.cs]` , para identificar os arquivos e pastas aplicáveis, os arquivos AnalyzerConfig globais não têm cabeçalhos de seção. Em vez disso, eles exigem uma entrada de nível superior do formulário `is_global = true` para diferenciá-los de EditorConfig arquivos regulares. Isso indica que todas as opções no arquivo se aplicam a todo o projeto. Por exemplo:

```ini
is_global = true
<option_name> = <option_value>
```

### <a name="naming"></a>Nomenclatura

Ao contrário dos EditorConfig arquivos, que devem ser nomeados `.editorconfig` , os arquivos de configuração global não precisam ter um nome ou extensão específico. No entanto, se você nomear esses arquivos como `.globalconfig` eles serão aplicados implicitamente a todos os projetos em C# e Visual Basic dentro da pasta atual, incluindo subpastas. Caso contrário, você deve adicionar explicitamente o `GlobalAnalyzerConfigFiles` item ao seu arquivo de projeto do MSBuild:

```xml
<ItemGroup>
  <GlobalAnalyzerConfigFiles Include="<path_to_global_analyzer_config>" />
</ItemGroup>
```

> [!NOTE]
> A entrada de nível superior `is_global = true` é necessária mesmo quando o arquivo é nomeado `.globalconfig` .

### <a name="example"></a>Exemplo

A seguir está um exemplo de arquivo AnalyzerConfig global para configurar as opções e a severidade da regra no nível do projeto:

```ini
# Top level entry required to mark this as a global AnalyzerConfig file
is_global = true

# NOTE: No section headers for configuration entries

#### .NET Coding Conventions ####

# this. and Me. preferences
dotnet_style_qualification_for_method = true:warning

#### Diagnostic configuration ####

# CA1000: Do not declare static members on generic types
dotnet_diagnostic.CA1000.severity = warning
```

## <a name="precedence"></a>Precedência

Os arquivos EditorConfig e os arquivos AnalyzerConfig globais especificam um par chave-valor para cada opção. Os conflitos surgem quando há várias entradas com a mesma chave, mas valores diferentes.

### <a name="general-options"></a>Opções gerais

Quando ocorrem conflitos entre as opções, as seguintes regras de precedência são usadas para resolver os conflitos:

- Entradas conflitantes no mesmo arquivo de configuração: a entrada que aparece mais adiante no arquivo vence. Isso é verdadeiro para entradas conflitantes dentro de um único EditorConfig arquivo e também dentro de um único arquivo AnalyzerConfig global.

- Entradas conflitantes em dois EditorConfig arquivos: a entrada no EditorConfig arquivo que é mais profunda no sistema de arquivos e, portanto, tem um caminho de arquivo mais longo, o WINS.

- Entradas conflitantes em dois arquivos AnalyzerConfig globais: um aviso do compilador é relatado e as duas entradas são ignoradas.

- Entradas conflitantes em um EditorConfig arquivo e um arquivo AnalyzerConfig global: a entrada no EditorConfig arquivo vence.

### <a name="severity-options"></a>Opções de severidade

As [regras de precedência gerais](#general-options) anteriores se aplicam a todas as opções especificadas em arquivos de configuração. Para opções de [configuração de gravidade](configuration-options.md#severity-level) , as seguintes regras de precedência adicionais se aplicam:

- As opções de severidade especificadas na linha de comando como opções do compilador ( `/nowarn` ou `/warnaserror` ) sempre substituem as opções de [configuração de gravidade](configuration-options.md#severity-level) especificadas em EditorConfig e em arquivos AnalyzerConfig globais.

- As opções de severidade também podem ser especificadas com um arquivo [RuleSet](/visualstudio/code-quality/using-rule-sets-to-group-code-analysis-rules) . No entanto, os arquivos de RuleSets são preteridos em favor EditorConfig e em arquivos AnalyzerConfig globais. É recomendável que você [Converta arquivos RuleSet em um EditorConfig arquivo equivalente](/visualstudio/code-quality/use-roslyn-analyzers#convert-an-existing-ruleset-file-to-editorconfig-file). A precedência para entradas de severidade conflitantes de um arquivo RuleSet e de EditorConfig arquivos AnalyzerConfig global é _indefinida_.

- Para obter informações sobre regras de precedência para opções de severidade relacionadas com chaves diferentes, por exemplo, quando severidades diferentes são especificadas para uma única regra e para a categoria na qual a regra se enquadra, consulte [Opções de configuração para análise de código](configuration-options.md#precedence).

## <a name="see-also"></a>Confira também

- [EditorConfig problema no design do vs global AnalyzerConfig](https://github.com/dotnet/roslyn/issues/47707)
