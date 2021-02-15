---
ms.openlocfilehash: 9f5f238e3d4222af1da3a1713e1b3e65de6e6f49
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91025374"
---
### <a name="wcf-pipeconnectiongethashalgorithm-now-uses-sha256"></a>PipeConnection.GetHashAlgorithm do WCF agora usa o SHA256

#### <a name="details"></a>Detalhes

A partir do .NET Framework 4.7.1, o Windows Communication Foundation usa o hash SHA256 para gerar nomes aleatórios para pipes nomeados. No .NET Framework 4.7 e nas versões anteriores, ele usa o hash SHA1.

#### <a name="suggestion"></a>Sugestão

Se houver problemas de compatibilidade com essa alteração no .NET Framework 4.7.1 ou uma versão posterior, é possível recusá-la adicionando a seguinte linha à seção `<runtime>` do arquivo app.config:

```xml
<configuration>
  <runtime>
    <AppContextSwitchOverrides value="Switch.System.ServiceModel.UseSha1InPipeConnectionGetHashAlgorithm=true" />
  </runtime>
</configuration>
```

| Name    | Valor   |
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
