---
title: Migrar soluções grandes para ASP.NET Core
description: Uma visão geral de como migrar aplicativos grandes do ASP.NET MVC para ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: e0fcf4b975678e81a71bac800cbe8bd01f1b8d17
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488485"
---
# <a name="migrate-large-solutions-to-aspnet-core"></a>Migrar soluções grandes para ASP.NET Core

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

A migração de grandes soluções do .NET Framework para o .NET Core requer algum planejamento. As dependências devem ser migradas ou atualizadas antes dos projetos que dependem delas. Há ferramentas que podem identificar dependências e oferecem ajuda com a migração para o .NET Core. Dependendo do aplicativo, seu escopo e padrões de uso atuais, estratégias diferentes podem ser empregadas durante a migração. Você os migra de uma só vez, ou ao longo do tempo, lado a lado com o sistema atual? Você encapsula o sistema atual em um novo e substitui incrementalmente sua funcionalidade?

Neste capítulo, você aprenderá como criar um plano de migração para uma solução grande, como usar ferramentas para ajudar na migração e algumas estratégias a serem consideradas para a migração em si.

## <a name="references"></a>Referências

- [Quais tópicos são importantes para migrar grandes aplicativos de API Web e MVC para o .NET Core?](https://twitter.com/ardalis/status/1313669040859217921)
- [Portabilidade do .NET Framework para o .NET Core](https://docs.microsoft.com/dotnet/core/porting/)

>[!div class="step-by-step"]
>[Anterior](testing-differences.md) 
> [Avançar](identify-migration-sequence.md)
