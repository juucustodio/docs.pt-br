---
title: 'Alteração significativa: controles da barra de status removidos'
description: Saiba mais sobre a alteração significativa no .NET 5,0, em que alguns controles de Windows Forms não estão mais disponíveis.
ms.date: 07/18/2020
ms.openlocfilehash: 70aaa20f3fee1f4c342c4d9e547b0658aaf533b1
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760490"
---
# <a name="removed-status-bar-controls"></a>Controles da barra de status removidos

A partir do .NET 5,0, alguns controles Windows Forms não estão mais disponíveis.

## <a name="change-description"></a>Descrição das alterações

A partir do .NET 5,0, alguns dos controles de Windows Forms relacionados à barra de status não estão mais disponíveis. Os controles de substituição com design e suporte melhores foram introduzidos no .NET Framework 2,0. Os controles preteridos foram removidos anteriormente das caixas de ferramentas do designer, mas ainda estavam disponíveis para serem usados. Agora, eles foram completamente removidos.

Os seguintes tipos não estão mais disponíveis:

* `StatusBar`
* `StatusBarDrawItemEventArgs`
* `StatusBarDrawItemEventHandler`
* `StatusBarPanel`
* `StatusBarPanelAutoSize`
* `StatusBarPanelBorderStyle`
* `StatusBarPanelClickEventArgs`
* `StatusBarPanelClickEventHandler`
* `StatusBarPanelStyle`

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="recommended-action"></a>Ação recomendada

Vá para as APIs de substituição para esses controles e seus cenários:

| Controle antigo (API) | Substituição recomendada                          |
|-------------------|--------------------------------------------------|
| StatusBar         | <xref:System.Windows.Forms.StatusStrip>          |
| StatusBarPanel    | <xref:System.Windows.Forms.ToolStripStatusLabel> |

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.Forms.StatusBar?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarDrawItemEventArgs?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarDrawItemEventHandler?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanel?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelAutoSize?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelBorderStyle?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelClickEventArgs?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelClickEventHandler?displayProperty=fullName>
- <xref:System.Windows.Forms.StatusBarPanelStyle?displayProperty=fullName>

<!--

### Affected APIs

- `T:System.Windows.Forms.StatusBar`
- `T:System.Windows.Forms.StatusBarDrawItemEventArgs`
- `T:System.Windows.Forms.StatusBarDrawItemEventHandler`
- `T:System.Windows.Forms.StatusBarPanel`
- `T:System.Windows.Forms.StatusBarPanelAutoSize`
- `T:System.Windows.Forms.StatusBarPanelBorderStyle`
- `T:System.Windows.Forms.StatusBarPanelClickEventArgs`
- `T:System.Windows.Forms.StatusBarPanelClickEventHandler`
- `T:System.Windows.Forms.StatusBarPanelStyle`

### Category

Windows Forms

-->
