---
title: Opções de configuração de regra de qualidade de código
description: Saiba como especificar opções de configuração adicionais para regras de qualidade de código.
ms.date: 09/24/2020
ms.topic: conceptual
no-loc:
- EditorConfig
ms.openlocfilehash: 2721d4e8fda6012b304637477c3618ee0ff2ea18
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99752061"
---
# <a name="code-quality-rule-configuration-options"></a>Opções de configuração de regra de qualidade de código

As regras de *qualidade de código* têm opções de configuração adicionais, além de apenas [configurar sua gravidade](configuration-options.md#severity-level). Por exemplo, cada analisador de qualidade de código pode ser configurado para se aplicar somente a partes específicas da sua base de códigos. Você especifica essas opções adicionando pares chave-valor ao mesmo [EditorConfig](https://editorconfig.org) arquivo em que você especifica severidades de regra e preferências gerais do editor.

## <a name="option-scopes"></a>Escopos de opção

Cada opção de refinamento pode ser configurada para todas as regras, para uma categoria de regras (por exemplo, segurança ou Design) ou para uma regra específica.

### <a name="all-rules"></a>Todas as regras

A sintaxe para configurar uma opção para *todas* as regras é a seguinte:

|Sintaxe|Exemplo|
|-|-|
| dotnet_code_quality. OptionName = optionvalue | `dotnet_code_quality.api_surface = public` |

### <a name="category-of-rules"></a>Categoria de regras

A sintaxe para configurar uma opção para uma [ *categoria* de regras](categories.md) é a seguinte:

|Sintaxe|Exemplo|
|-|-|
| dotnet_code_quality. RuleCategory. optionName = optionvalue | `dotnet_code_quality.Naming.api_surface = public` |

### <a name="specific-rule"></a>Regra específica

A sintaxe para configurar uma opção para uma regra *específica* é a seguinte:

|Sintaxe|Exemplo|
|-|-|
| dotnet_code_quality. RuleId. ValorDeOpção = optionvalue | `dotnet_code_quality.CA1040.api_surface = public` |

## <a name="options"></a>Opções

Esta seção lista algumas das opções disponíveis. Para ver a lista completa de opções disponíveis, consulte [configuração do analisador](https://github.com/dotnet/roslyn-analyzers/blob/master/docs/Analyzer%20Configuration.md).

### <a name="api_surface"></a>api_surface

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Qual parte da superfície da API deve ser analisada | `public`<br/>`internal` ou `friend`<br/>`private`<br/>`all`<br/><br/>Separe vários valores com uma vírgula (,) | `public` | [CA1000](quality-rules/ca1000.md) [CA1003](quality-rules/ca1003.md) [CA1008](quality-rules/ca1008.md) [CA1010](quality-rules/ca1010.md)<br/>[CA1012](quality-rules/ca1012.md) [CA1024](quality-rules/ca1024.md) [CA1027](quality-rules/ca1027.md) [CA1028](quality-rules/ca1028.md)<br/>[CA1030](quality-rules/ca1030.md) [CA1036](quality-rules/ca1036.md) [CA1040](quality-rules/ca1040.md) [CA1041](quality-rules/ca1041.md)<br/>[CA1043](quality-rules/ca1043.md) [CA1044](quality-rules/ca1044.md) [CA1051](quality-rules/ca1051.md) [CA1052](quality-rules/ca1052.md)<br/>[CA1054](quality-rules/ca1054.md) [CA1055](quality-rules/ca1055.md) [CA1056](quality-rules/ca1056.md) [CA1058](quality-rules/ca1058.md)<br/>[CA1063](quality-rules/ca1063.md) [CA1708](quality-rules/ca1708.md) [CA1710](quality-rules/ca1710.md) [CA1711](quality-rules/ca1711.md)<br/>[CA1714](quality-rules/ca1714.md) [CA1715](quality-rules/ca1715.md) [CA1716](quality-rules/ca1716.md) [CA1717](quality-rules/ca1717.md)<br/>[CA1720](quality-rules/ca1720.md) [CA1721](quality-rules/ca1721.md) [CA1725](quality-rules/ca1725.md) [CA1801](quality-rules/ca1801.md)<br/>[CA1802](quality-rules/ca1802.md) [CA1815](quality-rules/ca1815.md) [CA1819](quality-rules/ca1819.md) [CA2217](quality-rules/ca2217.md)<br/>[CA2225](quality-rules/ca2225.md) [CA2226](quality-rules/ca2226.md) [CA2231](quality-rules/ca2231.md) [CA2234](quality-rules/ca2234.md)<br/>|

### <a name="exclude_async_void_methods"></a>exclude_async_void_methods

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Se os métodos assíncronos que não retornam um valor devem ser ignorados | `true`<br/>`false` | `false` | [CA2007](quality-rules/ca2007.md) |

> [!NOTE]
> Essa opção foi nomeada `skip_async_void_methods` em uma versão anterior.

### <a name="exclude_single_letter_type_parameters"></a>exclude_single_letter_type_parameters

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Se os [parâmetros de tipo](../../csharp/programming-guide/generics/generic-type-parameters.md) de caractere único devem ser excluídos da regra, por exemplo, `S` em `Collection<S>` | `true`<br/>`false` | `false` | [CA1715](quality-rules/ca1715.md) |

> [!NOTE]
> Essa opção foi nomeada `allow_single_letter_type_parameters` em uma versão anterior.

### <a name="output_kind"></a>output_kind

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Especifica que o código em um projeto que gera esse tipo de assembly deve ser analisado | Um ou mais campos da <xref:Microsoft.CodeAnalysis.OutputKind> enumeração<br/><br/>Separe vários valores com uma vírgula (,) | Todos os tipos de saída | [CA2007](quality-rules/ca2007.md) |

### <a name="required_modifiers"></a>required_modifiers

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Especifica os modificadores necessários para as APIs que devem ser analisadas | Um ou mais valores da tabela de modificadores permitidos abaixo<br/><br/>Separe vários valores com uma vírgula (,) | Depende de cada regra | [CA1802](quality-rules/ca1802.md) |

| Modificador permitido | Resumo |
| --- | --- |
| `none` | Nenhum requisito de modificador |
| `static` ou `Shared` | Deve ser declarado como `static` ( `Shared` em Visual Basic) |
| `const` | Deve ser declarado como `const` |
| `readonly` | Deve ser declarado como `readonly` |
| `abstract` | Deve ser declarado como `abstract` |
| `virtual` | Deve ser declarado como `virtual` |
| `override` | Deve ser declarado como `override` |
| `sealed` | Deve ser declarado como `sealed` |
| `extern` | Deve ser declarado como `extern` |
| `async` | Deve ser declarado como `async` |

### <a name="exclude_extension_method_this_parameter"></a>exclude_extension_method_this_parameter

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Se deseja ignorar a análise para o `this` parâmetro de métodos de extensão | `true`<br/>`false` | `false` | [CA1062](quality-rules/ca1062.md) |

### <a name="null_check_validation_methods"></a>null_check_validation_methods

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Os nomes dos métodos de validação de verificação nula que validam os argumentos passados para o método são não nulos | Formatos de nome de método permitidos (separados por `|` ):<br/> -Somente nome do método (inclui todos os métodos com o nome, independentemente do tipo ou namespace que o contém)<br/> -Nomes totalmente qualificados no [formato de ID de documentação](https://github.com/dotnet/csharplang/blob/master/spec/documentation-comments.md#id-string-format)do símbolo, com um `M:` prefixo opcional | Nenhum | [CA1062](quality-rules/ca1062.md) |

### <a name="additional_string_formatting_methods"></a>additional_string_formatting_methods

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Nomes de métodos de formatação de cadeia de caracteres adicionais | Formatos de nome de método permitidos (separados por `|` ):<br/> -Somente nome do método (inclui todos os métodos com o nome, independentemente do tipo ou namespace que o contém)<br/> -Nomes totalmente qualificados no [formato de ID de documentação](/dotnet/csharp/language-reference/language-specification/documentation-comments#id-string-format)do símbolo, com um `M:` prefixo opcional | Nenhum | [CA2241](quality-rules/ca2241.md) |

### <a name="excluded_type_names_with_derived_types"></a>excluded_type_names_with_derived_types

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Nomes de tipos, de modo que o tipo e todos os seus tipos derivados sejam excluídos para análise | Formatos de nome de símbolo permitidos (separados por `|` ):<br/> -Somente nome do tipo (inclui todos os tipos com o nome, independentemente do tipo ou namespace que a contém)<br/> -Nomes totalmente qualificados no [formato de ID de documentação](/dotnet/csharp/language-reference/language-specification/documentation-comments#id-string-format)do símbolo, com um `T:` prefixo opcional | Nenhum | [CA1303](quality-rules/ca1303.md) |

### <a name="excluded_symbol_names"></a>excluded_symbol_names

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Nomes de símbolos que são excluídos para análise | Formatos de nome de símbolo permitidos (separados por `|` ):<br/> -Somente nome do símbolo (inclui todos os símbolos com o nome, independentemente do tipo ou namespace que o contém)<br/> -Nomes totalmente qualificados no [formato de ID de documentação](/dotnet/csharp/language-reference/language-specification/documentation-comments#id-string-format)do símbolo. Cada nome de símbolo requer um prefixo de tipo de símbolo, como `M:` prefixo para métodos, `T:` prefixo para tipos e `N:` prefixo para namespaces.<br/> - `.ctor` para construtores e `.cctor` para construtores estáticos | Nenhum | [CA1062](quality-rules/ca1062.md) [CA1303](quality-rules/ca1303.md) [CA2000](quality-rules/ca2000.md) [CA2100](quality-rules/ca2100.md) [CA2301](quality-rules/ca2301.md) [CA2302](quality-rules/ca2302.md)<br/>[CA2311](quality-rules/ca2311.md) [CA2312](quality-rules/ca2312.md) [CA2321](quality-rules/ca2321.md) [CA2322](quality-rules/ca2322.md) [CA2327](quality-rules/ca2327.md) [CA2328](quality-rules/ca2328.md)<br/>[CA2329](quality-rules/ca2329.md) [CA2330](quality-rules/ca2330.md) [CA3001](quality-rules/ca3001.md) [CA3002](quality-rules/ca3002.md) [CA3003](quality-rules/ca3003.md) [CA3004](quality-rules/ca3004.md)<br/>[CA3005](quality-rules/ca3005.md) [CA3006](quality-rules/ca3006.md) [CA3007](quality-rules/ca3007.md) [CA3008](quality-rules/ca3008.md) [CA3009](quality-rules/ca3009.md) [CA3010](quality-rules/ca3010.md)<br/>[CA3011](quality-rules/ca3011.md) [CA3012](quality-rules/ca3012.md) [CA5361](quality-rules/ca5361.md) CA5376 CA5377 [CA5378](quality-rules/ca5378.md)<br/>[CA5380](quality-rules/ca5380.md) [CA5381](quality-rules/ca5381.md) CA5382 CA5383 CA5384 CA5387<br/>CA5388 [CA5389](quality-rules/ca5389.md) CA5390 |

### <a name="disallowed_symbol_names"></a>disallowed_symbol_names

| Descrição | Valores permitidos | Valor padrão | Regras configuráveis |
| - | - | - | - |
| Nomes de símbolos que não são permitidos no contexto da análise | Formatos de nome de símbolo permitidos (separados por `|` ):<br/> -Somente nome do símbolo (inclui todos os símbolos com o nome, independentemente do tipo ou namespace que o contém)<br/> -Nomes totalmente qualificados no [formato de ID de documentação](/dotnet/csharp/language-reference/language-specification/documentation-comments#id-string-format)do símbolo. Cada nome de símbolo requer um prefixo de tipo de símbolo, como `M:` prefixo para métodos, `T:` prefixo para tipos e `N:` prefixo para namespaces.<br/> - `.ctor` para construtores e `.cctor` para construtores estáticos | Nenhum | [CA1031](quality-rules/ca1031.md) |
