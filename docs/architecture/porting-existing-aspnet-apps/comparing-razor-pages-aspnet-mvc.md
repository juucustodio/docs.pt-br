---
title: Comparar Razor Pages com o MVC do ASP.NET
description: Razor Pages oferecem uma maneira melhor de organizar as responsabilidades do que as exibições tradicionais do MVC para aplicativos baseados em página. Saiba como eles se comparam à abordagem ASP.NET MVC tradicional nesta seção.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 3a113cea52c32b436d357f64d26eb31c722349ee
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488411"
---
# <a name="compare-razor-pages-to-aspnet-mvc"></a>Comparar Razor Pages com o MVC do ASP.NET

Razor Pages é a maneira preferida de criar aplicativos baseados em página ou em formulário no ASP.NET Core. A partir dos [documentos](https://docs.microsoft.com/aspnet/core/razor-pages/), "Razor Pages pode tornar a codificação de cenários voltados para a página mais fácil e mais produtiva do que usar controladores e exibições". Se seu aplicativo ASP.NET MVC fizer uso intensivo de exibições, convém considerar a migração de ações e exibições para Razor Pages.

Um aplicativo MVC típico baseado em exibição com rigidez de tipos usará um controlador para conter uma ou mais ações. O controlador irá interagir com o modelo de domínio ou de dados e criará uma instância de uma classe ViewModel. Em seguida, essa classe ViewModel é passada para a exibição associada a essa ação. Usar essa abordagem, juntamente com a estrutura de pastas padrão de aplicativos MVC, para adicionar uma nova página a um aplicativo, requer a modificação de um controlador em uma pasta, uma exibição em uma subpasta aninhada em outra pasta e um ViewModel em outra pasta.

Razor Pages agrupar a ação (agora um *manipulador*) e o ViewModel (chamado de *PageModel*) em uma classe e vincular essa classe à exibição (chamada de página Razor). Todos os Razor Pages vão para uma pasta de *páginas* na raiz do projeto de ASP.NET Core. Razor Pages usar uma Convenção de roteamento com base em seu nome e local dentro dessa pasta. Os manipuladores se comportam exatamente como métodos de ação, mas têm o verbo HTTP que eles manipulam em seu nome (por exemplo, `OnGet` ). Eles também não precisam, necessariamente, retornar, pois, por padrão, eles são considerados para retornar a página com a qual estão associados. Isso tende a manter Razor Pages e seus manipuladores menores e mais focados ao mesmo tempo, facilitando a localização e o trabalho com todos os arquivos necessários para adicionar ou modificar uma parte específica de um aplicativo.

Como parte de uma mudança do ASP.NET MVC para o ASP.NET Core, as equipes devem considerar se desejam migrar controladores e exibições para ASP.NET Core controladores e exibições, ou para Razor Pages. O primeiro provavelmente exigirá um esforço geral um pouco menor, mas não permitirá que a equipe Aproveite os benefícios de Razor Pages sobre a organização de arquivos tradicional baseada em exibição.

## <a name="references"></a>Referências

- [Introdução a Páginas do Razor no ASP.NET Core](https://docs.microsoft.com/aspnet/core/razor-pages/)
- [Aplicativos ASP.NET Core mais simples com Razor Pages](https://docs.microsoft.com/archive/msdn-magazine/2017/september/asp-net-core-simpler-asp-net-mvc-apps-with-razor-pages)

>[!div class="step-by-step"]
>[Anterior](routing-differences.md) 
> [Avançar](webapi-differences.md)
