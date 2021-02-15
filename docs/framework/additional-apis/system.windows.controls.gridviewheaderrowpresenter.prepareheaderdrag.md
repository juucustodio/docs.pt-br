---
title: Método PrepareHeaderDrag (System. Windows. Controls. GridViewHeaderRowPresenter)
description: Saiba mais sobre o método WPF privado chamado PrepareHeaderDrag.
ms.date: 09/25/2020
ms.technology: dotnet-wpf
topic_type:
- apiref
api_name:
- System.Windows.Controls.GridViewHeaderRowPresenter.PrepareHeaderDrag
api_location:
- PresentationFramework.dll
api_type:
- Assembly
ms.openlocfilehash: 6d806b8a50de3234cd04198f4ab86621dcd6ede1
ms.sourcegitcommit: eb7e87496f42361b1da98562dd75b516c9d58bbc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91877736"
---
# <a name="prepareheaderdrag-method"></a>Método PrepareHeaderDrag

Prepara o cabeçalho de coluna especificado para reordenação.

```csharp
private void PrepareHeaderDrag(GridViewColumnHeader header, Point pos, Point relativePos, bool cancelInvoke)
```

> [!WARNING]
> Esse método é privado e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="parameters"></a>Parâmetros

`header` <xref:System.Windows.Controls.GridViewColumnHeader>\
O cabeçalho da coluna a ser preparada para reordenação.

`pos` <xref:System.Windows.Point>\
A posição, em relação a <xref:System.Windows.Controls.GridViewHeaderRowPresenter> , onde o arrasto é iniciado.

`relativePos` <xref:System.Windows.Point>\
A posição, em relação a `header` , onde o arrasto é iniciado.

`cancelInvoke` <xref:System.Boolean>\
`true` para cancelar a reordenação; caso contrário, `false` .

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Windows.Controls>

**Assembly:** PresentationFramework.dll

## <a name="see-also"></a>Confira também

- <xref:System.Windows.Controls.GridViewHeaderRowPresenter>
