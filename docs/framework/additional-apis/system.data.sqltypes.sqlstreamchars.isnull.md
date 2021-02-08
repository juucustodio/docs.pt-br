---
description: 'Saiba mais sobre a propriedade: SqlStreamChars. IsNull'
title: Propriedade SqlStreamChars. IsNull (System. Data. SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/19/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.IsNull
- System.Data.SqlTypes.SqlStreamChars.get_IsNull
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: b1408a8ba9cd1c38f73d5fa6b818f441d6223bc8
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99791914"
---
# <a name="sqlstreamcharsisnull-property"></a>Propriedade SqlStreamChars. IsNull

Quando substituído em uma classe derivada, obtém um valor que indica se o fluxo é `null` . O assembly que contém essa propriedade tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

## <a name="syntax"></a>Syntax

```csharp
public abstract bool IsNull { get; }
```

## <a name="property-value"></a>Valor da propriedade

<xref:System.Boolean>\
`true` Se o fluxo for `null` ; caso contrário, `false` .

## <a name="remarks"></a>Comentários

> [!WARNING]
> A `SqlStreamChars.IsNull` propriedade é privada e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa propriedade em um aplicativo de produção em nenhuma circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Data.SqlTypes>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
