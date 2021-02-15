---
title: Diferenças de arquitetura entre o ASP.NET MVC e o ASP.NET Core
description: Examine as diferenças de arquitetura entre ASP.NET e ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 0e546465a3da6971a118c65114af81c3a387e00e
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488416"
---
# <a name="architectural-differences-between-aspnet-mvc-and-aspnet-core"></a>Diferenças de arquitetura entre o ASP.NET MVC e o ASP.NET Core

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Há muitas diferenças de arquitetura entre o ASP.NET MVC em .NET Framework e ASP.NET Core. É importante ter uma ampla compreensão dessas diferenças, uma vez que as equipes avaliam o trabalho envolvido em portar seus aplicativos MVC ASP.NET para ASP.NET Core. Este capítulo analisa cada uma das maneiras em que ASP.NET Core difere substancialmente do ASP.NET MVC.

## <a name="breaking-changes"></a>Alterações de quebra

O .NET Core é uma reescrita de plataforma cruzada de .NET Framework. Há muitas [alterações significativas entre as duas estruturas](https://docs.microsoft.com/dotnet/core/compatibility/fx-core). As seções a seguir identificam diferenças específicas entre como o ASP.NET MVC e os aplicativos ASP.NET Core são projetados e desenvolvidos. Tome cuidado para examinar também a documentação para determinar quais bibliotecas de estrutura você está usando que talvez precisem ser alteradas. Em muitos casos, um pacote NuGet de substituição existe para preencher as lacunas restantes entre .NET Framework e o .NET Core. Em casos raros, talvez seja necessário encontrar uma solução de terceiros ou implementar um novo código personalizado para resolver incompatibilidades.

>[!div class="step-by-step"]
>[Anterior](additional-migration-resources.md) 
> [Avançar](app-startup-differences.md)
