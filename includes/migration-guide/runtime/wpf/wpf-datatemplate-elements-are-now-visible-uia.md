---
ms.openlocfilehash: 4394e69dafeb6cce2d7719a67bbce396d3bc1086
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89497909"
---
### <a name="wpf-datatemplate-elements-are-now-visible-to-uia"></a>Elementos DataTemplate do WPF agora são visíveis à UIA

#### <a name="details"></a>Detalhes

Anteriormente, os elementos <xref:System.Windows.DataTemplate?displayProperty=fullName> eram invisíveis à Automação da Interface do Usuário. A partir da versão 4.5, a Automação da Interface do Usuário detectar esses elementos. Isso é útil em muitos casos, mas pode arruinar os testes que dependem das árvores UIA que não contêm elementos <xref:System.Windows.DataTemplate?displayProperty=fullName>.

#### <a name="suggestion"></a>Sugestão

Os testes de Automação da Interface do Usuário para esse aplicativo talvez precisem ser atualizados para contabilizar a árvore UIA agora, incluindo elementos <xref:System.Windows.DataTemplate?displayProperty=fullName> anteriormente invisíveis. Por exemplo, os testes que esperam que alguns elementos fiquem próximos uns dos outros agora podem precisar esperar elementos UIA anteriormente invisíveis entre eles. Ou os testes que dependem de determinadas contagens ou de índices para elementos UIA talvez precisem ser atualizados com novos valores.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Microsoft Edge|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.DataTemplate.%23ctor>
- <xref:System.Windows.DataTemplate.%23ctor(System.Object)>

<!--

#### Affected APIs

- `M:System.Windows.DataTemplate.#ctor`
- `M:System.Windows.DataTemplate.#ctor(System.Object)`

-->
