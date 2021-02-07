---
description: 'Saiba mais sobre: Propriedade SslState. SslProtocol'
title: Propriedade SslState. SslProtocol (System .net. Security)
ms.date: 10/21/2019
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Security.SslState.SslProtocol
- System.Net.Security.SslState.get_SslProtocol
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: b0b9bebf23fcd8d643d06f1cff10c260c77a7c08
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699617"
---
# <a name="sslstatesslprotocol-property"></a>Propriedade SslState. SslProtocol

Obtém as versões do protocolo SSL.

## <a name="syntax"></a>Syntax

```csharp
internal SslProtocols SslProtocol { get; }
```

## <a name="property-value"></a>Valor da propriedade

<xref:System.Security.Authentication.SslProtocols>  
Uma combinação de bits de bit que especifica as versões de protocolo SSL.

## <a name="remarks"></a>Comentários

> [!WARNING]
> A `SslState.SslProtocol` propriedade é interna e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa propriedade em um aplicativo de produção em nenhuma circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Net.Security>

**Assembly:** Sistema (em System.dll)

**.NET Framework versões:** Disponível desde 2,0.
