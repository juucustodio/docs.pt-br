---
description: 'Saiba mais sobre: classe ComNetOS'
title: Classe ComNetOS (System.Net)
ms.date: 06/12/2020
ms.technology: dotnet-networking
topic_type:
- apiref
api_name:
- System.Net.ComNetOS
- System.Net.ComNetOS.IsWin7orLater
api_location:
- System.dll
api_type:
- Assembly
ms.openlocfilehash: 7376fe4a5e02818907cb71573451fffb3a3667cb
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99802522"
---
# <a name="comnetos-class"></a>Classe ComNetOS

Fornece informações sobre o sistema operacional atual, como sua versão e o tipo de instalação (cliente ou servidor). Essa classe não pode ser herdada.
  
```csharp  
internal static class ComNetOS
```

> [!WARNING]
> Essa classe é interna e não deve ser usada diretamente no seu código.
>
> A Microsoft não oferece suporte ao uso dessa classe em um aplicativo de produção em nenhuma circunstância.

## <a name="iswin7orlater-field"></a>Campo IsWin7orLater

Especifica se a versão do sistema operacional é o Windows 7 ou posterior.

```csharp
internal static readonly bool IsWin7orLater
```

## <a name="requirements"></a>Requisitos

**Namespace:** <xref:System.Net>

**Assembly:** Sistema (em System.dll)
