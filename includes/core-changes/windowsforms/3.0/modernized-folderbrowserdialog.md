---
ms.openlocfilehash: 27c6353f8f71254a505b434921f4b1e61e64cdda
ms.sourcegitcommit: 2b878d7011306b215dbf3d5dc9c1e78355a6dcd5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2021
ms.locfileid: "98758143"
---
### <a name="modernization-of-the-folderbrowserdialog"></a>Modernização do FolderBrowserDialog

O <xref:System.Windows.Forms.FolderBrowserDialog> controle foi alterado em aplicativos Windows Forms para .NET Core.

#### <a name="change-description"></a>Descrição das alterações

Na .NET Framework, o Windows Forms usa a caixa de diálogo a seguir para o <xref:System.Windows.Forms.FolderBrowserDialog> controle:

![O FolderBrowserDialogControl no .NET Framework](~/docs/images/core-changes/windowsforms/modernized-folderbrowserdialog/folderdlg-framework.png)

No .NET Core 3,0, Windows Forms usa um controle baseado em COM mais recente que foi introduzido no Windows Vista:

![O FolderBrowserDialogControl no .NET Core](~/docs/images/core-changes/windowsforms/modernized-folderbrowserdialog/folderdlg-core.png)

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="recommended-action"></a>Ação recomendada

A caixa de diálogo será atualizada automaticamente.

Se você quiser manter a caixa de diálogo original, defina a <xref:System.Windows.Forms.FolderBrowserDialog.AutoUpgradeEnabled?displayProperty=nameWithType> propriedade como `false` antes de mostrar a caixa de diálogo, conforme ilustrado pelo fragmento de código a seguir:

```csharp
var dialog = new FolderBrowserDialog();
dialog.AutoUpgradeEnabled = false;
dialog.ShowDialog();
```

#### <a name="category"></a>Categoria

Windows Forms

#### <a name="affected-apis"></a>APIs afetadas

- <xref:System.Windows.Forms.FolderBrowserDialog>

<!--

#### Affected APIs

- `T:System.Windows.Forms.FolderBrowserDialog`

-->
