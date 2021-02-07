---
description: 'Saiba mais sobre: Propriedade PooledStream. NetworkStream'
title: Propriedade PooledStream. NetworkStream (System.Net)
ms.date: 10/21/2019
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.PooledStream.NetworkStream
- System.Net.PooledStream.get_NetworkStream
- System.Net.PooledStream.set_NetworkStream
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 8a4f1d6bd9297028e763ef73bf96f85cbbfdafd6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699630"
---
# <a name="pooledstreamnetworkstream-property"></a>Propriedade PooledStream. NetworkStream

Obtém ou define o fluxo de rede para o `PooledStream` soquete.

## <a name="syntax"></a>Syntax

```csharp
internal NetworkStream NetworkStream { get; set; }
```

## <a name="property-value"></a>Valor da propriedade

<xref:System.Net.Sockets.NetworkStream>  
O fluxo de rede para o `PooledStream` soquete.

## <a name="remarks"></a>Comentários

> [!WARNING]
> A `PooledStream.NetworkStream` propriedade é interna e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa propriedade em um aplicativo de produção em nenhuma circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Net>

**Assembly:** Sistema (em System.dll)

**.NET Framework versões:** Disponível desde 2,0.
