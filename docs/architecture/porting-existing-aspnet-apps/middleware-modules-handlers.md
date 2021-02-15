---
title: Comparar middleware com módulos e manipuladores
description: Esta seção explora as diferenças na estrutura de aplicativos ASP.NET que usam manipuladores e módulos com ASP.NET Core aplicativos que definem o middleware para seus pipelines de tratamento de solicitação.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 5852aa82e58010882bda5424021302c60ba62d83
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488491"
---
# <a name="compare-middleware-to-modules-and-handlers"></a>Comparar middleware com módulos e manipuladores

Se seu aplicativo de API Web ou MVC existente do ASP.NET usa OWIN/Katana, provavelmente você já está familiarizado com o conceito de middleware e portando-o para ASP.NET Core deve ser razoavelmente simples. No entanto, a maioria dos aplicativos ASP.NET depende de módulos HTTP e manipuladores HTTP em vez de middleware. Migrá-los para ASP.NET Core requer esforço extra.

## <a name="aspnet-modules-and-handlers"></a>Módulos e manipuladores ASP.NET

Os [módulos http e os manipuladores HTTP](https://docs.microsoft.com/troubleshoot/aspnet/http-modules-handlers) são parte integrante da arquitetura ASP.net. Enquanto uma solicitação está sendo processada, cada solicitação é processada por vários módulos HTTP (por exemplo, o módulo de autenticação e o módulo de sessão) e, em seguida, é processado por um único manipulador HTTP. Depois que o manipulador tiver processado a solicitação, a solicitação fluirá de volta pelos módulos HTTP.

Se seu aplicativo estiver usando módulos HTTP ou manipuladores HTTP personalizados, você precisará de um plano para migrá-los para ASP.NET Core. A substituição mais provável no ASP.NET Core é o middleware.

## <a name="aspnet-core-middleware"></a>Middleware ASP.NET Core

ASP.NET Core define um pipeline de solicitação no método de cada aplicativo `Configure` . Esse pipeline de solicitação define como uma solicitação de entrada é manipulada pelo aplicativo, com cada método no pipeline que chama o método Next até que eventualmente um método seja encerrado e a cadeia de *middleware* seja encerrada e retorne o backup da pilha. O middleware pode direcionar todas as solicitações ou pode ser configurado para mapear apenas para determinadas solicitações com base no caminho solicitado ou em outros fatores. Ele pode ser configurado totalmente no `Configure` método de um aplicativo ou implementado em uma classe separada.

O comportamento em um aplicativo MVC ASP.NET que usa módulos HTTP provavelmente é mais adequado para o [middleware personalizado](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/?view=aspnetcore-3.1&preserve-view=true). Os manipuladores HTTP personalizados podem ser substituídos por rotas personalizadas ou pontos de extremidade que respondem ao mesmo caminho.

## <a name="references"></a>Referências

- [Módulos HTTP ASP.NET e manipuladores HTTP](https://docs.microsoft.com/troubleshoot/aspnet/http-modules-handlers)
- [Middleware ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/middleware/?view=aspnetcore-3.1&preserve-view=true)

>[!div class="step-by-step"]
>[Anterior](dependency-injection-differences.md) 
> [Avançar](configuration-differences.md)
