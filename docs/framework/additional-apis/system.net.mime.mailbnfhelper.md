---
description: 'Saiba mais sobre: classe MailBnfHelper'
title: Classe MailBnfHelper (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.Mime.MailBnfHelper
- System.Net.Mime.MailBnfHelper.Ascii7bitMaxValue
- System.Net.Mime.MailBnfHelper.Atext
- System.Net.Mime.MailBnfHelper.CR
- System.Net.Mime.MailBnfHelper.Ctext
- System.Net.Mime.MailBnfHelper.Dot
- System.Net.Mime.MailBnfHelper.EndComment
- System.Net.Mime.MailBnfHelper.LF
- System.Net.Mime.MailBnfHelper.Space
- System.Net.Mime.MailBnfHelper.StartComment
- System.Net.Mime.MailBnfHelper.Tab
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 942b5c423d2f63985a8f7840f69d956bbade7582
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99699643"
---
# <a name="mailbnfhelper-class"></a>Classe MailBnfHelper

Contém métodos de utilitário para análise de cadeias de caracteres formatadas por mensagem da Internet. Essa classe não pode ser herdada.

```csharp
internal static class MailBnfHelper
```

> [!WARNING]
> Essa classe é interna e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa classe em um aplicativo de produção em nenhuma circunstância.

## <a name="ascii7bitmaxvalue-field"></a>Campo Ascii7bitMaxValue

Representa o valor ASCII máximo de 7 bits.

```csharp
internal static readonly int Ascii7bitMaxValue
```

## <a name="atext-field"></a>Campo Atext

Representa os caracteres permitidos em Atoms.

```csharp
internal static bool[] Atext
```

## <a name="cr-field"></a>Campo CR

Representa o caractere de retorno de carro.

```csharp
internal static readonly char CR
```

## <a name="ctext-field"></a>Campo CTEXT

Representa os caracteres permitidos dentro de comentários.

```csharp
internal static bool[] Ctext
```

## <a name="dot-field"></a>Campo de ponto

Representa o caractere de parada completa ( `.` ).

```csharp
internal static readonly char Dot
```

## <a name="endcomment-field"></a>Campo endcomment

Representa o caractere que especifica o final de um comentário.

```csharp
internal static readonly char EndComment
```

## <a name="lf-field"></a>Campo LF

Representa o caractere de alimentação de linha.

```csharp
internal static readonly char LF
```

## <a name="space-field"></a>Campo de espaço

Representa o caractere de espaço.

```csharp
internal static readonly char Space
```

## <a name="startcomment-field"></a>Campo StartComment

Representa o caractere que especifica o início de um comentário.

```csharp
internal static readonly char StartComment
```

## <a name="tab-field"></a>Campo de guia

Representa o caractere de tabulação.

```csharp
internal static readonly char Tab
```

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Net>

**Assembly:** Sistema (em System.dll)
