---
title: Como verificar se cadeias de caracteres estão em um formato de email válido
description: Leia um exemplo de como uma expressão regular verifica se as cadeias de caracteres estão em um formato de email válido no .NET.
ms.date: 06/30/2020
ms.technology: dotnet-standard
dev_langs:
- csharp
- vb
helpviewer_keywords:
- regular expressions, examples
- user input, examples
- Regex.IsMatch method
- regular expressions [.NET Framework], examples
- examples [Visual Basic], strings
- IsValidEmail
- validation, email strings
- input, checking
- strings [.NET Framework], examples [Visual Basic]
- email [.NET Framework], validating
- IsMatch method
ms.assetid: 7536af08-4e86-4953-98a1-a8298623df92
ms.openlocfilehash: 90e79af649727330c2afa1ccb8c64ffe34733f92
ms.sourcegitcommit: 6d4ee46871deb9ea1e45bb5f3784474e240bbc26
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/11/2020
ms.locfileid: "90022942"
---
# <a name="how-to-verify-that-strings-are-in-valid-email-format"></a>Como verificar se cadeias de caracteres estão em um formato de email válido

O exemplo a seguir usa uma expressão regular para verificar se uma cadeia de caracteres está no formato de email válido.

Essa expressão regular é comparativamente simples para o que realmente pode ser usado como um email. Usar uma expressão regular para validar um email é útil para verificar se a estrutura de um email está correta, mas não é uma substituição para verificar se o email realmente existe.

✔️ usar uma pequena expressão regular para verificar a estrutura válida de um email.

✔️ enviar um email de teste para o endereço fornecido por um usuário do seu aplicativo.

❌ Não use uma expressão regular como a única maneira de validar um email.

Se você tentar criar a expressão regular _perfeita_ para validar que a estrutura de um email está correta, a expressão se torna tão complexa que é incrivelmente difícil de Depurar ou melhorar. As expressões regulares não podem validar um email existente, mesmo se ele estiver estruturado corretamente. A melhor maneira de validar um email é enviar um email de teste para o endereço.

[!INCLUDE [regex](../../../includes/regex.md)]

## <a name="example"></a>Exemplo

O exemplo define um `IsValidEmail` método, que retorna `true` se a cadeia de caracteres contém um endereço de email válido e `false` , se não for, mas não executará nenhuma outra ação.

Para verificar se o endereço de email é válido, o método `IsValidEmail` chama o método <xref:System.Text.RegularExpressions.Regex.Replace%28System.String%2CSystem.String%2CSystem.Text.RegularExpressions.MatchEvaluator%29?displayProperty=nameWithType> com o padrão da expressão regular `(@)(.+)$` para separar o nome de domínio do endereço de email. O terceiro parâmetro é um representante <xref:System.Text.RegularExpressions.MatchEvaluator>, que representa o método que processa e substitui o texto correspondente. O padrão da expressão regular é interpretado da seguinte maneira.

| Padrão | Descrição                                                                         |
|---------|-------------------------------------------------------------------------------------|
| `(@)`   | Coincida o caractere @. Essa parte é o primeiro grupo de captura.                           |
| `(.+)`  | Coincida uma ou mais ocorrências de qualquer caractere. Essa parte é o segundo grupo de captura. |
| `$`     | Encerrar a correspondência ao final da cadeia de caracteres.                                             |

O nome de domínio com o caractere @ é passado para o método `DomainMapper`, que usa a classe <xref:System.Globalization.IdnMapping> para converter caracteres Unicode fora do intervalo de caracteres US-ASCII em Punycode. O método também define o sinalizador `invalid` como `True`, caso o método <xref:System.Globalization.IdnMapping.GetAscii%2A?displayProperty=nameWithType> detecte algum caractere inválido no nome do domínio. O método retorna o nome de domínio Punycode precedido pelo símbolo @ para o método `IsValidEmail`.

> [!TIP]
> É recomendável que você use o padrão de `(@)(.+)$` expressão regular simples para normalizar o domínio e, em seguida, retornar um valor indicando que ele passou ou falhou. No entanto, o exemplo neste artigo descreve como usar uma expressão regular para validar o email. Independentemente de como você valida um email, você deve sempre enviar um email de teste para o endereço para verificar se ele existe.

Em seguida, o método `IsValidEmail` chama o método <xref:System.Text.RegularExpressions.Regex.IsMatch%28System.String%2CSystem.String%29?displayProperty=nameWithType> para verificar se o endereço está adequado para um padrão de expressão regular.

O `IsValidEmail` método simplesmente determina se o formato de email é válido para um endereço de email, ele não valida se o email existe. Além disso, o `IsValidEmail` método não verifica se o nome de domínio de nível superior é um nome de domínio válido listado no [banco de dados da zona raiz IANA](https://www.iana.org/domains/root/db), o que exigiria uma operação de pesquisa.

:::code language="csharp" source="snippets/how-to-verify-that-strings-are-in-valid-email-format/csharp/RegexUtilities.cs":::

:::code language="vb" source="snippets/how-to-verify-that-strings-are-in-valid-email-format/vb/RegexUtilities.vb":::

Neste exemplo, o padrão de expressão regular `^[^@\s]+@[^@\s]+\.[^@\s]+$` é interpretado conforme mostrado na tabela a seguir. A expressão regular é compilada usando o <xref:System.Text.RegularExpressions.RegexOptions.IgnoreCase?displayProperty=nameWithType> sinalizador.

| Padrão   | Descrição                                                                              |
|-----------|------------------------------------------------------------------------------------------|
| `^`       | Comece a correspondência no início da cadeia de caracteres.                                              |
| `[^@\s]+` | Corresponder uma ou mais ocorrências de qualquer caractere além do caractere @ ou espaço em branco. |
| `@`       | Coincida o caractere @.                                                                   |
| `[^@\s]+` | Corresponder uma ou mais ocorrências de qualquer caractere além do caractere @ ou espaço em branco. |
| `\.`      | Corresponder a um único caractere de ponto.                                                         |
| `[^@\s]+` | Corresponder uma ou mais ocorrências de qualquer caractere além do caractere @ ou espaço em branco. |
| `$`       | Encerrar a correspondência ao final da cadeia de caracteres.                                                  |

> [!IMPORTANT]
> Esta expressão regular não se destina a abranger todos os aspectos de um endereço de email válido. Ele é fornecido como um exemplo para você estender conforme necessário.

## <a name="see-also"></a>Consulte também

- [Expressões regulares do .NET Framework](regular-expressions.md)
- [Com que distância uma validação de endereço de email deve ser tomada?](https://softwareengineering.stackexchange.com/questions/78353/how-far-should-one-take-e-mail-address-validation#78363)
