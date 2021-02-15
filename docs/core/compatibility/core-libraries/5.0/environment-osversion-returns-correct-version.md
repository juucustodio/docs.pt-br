---
title: 'Alteração significativa: Environment. OSVersion retorna a versão correta do sistema operacional'
description: Saiba mais sobre a alteração significativa do .NET 5,0 em bibliotecas principais do .NET em que Environment. OSVersion retorna a versão real do sistema operacional em vez de, por exemplo, o sistema operacional selecionado para compatibilidade de aplicativos.
ms.date: 11/01/2020
ms.openlocfilehash: c810d9a7a028a0c60c30d69e78a9b9c695d933ef
ms.sourcegitcommit: 81f1bba2c97a67b5ca76bcc57b37333ffca60c7b
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/10/2020
ms.locfileid: "97009515"
---
# <a name="environmentosversion-returns-the-correct-operating-system-version"></a>Environment. OSVersion retorna a versão correta do sistema operacional

<xref:System.Environment.OSVersion?displayProperty=nameWithType> Retorna a versão real do sistema operacional (SO) em vez de, por exemplo, o sistema operacional selecionado para compatibilidade de aplicativos.

## <a name="change-description"></a>Descrição da alteração

Nas versões anteriores do .NET, <xref:System.Environment.OSVersion?displayProperty=nameWithType> retorna uma versão do sistema operacional que pode estar incorreta quando um aplicativo é executado no modo de compatibilidade do Windows. Para obter mais informações, consulte [comentários da função GetVersionExA](/windows/win32/api/sysinfoapi/nf-sysinfoapi-getversionexa#remarks). No macOS, <xref:System.Environment.OSVersion?displayProperty=nameWithType> retorna a versão de kernel Darwin subjacente.

A partir do .NET 5,0, <xref:System.Environment.OSVersion?displayProperty=nameWithType> retorna a versão real do sistema operacional para Windows e MacOS.

A tabela a seguir mostra a diferença no comportamento.

|  | Versões anteriores do .NET | .NET 5 + |
|--|------------------------|---------|
| Windows | 6.2.9200.0 | 10.0.19042.0 |
| macOS | 19.6.0.0 | 10.15.7 |

## <a name="reason-for-change"></a>Motivo da alteração

Os usuários dessa propriedade esperam que ele retorne a versão real do sistema operacional. A maioria dos aplicativos .NET não especifica sua versão com suporte no manifesto do aplicativo e, portanto, obtém a versão padrão com suporte do host dotnet. Como resultado, o Shim de compatibilidade raramente é significativo para o aplicativo em execução. Quando o Windows libera uma nova versão e um host dotnet mais antigo ainda está em uso, esses aplicativos podem obter uma versão incorreta do sistema operacional. Retornar a versão real é mais embutido com as expectativas dos desenvolvedores desta API.

Com a introdução de <xref:System.OperatingSystem.IsWindowsVersionAtLeast%2A?displayProperty=nameWithType> , <xref:System.OperatingSystem.IsMacOSVersionAtLeast%2A?displayProperty=nameWithType> e <xref:System.Runtime.Versioning.SupportedOSPlatformAttribute?displayProperty=nameWithType> no .NET 5,0, <xref:System.Environment.OSVersion?displayProperty=nameWithType> foi alterada para ser consistente para Windows e MacOS.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Revise e teste qualquer código que use <xref:System.Environment.OSVersion?displayProperty=nameWithType> para garantir que ele se comporta conforme o desejado.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Environment.OSVersion?displayProperty=fullName>

<!--

### Category

Core .NET libraries

### Affected APIs

- `P:System.Environment.OSVersion`

-->
