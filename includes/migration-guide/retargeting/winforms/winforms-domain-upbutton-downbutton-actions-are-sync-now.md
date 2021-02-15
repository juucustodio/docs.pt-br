---
ms.openlocfilehash: c64431fd651fd7d53fb46231c6acc10c5cb43fff
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606907"
---
### <a name="winforms-domain-upbutton-and-downbutton-actions-are-in-sync-now"></a>As ações de upbutton e downbutton de domínio do WinForm agora estão sincronizadas

#### <a name="details"></a>Detalhes

No .NET Framework 4.7.1 e nas versões anteriores, a ação <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> do controle <xref:System.Windows.Forms.DomainUpDown> é ignorada quando o texto do controle está presente e o desenvolvedor precisa usar a ação <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType> no controle antes de usar a ação <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType>. Começando com o .NET Framework 4.7.2, as ações <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType> e <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType> funcionam de forma independente neste cenário e permanecem em sincronização.

#### <a name="suggestion"></a>Sugestão

Para que o aplicativo se beneficie dessas alterações, ele deverá ser executado no .NET Framework 4.7.2 ou posterior. O aplicativo pode se beneficiar dessas alterações de uma das seguintes maneiras:

- Ser recompilado para ser direcionado ao .NET Framework 4.7.2. Essa alteração é habilitada por padrão nos aplicativos do Windows Forms direcionados ao .NET Framework 4.7.2 ou posterior.
- Recusar o comportamento de rolagem herdado adicionando a seguinte [Opção de AppContext](../../../../docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) à seção `<runtime>` do arquivo de configuração de aplicativo e configurando-a como `false`, como mostra o exemplo a seguir.

<pre><code class="lang-xml">&lt;runtime&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Forms.DomainUpDown.UseLegacyScrolling=false&quot;/&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;</code></pre>

| Name    | Valor       |
|:--------|:------------|
| Escopo   | Microsoft Edge        |
| Versão | 4.7.2       |
| Tipo    | Redirecionando |

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.Forms.DomainUpDown.UpButton?displayProperty=nameWithType>
- <xref:System.Windows.Forms.DomainUpDown.DownButton?displayProperty=nameWithType>
