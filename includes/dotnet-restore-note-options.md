---
ms.openlocfilehash: 19002cce40fdc929716a761a5e01303be4decb35
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90537816"
---
Você não precisa executar [`dotnet restore`](~/docs/core/tools/dotnet-restore.md) o porque ele é executado implicitamente por todos os comandos que exigem a ocorrência de uma restauração, como,,,, `dotnet new` `dotnet build` `dotnet run` `dotnet test` `dotnet publish` e `dotnet pack` . Para desabilitar a restauração implícita, use a `--no-restore` opção.

O `dotnet restore` comando ainda é útil em determinados cenários em que a restauração explícita faz sentido, como [compilações de integração contínua em Azure DevOps Services](/azure/devops/build-release/apps/aspnet/build-aspnet-core) ou em sistemas de compilação que precisam controlar explicitamente quando a restauração ocorre.

Para obter informações sobre como gerenciar feeds do NuGet, consulte a [ `dotnet restore` documentação](../docs/core/tools/dotnet-restore.md).

Esse comando oferece suporte às `dotnet restore` opções quando passadas na forma longa (por exemplo, `--source` ). Opções de formato curto, como `-s`, não são compatíveis.
