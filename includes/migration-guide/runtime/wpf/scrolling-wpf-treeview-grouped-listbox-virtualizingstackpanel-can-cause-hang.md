---
ms.openlocfilehash: 31ada197db36be192317e32a37a353d375d9cc65
ms.sourcegitcommit: cbacb5d2cebbf044547f6af6e74a9de866800985
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/05/2020
ms.locfileid: "89496506"
---
### <a name="scrolling-a-wpf-treeview-or-grouped-listbox-in-a-virtualizingstackpanel-can-cause-a-hang"></a>Rolar em uma TreeView ou ListBox agrupada no WPF em um VirtualizingStackPanel pode causar travamento

#### <a name="details"></a>Detalhes

No .NET Framework v4.5, rolar em uma <xref:System.Windows.Controls.TreeView?displayProperty=fullName> do WPF em um painel de pilha virtualizado poderá causar travamentos se houver margens no visor (entre os itens na <xref:System.Windows.Controls.TreeView?displayProperty=fullName>, por exemplo, ou em um elemento ItemsPresenter). Além disso, em alguns casos, itens de tamanhos diferentes no modo de exibição podem causar instabilidade, mesmo se não houver margens.

#### <a name="suggestion"></a>Sugestão

Esse bug pode ser evitado com a o upgrade para o .NET Framework 4.5.1. Como alternativa, as margens poderão ser removidas das coleções de exibições (como <xref:System.Windows.Controls.TreeView?displayProperty=fullName>s) em painéis de pilha virtualizados se todos os itens contidos forem do mesmo tamanho.

| Nome    | Valor       |
|:--------|:------------|
| Escopo   |Principal|
|Versão|4.5|
|Tipo|Runtime|

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.Controls.VirtualizingStackPanel.SetIsVirtualizing(System.Windows.DependencyObject,System.Boolean)?displayProperty=nameWithType>

<!--

#### Affected APIs

- `M:System.Windows.Controls.VirtualizingStackPanel.SetIsVirtualizing(System.Windows.DependencyObject,System.Boolean)`

-->
