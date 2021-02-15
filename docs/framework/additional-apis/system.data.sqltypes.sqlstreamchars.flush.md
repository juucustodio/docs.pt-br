---
description: 'Saiba mais sobre: método SqlStreamChars. Flush'
title: Método SqlStreamChars. Flush (System. Data. SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/20/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.Flush
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: 8f519ffb8248a17608319eb0fbfe598f9ee3487a
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99684458"
---
# <a name="sqlstreamcharsflush-method"></a>Método SqlStreamChars. Flush

Quando é substituído em uma classe derivada, limpa todos os buffers nesse fluxo e faz com que todos os dados armazenados em buffer sejam gravados no dispositivo subjacente. O assembly que contém esse método tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

## <a name="syntax"></a>Sintaxe

```csharp
public abstract void Flush ();
```

## <a name="remarks"></a>Comentários

> [!WARNING]
> O `SqlStreamChars.Flush` método é privado e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Data.SqlTypes>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
