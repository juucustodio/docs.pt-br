---
description: 'Saiba mais sobre o método: SqlStreamChars. SetLength (Int64)'
title: Método SqlStreamChars. SetLength (Int64) (System. Data. SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/20/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.SetLength
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: d10ce55126ae09062fe895c3a686ce5d94174554
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99804134"
---
# <a name="sqlstreamcharssetlengthint64-method"></a>Método SqlStreamChars. SetLength (Int64)

Quando substituído em uma classe derivada, libera os recursos usados pelo fluxo. O assembly que contém esse método tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

```csharp
public abstract void SetLength (long value);
```

## <a name="parameters"></a>Parâmetros

`value`\
O tamanho desejado do fluxo atual em bytes.

## <a name="remarks"></a>Comentários

> [!WARNING]
> O `SqlStreamChars.SetLength` método é privado e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Data.SqlTypes>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
