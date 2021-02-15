---
ms.openlocfilehash: 3506653bfc749ae3d8002715ca72ca89de7a681b
ms.sourcegitcommit: d2db216e46323f73b32ae312c9e4135258e5d68e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/22/2020
ms.locfileid: "91024959"
---
### <a name="wcf-addressheadercollection-now-throws-an-argumentexception-if-an-addressheader-element-is-null"></a>AddressHeaderCollection do WCF agora gera ArgumentException se um elemento addressHeader for nulo

#### <a name="details"></a>Detalhes

A partir do .NET Framework 4.7.1, o construtor <xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})> gera <xref:System.ArgumentException> se um elemento for `null`. No .NET Framework 4.7 e versões anteriores, nenhuma exceção é gerada.

#### <a name="suggestion"></a>Sugestão

Se você encontrar problemas de compatibilidade com essa alteração no .NET Framework 4.7.1 ou em uma versão posterior, poderá recusar isso adicionando a seguinte linha à `<runtime>` seção do arquivo app.config:

```xml
<configuration>
  <runtime>
    <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableAddressHeaderCollectionValidation=true" />
  </runtime>
</configuration>
```

| Name    | Valor   |
|:--------|:--------|
| Escopo   | Secundária   |
| Versão | 4.7.1   |
| Tipo    | Runtime |

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.ServiceModel.Channels.AddressHeaderCollection.%23ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})>

<!--

#### Affected APIs

- `M:System.ServiceModel.Channels.AddressHeaderCollection.#ctor(System.Collections.Generic.IEnumerable{System.ServiceModel.Channels.AddressHeader})`

-->
