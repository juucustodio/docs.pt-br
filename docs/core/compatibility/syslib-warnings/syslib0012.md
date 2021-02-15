---
title: Aviso de SYSLIB0012
description: Saiba mais sobre o obsoletions que gera SYSLIB0012 de aviso de tempo de compilação.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 9b3fa94029efb2343e6dbbeb3ae36195f0956523
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596426"
---
# <a name="syslib0012-assemblycodebase-and-assemblyescapedcodebase-are-obsolete"></a>SYSLIB0012: assembly. CodeBase e assembly. EscapedCodeBase são obsoletos

As seguintes APIs são marcadas como obsoletas, a partir do .NET 5,0. Usá-los no código gera aviso `SYSLIB0012` no momento da compilação.

- <xref:System.Reflection.Assembly.CodeBase?displayProperty=nameWithType>
- <xref:System.Reflection.Assembly.EscapedCodeBase?displayProperty=nameWithType>

## <a name="workarounds"></a>Soluções Alternativas

Use <xref:System.Reflection.Assembly.Location?displayProperty=nameWithType> em seu lugar.

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]
