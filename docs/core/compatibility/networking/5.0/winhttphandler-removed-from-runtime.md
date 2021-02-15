---
title: 'Alteração significativa: WinHttpHandler removido do tempo de execução do .NET'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que o WinHttpHandler foi removido do tempo de execução do .NET.
ms.date: 10/18/2020
ms.openlocfilehash: f8b9910ade8d459133791a23704d624a91cc5dff
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760355"
---
# <a name="winhttphandler-removed-from-net-runtime"></a>WinHttpHandler removido do tempo de execução do .NET

A `WinHttpHandler` classe foi removida do assembly *System.Net.Http.dll* . Agora, ele está disponível apenas como um [pacote NuGet](https://www.nuget.org/packages/System.Net.Http.WinHttpHandler/)fora de banda (OOB).

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, a <xref:System.Net.Http.WinHttpHandler> classe está disponível como parte das principais bibliotecas do .net. A partir do .NET 5,0, a <xref:System.Net.Http.WinHttpHandler> classe só está disponível como um [pacote NuGet](https://www.nuget.org/packages/System.Net.Http.WinHttpHandler/)instalado separadamente.

## <a name="recommended-action"></a>Ação recomendada

Instale o [pacote NuGet System .net. http. WinHttpHandler](https://www.nuget.org/packages/System.Net.Http.WinHttpHandler/). Ou, se você não precisar de recursos específicos do WinHTTP, use <xref:System.Net.Http.SocketsHttpHandler> em vez disso.

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Net.Http.WinHttpHandler?displayProperty=fullName>

<!--

### Affected APIs

- `T:System.Net.Http.WinHttpHandler`

### Category

Networking

-->
