---
title: 'Alteração significativa: Signalr: protocolo Hub MessagePack movido para o pacote MessagePack 2. x'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core o Signaler 5,0 intitulado: protocolo Hub MessagePack movido para o pacote MessagePack 2. x'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: 1e666c40d7046233c9fb06af819b901fd1251b06
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760529"
---
# <a name="signalr-messagepack-hub-protocol-moved-to-messagepack-2x-package"></a>Signalr: protocolo Hub MessagePack movido para o pacote MessagePack 2. x

O protocolo ASP.NET Core de [Hub MessagePack](/aspnet/core/signalr/messagepackhubprotocol) signalr não usa o [pacote NuGet MessagePack](https://www.nuget.org/packages/MessagePack) para serialização MessagePack. ASP.NET Core 5,0 atualiza o pacote de 1. x para a versão mais recente do pacote 2. x.

Para obter uma discussão sobre esse problema, consulte [dotnet/aspnetcore # 18692](https://github.com/dotnet/aspnetcore/issues/18692).

## <a name="version-introduced"></a>Versão introduzida

5,0 visualização 1

## <a name="old-behavior"></a>Comportamento antigo

ASP.NET Core Signalr usou o pacote MessagePack 1. x para serializar e desserializar mensagens MessagePack.

## <a name="new-behavior"></a>Novo comportamento

ASP.NET Core Signalr usa o pacote MessagePack 2. x para serializar e desserializar mensagens MessagePack.

## <a name="reason-for-change"></a>Motivo da alteração

As melhorias mais recentes no pacote MessagePack 2. x adicionam uma funcionalidade útil.

## <a name="recommended-action"></a>Ação recomendada

Essa alteração significativa se aplica quando:

* Definindo ou Configurando valores em <xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions> .
* Usar as APIs do MessagePack diretamente e usar o protocolo Hub MessagePack do ASP.NET Core Signalr no mesmo projeto. A versão mais recente será carregada em vez da versão anterior.

Para obter diretrizes de migração dos autores de pacotes, consulte [migrando do MessagePack v1. x para o MessagePack v2. x](https://github.com/neuecc/MessagePack-CSharp/blob/master/doc/migration.md). Alguns aspectos da serialização e desserialização de mensagens são afetados. Especificamente, há [alterações comportamentais em como os valores de data e hora são serializados](https://github.com/neuecc/MessagePack-CSharp/blob/master/doc/migration.md#behavioral-changes).

## <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

`T:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions`

-->
