---
title: Arquitetando aplicativos .NET nativos de nuvem para o Azure
description: Um guia para a criação de aplicativos nativos de nuvem que aproveitam contêineres, microservices e recursos sem servidor do Azure.
author: ardalis
ms.date: 01/19/2021
ms.openlocfilehash: ad641517f9dc24aed9180cf6a092f4754739bceb
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506117"
---
# <a name="architecting-cloud-native-net-applications-for-azure"></a>Arquitetando aplicativos .NET nativos de nuvem para o Azure

![imagem da capa](./media/cover.png)

**Edição v 1.0.2**

Consulte o [changelog](https://aka.ms/cn-ebook-changelog) para obter as atualizações do livro e as contribuições da Comunidade.

PUBLICADO POR

Divisão de Desenvolvedores Microsoft, equipes dos produtos .NET e Visual Studio

Uma divisão da Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright &copy; 2021 da Microsoft Corporation

Todos os direitos reservados. Nenhuma parte do conteúdo deste guia pode ser reproduzida ou transmitida de nenhuma forma nem por nenhum meio sem a permissão por escrito do publicador.

Este livro é fornecido “no estado em que se encontra” e expressa os pontos de vista e as opiniões do autor. Os pontos de vista, as opiniões e as informações expressos neste livro, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.

 Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios. Nenhuma associação ou conexão real é intencional ou deve ser inferida.

A Microsoft e as marcas listadas em <https://www.microsoft.com> na página da Web "Marcas" são marcas comerciais do grupo de empresas Microsoft.

Mac e macOS são marcas comerciais da Apple Inc.

O logotipo de redistribuição do Docker é uma marca registrada do Docker, Inc. usada pela permissão.

Todas as outras marcas e logotipos são propriedade de seus respectivos proprietários.

Autores:

> **Rob Vettor**, arquiteto de sistema de nuvem principal/arquiteto de IP- [thinkingincloudnative.com](https://thinkingincloudnative.com/about/), Microsoft
>
> **Steve "ardalis" Smith**, arquiteto de software e instrutor- [Ardalis.com](https://ardalis.com)

Participantes e revisores:

> **Cesar de la Torre**, gerente de programa principal, equipe do .net, Microsoft
>
> **Nish Anil**, gerente de programas sênior, equipe do .net, Microsoft
>
> **Jeremy Likness**, gerente de programas sênior, equipe do .net, Microsoft
>
> **Cecil Phillip**, defensora da nuvem sênior, Microsoft
>
> **Pedro Ghosh**, consultor principal da Neudesic

Editores:

> **Maira Wenzel**, gerente de programas, equipe do .net, Microsoft

> **David Pinheiro**, desenvolvedor de conteúdo sênior, documentos do .net, Microsoft

## <a name="version"></a>Versão

Este guia foi escrito para abranger a versão do **.NET 5** junto com muitas atualizações adicionais relacionadas à mesma "onda" de tecnologias (isto é, Azure e tecnologias de terceiros adicionais) que coincidem no tempo com a versão do .NET 5.

## <a name="who-should-use-this-guide"></a>Quem deve usar este guia

O público-alvo deste guia é, principalmente, desenvolvedores, líderes de desenvolvimento e arquitetos interessados em aprender a criar aplicativos projetados para a nuvem.

Um público-alvo secundário são responsáveis pelas decisões técnicas que planejam escolher se desejam criar seus aplicativos usando uma abordagem nativa de nuvem.

## <a name="how-you-can-use-this-guide"></a>Como você pode usar este guia

Este guia começa definindo a nuvem nativa e introduzindo um aplicativo de referência criado usando princípios e tecnologias nativas de nuvem. Além desses dois primeiros capítulos, o restante do livro é dividido em capítulos específicos focados em tópicos comuns à maioria dos aplicativos nativos de nuvem. Você pode ir para qualquer um desses capítulos para saber mais sobre abordagens nativas de nuvem para:

- Dados e acesso a dados
- Padrões de comunicação
- Dimensionamento e escalabilidade
- Resiliência do aplicativo
- Monitoramento e integridade
- Identidade e segurança
- DevOps

Este guia está disponível em formato [PDF](https://dotnet.microsoft.com/download/e-book/cloud-native-azure/pdf) e online. Fique à vontade para encaminhar este documento ou links para sua versão online para sua equipe para ajudar a garantir uma compreensão comum desses tópicos. A maioria desses tópicos se beneficia de uma compreensão consistente dos princípios e padrões subjacentes, bem como das compensações envolvidas em decisões relacionadas a esses tópicos. Nosso objetivo com este documento é equipar equipes e seus líderes com as informações de que precisam para tomar decisões bem informadas sobre a arquitetura, o desenvolvimento e a hospedagem dos seus aplicativos.

## <a name="send-your-feedback"></a>Envie seus comentários

Este livro e exemplos relacionados estão em constante evolução, para que seus comentários sejam bem-vindos! Se você tiver comentários sobre como esse livro pode ser melhorado, use a seção de comentários na parte inferior de qualquer página criada com base nos [problemas do GitHub](https://github.com/dotnet/docs/issues).

>[!div class="step-by-step"]
>[Próximo](introduction.md)
