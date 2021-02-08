---
description: 'Saiba mais sobre a propriedade: SqlStreamChars. Length'
title: Propriedade SqlStreamChars. Length (System. Data. SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/19/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.Length
- System.Data.SqlTypes.SqlStreamChars.get_Length
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: b0a9686cadc6d4018c7f291f0326b71195fd5cf5
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802587"
---
# <a name="sqlstreamcharslength-property"></a>Propriedade SqlStreamChars. Length

Quando substituído em uma classe derivada, obtém o comprimento do fluxo atual. O assembly que contém essa propriedade tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

## <a name="syntax"></a>Syntax

```csharp
public abstract long Length { get; }
```

## <a name="property-value"></a>Valor da propriedade

<xref:System.Int64>\
O comprimento do fluxo.

## <a name="remarks"></a>Comentários

> [!WARNING]
> A `SqlStreamChars.Length` propriedade é privada e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa propriedade em um aplicativo de produção em nenhuma circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Data.SqlTypes>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
