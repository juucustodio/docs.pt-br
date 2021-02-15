---
title: Comparar ASP.NET Identity e ASP.NET Core identidade
description: Esta seção examina as diferenças entre ASP.NET Identity e ASP.NET Core identidade, que são especialmente importantes ao planejar uma migração do .NET Framework para o .NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: bf915c7343b0c8060ef8192387a3cec33a1f0eea
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488377"
---
# <a name="compare-aspnet-identity-and-aspnet-core-identity"></a>Comparar ASP.NET Identity e ASP.NET Core identidade

No ASP.NET MVC, os recursos de identidade normalmente são configurados em *IdentityConfig.cs* na pasta *App_Start* . Examine como isso é configurado no aplicativo existente e compare-o com a [configuração necessária para ASP.NET Core identidade](https://docs.microsoft.com/aspnet/core/security/authentication/identity-configuration) no *Startup.cs*.

ASP.NET Identity é uma API que dá suporte à funcionalidade de logon da interface do usuário e gerencia usuários, senhas, dados de perfil, funções, declarações, tokens, confirmações de email e muito mais. Ele dá suporte a provedores de logon externos, como Facebook, Google, Microsoft e Twitter.

Se seu aplicativo ASP.NET MVC estiver usando a associação do ASP.NET, você encontrará um guia para [migrar da autenticação de associação do ASP.net para a identidade do ASP.NET Core 2,0](https://docs.microsoft.com/aspnet/core/migration/proper-to-2x/membership-to-core-identity). Isso é principalmente um exercício de migração de dados, na conclusão da qual você deve ser capaz de usar ASP.NET Core identidade com os registros de usuário migrados.

Se você migrar seus usuários do ASP.NET Identity para ASP.NET Core identidade, talvez seja necessário atualizar seus hashes de senha ou controlar quais senhas são codificadas com a nova abordagem de identidade ASP.NET Core ou a abordagem ASP.NET Identity mais antiga. [Essa abordagem descrita em Stack Overflow](https://stackoverflow.com/a/57074910/13729) fornece algumas opções para migrar hashes de senha de usuário ao longo do tempo, em vez de todos de uma vez.

Uma das maiores diferenças quando se trata de ASP.NET Core identidade em comparação com ASP.NET Identity é o mínimo de código que você precisa incluir em seu projeto. ASP.NET Core identidade agora é fornecida como uma biblioteca de classes Razor, o que significa que sua interface do usuário e lógica estão todas disponíveis em um pacote NuGet. Você pode substituir a interface do usuário e a lógica existentes [scaffoldingndo os arquivos de identidade de ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/authentication/scaffold-identity) , mas mesmo nesse caso, você precisa apenas Scaffold as páginas que deseja modificar, e não cada uma que exista.

## <a name="migrate-from-owin--katana"></a>Migrar do OWIN/Katana

Os recursos a seguir oferecem algumas diretrizes para migrar do OWIN/katana:

- [Migração](https://docs.microsoft.com/aspnet/core/migration/proper-to-2x/#globalasax-file-replacement)
- [Katana para ASPNET 5](https://devblogs.microsoft.com/aspnet/katana-asp-net-5-and-bridging-the-gap/)

## <a name="references"></a>Referências

- [Migrar autenticação e identidade para ASP.NET Core](https://docs.microsoft.com/aspnet/core/migration/identity)
- [Introdução à identidade no ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/authorization/introduction)
- [Configurar identidade de ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/authentication/identity-configuration)
- [Identidade Scaffold em projetos ASP.NET Core](https://docs.microsoft.com/aspnet/core/security/authentication/scaffold-identity)

>[!div class="step-by-step"]
>[Anterior](authentication-differences.md) 
> [Avançar](controller-differences.md)
