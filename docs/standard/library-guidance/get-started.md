---
title: Introdução à criação de bibliotecas do .NET de alta qualidade
description: Introdução à criação de bibliotecas do .NET.
ms.date: 10/02/2018
ms.openlocfilehash: 10576219d8470a171ad0f1f347196999b2a2ee03
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/15/2020
ms.locfileid: "75706485"
---
# <a name="get-started"></a>Introdução

## <a name="cross-platform-targeting"></a>[Direcionamento multiplataforma](./cross-platform-targeting.md)

Como usar o .NET Standard e multiplataforma para criar bibliotecas de multiplataforma. O .NET é executado em muitos locais e boas bibliotecas do .NET devem buscar dar suporte a tantas plataformas e desenvolvedores quanto possível.

## <a name="strong-naming"></a>[Nomenclatura forte](./strong-naming.md)

Saiba mais sobre o nome forte e suas vantagens e desvantagens. Dar um nome forte a uma biblioteca .NET permite que a maioria dos desenvolvedores use-a e é uma prática recomendada.

## <a name="nuget-and-open-source-libraries"></a>[Bibliotecas do NuGet e de software livre](./nuget.md)

A melhor maneira de criar pacotes do NuGet para bibliotecas do .NET de código-fonte aberto, incluindo metadados recomendados para todos os pacotes publicamente publicados em NuGet.org.

### <a name="dependencies"></a>[Dependências](./dependencies.md)

O NuGet torna fácil usar pacotes existentes ao criar uma biblioteca do .NET. Saiba mais sobre as origens comuns de atrito de dependências do NuGet e como evitá-las.

### <a name="source-link"></a>[Source Link](./sourcelink.md)

O Source Link é uma ótima ferramenta que permite aos usuários da biblioteca .NET intervir no código-fonte durante a depuração. Este artigo é uma visão geral do que é o Source Link e por que você deve usá-lo.

### <a name="publishing"></a>[Publicando](./publish-nuget-package.md)

Embora o NuGet.org seja o repositório mais amplamente conhecido e usado, há muitos locais para publicar pacotes do NuGet. Saiba mais sobre os diferentes repositórios de pacote do NuGet disponíveis e práticas recomendadas de segurança para a publicação de uma biblioteca do .NET.

## <a name="versioning"></a>[Controle de versão](./versioning.md)

Boas bibliotecas do .NET evoluem ao longo do tempo, adicionando recursos, corrigindo bugs e melhorando o desempenho em versões posteriores. Saiba mais sobre os vários números de versão e como comunicar alterações interruptivas para os desenvolvedores.

### <a name="breaking-changes"></a>[Alterações interruptivas](./breaking-changes.md)

É importante que uma biblioteca .NET encontre um equilíbrio entre a estabilidade para usuários existentes e a inovação para o futuro. Saiba mais sobre os diferentes tipos de alterações interruptivas e estratégias para adição de novos recursos, ao mesmo tempo mantendo a compatibilidade com versões anteriores.

>[!div class="step-by-step"]
>[Anterior](index.md) 
> [Avançar](cross-platform-targeting.md)
