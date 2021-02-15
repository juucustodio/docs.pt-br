---
title: Método FindHeaderByColumn (System. Windows. Controls. GridViewHeaderRowPresenter)
description: Saiba mais sobre o método WPF privado chamado FindHeaderByColumn.
ms.date: 09/25/2020
ms.technology: dotnet-wpf
topic_type:
- apiref
api_name:
- System.Windows.Controls.GridViewHeaderRowPresenter.FindHeaderByColumn
api_location:
- PresentationFramework.dll
api_type:
- Assembly
ms.openlocfilehash: 88ed2928f86602d1078488354de6d5267c0311f5
ms.sourcegitcommit: eb7e87496f42361b1da98562dd75b516c9d58bbc
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/09/2020
ms.locfileid: "91877739"
---
# <a name="findheaderbycolumn-method"></a>Método FindHeaderByColumn

Localiza o cabeçalho de coluna da coluna especificada na árvore visual.

```csharp
private GridViewColumnHeader FindHeaderByColumn(GridViewColumn column)
```

> [!WARNING]
> Esse método é privado e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="parameters"></a>Parâmetros

`column` <xref:System.Windows.Controls.GridViewColumn>\
A coluna cujo cabeçalho deve ser encontrado e retornado.

## <a name="return-value"></a>Valor retornado

<xref:System.Windows.Controls.GridViewColumnHeader>\
O cabeçalho da coluna especificada ou `null` se a coluna especificada não existir.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Windows.Controls>

**Assembly:** PresentationFramework.dll

## <a name="see-also"></a>Confira também

- <xref:System.Windows.Controls.GridViewHeaderRowPresenter>
