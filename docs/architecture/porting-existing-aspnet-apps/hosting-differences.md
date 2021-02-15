---
title: Diferenças de hospedagem entre o ASP.NET MVC e o ASP.NET Core
description: Uma visão geral das diferenças entre como os aplicativos ASP.NET MVC são hospedados versus ASP.NET Core aplicativos.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: e7cc26bfeb1c01a9d60878dacfe0439d1b718f68
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488382"
---
# <a name="hosting-differences-between-aspnet-mvc-and-aspnet-core"></a>Diferenças de hospedagem entre o ASP.NET MVC e o ASP.NET Core

Os aplicativos ASP.NET MVC são hospedados no IIS e podem depender da configuração do IIS para seu comportamento. Isso geralmente inclui [módulos do IIS](https://docs.microsoft.com/iis/get-started/introduction-to-iis/iis-modules-overview). Como parte da revisão de um aplicativo para se preparar para a porta de ti do ASP.NET MVC para ASP.NET Core, as equipes devem identificar quais módulos, se houver, estão usando a partir da lista de módulos do IIS instalados em seu servidor.

[ASP.NET Core aplicativos podem ser executados em vários servidores diferentes](https://docs.microsoft.com/aspnet/core/fundamentals/servers/). O servidor de plataforma cruzada padrão, Kestrel, é uma boa opção padrão. Os aplicativos em execução no Kestrel podem ser hospedados pelo IIS, sendo executados em um processo separado. No Windows, os aplicativos também podem ser executados em processo no IIS ou usando HTTP.sys. O Kestrel geralmente é recomendado para melhor desempenho. O HTTP.sys pode ser usado em cenários em que o aplicativo é exposto à Internet e as funcionalidades necessárias são compatíveis com HTTP.sys, mas não com Kestrel.

Kestrel não tem um equivalente a módulos do IIS (embora aplicativos hospedados no IIS ainda possam aproveitar os módulos do IIS). Para atingir o comportamento equivalente, o middleware configurado no aplicativo ASP.NET Core em si é normalmente usado.

## <a name="references"></a>Referências

- [Módulos do IIS](https://docs.microsoft.com/iis/get-started/introduction-to-iis/iis-modules-overview)
- [Servidores ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/servers/)

>[!div class="step-by-step"]
>[Anterior](app-startup-differences.md) 
> [Avançar](serving-static-files.md)
