---
description: 'Saiba mais sobre: Propriedade SqlStreamChars. CanSeek'
title: Propriedade SqlStreamChars. CanSeek (System. Data. SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/19/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.CanSeek
- System.Data.SqlTypes.SqlStreamChars.get_CanSeek
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: 5919a66bef9ac31e0ef15ad4af64b456700605f7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802613"
---
# <a name="sqlstreamcharscanseek-property"></a>Propriedade SqlStreamChars. CanSeek

Quando substituído em uma classe derivada, obtém um valor que indica se o fluxo atual dá suporte à operação de busca. O assembly que contém essa propriedade tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

```csharp
public abstract bool CanSeek { get; }
```

## <a name="property-value"></a>Valor da propriedade

<xref:System.Boolean>\
`true` Se o fluxo atual der suporte à operação de busca; caso contrário, `false` .

## <a name="remarks"></a>Comentários

> [!WARNING]
> A `SqlStreamChars.CanSeek` propriedade é privada e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa propriedade em um aplicativo de produção em nenhuma circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Data.SqlTypes>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
