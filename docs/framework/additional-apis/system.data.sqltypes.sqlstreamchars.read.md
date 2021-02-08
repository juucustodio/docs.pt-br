---
description: 'Saiba mais sobre: método SqlStreamChars. Read (Char [], Int32, Int32)'
title: Método SqlStreamChars. Read (Char [], Int32, Int32) (System. Data. SqlTypes)
author: stevestein
ms.author: sstein
ms.date: 12/20/2018
ms.technology: dotnet-data
topic_type:
- apiref
api_name:
- System.Data.SqlTypes.SqlStreamChars.Read
api_location:
- System.Data.dll
api_type:
- Assembly
ms.openlocfilehash: a899ddff7b7242fcc32aaf7b7f7794970596027b
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802574"
---
# <a name="sqlstreamcharsreadchar-int32-int32-method"></a>Método SqlStreamChars. Read (Char [], Int32, Int32)

Quando substituído em uma classe derivada, o lê o próximo conjunto de caracteres do fluxo de entrada. O assembly que contém esse método tem uma relação Friend com SQLAccess.dll. Ele é destinado ao uso por SQL Server. Para outros bancos de dados, use o mecanismo de hospedagem fornecido por esse banco.

```csharp
public abstract int Read (char[] buffer, int offset, int count);
```

## <a name="parameters"></a>Parâmetros

`buffer`\
Uma matriz char a ser lida.

`offset`\
Um deslocamento relativo à origem.

`count`\
O número de caracteres a serem lidos do fluxo atual.

## <a name="returns"></a>Retornos

<xref:System.Int32>\
O número total de caracteres lidos no buffer.

## <a name="remarks"></a>Comentários

> [!WARNING]
> O `SqlStreamChars.Read` método é privado e não deve ser usado diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso desse método em um aplicativo de produção em qualquer circunstância.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Data.SqlTypes>

**Assembly:** System.Data (em System.Data.dll)

**.NET Framework versões:** Disponível desde 2,0.
