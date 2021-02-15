---
description: 'Saiba mais sobre o método: SqlStreamChars. Close'
title: Método SqlStreamChars. Close (System. Data. SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/20/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.Close
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: 27f2ea6e288d166f3b63979a83a1cf80eeced334
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99782371"
---
# <a name="sqlstreamcharsclose-method"></a>Método SqlStreamChars. Close

Fecha o fluxo atual e libera todos os recursos do sistema associados ao fluxo. O assembly que contém esse método tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

```csharp
public virtual void Close ();
```

## <a name="remarks"></a>Comentários

> [!WARNING]
> O `SqlStreamChars.Close` método é privado e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Data.SqlTypes>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
