---
ms.openlocfilehash: d61a3b3dd855d783d7bff7cb74e5b84969e60860
ms.sourcegitcommit: 97405ed212f69b0a32faa66a5d5fae7e76628b68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2020
ms.locfileid: "91608036"
---
### <a name="aspnet-incorrect-multipart-handling-may-result-in-lost-form-data"></a>ASP.NET A manipulação incorreta com várias partes pode resultar na perda dos dados de formulário.

#### <a name="details"></a>Detalhes

Em aplicativos direcionados .NET Framework 4.7.2 e versões anteriores, o ASP.NET pode analisar incorretamente valores de limite de várias partes, resultando na indisponibilidade dos dados de formulário durante a execução da solicitação. Os aplicativos que direcionam o .NET Framework 4.8 ou versões posteriores analisam corretamente os dados com várias partes para que os valores de formulário estejam disponíveis durante a execução da solicitação.

#### <a name="suggestion"></a>Sugestão

Começando com aplicativos em execução no .NET Framework 4.8, ao direcionar o .NET Framework 4.8 ou posterior usando o elemento <code>targetFrameworkVersion</code>, o comportamento padrão é alterado para retirar os delimitadores. Ao direcionar versões anteriores da estrutura ou não usar <code>targetFrameworkVersion</code>, ainda são retornados delimitadores à direita para alguns valores. Esse comportamento também pode ser explicitamente controlado com um <code>appSetting</code>:<pre><code class="lang-xml">&lt;configuration&gt;&#13;&#10;&lt;appSettings&gt;&#13;&#10;...&#13;&#10;&lt;add key=&quot;aspnet:UseLegacyMultiValueHeaderHandling&quot;  value=&quot;true&quot;/&gt;&#13;&#10;...&#13;&#10;&lt;/appSettings&gt;&#13;&#10;&lt;/configuration&gt;&#13;&#10;</code></pre>

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Unknown|
|Versão|4.8|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Web.HttpRequest.Form?displayProperty=nameWithType>
- <xref:System.Web.HttpRequest.Files?displayProperty=nameWithType>
- <xref:System.Web.HttpRequest.ContentEncoding?displayProperty=nameWithType>

<!--

#### Affected APIs

- `P:System.Web.HttpRequest.Form`
- `P:System.Web.HttpRequest.Files`
- `P:System.Web.HttpRequest.ContentEncoding`

-->
