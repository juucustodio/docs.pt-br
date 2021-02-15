---
ms.openlocfilehash: a4476fbff572c004632153e5a98812c241efca57
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031961"
---
### <a name="openssl-versions-on-macos"></a>Versões do OpenSSL no macOS

Os tempos de execução do .NET Core 3,0 e posteriores no MacOS agora preferem as versões do OpenSSL 1.1. x às versões do OpenSSL 1.0. x para os <xref:System.Security.Cryptography.AesCcm> <xref:System.Security.Cryptography.AesGcm> tipos,, <xref:System.Security.Cryptography.DSAOpenSsl> , <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl> ,, <xref:System.Security.Cryptography.ECDsaOpenSsl> <xref:System.Security.Cryptography.RSAOpenSsl> e <xref:System.Security.Cryptography.SafeEvpPKeyHandle> .

O tempo de execução do .NET Core 2,1 agora dá suporte às versões do OpenSSL 1.1. x, mas ainda prefere as versões do OpenSSL 1.0. x.

#### <a name="change-description"></a>Descrição das alterações

Anteriormente, o tempo de execução do .NET Core usava as versões do OpenSSL 1.0. x no macOS para tipos que interagem com o OpenSSL. A versão mais recente do OpenSSL 1.0. x, OpenSSL 1.0.2, agora está sem suporte. Para manter os tipos que usam o OpenSSL nas versões com suporte do OpenSSL, os tempos de execução do .NET Core 3,0 e posteriores agora usam versões mais recentes do OpenSSL no macOS.

Com essa alteração, o comportamento dos tempos de execução do .NET Core no macOS é o seguinte:

- Os tempos de execução do .NET Core 3,0 e versões posteriores usam o OpenSSL 1.1. x, se disponível, e retornarão ao OpenSSL 1.0. x somente se não houver nenhuma versão 1.1. x disponível.

  Para chamadores que usam os tipos de interoperabilidade OpenSSL com P/Invokes personalizados, siga as orientações em <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> comentários. Seu aplicativo poderá falhar se você não verificar o <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion> valor.

- O tempo de execução do .NET Core 2,1 usa o OpenSSL 1.0. x, se estiver disponível, e voltará ao OpenSSL 1.1. x se não houver nenhuma versão 1.0. x disponível.

  O tempo de execução 2,1 prefere a versão anterior do OpenSSL porque a <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> propriedade não existe no .NET Core 2,1, portanto, a versão do OpenSSL não pode ser determinada de forma confiável no tempo de execução.

#### <a name="version-introduced"></a>Versão introduzida

- 2.1.16 do .NET Core
- 3.0.3 do .NET Core
- 3.1.2 do .NET Core

#### <a name="recommended-action"></a>Ação recomendada

- Desinstale o OpenSSL versão 1.0.2 se ele não for mais necessário.

- Instale o OpenSSL 1.1. x se você usar <xref:System.Security.Cryptography.AesCcm> os <xref:System.Security.Cryptography.AesGcm> tipos,,,,, <xref:System.Security.Cryptography.DSAOpenSsl> <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl> <xref:System.Security.Cryptography.ECDsaOpenSsl> <xref:System.Security.Cryptography.RSAOpenSsl> ou <xref:System.Security.Cryptography.SafeEvpPKeyHandle> .

- Se você usar os tipos de interoperabilidade OpenSSL com P/Invokes personalizados, siga as orientações em <xref:System.Security.Cryptography.SafeEvpPKeyHandle.OpenSslVersion?displayProperty=nameWithType> comentários.

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Security.Cryptography.AesCcm?displayProperty=fullName>
- <xref:System.Security.Cryptography.AesGcm?displayProperty=fullName>
- <xref:System.Security.Cryptography.DSAOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.ECDiffieHellmanOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.ECDsaOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.RSAOpenSsl?displayProperty=fullName>
- <xref:System.Security.Cryptography.SafeEvpPKeyHandle?displayProperty=fullName>

<!--

#### Affected APIs

- `T:System.Security.Cryptography.AesCcm``
- `T:System.Security.Cryptography.AesGcm`
- `T:System.Security.Cryptography.DSAOpenSsl`
- `T:System.Security.Cryptography.ECDiffieHellmanOpenSsl`
- `T:System.Security.Cryptography.ECDsaOpenSsl`
- `T:System.Security.Cryptography.RSAOpenSsl`
- `T:System.Security.Cryptography.SafeEvpPKeyHandle`

-->
