---
title: 'Alteração significativa: Socket. LocalEndPoint é atualizado após chamar SendToAsync'
description: Saiba mais sobre a alteração significativa no .NET 5,0 em que o SendToAsync agora atualiza o valor da propriedade ponto de extremidade local para o endereço local do soquete.
ms.date: 10/18/2020
ms.openlocfilehash: 53d7da350eac6e65832012331044427fd90fe796
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760359"
---
# <a name="socketlocalendpoint-is-updated-after-calling-sendtoasync"></a>Socket. LocalEndPoint é atualizado após chamar SendToAsync

<xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)?displayProperty=nameWithType> Agora atualiza o valor da <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> propriedade para o endereço local do soquete.

## <a name="version-introduced"></a>Versão introduzida

5.0

## <a name="change-description"></a>Descrição das alterações

Nas versões anteriores do .NET, <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)?displayProperty=nameWithType> o não altera o valor da <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> Propriedade na instância de soquete. A partir do .NET 5,0, quando é <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)> concluído com êxito, o valor de <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> é o endereço local do soquete implicitamente ligado. Esse novo comportamento é consistente com o comportamento de <xref:System.Net.Sockets.Socket.SendTo(System.Byte[],System.Net.EndPoint)> e <xref:System.Net.Sockets.Socket.BeginSendTo(System.Byte[],System.Int32,System.Int32,System.Net.Sockets.SocketFlags,System.Net.EndPoint,System.AsyncCallback,System.Object)> / <xref:System.Net.Sockets.Socket.EndSendTo(System.IAsyncResult)> .

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração [corrige um bug](https://github.com/dotnet/runtime/issues/915) e torna o comportamento consistente entre `SendTo` variantes.

## <a name="recommended-action"></a>Ação recomendada

Altere qualquer código que assuma que <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)> não alterará o valor de <xref:System.Net.Sockets.Socket.LocalEndPoint?displayProperty=nameWithType> .

## <a name="affected-apis"></a>APIs afetadas

- <xref:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)?displayProperty=fullName>

<!--

### Affected APIs

- `M:System.Net.Sockets.Socket.SendToAsync(System.Net.Sockets.SocketAsyncEventArgs)`

### Category

Networking

-->
