---
title: Portando aplicativos ASP.NET existentes para o .NET Core
description: Um guia gratuito para converter ASP.NET MVC e aplicativos de API Web para ASP.NET Core.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: 36c0cdbe03fb97ae82336d53e15be2108e9c6367
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488374"
---
# <a name="porting-existing-aspnet-apps-to-net-core"></a>Portando aplicativos ASP.NET existentes para o .NET Core

![imagem da capa](./media/index/porting-existing-aspnet-apps.png)

[!INCLUDE [book-preview](../../../includes/book-preview.md)]

PUBLICADO POR

Divisão de Desenvolvedores Microsoft, equipes dos produtos .NET e Visual Studio

Uma divisão da Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright &copy; 2020 da Microsoft Corporation

Todos os direitos reservados. Nenhuma parte do conteúdo deste livro pode ser reproduzida ou transmitida de qualquer forma ou por qualquer meio sem a permissão por escrito do Publicador.

Este livro é fornecido “no estado em que se encontra” e expressa os pontos de vista e as opiniões do autor. Os pontos de vista, as opiniões e as informações expressos neste livro, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.

 Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios. Nenhuma associação ou conexão real é intencional ou deve ser inferida.

A Microsoft e as marcas listadas em <https://www.microsoft.com> na página da Web "Marcas" são marcas comerciais do grupo de empresas Microsoft.

Mac e macOS são marcas comerciais da Apple Inc.

O logotipo de redistribuição do Docker é uma marca registrada do Docker, Inc. usada pela permissão.

Todas as outras marcas e logotipos são propriedade de seus respectivos proprietários.

Autores:

> **Steve "ardalis" Smith**, arquiteto de software e instrutor- [Ardalis.com](https://ardalis.com)

Participantes e revisores:

> **Nish Anil**, gerente de programas sênior, equipe do .net, Microsoft

> **Mike Rousos**, engenheiro de software principal, equipe do .net, Microsoft

> **Scott Addie**, desenvolvedor de conteúdo sênior, equipe do .net, Microsoft

> **David Pinheiro**, desenvolvedor de conteúdo sênior, equipe do .net, Microsoft

## <a name="version"></a>Versão

Este guia aborda o **.NET Core 3,1** e as atualizações relacionadas à mesma tecnologia "Wave" (ou seja, o Azure e outras tecnologias de terceiros) que coincidem no tempo com a versão 3,1 do .NET Core. A atualização do .NET Core 3,1 para o .NET 5,0 (a próxima versão) é relativamente simples e certamente exigirá substancialmente menos esforço do que a porta do .NET Framework para o .NET Core. A migração do .NET Framework 4. x para o .NET 5,0 será semelhante à migração para o .NET Core 3,1. Para obter mais informações, consulte [escolhendo a versão correta do .NET Core](choose-net-core-version.md).

## <a name="who-should-use-this-guide"></a>Quem deve usar este guia

O público-alvo deste guia são desenvolvedores, líderes de desenvolvimento e arquitetos interessados em migrar seus aplicativos existentes escritos para o ASP.NET MVC e a API da Web (.NET Framework 4. x) para o .NET Core. O ASP.NET Web Forms desenvolvedores se beneficiarão deste guia, mas também deverá ler o mais alto [para desenvolvedores de Web Forms ASP.net](https://docs.microsoft.com/dotnet/architecture/blazor-for-web-forms-developers/) , e-book.

Um público-alvo secundário são os tomadores de decisões técnicas que planejam quando mover seus aplicativos para o .NET Core.

O público-alvo deste livro são os desenvolvedores .NET com aplicativos grandes e existentes que são executados no ASP.NET MVC e na API da Web. Os aplicativos criados no ASP.NET Web Forms estão fora do foco deste livro, embora grande parte das informações comparando .NET Framework e .NET Core ainda seja relevante.

## <a name="how-you-can-use-this-guide"></a>Como você pode usar este guia

Você pode ler este livro diretamente, pois esperamos que muitos leitores façam. Este livro fornecerá primeiro as considerações sobre se você deve portar seu aplicativo. Esse conteúdo é seguido por diferenças de arquitetura entre o .NET Framework e o .NET Core. A partir daí, você aprenderá estratégias para migrar uma solução grande ao longo do tempo e como portar um aplicativo real. Em seguida, o livro inclui cenários de implantação que abordam a necessidade de executar aplicativos diferentes enquanto aparecem como um único aplicativo para os usuários. O livro termina com dois estudos de caso que descrevem aplicativos reais que foram migrados do ASP.NET MVC para o ASP.NET Core.

Se você optar por começar do primeiro capítulo, poderá fazer referência a qualquer um desses capítulos para saber mais sobre conceitos específicos:

- [Diferenças de arquitetura](architectural-differences.md)
- [Migrar soluções grandes](migrate-large-solutions.md)
- [Migração de exemplo](example-migration-eshop.md)
- [Cenários de implantação](deployment-scenarios.md)

Este guia está disponível em [formato PDF](https://aka.ms/aspnet-porting-ebook) e online. Sinta-se à vontade para encaminhar este documento ou links para sua versão online para sua equipe a fim de garantir uma compreensão comum desses conceitos.

## <a name="send-your-feedback"></a>Envie seus comentários

Este livro e exemplos relacionados estão em constante evolução, para que seus comentários sejam bem-vindos! Se você tiver comentários sobre como esse livro pode ser melhorado, use a seção de comentários na parte inferior de qualquer página criada com base nos [problemas do GitHub](https://github.com/dotnet/docs/issues).

>[!div class="step-by-step"]
>[Próximo](introduction.md)
