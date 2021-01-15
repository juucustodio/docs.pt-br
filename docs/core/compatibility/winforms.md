---
title: Alterações interruptivas do Windows Forms
description: Lista as alterações interruptivas no Windows Forms para o .NET Core 3.0 e 3.1.
ms.date: 09/08/2020
ms.openlocfilehash: b944f7eea89b61f41feb8eef99e949c2d6017960
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95726425"
---
# <a name="breaking-changes-in-windows-forms-for-net-core-30-and-31"></a>Alterações interruptivas no Windows Forms para o .NET Core 3.0 e 3.1

Windows Forms suporte foi adicionado ao .NET Core na versão 3,0. Este artigo lista as alterações interruptivas para Windows Forms segundo versão do .NET na qual elas foram introduzidas. Se você estiver atualizando um aplicativo Windows Forms de .NET Framework ou de uma versão anterior do .NET Core (3,0 ou posterior), este artigo se aplicará a você.

As seguintes alterações interruptivas estão documentadas nesta página:

| Alteração interruptiva | Versão introduzida |
| - | :-: |
| [Controles removidos](#removed-controls) | 3.1 |
| [Evento CellFormatting não gerado se ToolTip for mostrado](#cellformatting-event-not-raised-if-tooltip-is-shown) | 3.1 |
| [Control. DefaultFont alterado para Segoe UI 9 pt](#default-control-font-changed-to-segoe-ui-9-pt) | 3.0 |
| [Modernização do FolderBrowserDialog](#modernization-of-the-folderbrowserdialog) | 3.0 |
| [SerializableAttribute removido de alguns tipos de Windows Forms](#serializableattribute-removed-from-some-windows-forms-types) | 3.0 |
| [Não há suporte para a opção de compatibilidade AllowUpdateChildControlIndexForTabControls](#allowupdatechildcontrolindexfortabcontrols-compatibility-switch-not-supported) | 3.0 |
| [Não há suporte para a opção de compatibilidade DomainUpDown. UseLegacyScrolling](#domainupdownuselegacyscrolling-compatibility-switch-not-supported) | 3.0 |
| [Não há suporte para a opção de compatibilidade DoNotLoadLatestRichEditControl](#donotloadlatestricheditcontrol-compatibility-switch-not-supported) | 3.0 |
| [Não há suporte para a opção de compatibilidade DoNotSupportSelectAllShortcutInMultilineTextBox](#donotsupportselectallshortcutinmultilinetextbox-compatibility-switch-not-supported) | 3.0 |
| [Não há suporte para a opção de compatibilidade DontSupportReentrantFilterMessage](#dontsupportreentrantfiltermessage-compatibility-switch-not-supported) | 3.0 |
| [Não há suporte para a opção de compatibilidade EnableVisualStyleValidation](#enablevisualstylevalidation-compatibility-switch-not-supported) | 3.0 |
| [Não há suporte para a opção de compatibilidade UseLegacyContextMenuStripSourceControlValue](#uselegacycontextmenustripsourcecontrolvalue-compatibility-switch-not-supported) | 3.0 |
| [Não há suporte para a opção de compatibilidade UseLegacyImages](#uselegacyimages-compatibility-switch-not-supported) | 3.0 |

## <a name="net-core-31"></a>.NET Core 3.1

[!INCLUDE[Removed controls](~/includes/core-changes/windowsforms/3.1/remove-controls-3.1.md)]

***

[!INCLUDE[CellFormatting event](~/includes/core-changes/windowsforms/3.1/cellformatting-event-not-raised.md)]

**_

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Control.DefaultFont changed to Segoe UI 9pt](~/includes/core-changes/windowsforms/3.0/control-defaultfont-changed.md)]

_*_

[!INCLUDE[Modernization of the FolderBrowserDialog](~/includes/core-changes/windowsforms/3.0/modernized-folderbrowserdialog.md)]

_*_

[!INCLUDE[SerializableAttribute removed from some Windows Forms types](~/includes/core-changes/windowsforms/3.0/remove-serializationattribute.md)]

_*_

[!INCLUDE[Switch.System.Windows.Forms.AllowUpdateChildControlIndexForTabControls compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-allowupdatechildcontrolindexfortabcontrols.md)]

_*_

[!INCLUDE[Switch.System.Windows.Forms.DomainUpDown.UseLegacyScrolling compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyscrolling.md)]

_*_

[!INCLUDE[Switch.System.Windows.Forms.DoNotLoadLatestRichEditControl compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotloadlatestricheditcontrol.md)]

_*_

[!INCLUDE[Switch.System.Windows.Forms.DoNotSupportSelectAllShortcutInMultilineTextBox compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-donotsupportselectallshortcutinmultilinetextbox.md)]

_*_

[!INCLUDE[Switch.System.Windows.Forms.DontSupportReentrantFilterMessage compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-dontsupportreentrantfiltermessage.md)]

_*_

[!INCLUDE[Switch.System.Windows.Forms.EnableVisualStyleValidation compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-enablevisualstylevalidation.md)]

_*_

[!INCLUDE[Switch.System.Windows.Forms.UseLegacyContextMenuStripSourceControlValue compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacycontextmenustripsourcecontrolvalue.md)]

_*_

[!INCLUDE[Switch.System.Windows.Forms.UseLegacyImages compatibility switch not supported](~/includes/core-changes/windowsforms/3.0/deprecate-uselegacyimages.md)]

_**

## <a name="see-also"></a>Confira também

- [Porta um aplicativo de Windows Forms para o .NET Core](/dotnet/desktop/winforms/migration/?view=netdesktop-5.0&preserve-view=true)
