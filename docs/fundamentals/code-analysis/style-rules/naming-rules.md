---
title: Regras de nomenclatura de estilo de código
description: Saiba mais sobre as regras de estilo de código do .NET para elementos de código de nomenclatura.
ms.date: 09/25/2020
ms.topic: reference
author: gewarren
ms.author: gewarren
dev_langs:
- CSharp
- VB
f1_keywords:
- IDE1006
- naming rules
helpviewer_keywords:
- IDE1006
- naming code style rules [EditorConfig]
- naming rules
- EditorConfig naming conventions
ms.openlocfilehash: 1fce275204b729b4d23729ca432e06a5a249620d
ms.sourcegitcommit: 78eb25647b0c750cd80354ebd6ce83a60668e22c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/29/2021
ms.locfileid: "99065129"
---
# <a name="naming-rules"></a>Regras de nomenclatura

Em seu `.editorconfig` arquivo, você pode definir **regras de nomenclatura** para como elementos de código de linguagem de programação .net, como &mdash; classes, propriedades e métodos, &mdash; devem ser nomeados. Por exemplo, você pode especificar que os membros públicos devem estar em letras maiúsculas ou que os campos particulares devem começar com `_` .

Uma regra de nomenclatura tem três componentes:

* O **grupo** &mdash; de símbolos ao qual se aplica a regra.
* O **estilo de nomenclatura** a ser associado à regra.
* A severidade para impor a Convenção.

## <a name="general-syntax"></a>Sintaxe geral

Para definir uma regra de nomenclatura, um grupo de símbolos ou um estilo de nomenclatura, defina uma ou mais propriedades usando a seguinte sintaxe:

```ini
<kind>.<title>.<propertyName> = <propertyValue>
```

Cada propriedade só deve ser definida uma vez, mas algumas configurações permitem vários valores separados por vírgula.

A ordem das propriedades não é importante.

### \<kind>

**\<kind>** Especifica qual tipo de elemento está sendo definido como &mdash; regra de nomenclatura, grupo de símbolos ou estilo de nomenclatura &mdash; e deve ser um dos seguintes:

| Para definir uma propriedade para | Usar o \<kind> valor | Exemplo |
| --- | --- | -- |
| Regra de nomenclatura | `dotnet_naming_rule` | `dotnet_naming_rule.types_should_be_pascal_case.severity = suggestion` |
| Grupo de símbolos | `dotnet_naming_symbols` | `dotnet_naming_symbols.interface.applicable_kinds = interface` |
| Estilo de nomenclatura | `dotnet_naming_style` | `dotnet_naming_style.pascal_case.capitalization = pascal_case` |

Cada tipo de &mdash; [regra de nomenclatura](#naming-rule-properties)de definição, [grupo de símbolos](#symbol-group-properties)ou [estilo de nomenclatura](#naming-style-properties) &mdash; tem suas próprias propriedades com suporte, conforme descrito nas seções a seguir.

### \<title>

**\<title>** é um nome descritivo que você escolhe que associa várias configurações de propriedade em uma única definição. Por exemplo, as propriedades a seguir produzem duas definições de grupo `interface` de símbolos e `types` , cada uma delas tem duas propriedades definidas.

```ini
dotnet_naming_symbols.interface.applicable_kinds = interface
dotnet_naming_symbols.interface.applicable_accessibilities = public, internal, private, protected, protected_internal, private_protected

dotnet_naming_symbols.types.applicable_kinds = class, struct, interface, enum, delegate
dotnet_naming_symbols.types.applicable_accessibilities = public, internal, private, protected, protected_internal, private_protected
```

## <a name="naming-rule-properties"></a>Propriedades da regra de nomenclatura

Todas as propriedades de regra de nomenclatura são necessárias para que uma regra entre em vigor.

| Propriedade | Descrição |
| -- | -- |
| `symbols` | O título de um grupo de símbolos; a regra de nomenclatura será aplicada aos símbolos neste grupo |
| `style` | O título do estilo de nomenclatura que deve ser associado a esta regra |
| `severity` |  Define a severidade com a qual impor a regra de nomenclatura. Defina o valor associado como um dos níveis de [severidade](../configuration-options.md#severity-level)disponíveis. <sup>1</sup> |

**Observações:**

1. A especificação de severidade dentro de uma regra de nomenclatura só é respeitada dentro de IDEs de desenvolvimento, como o Visual Studio. Essa configuração não é compreendida pelos compiladores C# ou VB, portanto não é respeitada durante a compilação. Para impor regras de estilo de nomenclatura na compilação, você deve definir a severidade usando a [configuração de severidade de regra de código](#rule-id-ide1006-naming-rule-violation). Para saber mais, confira este [problema do GitHub](https://github.com/dotnet/roslyn/issues/44201).

## <a name="symbol-group-properties"></a>Propriedades do grupo de símbolos

Você pode definir as seguintes propriedades para grupos de símbolos, para limitar quais símbolos estão incluídos no grupo. Para especificar vários valores para uma única propriedade, separe os valores com uma vírgula.

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| -- | -- | -- | -- |
| `applicable_kinds` | Tipos de símbolos no grupo <sup>1</sup> | `*` (use este valor para especificar todos os símbolos)<br/>`namespace`<br/>`class`<br/>`struct`<br/>`interface`<br/>`enum`<br/>`property`<br/>`method`<br/>`field`<br/>`event`<br/>`delegate`<br/>`parameter`<br/>`type_parameter`<br/>`local`<br/>`local_function` | Yes |
| `applicable_accessibilities` | Níveis de acessibilidade dos símbolos no grupo | `*` (use este valor para especificar todos os níveis de acessibilidade)<br/>`public`<br/>`internal` ou `friend`<br/>`private`<br/>`protected`<br/>`protected_internal` ou `protected_friend`<br/>`private_protected`<br/>`local` (para símbolos definidos dentro de um método) | Yes |
| `required_modifiers` | Corresponder apenas símbolos com _todos_ os modificadores especificados <sup>2</sup> | `abstract` ou `must_inherit`<br/>`async`<br/>`const`<br/>`readonly`<br/>`static` ou `shared` <sup>3</sup> | No |

**Observações:**

1. Atualmente, não há suporte para membros de tupla no `applicable_kinds` .
2. O grupo de símbolos corresponde a _todos_ os modificadores na `required_modifiers` propriedade.  Se você omitir essa propriedade, nenhum modificador específico será necessário para uma correspondência. Isso significa que os modificadores de um símbolo não têm efeito sobre a opção de aplicar essa regra ou não.
3. Se o grupo tiver `static` ou `shared` na `required_modifiers` propriedade, o grupo também incluirá `const` símbolos, pois eles são implicitamente `static` / `Shared` . No entanto, se você não quiser que a `static` regra de nomenclatura se aplique a `const` símbolos, poderá criar uma nova regra de nomenclatura com um grupo de símbolos de `const` .

## <a name="naming-style-properties"></a>Propriedades de estilo de nomenclatura

Um estilo de nomenclatura define as convenções que você deseja impor com a regra. Por exemplo:

* Colocar em maiúsculas com `PascalCase`
* Começa com `m_`
* Termina com `_g`
* Separar palavras com `__`

Você pode definir as seguintes propriedades para um estilo de nomenclatura:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| -- | -- | -- | -- |
| `capitalization` | Estilo de capitalização de palavras dentro do símbolo | `pascal_case`<br/>`camel_case`<br/>`first_word_upper`<br/>`all_upper`<br/>`all_lower` | Sim<sup>1</sup> |
| `required_prefix` | Deve começar com estes caracteres | | No |
| `required_suffix` | Deve terminar com estes caracteres | | No |
| `word_separator` | As palavras dentro do símbolo precisam ser separadas com este caractere | | No |

**Observações:**

1. É necessário especificar um estilo de uso de maiúsculas como parte do seu estilo de nomenclatura; caso contrário, o estilo de nomenclatura poderá ser ignorado.

## <a name="rule-order"></a>Ordem das regras

A ordem na qual as regras de nomenclatura são definidas em um arquivo EditorConfig não importa. As regras de nomenclatura são ordenadas automaticamente de acordo com a definição das próprias regras. A [extensão de serviço de linguagem EditorConfig](https://marketplace.visualstudio.com/items?itemName=MadsKristensen.EditorConfig) pode analisar um arquivo EditorConfig e casos de relatório em que a ordenação de regra no arquivo é diferente do que o compilador usará em tempo de execução.

> [!NOTE]
>
> Se você estiver usando uma versão do Visual Studio anterior à versão 16,2 do Visual Studio 2019, as regras de nomenclatura deverão ser ordenadas da mais específica para a menos específica no arquivo EditorConfig. A primeira regra encontrada que pode ser aplicada é a única regra que é aplicada. No entanto, se houver várias *propriedades* de regras com o mesmo nome, a propriedade mais recente encontrada com esse nome terá precedência. Confira mais informações em [Precedência e hierarquia de arquivos](/visualstudio/ide/create-portable-custom-editor-options#file-hierarchy-and-precedence).

## <a name="default-naming-styles"></a>Estilos de nomenclatura padrão

Se você não especificar nenhuma regra de nomenclatura personalizada, os seguintes estilos padrão serão usados:

- Para classes, estruturas, enumerações, propriedades e eventos com acessibilidade `public`, `private`, `internal`, `protected` ou `protected_internal`, o estilo de nomenclatura padrão é Pascal case.

- Para interfaces com acessibilidade `public`, `private`, `internal`, `protected` ou `protected_internal`, o estilo de nomenclatura padrão é Pascal case com o prefixo necessário **I**.

## <a name="code-rule-id-ide1006-naming-rule-violation"></a><a name="rule-id-ide1006-naming-rule-violation"></a>ID da regra de código: `IDE1006 (Naming rule violation)`

Todas as opções de nomenclatura têm ID `IDE1006` de regra e título `Naming rule violation` . Você pode configurar a severidade de violações de nomenclatura globalmente em um arquivo EditorConfig com a seguinte sintaxe:

```ini
dotnet_diagnostic.IDE1006.severity = <severity value>
```

O valor de severidade deve ser `warning` ou `error` ser [imposto na compilação](../overview.md#code-style-analysis). Para todos os valores de severidade possíveis, consulte [nível de severidade](../configuration-options.md#severity-level).

## <a name="example"></a>Exemplo

O arquivo *.editorconfig* a seguir contém uma convenção de nomenclatura que especifica que propriedades públicas, métodos, campos, eventos e delegados devem sempre ser escritos com maiúsculas. Observe que esta convenção de nomenclatura especifica vários tipos de símbolo aos quais aplicar a regra, usando uma vírgula para separar os valores.

```ini
[*.{cs,vb}]

# Defining the 'public_symbols' symbol group
dotnet_naming_symbols.public_symbols.applicable_kinds           = property,method,field,event,delegate
dotnet_naming_symbols.public_symbols.applicable_accessibilities = public
dotnet_naming_symbols.public_symbols.required_modifiers         = readonly

# Defining the `first_word_upper_case_style` naming style
dotnet_naming_style.first_word_upper_case_style.capitalization = first_word_upper

# Defining the `public_members_must_be_capitalized` naming rule, by setting the symbol group to the 'public symbols' symbol group,
dotnet_naming_rule.public_members_must_be_capitalized.symbols   = public_symbols
# setting the naming style to the `first_word_upper_case_style` naming style,
dotnet_naming_rule.public_members_must_be_capitalized.style    = first_word_upper_case_style
# and setting the severity.
dotnet_naming_rule.public_members_must_be_capitalized.severity = suggestion
```

## <a name="see-also"></a>Confira também

- [Regras de linguagem](language-rules.md)
- [Regras de formatação](formatting-rules.md)
- [Regras de nomenclatura Roslyn](https://github.com/dotnet/roslyn/blob/master/.editorconfig#L63)
- [Referência de regras de estilo de código .NET](index.md)
