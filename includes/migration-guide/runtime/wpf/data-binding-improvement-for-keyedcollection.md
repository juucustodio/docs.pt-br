---
ms.openlocfilehash: 8964cd2f69e95e4078001997ad5a5d126ce42d7b
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497381"
---
### <a name="data-binding-improvement-for-keyedcollection"></a>Melhoria de Associação de Dados para KeyedCollection

#### <a name="details"></a>Detalhes

Corrigido o <xref:System.Windows.Data.Binding> uso incorreto de um indexador de IList quando o objeto de origem declara um indexador personalizado com a mesma assinatura (por exemplo, &lt; TItem &gt; ).

#### <a name="suggestion"></a>Sugestão

Para que um aplicativo destinado a uma versão mais antiga se beneficie dessa alteração, ele deve ser executado no .NET Framework 4,8 ou posterior e deve aceitar a alteração adicionando o seguinte [comutador AppContext](https://docs.microsoft.com/dotnet/framework/configure-apps/file-schema/runtime/appcontextswitchoverrides-element) à <code>&lt;runtime&gt;</code> seção do arquivo de configuração do aplicativo e definindo-o como <code>false</code> :<pre><code class="lang-xml">&lt;?xml version=&quot;1.0&quot; encoding=&quot;utf-8&quot;?&gt;&#13;&#10;&lt;configuration&gt;&#13;&#10;&lt;startup&gt;&#13;&#10;&lt;supportedRuntime version=&quot;v4.0&quot; sku=&quot;.NETFramework,Version=v4.7&quot;/&gt;&#13;&#10;&lt;/startup&gt;&#13;&#10;&lt;runtime&gt;&#13;&#10;&lt;!-- AppContextSwitchOverrides value attribute is in the form of &#39;key1=true/false;key2=true/false  --&gt;&#13;&#10;&lt;AppContextSwitchOverrides value=&quot;Switch.System.Windows.Data.Binding.IListIndexerHidesCustomIndexer=false&quot; /&gt;&#13;&#10;&lt;/runtime&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Principal|
|Versão|4.8|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
