---
ms.openlocfilehash: 6ffd4147a99a59d0a2e50d3f88279608e286aed1
ms.sourcegitcommit: aa6d8a90a4f5d8fe0f6e967980b8c98433f05a44
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/16/2020
ms.locfileid: "90679951"
---
### <a name="cryptostreamdispose-transforms-final-block-only-when-writing"></a>CryptoStream. Dispose transforma o bloco final somente durante a gravação

O <xref:System.Security.Cryptography.CryptoStream.Dispose%2A?displayProperty=nameWithType> método, que é usado para concluir `CryptoStream` as operações, não tenta mais transformar o bloco final durante a leitura.

#### <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, se um usuário realizou uma leitura incompleta ao usar <xref:System.Security.Cryptography.CryptoStream> no <xref:System.Security.Cryptography.CryptoStreamMode.Read> modo, o <xref:System.Security.Cryptography.CryptoStream.Dispose%2A> método poderia gerar uma exceção (por exemplo, ao usar AES com preenchimento). A exceção foi gerada porque o bloco final tentou ser transformado, mas os dados estavam incompletos.

No .NET Core 3,0 e versões posteriores, <xref:System.Security.Cryptography.CryptoStream.Dispose%2A> o não tenta mais transformar o bloco final ao ler, o que permite leituras incompletas.

#### <a name="reason-for-change"></a>Motivo da alteração

Essa alteração permite leituras incompletas do fluxo de criptografia quando uma operação de rede é cancelada, sem a necessidade de capturar uma exceção.

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="recommended-action"></a>Ação recomendada

A maioria dos aplicativos não deve ser afetada por essa alteração.

Se seu aplicativo capturou anteriormente uma exceção no caso de uma leitura incompleta, você pode excluir esse `catch` bloco.
Se seu aplicativo usou a transformação do bloco final em cenários de hash, talvez seja necessário garantir que todo o fluxo seja lido antes de ser Descartado.

#### <a name="category"></a>Categoria

Criptografia

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Security.Cryptography.CryptoStream.Dispose%2A?displayProperty=fullName>

<!--

#### Affected APIs

- `M:System.Security.Cryptography.CryptoStream.Dispose`

-->
