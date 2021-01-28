---
title: Regras de linguagem de estilo de código
description: Saiba mais sobre as diferentes regras de estilo de código para usar as construções de linguagem C# e Visual Basic.
ms.date: 09/25/2020
ms.topic: reference
author: gewarren
ms.author: gewarren
dev_langs:
- CSharp
- VB
helpviewer_keywords:
- language code style rules [EditorConfig]
- language rules
- EditorConfig language conventions
ms.openlocfilehash: 2aa2261534363f1da6a2109f092e08d210ebd915
ms.sourcegitcommit: 7e42488c2f8f63f6d499b5f8fb1dec5bac9ad254
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/28/2021
ms.locfileid: "98957969"
---
# <a name="language-rules"></a>Regras de linguagem

As regras de linguagem do estilo de código afetam como várias construções de linguagens de programação do .NET, por exemplo, modificadores e parênteses, são usadas. As regras se enquadram nas seguintes categorias:

- [Regras de estilo .net](#net-style-rules): regras que se aplicam a C# e Visual Basic. Os nomes da opção EditorConfig para essas regras começam com o `dotnet_style_` prefixo.
- [Regras de estilo c#](#c-style-rules): regras que são específicas apenas para a linguagem C#. Os nomes da opção EditorConfig para essas regras começam com o `csharp_style_` prefixo.
- [Regras de estilo de Visual Basic](#visual-basic-style-rules): regras que são específicas somente para o idioma Visual BSIC. Os nomes da opção EditorConfig para essas regras começam com o `visual_basic_style_` prefixo.

## <a name="option-format"></a>Formato da opção

As opções para regras de idioma podem ser especificadas em um arquivo EditorConfig com o seguinte formato:

`option_name = value` (Visual Studio 2019 versão 16,9 Preview 2 e posterior)

ou

`option_name = value:severity`

- **Valor**

  Para cada regra de idioma, você especifica um valor que define se ou quando preferir o estilo. Muitas regras aceitam um valor de `true` (prefira esse estilo) ou `false` (não prefiro esse estilo). Outras regras aceitam valores como `when_on_single_line` ou `never` .

- **Severidade** (opcional no Visual Studio 2019 versão 16,9 Preview 2 e versões posteriores)

  A segunda parte da regra especifica o [nível de severidade](../configuration-options.md#severity-level) para a regra. Quando especificado dessa forma, a configuração de gravidade só é respeitada dentro de IDEs de desenvolvimento, como o Visual Studio. Ele *não* é respeitado durante a compilação.

  Para impor regras de estilo de código no momento da compilação, defina a severidade usando a sintaxe de configuração de severidade baseada em ID de regra para analisadores em vez disso. A sintaxe assume a forma `dotnet_diagnostic.<rule ID>.severity = <severity>` , por exemplo, `dotnet_diagnostic.IDE0040.severity = silent` . Para obter mais informações, consulte [nível de severidade](../configuration-options.md#severity-level).

> [!TIP]
>
> A partir do Visual Studio 2019 versão 16,3, você pode configurar regras de estilo de código no menu de lâmpada de [ações rápidas](/visualstudio/ide/quick-actions) após a ocorrência de uma violação de estilo. Para obter mais informações, consulte [Configurar automaticamente estilos de código no Visual Studio](/visualstudio/ide/editorconfig-language-conventions#automatically-configure-code-styles-in-visual-studio).

## <a name="net-style-rules"></a>Regras de estilo .NET

As regras de estilo nesta seção são aplicáveis tanto para C# quanto para Visual Basic.

- [qualificadores ' this. ' e ' me. '](ide0003-ide0009.md)
  - [dotnet_style_qualification_for_field](ide0003-ide0009.md#dotnet_style_qualification_for_field)
  - [dotnet_style_qualification_for_property](ide0003-ide0009.md#dotnet_style_qualification_for_property)
  - [dotnet_style_qualification_for_method](ide0003-ide0009.md#dotnet_style_qualification_for_method)
  - [dotnet_style_qualification_for_event](ide0003-ide0009.md#dotnet_style_qualification_for_event)
- [Palavras-chave de linguagem em vez de nomes de tipo de estrutura para referências de tipo](ide0049.md)
  - [dotnet_style_predefined_type_for_locals_parameters_members](ide0049.md#dotnet_style_predefined_type_for_locals_parameters_members)
  - [dotnet_style_predefined_type_for_member_access](ide0049.md#dotnet_style_predefined_type_for_member_access)
- [Preferências do modificador](modifier-preferences.md#net-modifier-preferences)
  - [dotnet_style_require_accessibility_modifiers](ide0040.md#dotnet_style_require_accessibility_modifiers)
  - [csharp_preferred_modifier_order](ide0036.md#csharp_preferred_modifier_order)
  - [visual_basic_preferred_modifier_order](ide0036.md#visual_basic_preferred_modifier_order)
  - [dotnet_style_readonly_field](ide0044.md#dotnet_style_readonly_field)
- [Preferências de parênteses](ide0047-ide0048.md)
  - [dotnet_style_parentheses_in_arithmetic_binary_operators](ide0047-ide0048.md#dotnet_style_parentheses_in_arithmetic_binary_operators)
  - [dotnet_style_parentheses_in_relational_binary_operators](ide0047-ide0048.md#dotnet_style_parentheses_in_relational_binary_operators)
  - [dotnet_style_parentheses_in_other_binary_operators](ide0047-ide0048.md#dotnet_style_parentheses_in_other_binary_operators)
  - [dotnet_style_parentheses_in_other_operators](ide0047-ide0048.md#dotnet_style_parentheses_in_other_operators)
- [Preferências de nível de expressão](expression-level-preferences.md#net-expression-level-preferences)
  - [dotnet_style_object_initializer](ide0017.md#dotnet_style_object_initializer)
  - [dotnet_style_collection_initializer](ide0028.md#dotnet_style_collection_initializer)
  - [dotnet_style_explicit_tuple_names](ide0033.md#dotnet_style_explicit_tuple_names)
  - [dotnet_style_prefer_inferred_tuple_names](ide0037.md#dotnet_style_prefer_inferred_tuple_names)
  - [dotnet_style_prefer_inferred_anonymous_type_member_names](ide0037.md#dotnet_style_prefer_inferred_anonymous_type_member_names)
  - [dotnet_style_prefer_auto_properties](ide0032.md#dotnet_style_prefer_auto_properties)
  - [dotnet_style_prefer_conditional_expression_over_assignment](ide0045.md#dotnet_style_prefer_conditional_expression_over_assignment)
  - [dotnet_style_prefer_conditional_expression_over_return](ide0046.md#dotnet_style_prefer_conditional_expression_over_return)
  - [dotnet_style_prefer_compound_assignment](ide0054-ide0074.md#dotnet_style_prefer_compound_assignment)
  - [dotnet_style_prefer_simplified_interpolation](ide0071.md#dotnet_style_prefer_simplified_interpolation)
  - [dotnet_style_prefer_simplified_boolean_expressions](ide0075.md#dotnet_style_prefer_simplified_boolean_expressions)
  - [Adicionar casos ausentes à instrução switch](ide0010.md) -essa regra não tem nenhuma opção de estilo de código.
  - [Converter tipo anônimo em tupla](ide0050.md) – essa regra não tem nenhuma opção de estilo de código.
  - [Use ' System. hashCode. Combine '](ide0070.md) – essa regra não tem nenhuma opção de estilo de código.
  - [Converter ' typeof ' em ' nameof '](ide0082.md) -essa regra não tem nenhuma opção de estilo de código.
- [Preferências de verificação nula](null-checking-preferences.md#net-null-checking-preferences)
  - [dotnet_style_coalesce_expression](ide0029-ide0030.md#dotnet_style_coalesce_expression)
  - [dotnet_style_null_propagation](ide0031.md#dotnet_style_null_propagation)
  - [dotnet_style_prefer_is_null_check_over_reference_equality_method](ide0041.md#dotnet_style_prefer_is_null_check_over_reference_equality_method)
- [Preferências de cabeçalho de arquivo](ide0073.md)
  - [file_header_template](ide0073.md#file_header_template)

## <a name="c-style-rules"></a>Regras de estilo C#

As regras de estilo nesta seção são aplicáveis somente à linguagem C#.

- [preferências de ' var '](ide0007-ide0008.md)
  - [csharp_style_var_for_built_in_types](ide0007-ide0008.md#csharp_style_var_for_built_in_types)
  - [csharp_style_var_when_type_is_apparent](ide0007-ide0008.md#csharp_style_var_when_type_is_apparent)
  - [csharp_style_var_elsewhere](ide0007-ide0008.md#csharp_style_var_elsewhere)
- [Membros aptos para expressão](expression-bodied-members.md)
  - [csharp_style_expression_bodied_methods](ide0022.md#csharp_style_expression_bodied_methods)
  - [csharp_style_expression_bodied_constructors](ide0021.md#csharp_style_expression_bodied_constructors)
  - [csharp_style_expression_bodied_operators](ide0023-ide0024.md#csharp_style_expression_bodied_operators)
  - [csharp_style_expression_bodied_properties](ide0025.md#csharp_style_expression_bodied_properties)
  - [csharp_style_expression_bodied_indexers](ide0026.md#csharp_style_expression_bodied_indexers)
  - [csharp_style_expression_bodied_accessors](ide0027.md#csharp_style_expression_bodied_accessors)
  - [csharp_style_expression_bodied_lambdas](ide0053.md#csharp_style_expression_bodied_lambdas)
  - [csharp_style_expression_bodied_local_functions](ide0061.md#csharp_style_expression_bodied_local_functions)
- [Preferências de correspondência de padrões](pattern-matching-preferences.md)
  - [csharp_style_pattern_matching_over_is_with_cast_check](ide0020-ide0038.md#csharp_style_pattern_matching_over_is_with_cast_check)
  - [csharp_style_pattern_matching_over_as_with_null_check](ide0019.md#csharp_style_pattern_matching_over_as_with_null_check)
  - [csharp_style_prefer_switch_expression](ide0066.md#csharp_style_prefer_switch_expression)
  - [csharp_style_prefer_pattern_matching](ide0078.md#csharp_style_prefer_pattern_matching)
  - [csharp_style_prefer_not_pattern](ide0083.md#csharp_style_prefer_not_pattern)
- [Preferências de nível de expressão](expression-level-preferences.md#c-expression-level-preferences)
  - [csharp_style_inlined_variable_declaration](ide0018.md#csharp_style_inlined_variable_declaration)
  - [csharp_prefer_simple_default_expression](ide0034.md#csharp_prefer_simple_default_expression)
  - [csharp_style_pattern_local_over_anonymous_function](ide0039.md#csharp_style_pattern_local_over_anonymous_function)
  - [csharp_style_deconstructed_variable_declaration](ide0042.md#csharp_style_deconstructed_variable_declaration)
  - [csharp_style_prefer_index_operator](ide0056.md#csharp_style_prefer_index_operator)
  - [csharp_style_prefer_range_operator](ide0057.md#csharp_style_prefer_range_operator)
  - [csharp_style_implicit_object_creation_when_type_is_apparent](ide0090.md#csharp_style_implicit_object_creation_when_type_is_apparent)
  - [Adicionar casos ausentes à expressão de switch](ide0072.md) – essa regra não tem nenhuma opção de estilo de código.
- [Preferências de verificação "NULL"](null-checking-preferences.md#c-null-checking-preferences)
  - [csharp_style_throw_expression](ide0016.md#csharp_style_throw_expression)
  - [csharp_style_conditional_delegate_call](ide1005.md#csharp_style_conditional_delegate_call)
- [Preferências de bloco de código](code-block-preferences.md)
  - [csharp_prefer_braces](ide0011.md#csharp_prefer_braces)
  - [csharp_prefer_simple_using_statement](ide0063.md#csharp_prefer_simple_using_statement)
- [preferências de diretiva ' Using '](ide0065.md)
  - [csharp_using_directive_placement](ide0065.md#csharp_using_directive_placement)
- [Preferências do modificador](modifier-preferences.md#c-modifier-preferences)
  - [csharp_prefer_static_local_function](ide0062.md#csharp_prefer_static_local_function)
  - [Tornar os campos de struct graváveis](ide0064.md) – essa regra não tem nenhuma opção de estilo de código.

## <a name="visual-basic-style-rules"></a>Regras de estilo de Visual Basic

As regras de estilo nesta seção são aplicáveis somente ao idioma Visual Basic.

- [Preferências de correspondência de padrões](pattern-matching-preferences.md)
  - [visual_basic_style_prefer_isnot_expression](ide0084.md#visual_basic_style_prefer_isnot_expression)

## <a name="see-also"></a>Confira também

- [Regras de código desnecessárias](unnecessary-code-rules.md)
- [Regras de formatação](formatting-rules.md)
- [Regras de nomenclatura](naming-rules.md)
- [Referência de regras de estilo de código .NET](index.md)
