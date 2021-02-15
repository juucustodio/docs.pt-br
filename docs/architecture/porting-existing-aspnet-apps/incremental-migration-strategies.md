---
title: Estratégias para migrar incrementalmente
description: Quais estratégias as equipes podem adotar, permitindo que migrem aplicativos grandes do ASP.NET MVC para o .NET Core de maneira incremental?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: aa51f6157185069540042cce2d7bf783cbc253aa
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488376"
---
# <a name="strategies-for-migrating-incrementally"></a>Estratégias para migrar incrementalmente

O maior desafio com a migração de qualquer aplicativo grande é determinar como dividir o processo em tarefas menores. Há várias estratégias que podem ser aplicadas para essa finalidade, incluindo dividir o aplicativo em camadas horizontais, como interface do usuário, acesso a dados, lógica de negócios ou dividir o aplicativo em aplicativos separados e menores. Outra estratégia é atualizar alguns ou todos os aplicativos para diferentes versões de estrutura no caminho para uma versão recente do .NET Core.

Considere o desafio de migrar um aplicativo ASP.NET 4,5 grande. Uma abordagem é migrar diretamente do .NET Framework 4,5 para o .NET Core 3,1. No entanto, essa abordagem precisa considerar cada alteração significativa entre as duas estruturas e versões, que são substanciais.

Uma adição recente ao ecossistema do .NET que ajuda na interoperabilidade entre diferentes .NET Frameworks é [.net Standard](https://dotnet.microsoft.com/platform/dotnet-standard). .NET Standard permite que as bibliotecas sejam criadas com base no conjunto acordado de APIs comuns, garantindo que elas possam ser usadas em qualquer aplicativo .NET. .NET Standard 2,0 é notável porque abrange a maioria das funcionalidades da biblioteca de classes base usada pela maioria dos aplicativos .NET Framework e .NET Core. Infelizmente, a versão mais antiga do .NET com suporte para .NET Standard 2,0 é .NET Framework 4.6.1, e há várias atualizações no .NET Framework 4,8 que o tornam uma opção atraente para as atualizações iniciais.

Uma abordagem para atualizar incrementalmente um sistema .NET Framework 4,5 é primeiro atualizar suas bibliotecas de classes para .NET Framework 4,8. Em seguida, modifique essas bibliotecas para que sejam .NET Standard bibliotecas de classe. Use multi-Targeting e compilação condicional, se necessário. Essa etapa pode ser útil em cenários em que as dependências de aplicativo exigem .NET Framework e não podem ser facilmente portadas diretamente para usar .NET Standard e .NET Core. Como .NET Framework bibliotecas podem ser consumidas por ASP.NET Core aplicativos 2,1, a próxima etapa é migrar parte ou toda a funcionalidade da Web do aplicativo para ASP.NET Core 2,1 (conforme descrito no [capítulo anterior](choose-net-core-version.md)).

Depois que o aplicativo estiver em execução no ASP.NET Core 2,1, migrá-lo para ASP.NET Core 3,1 em isolamento é relativamente simples. O desafio mais provável durante essa etapa é a atualização de dependências incompatíveis para dar suporte ao .NET Core e, possivelmente, a versões mais altas do .NET Standard. Para aplicativos que não têm dependências problemáticas em bibliotecas somente .NET Framework, há pouco motivo para atualizar para o ASP.NET Core 2,1. Portar diretamente para ASP.NET Core 3,1 faz mais sentido e requer menos esforço.

Quando o aplicativo está em execução no .NET Core 3,1, migrar para a versão atual do .NET 5,0 é relativamente simples. O processo envolve principalmente a atualização da estrutura de destino dos seus arquivos de projeto e suas dependências de pacote NuGet associadas. Embora haja várias [alterações significativas a serem consideradas](/dotnet/core/compatibility/3.1-5.0), a maioria dos aplicativos não exige modificações significativas para passar do .net Core 3,1 para o .NET 5,0. É provável que o fator de decisão principal na [escolha entre o .NET Core 3,1 e o .net 5,0 seja compatível](choose-net-core-version.md).

## <a name="references"></a>Referências

- [O que é .NET Standard?](https://dotnet.microsoft.com/platform/dotnet-standard)
- [Apresentando o .NET 5](https://devblogs.microsoft.com/dotnet/introducing-net-5/)
- [Migrar do ASP.NET Core 3,1 para 5,0](https://docs.microsoft.com/aspnet/core/migration/31-to-50)

>[!div class="step-by-step"]
>[Anterior](choose-net-core-version.md) 
> [Avançar](migrate-web-forms.md)
