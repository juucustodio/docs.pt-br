---
ms.openlocfilehash: aadf5eb85c8736c29639d49bc8baf21545d2467c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90606327"
---
### <a name="net-com-successfully-marshals-byref-safearray-parameters-on-events"></a>O .NET COM realiza marshaling bem-sucedido de parâmetros ByRef SafeArray em eventos

#### <a name="details"></a>Detalhes

No .NET Framework 4.7.2 e versões anteriores, um parâmetro ByRef [SafeArray](/windows/desktop/api/oaidl/ns-oaidl-safearray) em um evento COM falharia realizar marshaling de volta para o código nativo.  Com essa alteração, agora o marshal do [SafeArray](/windows/desktop/api/oaidl/ns-oaidl-safearray) foi realizado com êxito.<ul><li>[x] Quirked</li></ul>

#### <a name="suggestion"></a>Sugestão

Se a realização de marshal dos parâmetros ByRef SafeArray corretamente em eventos COM interromper a execução, será possível desabilitar esse código adicionando a seguinte opção de configuração à sua configuração de aplicativo:<pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;Switch.System.Runtime.InteropServices.DoNotMarshalOutByrefSafeArrayOnInvoke&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>

| Name    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.8|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
