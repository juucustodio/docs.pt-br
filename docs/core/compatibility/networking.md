---
title: Alterações interruptivas relacionadas à rede
description: Lista as alterações interruptivas relacionadas à rede no .NET Core 2.0 e 3.0.
ms.date: 05/05/2020
ms.openlocfilehash: 761c6481888bcb8e91f7b4212355aca067632495
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95689206"
---
# <a name="networking-breaking-changes-in-net-core-20-and-30"></a>Alterações interruptivas relacionadas à rede no .NET Core 2.0 e 3.0

As seguintes alterações interruptivas estão documentadas nesta página:

| Alteração interruptiva | Versão introduzida |
| - | - |
| [Valor padrão de HttpRequestMessage. Version alterado para 1,1](#default-value-of-httprequestmessageversion-changed-to-11) | 3.0 |
| [WebClient. CancelAsync nem sempre cancela imediatamente](#webclientcancelasync-doesnt-always-cancel-immediately) | 2,0 |

## <a name="net-core-30"></a>.NET Core 3.0

[!INCLUDE[Default value of HttpRequestMessage.Version changed to 1.1](~/includes/core-changes/networking/3.0/httprequestmessage-version-change.md)]

***

## <a name="net-core-20"></a>.NET Core 2.0

[!INCLUDE [behavior-change-webclient-cancelasync](../../../includes/core-changes/networking/2.0/behavior-change-webclient-cancelasync.md)]

***
