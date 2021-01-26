---
title: 'Alteração significativa: construtores não públicos sem parâmetros não usados para desserialização'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que construtores não públicos sem parâmetros não são mais usados para desserialização com JsonSerializer.
ms.date: 10/18/2020
ms.openlocfilehash: a2ea54b6a76692dae7d6e01b06b11218d66b1cd7
ms.sourcegitcommit: 4d5e25a46aa7cd0d29b4b9227b92987354d444c4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/26/2021
ms.locfileid: "98794700"
---
# <a name="non-public-parameterless-constructors-not-used-for-deserialization"></a>Construtores não públicos sem parâmetros não usados para desserialização

Para consistência em todos os monikers de estrutura de destino com suporte (TFMs), não públicos, construtores sem parâmetros não são mais usados para desserialização com <xref:System.Text.Json.JsonSerializer> , por padrão.

## <a name="change-description"></a>Descrição das alterações

OsSystem.Text.Jsautônomos [ em pacotes NuGet](https://www.nuget.org/packages/System.Text.Json/) que dão suporte ao .net Standard 2,0 e superior, ou seja, as versões 4.6.0-4.7.2, se comportam de forma inconsistente com o comportamento interno no .net Core 3,0 e 3,1. No .NET Core 3. x, construtores internos e privados podem ser usados para desserialização. Nos pacotes autônomos, não são permitidos construtores não públicos, e um <xref:System.MissingMethodException> será gerado se nenhum construtor público sem parâmetros for definido.

A partir do .NET 5,0 e System.Text.Jsno pacote NuGet 5.0.0, o comportamento é consistente entre o pacote NuGet e as APIs internas. Construtores não públicos, incluindo construtores sem parâmetros, são ignorados pelo serializador por padrão. O serializador usa um dos seguintes construtores para desserialização:

- Construtor público anotado com <xref:System.Text.Json.Serialization.JsonConstructorAttribute> .
- Construtor público sem parâmetros.
- Construtor com parâmetros públicos (se for o único construtor público presente).

Se nenhum desses construtores estiver disponível, um <xref:System.NotSupportedException> será gerado se você tentar desserializar o tipo.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="reason-for-change"></a>Motivo da alteração

- Para impor um comportamento consistente entre todos os TFMs (monikers de estrutura de destino) que se <xref:System.Text.Json?displayProperty=fullName> baseiam para o (.NET Core 3,0 e versões posteriores e .NET Standard 2,0)
- Porque <xref:System.Text.Json.JsonSerializer> não deve chamar a área da superfície não pública de um tipo, seja um construtor, uma propriedade ou um campo.

## <a name="recommended-action"></a>Ação recomendada

- Se você possui o tipo e é viável, torne o construtor sem parâmetros público.
- Caso contrário, implemente um <xref:System.Text.Json.Serialization.JsonConverter%601> para o tipo e controle o comportamento de desserialização. Você pode chamar um construtor não público de uma <xref:System.Text.Json.Serialization.JsonConverter%601> implementação se as regras de acessibilidade do C# para esse cenário permitirem.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>
- <xref:System.Text.Json.JsonSerializer.DeserializeAsync%2A?displayProperty=fullName>

<!--

### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`
- `Overload:System.Text.Json.JsonSerializer.DeserializeAsync`

### Category

Serialization

-->
