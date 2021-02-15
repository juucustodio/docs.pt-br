---
ms.openlocfilehash: 77e231f8ef1dde8a263b8622311099a4a404062d
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606671"
---
### <a name="hwndhost-now-correctly-resizes-child-hwnd-during-dpi-changes"></a>Agora o HwndHost redimensiona corretamente HWND filho durante alterações de DPI

#### <a name="details"></a>Detalhes

No .NET Framework 4.7.2 e versões anteriores, quando o WPF estava sendo executado no modo Com reconhecimento por monitor, os controles hospedados em <xref:System.Windows.Interop.HwndHost> não foram dimensionados corretamente após alterações de DPI, por exemplo, ao migrar aplicativos de um monitor para outro. Com essa correção, os controles hospedados são dimensionados apropriadamente.

#### <a name="suggestion"></a>Sugestão

Para que o aplicativo se beneficie dessas alterações, ele deve ser executado no .NET Framework 4.7.2 ou posterior e aceitar esse comportamento definindo o seguinte comutador [AppContext](../../../../docs/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element.md) na seção `<runtime>` do arquivo de configuração do aplicativo `false`, conforme mostrado pelo exemplo a seguir.

<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;startup&gt;&#13;&#10;&lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.7&quot;/&gt;&#13;&#10;&lt;/startup&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.DoNotUsePresentationDpiCapabilityTier2OrGreater=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| Name    | Valor       |
|:--------|:------------|
| Escopo   | Principal       |
| Versão | 4.8         |
| Tipo    | Redirecionando |
