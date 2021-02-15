---
title: Comparar o signalr ASP.NET e o sinalizador de ASP.NET Core
description: Como ASP.NET Core Signalr difere de seu antecessor, ASP.NET Signalr?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: f3605112da59fe7e014606aab170ea21aa892222
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488478"
---
# <a name="compare-aspnet-signalr-and-aspnet-core-signalr"></a>Comparar o signalr ASP.NET e o sinalizador de ASP.NET Core

ASP.NET Core Signalr é incompatível com clientes ou servidores usando o Signalr ASP.NET. Você precisará atualizar os clientes e o servidor para usar o Signalr ASP.NET Core. Algumas diferenças são descritas nesta seção, enquanto a lista completa está disponível nos [documentos](https://docs.microsoft.com/aspnet/core/signalr/version-differences). ASP.NET Core Signalr requer o .NET Core 2,1 ou superior.

## <a name="feature-differences"></a>Diferenças de recursos

- O Signalr ASP.NET tenta automaticamente reconectar as conexões ignoradas; Esse comportamento é opcional para clientes sinalizadores ASP.NET Core
- Ambas as estruturas dão suporte a JSON; ASP.NET Core Signalr também dá suporte a um protocolo binário baseado em MessagePack, e os protocolos personalizados podem ser criados.
- O transporte de quadro contínuo, com suporte do Signalr ASP.NET, não tem suporte no Signalr ASP.NET Core.
- ASP.NET Core Signalr deve ser configurado adicionando `services.AddSignalR()` e `app.UseEndpoints` em `Startup.ConfigureServices` e `Startup.Configure` , respectivamente.
- ASP.NET Core Signalr requer sessões adesivas; O Signalr ASP.NET não.
- ASP.NET Core simplifica o modelo de conexão; as conexões são feitas apenas para um único Hub.
- ASP.NET Core Signalr dá suporte ao streaming de dados do hub para o cliente.
- ASP.NET Core Signalr não dá suporte à passagem de estado entre clientes e o Hub.
- A `PersistentConnection` classe não existe no ASP.NET Core signalr.
- O Signalr ASP.NET dá suporte a SQL Server e Redis. ASP.NET Core Signalr dá suporte ao [signalr do Azure](https://docs.microsoft.com/azure/azure-signalr/) e Redis.

## <a name="references"></a>Referências

- [Diferenças entre o signalr ASP.NET e o sinalizador de ASP.NET Core](https://docs.microsoft.com/aspnet/core/signalr/version-differences)
- [Serviço Azure SignalR](https://docs.microsoft.com/azure/azure-signalr/)

>[!div class="step-by-step"]
>[Anterior](razor-differences.md) 
> [Avançar](testing-differences.md)
