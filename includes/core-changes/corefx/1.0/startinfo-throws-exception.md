---
ms.openlocfilehash: 92c03328414410d56a2ff5f445639757367b42c7
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96031952"
---
### <a name="processstartinfo-throws-invalidoperationexception-for-processes-you-didnt-start"></a>Process. StartInfo gera InvalidOperationException para processos que você não iniciou

Ler a <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> propriedade para processos que seu código não iniciou lança um <xref:System.InvalidOperationException> .

#### <a name="change-description"></a>Descrição das alterações

Em .NET Framework, o acesso à <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> propriedade para processos que seu código não iniciou retorna um <xref:System.Diagnostics.ProcessStartInfo> objeto fictício. O objeto fictício contém valores padrão para todas as suas propriedades, exceto <xref:System.Diagnostics.ProcessStartInfo.EnvironmentVariables> .

A partir do .NET Core 1,0, se você ler a <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> propriedade para um processo que não iniciou (ou seja, chamando <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> ), um <xref:System.InvalidOperationException> será lançado.

#### <a name="version-introduced"></a>Versão introduzida

1.0

#### <a name="recommended-action"></a>Ação recomendada

Não acesse a <xref:System.Diagnostics.Process.StartInfo?displayProperty=nameWithType> propriedade para processos que seu código não iniciou. Por exemplo, não leia esta propriedade para processos retornados por <xref:System.Diagnostics.Process.GetProcesses%2A?displayProperty=nameWithType> .

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Diagnostics.Process.StartInfo?displayProperty=fullName>

<!--

#### Affected APIs

- `P:System.Diagnostics.Process.StartInfo`

-->
