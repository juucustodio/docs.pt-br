---
title: 'Alteração significativa: Signalr: tipo de opções de protocolo Hub MessagePack alterado'
description: 'Saiba mais sobre a alteração significativa no ASP.NET Core o Signaler intitulada 5,0: tipo de opções do protocolo Hub MessagePack alterado'
author: scottaddie
ms.author: scaddie
ms.date: 10/01/2020
ms.openlocfilehash: b75dbec834699472f18b3058052274476bd9751d
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95760530"
---
# <a name="signalr-messagepack-hub-protocol-options-type-changed"></a>Signalr: tipo de opções de protocolo de Hub MessagePack alterado

O tipo de opções do protocolo Hub MessagePack do Signalr ASP.NET Core foi alterado de `IList<MessagePack.IFormatterResolver>` para o tipo da biblioteca [MessagePack](https://www.nuget.org/packages/MessagePack) `MessagePackSerializerOptions` .

Para discussão sobre essa alteração, consulte [dotnet/aspnetcore # 20506](https://github.com/dotnet/aspnetcore/issues/20506).

## <a name="version-introduced"></a>Versão introduzida

5,0 versão prévia 4

## <a name="old-behavior"></a>Comportamento antigo

Você pode adicionar às opções, conforme mostrado no exemplo a seguir:

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers.Add(MessagePack.Resolvers.StandardResolver.Instance);
    });
```

E substitua as opções da seguinte maneira:

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.FormatterResolvers = new List<MessagePack.IFormatterResolver>()
        {
            MessagePack.Resolvers.StandardResolver.Instance
        };
    });
```

## <a name="new-behavior"></a>Novo comportamento

Você pode adicionar às opções, conforme mostrado no exemplo a seguir:

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.SerializerOptions =
            options.SerializeOptions.WithResolver(MessagePack.Resolvers.StandardResolver.Instance);
    });
```

E substitua as opções da seguinte maneira:

```csharp
services.AddSignalR()
    .AddMessagePackProtocol(options =>
    {
        options.SerializerOptions = MessagePackSerializerOptions
                .Standard
                .WithResolver(MessagePack.Resolvers.StandardResolver.Instance)
                .WithSecurity(MessagePackSecurity.UntrustedData);
    });
```

## <a name="reason-for-change"></a>Motivo da alteração

Essa alteração faz parte da mudança para o MessagePack v2. x, que foi anunciado em [ASPNET/comunicados # 404](https://github.com/aspnet/Announcements/issues/404). A biblioteca v2. x adicionou uma API de opções que é mais fácil de usar e fornece mais recursos do que a lista de `MessagePack.IFormatterResolver` que foi exposta antes.

## <a name="recommended-action"></a>Ação recomendada

Essa alteração significativa afeta qualquer pessoa que esteja Configurando valores <xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions> . Se você estiver usando o protocolo ASP.NET Core de Hub MessagePack Signalr e modificando as opções, atualize seu uso para usar a nova API de opções, conforme mostrado acima.

## <a name="affected-apis"></a>APIs afetadas

<xref:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions?displayProperty=nameWithType>

<!--

### Category

ASP.NET Core

### Affected APIs

`T:Microsoft.AspNetCore.SignalR.MessagePackHubProtocolOptions`

-->
