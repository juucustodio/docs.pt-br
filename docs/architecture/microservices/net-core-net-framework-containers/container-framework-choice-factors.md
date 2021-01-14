---
title: Tabela de decisões. Estruturas .NET a serem usadas para o Docker
description: Arquitetura de microsserviços do .NET para aplicativos .NET em contêineres | Tabela de decisões, estruturas .NET a serem usadas para o Docker
ms.date: 01/13/2021
ms.openlocfilehash: 35f101b3f4030e081068677b3754363bf6cd8210
ms.sourcegitcommit: a4cecb7389f02c27e412b743f9189bd2a6dea4d6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/14/2021
ms.locfileid: "98188654"
---
# <a name="decision-table-net-frameworks-to-use-for-docker"></a>Tabela de decisões: estruturas .NET a serem usadas para o Docker

A tabela de decisão a seguir resume se o .NET Framework ou o .NET 5 deve ser usado. Lembre-se de que, para contêineres Linux, são necessários hosts do Docker baseados em Linux (VMs ou servidores) e de que, para contêineres do Windows, são necessários hosts do Docker baseados em Windows Server (VMs ou servidores).

> [!IMPORTANT]
> Os computadores de desenvolvimento executarão um host Docker, seja Linux ou Windows. Microsserviços relacionados que você deseja executar e testar em conjunto em uma solução precisarão ser executados na mesma plataforma de contêiner.

| Arquitetura/tipo de aplicativo | Contêineres do Linux | Contêineres do Windows |
|-------------------------|------------------|--------------------|
| Microsserviços em contêineres | .NET 5 | .NET 5 |
| Aplicativo monolítico | .NET 5 | .NET Framework <br/> .NET 5 |
| Melhores desempenho e escalabilidade da categoria | .NET 5 | .NET 5 |
| Migração do aplicativo herdado do Windows Server ("campo-marrom") para contêineres | -- | .NET Framework |
| Novo desenvolvimento baseado em contêiner ("campo-verde") | .NET 5 | .NET 5 |
| ASP.NET Core | .NET 5 | .NET 5 (recomendado) <br/> .NET Framework |
| ASP.NET 4 (MVC 5, API Web 2 e Web Forms) | -- | .NET Framework |
| Serviços SignalR | .NET Core 2.1 ou versão posterior | .NET Framework <br/> .NET Core 2.1 ou versão posterior |
| WCF, WF e outras estruturas herdadas | WCF no .NET Core (somente biblioteca de cliente) | .NET Framework <br/> WCF no .NET 5 (somente biblioteca de cliente) |
| Consumo de serviços do Azure | .NET 5 <br/> (eventualmente, a maioria dos serviços do Azure fornecerá SDKs de cliente para o .NET 5) | .NET Framework <br/> .NET 5 <br/> (eventualmente, a maioria dos serviços do Azure fornecerá SDKs de cliente para o .NET 5) |

>[!div class="step-by-step"]
>[Anterior](net-framework-container-scenarios.md) 
> [Avançar](net-container-os-targets.md)
