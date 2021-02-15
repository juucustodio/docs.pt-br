---
title: 'Alteração significativa: valor de FeedbackSize padrão para instâncias criadas por TripleDES. Create alterado'
description: Saiba mais sobre a alteração significativa no .NET 5,0, em que o valor padrão da propriedade FeedbackSize na instância TripleDES retornada de TripleDES. Create () foi alterado de 64 para 8.
ms.date: 10/16/2020
ms.openlocfilehash: 4179da17bf2e5cc5fcc7d64d83ba92119f912042
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760486"
---
# <a name="default-feedbacksize-value-for-instances-created-by-tripledescreate-changed"></a>Valor de FeedbackSize padrão para instâncias criadas por TripleDES. Create alterado

O valor padrão da <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize?displayProperty=nameWithType> Propriedade na <xref:System.Security.Cryptography.TripleDES> instância retornada de <xref:System.Security.Cryptography.TripleDES.Create?displayProperty=nameWithType> foi alterado de 64 para 8 para tornar a migração de .NET Framework mais fácil. Essa propriedade, a menos que usada diretamente no código do chamador, é usada somente quando a <xref:System.Security.Cryptography.SymmetricAlgorithm.Mode> propriedade é <xref:System.Security.Cryptography.CipherMode.CFB?displayProperty=nameWithType> .

O suporte para o <xref:System.Security.Cryptography.CipherMode.CFB> modo foi adicionado primeiro ao .net para a versão 5,0 RC1, portanto, somente os aplicativos .net 5,0 RC1 e .net 5,0 RC2 devem ser afetados por essa alteração.

## <a name="change-description"></a>Descrição das alterações

No .NET Core e nas versões anteriores de pré-lançamento do .NET 5,0, `TripleDES.Create().FeedbackSize` o tem um valor padrão de 64. A partir da versão RTM do .NET 5,0, `TripleDES.Create().FeedbackSize` tem um valor padrão de 8.

## <a name="reason-for-change"></a>Motivo da alteração

Em .NET Framework, a <xref:System.Security.Cryptography.TripleDES> classe base usa como padrão o valor de <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize> 64, mas a <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider> classe substitui o padrão por 8. Quando a <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize> propriedade foi introduzida no .NET Core na versão 2,0, esse mesmo comportamento foi preservado. No entanto, em .NET Framework, <xref:System.Security.Cryptography.TripleDES.Create?displayProperty=nameWithType> retorna uma instância do <xref:System.Security.Cryptography.TripleDESCryptoServiceProvider> , portanto, o valor padrão da fábrica de algoritmos é 8. Para .NET Core e .NET 5 +, a fábrica de algoritmos retorna uma implementação não pública, que, até agora, tinha um valor padrão de 64.

A alteração da <xref:System.Security.Cryptography.TripleDES> classe de implementação ' o <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize> valor para 8 permite que aplicativos escritos para .NET Framework que especificam o modo de codificação como <xref:System.Security.Cryptography.CipherMode.CFB> , mas que não tenham sido explicitamente atribuídos à <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize> propriedade, continuem a funcionar no .NET 5.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Os aplicativos que criptografam ou descriptografam dados nas versões RC1 ou RC2 do .NET 5,0 fazem isso com o CFB64, quando as seguintes condições são atendidas:

- Com uma <xref:System.Security.Cryptography.TripleDES> instância do <xref:System.Security.Cryptography.TripleDES.Create?displayProperty=nameWithType> .
- Usando o valor padrão para <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize> .
- Com a <xref:System.Security.Cryptography.SymmetricAlgorithm.Mode> propriedade definida como <xref:System.Security.Cryptography.CipherMode.CFB?displayProperty=nameWithType> .

Para manter esse comportamento, atribua a <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize> Propriedade a `64` .

Nem todas as `TripleDES` implementações usam o mesmo padrão para <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize> . Recomendamos que, se você usar o <xref:System.Security.Cryptography.CipherMode.CFB> modo de codificação em <xref:System.Security.Cryptography.TripleDES> instâncias, deverá sempre atribuir explicitamente o <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize> valor da propriedade.

```csharp
TripleDES cipher = TripleDES.Create();
cipher.Mode = CipherMode.CFB;
// Explicitly set the FeedbackSize for CFB to control between CFB8 and CFB64.
cipher.FeedbackSize = 8;
```

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Security.Cryptography.TripleDES.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize?displayProperty=fullName>

<!--

### Affected APIs

- `M:System.Security.Cryptography.TripleDES.Create`
- `P:System.Security.Cryptography.SymmetricAlgorithm.FeedbackSize`

### Category

- Cryptography

-->
