---
title: Escolha a versão correta do .NET Core
description: Como você deve determinar qual versão do .NET Core será direcionada?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 401eead986ee8b67ed15be609d0b5d228773312d
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488413"
---
# <a name="choose-the-right-net-core-version"></a>Escolha a versão correta do .NET Core

A maior consideração para a maioria das organizações ao escolher uma versão do .NET Core para o destino é o ciclo de vida do suporte. As versões de LTS (suporte a longo prazo) são entregues com menos frequência, mas têm uma janela de suporte mais longa do que as versões atuais (não LTS). Atualmente, as versões LTS estão agendadas para envio a cada ano. Os clientes podem escolher quais versões direcionar e podem instalar diferentes versões do .NET Core lado a lado no mesmo computador. As versões do LTS receberão apenas correções críticas e compatíveis ao longo de seu ciclo de vida. As versões atuais receberão essas mesmas correções e também serão atualizadas com inovações e recursos compatíveis. As versões de LTS têm suporte por três anos após sua versão inicial. As versões atuais recebem suporte por três meses após uma versão com LTS ou versão atual subsequente.

A maioria dos clientes que buscam migrar um grande aplicativo de .NET Framework para o .NET Core hoje provavelmente está procurando um destino estável, já que eles ainda não fizeram a mudança para uma versão anterior do .NET Core. Nesse caso, a melhor versão do .NET Core para o destino da migração é o .NET Core 3,1, que é a versão atual do LTS. O suporte para .NET Core 3,1 termina em 2022 de dezembro. A próxima versão de LTS planejada será o .NET 6,0, acompanhada para envio em novembro de 2021.

A atualização do .NET Core 3,1 para o .NET 5,0 (a próxima versão) requer muito menos esforço do que a porta do .NET Framework para o .NET Core. Por esse motivo, a recomendação para a maioria dos clientes é atualizar para o .NET Core 3,1 primeiro. Em seguida, decida se a próxima atualização deve ser para a versão atual mais recente (.NET 5,0) ou para aguardar a próxima versão de LTS (.NET 6,0) antes de atualizar.

Este livro pressupõe que os aplicativos .NET Framework serão atualizados para o .NET Core 3,1.

## <a name="references"></a>Referências

[Política de suporte do .NET Core e .NET 5](https://dotnet.microsoft.com/platform/support/policy/dotnet-core)

>[!div class="step-by-step"]
>[Anterior](migrate-aspnet-core-2-1.md) 
> [Avançar](incremental-migration-strategies.md)
