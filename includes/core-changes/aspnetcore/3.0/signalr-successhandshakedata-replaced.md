---
ms.openlocfilehash: 05aec429e28ef74515ef6988d5b064e6d16b7c1b
ms.sourcegitcommit: 0802ac583585110022beb6af8ea0b39188b77c43
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96032312"
---
### <a name="signalr-handshakeprotocolsuccesshandshakedata-replaced"></a>Signalr: HandshakeProtocol. SuccessHandshakeData substituído

O campo [HandshakeProtocol. SuccessHandshakeData](https://github.com/dotnet/aspnetcore/blob/c5b2bc0df2a0027832bf7d01dfb19ca39cd08ae6/src/SignalR/common/SignalR.Common/src/Protocol/HandshakeProtocol.cs#L27) foi removido e substituído por um método auxiliar que gera uma resposta de handshake com êxito, dada uma específica `IHubProtocol` .

#### <a name="version-introduced"></a>Versão introduzida

3.0

#### <a name="old-behavior"></a>Comportamento antigo

`HandshakeProtocol.SuccessHandshakeData` era um `public static ReadOnlyMemory<byte>` campo.

#### <a name="new-behavior"></a>Novo comportamento

`HandshakeProtocol.SuccessHandshakeData` foi substituído por um `static` `GetSuccessfulHandshake(IHubProtocol protocol)` método que retorna um `ReadOnlyMemory<byte>` com base no protocolo especificado.

#### <a name="reason-for-change"></a>Motivo da alteração

Campos adicionais foram adicionados à _resposta_ de handshake que são não constantes e mudam dependendo do protocolo selecionado.

#### <a name="recommended-action"></a>Ação recomendada

nenhuma. Esse tipo não é projetado para uso do código do usuário. É `public` , portanto, pode ser compartilhado entre o servidor e o cliente do signalr. Ele também pode ser usado por clientes do Signalr do cliente escritos em .NET. **Os usuários** do signalr não devem ser afetados por essa alteração.

#### <a name="category"></a>Categoria

ASP.NET Core

#### <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.SignalR.Protocol.HandshakeProtocol.SuccessHandshakeData?displayProperty=nameWithType>

<!--

#### Affected APIs

`F:Microsoft.AspNetCore.SignalR.Protocol.HandshakeProtocol.SuccessHandshakeData`

-->
