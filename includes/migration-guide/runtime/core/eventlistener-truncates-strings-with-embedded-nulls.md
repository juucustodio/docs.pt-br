---
ms.openlocfilehash: e47a24239872e3fe86ff6902f66b38daaa106598
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497663"
---
### <a name="eventlistener-truncates-strings-with-embedded-nulls"></a>EventListener trunca cadeias de caracteres com nulos inseridos

#### <a name="details"></a>Detalhes

<xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName> trunca cadeias de caracteres com nulos inseridos. Os caracteres nulos não são compatíveis com a classe <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName>. A alteração afeta apenas os aplicativos que usam <xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName> para ler dados <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> no processo e que usam caracteres nulos como delimitadores.

#### <a name="suggestion"></a>Sugestão

Os dados <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> devem ser atualizados, se possível, para não usar caracteres nulos inseridos.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.5.1|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Diagnostics.Tracing.EventListener.%23ctor>
- <xref:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel)?displayProperty=nameWithType>
- <xref:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel,System.Diagnostics.Tracing.EventKeywords)?displayProperty=nameWithType>
- <xref:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel,System.Diagnostics.Tracing.EventKeywords,System.Collections.Generic.IDictionary{System.String,System.String})?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Diagnostics.Tracing.EventListener.#ctor`
- `M:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel)`
- `M:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel,System.Diagnostics.Tracing.EventKeywords)`
- `M:System.Diagnostics.Tracing.EventListener.EnableEvents(System.Diagnostics.Tracing.EventSource,System.Diagnostics.Tracing.EventLevel,System.Diagnostics.Tracing.EventKeywords,System.Collections.Generic.IDictionary{System.String,System.String})`

-->
