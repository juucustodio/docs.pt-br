---
ms.openlocfilehash: f6553444e13416850a398ae5bcb6574f2a69bd2d
ms.sourcegitcommit: 721c3e4bdbb1ea0bb420818ec944c538fe5c513a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/01/2020
ms.locfileid: "96476528"
---
### <a name="improved-wcf-chain-trust-certificate-validation-for-nettcp-certificate-authentication"></a>Melhor validação do certificado de confiança de cadeia do WCF para autenticação de certificado do Net.Tcp

#### <a name="details"></a>Detalhes

O .NET framework 4.7.2 melhorou a validação do certificado de confiança de cadeia ao usar a autenticação de certificado com a segurança de transporte com o WCF. Com essa melhoria, os certificados do cliente que são usados para autenticar um servidor precisam ser configurados para autenticação do cliente.  Da mesma forma, os certificados do servidor usados para autenticar um servidor precisam ser configurados para autenticação do servidor. Com essa alteração, se o certificado raiz for desabilitado, a validação da cadeia de certificados falhará. A mesma alteração também foi feita para o .NET Framework 3.5 e as versões posteriores por meio do pacote cumulativo de segurança do Windows. Encontre mais informações [aqui](https://support.microsoft.com/help/4055269/security-only-update-for-net-framework-3-5-1-4-5-2-4-6-4-6-1-4-6-2-4-7). Essa alteração é habilitada por padrão e pode ser desabilitada por uma definição de configuração.

#### <a name="suggestion"></a>Sugestão

<ul><li>Valide se a certificação do servidor e do cliente têm o OID de EKU necessário. Caso contrário, atualize a certificação.</li><li>Valide se o certificado raiz é inválido. Nesse caso, atualize o certificado raiz.</li><li>Como recusar a alteração: se você não puder atualizar o certificado, poderá contornar temporariamente a alteração significativa com a definição de configuração a seguir, no entanto, a recusa da alteração deixará o sistema vulnerável ao problema de segurança.</li></ul><pre><code class="lang-xml">&lt;appSettings&gt;&#13;&#10;&lt;add key=&quot;wcf:useLegacyCertificateUsagePolicy&quot; value=&quot;true&quot; /&gt;&#13;&#10;&lt;/appSettings&gt;&#13;&#10;</code></pre>

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
