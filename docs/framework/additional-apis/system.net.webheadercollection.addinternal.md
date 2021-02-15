---
description: 'Saiba mais sobre: método webcabeçalhocollection. addinterna'
title: Método webcabeçalhocollection. addinterna (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.WebHeaderCollection.AddInternal
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 7bc84f84e6656dba5230b627fe9decfc4e0b4746
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699474"
---
# <a name="webheadercollectionaddinternal-method"></a>Método webcabeçalhocollection. addinterna

Adiciona um novo cabeçalho com o nome e o valor especificados à coleção, ignorando as verificações.

```csharp
internal void AddInternal(string name, string value)
```

> [!WARNING]
> Esse método é interno e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="parameters"></a>Parâmetros

- `name` <xref:System.String>

  O nome do cabeçalho.

- `value` <xref:System.String>

  O valor do cabeçalho.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Net>

**Assembly:** Sistema (em System.dll)
