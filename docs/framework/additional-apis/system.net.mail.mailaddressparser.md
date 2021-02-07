---
description: 'Saiba mais sobre: classe MailAddressParser'
title: Classe MailAddressParser (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Mail.MailAddressParser
- System.Net.Mail.MailAddressParser.ParseAddress
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 5ad534e731e283f5449b3b8cc8e87628716da9b0
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699760"
---
# <a name="mailaddressparser-class"></a>Classe MailAddressParser

Analisa endereços de email conforme descrito em RFC 2822. Essa classe não pode ser herdada.

```csharp
internal static class MailAddressParser
```

> [!WARNING]
> Essa classe é interna e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa classe em um aplicativo de produção em nenhuma circunstância.

## <a name="parseaddress-method"></a>Método ParseAddress

Analisa um único endereço de email da cadeia de caracteres especificada.

```csharp
internal static MailAddress ParseAddress(string data)
```

### <a name="parameters"></a>Parâmetros

`data` <xref:System.String>

A cadeia de caracteres que contém um endereço de email a ser analisado.

### <a name="return-value"></a>Valor retornado

<xref:System.Net.Mail.MailAddress>

Um endereço de email válido.

### <a name="exceptions"></a>Exceções

<xref:System.FormatException?displayProperty=nameWithType>

O endereço de email é inválido.

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Net>

**Assembly:** Sistema (em System.dll)
