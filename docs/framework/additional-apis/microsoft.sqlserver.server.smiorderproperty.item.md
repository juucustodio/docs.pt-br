---
description: 'Saiba mais sobre a propriedade: SmiOrderProperty. Item'
title: Propriedade SmiOrderProperty. Item (Microsoft. SqlServer. Server)
author: stevestein
ms.author: sstein
ms.date: 12/20/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- Microsoft.SqlServer.Server.SmiOrderProperty.Item
- Microsoft.SqlServer.Server.SmiOrderProperty.get_Item
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: fc2151d3f36a6746e80e2fd6d611a803b2c3162e
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99767980"
---
# <a name="smiorderpropertyitem-property"></a>Propriedade SmiOrderProperty. Item

Obtém a ordem da coluna para a entidade. O assembly que contém essa propriedade tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

## <a name="syntax"></a>Syntax

```csharp
internal SmiColumnOrder Item { get; }
```

## <a name="property-value"></a>Valor da propriedade

A ordem das colunas.

## <a name="remarks"></a>Comentários

> [!WARNING]
> A `SmiOrderProperty.Item` propriedade é interna e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa propriedade em um aplicativo de produção em nenhuma circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:Microsoft.SqlServer.Server>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
