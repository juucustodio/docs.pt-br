---
title: 'Alteração significativa: o caractere de desserialização requer uma cadeia de caracteres de caractere único'
description: Saiba mais sobre a alteração significativa no .NET 5,0, em que System.Text.Jsrequer uma cadeia de caracteres de caractere único no JSON ao desserializar para um destino Char.
ms.date: 12/15/2020
ms.openlocfilehash: 39a2d25b00bf8855cfbf46a4d78b8545052703e5
ms.sourcegitcommit: 635a0ff775d2447a81ef7233a599b8f88b162e5d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97633865"
---
# <a name="systemtextjson-requires-single-char-string-to-deserialize-a-char"></a>System.Text.Json requer uma cadeia de caracteres de caractere único para desserializar um Char

Para desserializar com êxito um <xref:System.Char> using <xref:System.Text.Json> , a cadeia de caracteres JSON deve conter um único caractere.

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, uma `char` cadeia de caracteres múltipla no JSON é desserializada com êxito para uma `char` propriedade ou campo. Somente a primeira `char` da cadeia de caracteres é usada, como no exemplo a seguir:

```csharp
// .NET Core 3.0 and 3.1: Returns the first char 'a'.
// .NET 5.0 and later: Throws JsonException because payload has more than one char.
char deserializedChar = JsonSerializer.Deserialize<char>("\"abc\"");
```

No .NET 5,0 e posterior, qualquer coisa que não seja uma `char` cadeia de caracteres única faz com que a <xref:System.Text.Json.JsonException> seja gerada quando o destino de desserialização for um `char` . A cadeia de caracteres de exemplo a seguir é desserializada com êxito em todas as versões do .NET:

```csharp
// Correct usage.
char deserializedChar = JsonSerializer.Deserialize<char>("\"a\"");
```

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="reason-for-change"></a>Motivo da alteração

A análise para desserialização deve ter sucesso apenas quando a carga fornecida é válida para o tipo de destino. Para um `char` tipo, a única carga válida é uma cadeia de `char` caracteres única.

## <a name="recommended-action"></a>Ação recomendada

Quando você desserializar JSON em um `char` destino, certifique-se de que a cadeia de caracteres consiste em um único `char` .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Text.Json.JsonSerializer.Deserialize%2A?displayProperty=fullName>

<!--

### Affected APIs

- `Overload:System.Text.Json.JsonSerializer.Deserialize`

### Category

Serialization

-->
