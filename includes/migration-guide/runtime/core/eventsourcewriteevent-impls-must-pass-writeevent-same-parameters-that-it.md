---
ms.openlocfilehash: 99a7fa0fcfce6d490a182f85709b5dd0e0e8c86f
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497051"
---
### <a name="eventsourcewriteevent-impls-must-pass-writeevent-the-same-parameters-that-it-received-plus-id"></a>EventSource.WriteEvent deve passar a WriteEvent os mesmos parâmetros que recebeu (mais ID)

#### <a name="details"></a>Detalhes

O runtime agora impõe o contrato que especifica o seguinte: uma classe derivada de <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> que define um método de evento ETW deve chamar o método de classe base <code>EventSource.WriteEvent</code> com a ID do evento seguido dos mesmos argumentos que o método de evento ETW passou.

#### <a name="suggestion"></a>Sugestão

Uma exceção <xref:System.IndexOutOfRangeException?displayProperty=fullName> será acionada se um <xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName> ler dados <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> no processo de uma origem de evento que viola esse contrato.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Secundária|
|Versão|4.5.1|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

Não detectável via análise de API.

<!--

#### Affected APIs

Not detectable via API analysis.

-->
