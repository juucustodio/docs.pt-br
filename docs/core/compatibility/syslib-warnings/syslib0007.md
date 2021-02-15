---
title: Aviso de SYSLIB0007
description: Saiba mais sobre o obsoletions que gera SYSLIB0007 de aviso de tempo de compilação.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: c011340665a0c53172bf5b23e032d78301b3cd72
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596442"
---
# <a name="syslib0007-default-implementations-of-cryptography-algorithms-not-supported"></a>SYSLIB0007: não há suporte para implementações padrão de algoritmos de criptografia

O sistema de configuração criptográfica no .NET Framework não permite a agilidade criptográfica adequada e não está presente no .NET Core e no .NET 5 +. . Os requisitos de compatibilidade com versões anteriores do NET também proíbem a estrutura de atualizar determinadas APIs de criptografia para acompanhar os avanços na criptografia. Como resultado, as seguintes APIs são marcadas como obsoletas, a partir do .NET 5,0. O uso dessas APIs gera aviso `SYSLIB0007` no momento da compilação.

- <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.HMAC.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=fullName>
- <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=fullName>

## <a name="workarounds"></a>Soluções Alternativas

- O curso de ação recomendado é substituir as chamadas para as APIs agora obsoletas por chamadas para métodos de fábrica para algoritmos específicos, por exemplo, <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType> . Isso lhe dá controle total sobre quais algoritmos são instanciados.

- Se você precisar manter a compatibilidade com as cargas existentes geradas por .NET Framework aplicativos que usam as APIs agora obsoletas, use as substituições sugeridas na tabela a seguir. A tabela fornece um mapeamento de .NET Framework algoritmos padrão para seus equivalentes do .NET 5 +.

  | .NET Framework | .NET Core/.NET 5.0 + substituição compatível | Comentários |
  | - | - | - |
  | <xref:System.Security.Cryptography.AsymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.RSA.Create?displayProperty=nameWithType> | |
  | <xref:System.Security.Cryptography.HashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.SHA1.Create?displayProperty=nameWithType> | O algoritmo SHA-1 é considerado desfeito. Considere o uso de um algoritmo mais forte, se possível. Consulte seu supervisor de segurança para obter mais diretrizes. |
  | <xref:System.Security.Cryptography.HMAC.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | O algoritmo HMACSHA1 não é recomendado para a maioria dos aplicativos modernos. Considere o uso de um algoritmo mais forte, se possível. Consulte seu supervisor de segurança para obter mais diretrizes. |
  | <xref:System.Security.Cryptography.KeyedHashAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.HMACSHA1.%23ctor> | O algoritmo HMACSHA1 não é recomendado para a maioria dos aplicativos modernos. Considere o uso de um algoritmo mais forte, se possível. Consulte seu supervisor de segurança para obter mais diretrizes. |
  | <xref:System.Security.Cryptography.SymmetricAlgorithm.Create?displayProperty=nameWithType> | <xref:System.Security.Cryptography.Aes.Create?displayProperty=nameWithType> |

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>Confira também

- [Não há suporte para a instanciação de implementações padrão de abstrações criptográficas](../cryptography/5.0/instantiating-default-implementations-of-cryptographic-abstractions-not-supported.md)
