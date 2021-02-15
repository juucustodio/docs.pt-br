---
description: 'Saiba mais sobre: Método MemoryStream. InternalGetOriginAndLength'
title: Método MemoryStream. InternalGetOriginAndLength (System.IO)
ms.date: 11/19/2019
topic_type:
- apiref
api_name:
- System.IO.MemoryStream.InternalGetOriginAndLength
api_location:
- mscorlib.dll
api_type:
- Assembly
ms.openlocfilehash: 4232852c0835a43454f36271a43062e1240297a5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802535"
---
# <a name="memorystreaminternalgetoriginandlength-method"></a>Método MemoryStream.InternalGetOriginAndLength

Obtém os valores internos de origem e o comprimento do fluxo de memória.

```csharp
internal void InternalGetOriginAndLength(out int origin, out int length)
```

## <a name="parameters"></a>Parâmetros

- `origin` <xref:System.Int32>\
  Quando esse método retorna, o deslocamento da matriz de bytes especificado ao criar um novo <xref:System.IO.MemoryStream> objeto. Contém 0 se a matriz de bytes foi criada pelo <xref:System.IO.MemoryStream> .

- `length` <xref:System.Int32>\
  Quando esse método retorna, o número de bytes dentro do fluxo de memória.

## <a name="remarks"></a>Comentários

> [!WARNING]
> O `MemoryStream.InternalGetOriginAndLength` método é interno e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.IO>

**Assembly:** mscorlib.dll (em mscorlib.dll)

**.NET Framework versões:** Disponível desde 2,0.
