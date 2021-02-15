---
title: Estratégias para migrar aplicativos Web Forms ASP.NET
description: Quais estratégias as equipes podem usar para migrar aplicativos ASP.NET Web Forms para o .NET Core?
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 0b37a37f047de50c347313be14a2228838da6995
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488484"
---
# <a name="strategies-for-migrating-aspnet-web-forms-apps"></a>Estratégias para migrar aplicativos Web Forms ASP.NET

Este livro oferece diretrizes para migrar grandes ASP.NET MVC e aplicativos de API Web para o .NET Core. Alguns desses aplicativos ASP.NET também podem incluir páginas Web Forms (*. aspx*) que devem ser resolvidas. O ASP.NET Web Forms não tem suporte no .NET Core (nem Páginas da Web do ASP.NET). Normalmente, a funcionalidade dessas páginas deve ser reescrita ao portar para ASP.NET Core. No entanto, há algumas estratégias que você pode aplicar antes ou durante essa migração para ajudar a reduzir o esforço geral necessário.

Web Forms continuará a ter suporte por algum tempo. Uma opção pode ser manter essa funcionalidade em um aplicativo ASP.NET 4. x.

## <a name="separate-business-logic-and-other-concerns"></a>Separar a lógica de negócios e outras preocupações

Quanto menos código em suas páginas do ASP.NET Web Forms, melhor. Quando possível, mantenha a lógica de negócios e outras preocupações como o acesso a dados em classes separadas, idealmente em bibliotecas de classes separadas. Essas bibliotecas de classes podem ser portadas para .NET Standard e consumidas por qualquer aplicativo ASP.NET Core.

## <a name="implement-client-behavior-and-web-apis"></a>Implementar o comportamento do cliente e APIs da Web

Considere a opção de implementar a lógica em Web Forms ou no navegador com a ajuda de chamadas à API. Favorecer o último. Há suporte para a migração de APIs para ASP.NET Core. O comportamento do lado do cliente deve ser independente da pilha do lado do servidor que seu aplicativo está usando. O uso dessa abordagem tem o benefício adicional de fornecer uma experiência de usuário mais responsiva.

## <a name="consider-blazor"></a>Considere o mais incrivelmente

O mais claro permite que você crie interfaces do site interativas da Web com C# em vez de JavaScript. Ele pode ser executado no servidor ou no navegador usando o Webassembly. Os aplicativos de Web Forms ASP.NET podem ser portados de página por página para aplicativos mais Incrivelmenteos. Para obter mais informações sobre como portar Web Forms aplicativos para um mais incrivelmente, consulte mais um [dos desenvolvedores de ASP.NET Web Forms](https://devblogs.microsoft.com/aspnet/blazor-aspnet-webforms-ebook/). Além disso, muitos Web Forms controles foram portados para um grande número de projetos de comunidade de software livre, muito mais [componentes de Web Forms](https://fritzandfriends.github.io/BlazorWebFormsComponents/). Com esses componentes, você pode portar Web Forms páginas com mais facilidade, mesmo se usarem os controles de Web Forms internos.

## <a name="summary"></a>Resumo

Não há suporte para a migração diretamente do ASP.NET Web Forms para ASP.NET Core. No entanto, há estratégias para facilitar a migração para ASP.NET Core. Você pode migrar sua funcionalidade de Web Forms para ASP.NET Core com êxito por:

* Manter a funcionalidade não Web fora de seus projetos.
* Usando APIs Web sempre que possível.
* Considerando o mais moderno como uma opção para uma interface do usuário mais moderna.

## <a name="references"></a>Referências

- [Livro eletrônico gratuito: mais incrivelmente para desenvolvedores de Web Forms ASP.NET](https://devblogs.microsoft.com/aspnet/blazor-aspnet-webforms-ebook/)
- [Componentes de Web Forms de mais incrivelmente (projeto da Comunidade)](https://fritzandfriends.github.io/BlazorWebFormsComponents/)

>[!div class="step-by-step"]
>[Anterior](incremental-migration-strategies.md) 
> [Avançar](deployment-strategies.md)
