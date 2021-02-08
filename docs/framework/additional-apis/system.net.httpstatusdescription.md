---
description: 'Saiba mais sobre: classe HttpStatusDescription'
title: Classe HttpStatusDescription (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.HttpStatusDescription
- System.Net.HttpStatusDescription.Get
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: fa135a6421397ce6b7be2af05d66aa8e81beafb7
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802496"
---
# <a name="httpstatusdescription-class"></a>Classe HttpStatusDescription

Fornece descrições de status HTTP padrão. Essa classe não pode ser herdada.

```csharp
internal static class HttpStatusDescription
```

> [!WARNING]
> Essa classe é interna e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa classe em um aplicativo de produção em nenhuma circunstância.

## <a name="get-method"></a>método Get

Retorna a descrição associada ao código de status HTTP especificado.

```csharp
internal static string Get(int code)
```

### <a name="parameters"></a>Parâmetros

`code` <xref:System.Int32>

O código de status HTTP, por exemplo, `404` .

### <a name="return-value"></a>Valor retornado

<xref:System.String?displayProperty=nameWithType>

A descrição do status HTTP.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Net>

**Assembly:** Sistema (em System.dll)
