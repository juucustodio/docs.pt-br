---
title: Aviso de SYSLIB0010
description: Saiba mais sobre o obsoletions que gera SYSLIB0010 de aviso de tempo de compilação.
ms.topic: reference
ms.date: 10/20/2020
ms.openlocfilehash: 289fb3f766a6e1d37bea8faec1896d20442f43f9
ms.sourcegitcommit: e301979e3049ce412d19b094c60ed95b316a8f8c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/16/2020
ms.locfileid: "97596428"
---
# <a name="syslib0010-unsupported-remoting-apis"></a>SYSLIB0010: APIs de comunicação remota sem suporte

A [comunicação remota do .net](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71)) é uma tecnologia herdada, e a infraestrutura existe somente no .NET Framework. As seguintes APIs relacionadas a comunicação remota são marcadas como obsoletas, a partir do .NET 5,0. Usá-los no código gera aviso `SYSLIB0010` no momento da compilação.

- <xref:System.MarshalByRefObject.GetLifetimeService?displayProperty=nameWithType>
- <xref:System.MarshalByRefObject.InitializeLifetimeService?displayProperty=nameWithType>

## <a name="workarounds"></a>Soluções Alternativas

Considere usar o WCF ou serviços REST baseados em HTTP para se comunicar com objetos em outros aplicativos ou entre computadores. Para obter mais informações, consulte [.NET Framework Technologies indisponíveis no .NET Core](../../porting/net-framework-tech-unavailable.md).

[!INCLUDE [suppress-syslib-warning](../../../../includes/suppress-syslib-warning.md)]

## <a name="see-also"></a>Confira também

- [Comunicação remota do .NET](/previous-versions/dotnet/netframework-1.1/kwdt6w2k(v=vs.71))
