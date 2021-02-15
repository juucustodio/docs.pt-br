---
title: Resumo
description: Um resumo e um conjunto de importantes argumentos para portar ASP.NET MVC e aplicativos Web API 2 para ASP.NET Core.
author: ardalis
ms.date: 12/16/2020
ms.openlocfilehash: 596ab8621008d1cdc16d841e8faede5f4a1fdd16
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488432"
---
# <a name="summary"></a>Resumo

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

Neste livro, você recebeu os recursos necessários para decidir se faz sentido portar os aplicativos ASP.NET existentes da sua organização em execução em .NET Framework para ASP.NET Core. Você aprendeu sobre [considerações importantes](migration-considerations.md) para escolher quando faz sentido migrar para o .NET Core e quando pode ser apropriado manter (partes do) seu aplicativo em .NET Framework. Há diferenças entre as versões do .NET Core e seus recursos e compatibilidades com .NET Framework, e você aprendeu a [escolher a versão correta do .NET Core para seu aplicativo](choose-net-core-version.md).

A portabilidade de um aplicativo grande geralmente envolve uma quantidade razoável de risco e esforço. Você aprendeu como mitigar esse risco empregando uma ou mais estratégias de [migração incremental](incremental-migration-strategies.md) junto com várias [estratégias de implantação](deployment-strategies.md) para manter os aplicativos parcialmente migrados em execução na produção.

Há muitas [diferenças de arquitetura entre ASP.net e ASP.NET Core](architectural-differences.md). No capítulo 2, você aprendeu sobre muitas dessas diferenças e como elas se relacionam à migração do seu aplicativo. Este capítulo abordou tudo, desde a [inicialização do aplicativo](app-startup-differences.md) e o [middleware](middleware-modules-handlers.md) de baixo nível até as diferenças de [controlador](controller-differences.md) de alto nível e [API da Web](webapi-differences.md) e os novos recursos, permitindo [cenários de teste muito melhores](testing-differences.md).

Aplicativos grandes geralmente são compostos de muitos projetos e pacotes, e as dependências podem desempenhar uma função importante para determinar como a migração pode ser fácil ou difícil. O [capítulo 3](migrate-large-solutions.md) ajudou [a identificar a sequência na qual migrar projetos](identify-migration-sequence.md) e [como compreender e atualizar as dependências do seu aplicativo](understand-update-dependencies.md). Ele também detalha [estratégias adicionais para a migração de aplicativos, mantendo-os em execução na produção](strategies-migrating-in-production.md).

No [capítulo 4, você viu como um aplicativo de referência MVC real ASP.net foi migrado para ASP.NET Core](example-migration-eshop.md). Este capítulo incluiu uma análise detalhada de todas as alterações necessárias para pegar o aplicativo existente e portá-lo para execução em ASP.NET Core. Consulte novamente se você tiver perguntas específicas sobre o processo de portabilidade e alguns de seus detalhes mais específicos.

Finalmente, o [capítulo 5 cenários de implantação específicos detalhados se concentrou no IIS](deployment-scenarios.md). Você viu como é possível usar o servidor Web do IIS existente para hospedar partes de seu aplicativo que foram modeladas para ASP.NET Core enquanto mantém a consistência das URLs públicas do aplicativo. O IIS inclui excelente suporte para regravação de URL e roteamento de solicitação que permite hospedar várias versões do seu site lado a lado ou mesmo em servidores diferentes, sem alteração nas URLs voltadas para o público que o aplicativo expõe.

>[!div class="step-by-step"]
>[Anterior](deployment-scenarios.md)
