---
ms.openlocfilehash: 7c0227980aa5d90f3788783088bcd7cd9509ed66
ms.sourcegitcommit: 261e0c98a111357692b3b63c596edf0cacf72991
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/18/2020
ms.locfileid: "90770808"
---
### <a name="wcf-msmqsecurehashalgorithm-default-value-is-now-sha256"></a>O valor padrão MsmqSecureHashAlgorithm do WCF agora é SHA256

#### <a name="details"></a>Detalhes

A partir do .NET Framework 4.7.1, o algoritmo de assinatura da mensagem padrão no WCF para mensagens Msmq é SHA256. No .NET Framework 4.7 e versões anteriores, o algoritmo de assinatura da mensagem padrão é SHA1.

#### <a name="suggestion"></a>Sugestão

Se você tiver problemas de compatibilidade com essa alteração no .NET Framework 4.7.1 ou posterior, poderá recusar a alteração adicionando a seguinte linha à `<runtime>` seção do arquivo de app.config:

```xml
<configuration>
  <runtime>
    <AppContextSwitchOverrides value=&quot;Switch.System.ServiceModel.UseSha1InMsmqEncryptionAlgorithm=true&quot; />
  </runtime>
</configuration>
```

| Nome    | Valor   |
|:--------|:--------|
| Escopo   | Secundária   |
| Versão | 4.7.1   |
| Tipo    | Runtime |

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
