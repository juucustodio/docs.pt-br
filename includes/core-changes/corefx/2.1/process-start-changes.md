---
ms.openlocfilehash: dcc64fe651b219ff1416c0afcdb4c6d275160f4b
ms.sourcegitcommit: 88fbb019b84c2d044d11fb4f6004aec07f2b25b1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/05/2021
ms.locfileid: "97911652"
---
### <a name="change-in-default-value-of-useshellexecute"></a>Alteração no valor padrão de UseShellExecute

<xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> tem um valor padrão de `false` no .NET Core. Em .NET Framework, seu valor padrão é `true` .

#### <a name="change-description"></a>Descrição das alterações

<xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> permite que você inicie um aplicativo diretamente, por exemplo, com um código como o `Process.Start("mspaint.exe")` que inicia o Paint. Ele também permite que você inicie indiretamente um aplicativo associado se <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> estiver definido como `true` . Em .NET Framework, o valor padrão para <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> é `true` , o que significa que o código como o `Process.Start("mytextfile.txt")` iniciaria o bloco de notas, se você tiver associado arquivos *. txt* com esse editor. Para evitar a inicialização indireta de um aplicativo no .NET Framework, você deve definir explicitamente <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> como `false` . No .NET Core, o valor padrão para <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> é `false` . Isso significa que, por padrão, os aplicativos associados não são iniciados quando você chama `Process.Start` .

As seguintes propriedades em <xref:System.Diagnostics.ProcessStartInfo?displayProperty=nameWithType> são funcionais somente quando o <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> é `true` :

- <xref:System.Diagnostics.ProcessStartInfo.CreateNoWindow?displayProperty=nameWithType>
- <xref:System.Diagnostics.ProcessStartInfo.ErrorDialog?displayProperty=nameWithType>
- <xref:System.Diagnostics.ProcessStartInfo.Verb?displayProperty=nameWithType>
- <xref:System.Diagnostics.ProcessStartInfo.WindowStyle?displayProperty=nameWithType>.

Essa alteração foi introduzida no .NET Core por motivos de desempenho. Normalmente, <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType> é usado para iniciar um aplicativo diretamente. Iniciar um aplicativo diretamente não precisa envolver o Shell do Windows e incorrer no custo de desempenho associado. Para tornar esse caso padrão mais rápido, o .NET Core altera o valor padrão de <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute?displayProperty=nameWithType> para `false` . Você pode aceitar o caminho mais lento se precisar dele.

#### <a name="version-introduced"></a>Versão introduzida

2.1

> [!NOTE]
> Em versões anteriores do .NET Core, o `UseShellExecute` não foi implementado para o Windows.

#### <a name="recommended-action"></a>Ação recomendada

Se seu aplicativo depender do comportamento antigo, chame <xref:System.Diagnostics.Process.Start(System.Diagnostics.ProcessStartInfo)?displayProperty=nameWithType> com <xref:System.Diagnostics.ProcessStartInfo.UseShellExecute> definido como `true` no <xref:System.Diagnostics.ProcessStartInfo> objeto.

#### <a name="category"></a>Categoria

Bibliotecas principais do .NET

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Diagnostics.Process.Start%2A?displayProperty=nameWithType>
- <xref:System.Diagnostics.ProcessStartInfo?displayProperty=nameWithType>

<!--

#### Affected APIs

- `Overload:System.Diagnostics.Process.Start`
- `M:System.Diagnostics.ProcessStartInfo`

-->
