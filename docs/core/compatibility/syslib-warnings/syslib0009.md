---
title: Aviso de SYSLIB0009
description: Saiba mais sobre o obsoletions que gera SYSLIB0009 de aviso de tempo de compilação.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 922fcc30b2b1577976e4e88e3f7631e19d4b2cce
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596438"
---
# <a name="syslib0009-the-authenticationmanager-authenticate-and-preauthenticate-methods-are-not-supported"></a>SYSLIB0009: não há suporte para os métodos de autenticação e de autenticidade do CustomTargetNameDictionary

As seguintes APIs estão marcadas como obsoletas, a partir do .NET 5,0. O uso dessas APIs gera aviso `SYSLIB0009` no momento da compilação.

- <xref:System.Net.AuthenticationManager.Authenticate%2A?displayProperty=nameWithType>
- <xref:System.Net.AuthenticationManager.PreAuthenticate%2A?displayProperty=nameWithType>

## <a name="suppress-the-warning"></a>Suprimir o aviso

Se você não puder alterar seu código, poderá suprimir o aviso por meio de uma `#pragma` diretiva ou `<NoWarn>` configuração de projeto. Para obter exemplos, consulte [suprimir avisos](../syslib-obsoletions.md#suppress-warnings).
