---
title: Aviso de SYSLIB0008
description: Saiba mais sobre o obsoletion que gera SYSLIB0008 de aviso de tempo de compilação.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 2b573f4b28cdf79107395f5cb38a4226d0ccc11e
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596427"
---
# <a name="syslib0008-createpdbgenerator-is-not-supported"></a>SYSLIB0008: não há suporte para CreatePdbGenerator

A <xref:System.Runtime.CompilerServices.DebugInfoGenerator.CreatePdbGenerator?displayProperty=nameWithType> API está marcada como obsoleta, começando no .net 5,0. O uso dessa API gera aviso `SYSLIB0008` no momento da compilação.

## <a name="suppress-the-warning"></a>Suprimir o aviso

Se você não puder alterar seu código, poderá suprimir o aviso por meio de uma `#pragma` diretiva ou `<NoWarn>` configuração de projeto. Para obter exemplos, consulte [suprimir avisos](../syslib-obsoletions.md#suppress-warnings).
