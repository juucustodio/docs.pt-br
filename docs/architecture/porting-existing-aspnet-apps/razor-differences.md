---
title: Comparar o uso do Razor no ASP.NET MVC e ASP.NET Core
description: Como o Razor é diferente entre o ASP.NET MVC e o ASP.NET Core?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 355506364e32283cb86bd21b82d7de672a974829
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488482"
---
# <a name="compare-razor-usage-in-aspnet-mvc-and-aspnet-core"></a>Comparar o uso do Razor no ASP.NET MVC e ASP.NET Core

A sintaxe básica do Razor não mudou substancialmente entre o ASP.NET MVC e o ASP.NET Core. No entanto, há certas diferenças, como a introdução de [auxiliares de marca](https://docs.microsoft.com/aspnet/core/mvc/views/tag-helpers/intro) e Razor pages, que devem ser considerados durante a migração. Se seu aplicativo fizer uso intenso da funcionalidade personalizada do Razor, consulte a [referência de sintaxe Razor para ASP.NET Core](https://docs.microsoft.com/aspnet/core/razor-pages) para ver quais alterações podem ser necessárias ao migrar para o ASP.NET Core.

## <a name="tag-helpers"></a>Auxiliares de Marca

Os Auxiliares de Marca permitem que o código do lado do servidor participe da criação e renderização de elementos HTML em arquivos do Razor. Eles oferecem muitas vantagens em relação aos auxiliares HTML e devem ser usados em vez de auxiliares HTML sempre que possível. Eles fornecem uma experiência de desenvolvimento amigável em HTML, pois eles se parecem com HTML padrão e são ignorados pela maioria das ferramentas projetadas para editar HTML. No _Visual Studio_, há suporte avançado do IntelliSense para a criação de marcação HTML e Razor com auxiliares de marca. Os auxiliares de marca podem fornecer um comportamento simples ou complexo da marcação declarativa em arquivos Razor.

## <a name="razor-pages"></a>Páginas do Razor

Razor Pages oferecem uma alternativa a controladores, ações e modos de exibição para aplicativos baseados em página e em formulário. [Razor Pages foram comparadas ao MVC ASP.net anteriormente neste capítulo](./comparing-razor-pages-aspnet-mvc.md).

## <a name="references"></a>Referências

- [Migrar do ASP.NET MVC para o ASP.NET Core MVC: controladores e exibições](https://docs.microsoft.com/aspnet/core/migration/mvc#migrate-controllers-and-views)
- [Auxiliares de Marca no ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/views/tag-helpers/intro)
- [Introdução a Páginas do Razor no ASP.NET Core](https://docs.microsoft.com/aspnet/core/razor-pages)
- [Referência da sintaxe Razor para ASP.NET Core](https://docs.microsoft.com/aspnet/core/razor-pages)

>[!div class="step-by-step"]
>[Anterior](controller-differences.md) 
> [Avançar](signalr-differences.md)
