---
ms.openlocfilehash: c8f017084fc1ec1eca636ef0178a40559e15b2c5
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496405"
---
### <a name="improved-wcf-chain-trust-certificate-validation-for-nettcp-certificate-authentication"></a>Melhor validação do certificado de confiança de cadeia do WCF para autenticação de certificado do Net.Tcp

#### <a name="details"></a>Detalhes

O .NET framework 4.7.2 melhorou a validação do certificado de confiança de cadeia ao usar a autenticação de certificado com a segurança de transporte com o WCF. Com essa melhoria, os certificados do cliente que são usados para autenticar um servidor precisam ser configurados para autenticação do cliente.  Da mesma forma, os certificados do servidor usados para autenticar um servidor precisam ser configurados para autenticação do servidor. Com essa alteração, se o certificado raiz for desabilitado, a validação da cadeia de certificados falhará. A mesma alteração também foi feita para o .NET Framework 3.5 e as versões posteriores por meio do pacote cumulativo de segurança do Windows. Encontre mais informações [aqui](https://support.microsoft.com/help/4055269/security-only-update-for-net-framework-3-5-1-4-5-2-4-6-4-6-1-4-6-2-4-7). Essa alteração é habilitada por padrão e pode ser desabilitada por uma definição de configuração.

#### <a name="suggestion"></a>Sugestão

<ul><li>Valide se a certificação do servidor e do cliente têm o OID de EKU necessário. Caso contrário, atualize a certificação.</li><li>Valide se o certificado raiz é inválido. Nesse caso, atualize o certificado raiz.</li><li>Como recusar a alteração: se você não puder atualizar o certificado, contorne temporariamente a alteração da falha com as definições de configuração a seguir. No entanto, recusar a alteração deixará seu sistema vulnerável ao problema de segurança.</li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;wcf:useLegacyCertificateUsagePolicy&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.7.2|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
