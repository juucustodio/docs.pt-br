---
description: 'Saiba mais sobre: Propriedade SqlChars. Stream'
title: Propriedade SqlChars. Stream (System. Data. SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/19/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlChars.Stream
- System.Data.SqlTypes.SqlChars.get_Stream
- System.Data.SqlTypes.SqlChars.set_Stream
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: 9af0df98b268a749d890ab1b40dddbbe98ced8d9
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802639"
---
# <a name="sqlcharsstream-property"></a>Propriedade SqlChars.Stream

Obtém ou define o fluxo de caracteres. O assembly que contém essa propriedade tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

```csharp
internal SqlStreamChars Stream { get; set; }
```

## <a name="property-value"></a>Valor da propriedade

`System.Data.SqlTypes.SqlStreamChars`\
O fluxo de caracteres.

## <a name="remarks"></a>Comentários

> [!WARNING]
> A `SqlChars.Stream` propriedade é interna e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa propriedade em um aplicativo de produção em nenhuma circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Data.SqlTypes>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
