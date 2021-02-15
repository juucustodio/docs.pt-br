---
title: Estratégias para migrar durante a execução na produção
description: Talvez não seja tenable migrar um aplicativo grande do ASP.NET MVC para ASP.NET Core tudo de uma só vez. Aprenda algumas estratégias para migrar um aplicativo para ASP.NET Core ao mesmo tempo em que os mantém em execução e em produção para os usuários existentes.
author: ardalis
ms.date: 11/13/2020
ms.openlocfilehash: be2016ab1faf3dc79f16c8d6219a670a74dc9cbd
ms.sourcegitcommit: 10e719780594efc781b15295e499c66f316068b8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/14/2021
ms.locfileid: "100488477"
---
# <a name="strategies-for-migrating-while-running-in-production"></a>Estratégias para migrar durante a execução na produção

Muitas equipes têm .NET Framework aplicativos que planejam migrar para o .NET Core, mas o aplicativo é tão grande que a migração requer uma quantidade significativa de tempo para ser concluída. O aplicativo original precisa residir enquanto a migração é feita por parte. Precisa haver uma maneira para as versões antigas e novas do aplicativo trabalharem juntas lado a lado, ou para que a versão antiga seja migrada no local, pelo menos algumas das formas, sem interrupções. As equipes podem empregar várias estratégias diferentes para dar suporte a essas metas.

## <a name="refactor-the-net-framework-solution"></a>Refatorar a solução de .NET Framework

Um bom lugar para começar se você planeja portar um aplicativo .NET Framework para o .NET Core é refatorá-lo para funcionar melhor com o .NET Core. Isso significa atualizar bibliotecas de classes individuais para direcionar .NET Standard e mover a maior parte da lógica de seus projetos ASP.NET MVC e para essas bibliotecas de classes. Qualquer código que você tenha em bibliotecas de .NET Standard deve se mover relativamente facilmente do .NET Framework para o .NET Core.

Ao refatorar, verifique se você está seguindo os conceitos básicos de refatoração. Por exemplo, crie testes que verifiquem o que o sistema faz antes de iniciar a refatoração. Execute estes testes quando terminar de confirmar que não alterou o comportamento do sistema. Talvez seja necessário adicionar testes de caracterização ao sistema se você ainda não tiver um bom pacote de testes automatizados nos quais pode confiar.

## <a name="extract-front-end-assets-to-a-cdn"></a>Extrair ativos de front-end para uma CDN

Se seus aplicativos .NET Framework incluírem muitos ativos estáticos, como scripts, arquivos CSS ou imagens, você poderá migrá-los para uma CDN separada. Em seguida, atualize o aplicativo existente para fazer referência aos links da CDN para esses ativos. Quando você porta o aplicativo para o .NET Core, esses arquivos estáticos não fazem parte da migração e você só continuará fazendo referência a eles da CDN no aplicativo ASP.NET Core.

## <a name="extract-and-migrate-individual-microservices"></a>Extrair e migrar microserviços individuais

Grandes .NET Framework aplicativos já podem ser compostos por sistemas front-end separados que podem ser migrados individualmente. Ou podem ser candidatos à migração para uma arquitetura de microserviços, com algumas partes de aplicativos MVC ASP.NET existentes sendo obtidos em novas implementações de microserviço ASP.NET Core. Você pode aprender mais sobre os microserviços no ebook eletrônico associado, [microservices do .net: arquitetura para aplicativos .net em contêineres](https://aka.ms/microservicesebook).

Por exemplo, o aplicativo existente pode ter um conjunto de recursos que ele usa relacionado à entrada e ao registro do usuário. Eles podem ser migrados para um microserviço separado, que poderia ser compilado e implantado usando ASP.NET Core e, em seguida, integrado ao aplicativo herdado .NET Framework. Em seguida, o aplicativo pode ter algumas páginas dedicadas para acompanhar o carrinho de compras do usuário individual. Essas páginas também podem ser extraídas em seu próprio microserviço separado e novamente integradas ao aplicativo existente. Dessa forma, o aplicativo .NET Framework original continua executando em produção, mas com mais e mais de seus recursos provenientes de microserviços do .NET Core modernos.

## <a name="deploy-multiple-versions-of-the-app-side-by-side-in-iis"></a>Implantar várias versões do aplicativo lado a lado no IIS

Usando uma combinação de cabeçalhos e redirecionamentos de host, um aplicativo MVC existente do ASP.NET pode ser configurado para ser executado lado a lado com um aplicativo ASP.NET Core no mesmo servidor IIS. Como partes de funcionalidade, como controladores individuais, são portadas para ASP.NET Core, suas rotas e URLs são mapeadas no IIS para direcionar o ASP.NET Core site ou o subaplicativo (os diretórios virtuais do IIS não têm suporte com aplicativos ASP.NET Core). Um aplicativo ASP.NET Core pode ser hospedado como um subaplicativo IIS (sub-app). A parte do caminho do subaplicativo se torna parte da URL raiz do aplicativo.

## <a name="apply-the-strangler-pattern"></a>Aplicar o padrão Estrangulador

Aplicativos grandes do ASP.NET MVC podem ser substituídos gradualmente por um novo aplicativo ASP.NET Core por meio da migração incremental de partes da funcionalidade. Uma abordagem para isso é chamada de [padrão Estrangulador](https://docs.microsoft.com/azure/architecture/patterns/strangler), chamado para Estrangulador Vines que Strangle e eventualmente subdividir árvores. Essa abordagem se baseia na primeira implementação de uma camada de fachada sobre a solução existente. Essa fachada deve ser criada usando a nova abordagem para o problema ou uma solução fora do mercado, como um gateway de API.

Quando a fachada estiver em vigor, você poderá encaminhar parte dela para um novo aplicativo ASP.NET Core. Ao portar mais do aplicativo de .NET Framework original para o .NET Core, você continuará atualizando a camada de fachada de forma adequada, enviando mais da funcionalidade total do façade's para o novo sistema. A Figura 3-5 mostra a progressão do padrão Estrangulador ao longo do tempo.

## <a name="multi-targeting-approaches"></a>Abordagens de vários destinos

Os aplicativos grandes que visam .NET Framework podem ser migrados para ASP.NET Core ao longo do tempo usando vários caminhos de código e separados para cada estrutura. Por exemplo, o código que deve ser executado em ambos os ambientes poderia ser modificado com diretivas de [pré-processador `#if` ](https://docs.microsoft.com/dotnet/csharp/language-reference/preprocessor-directives/preprocessor-if) para implementar diferentes funcionalidades ou usar dependências diferentes quando executado em .NET Framework em vez do .NET Core. Outra opção é modificar arquivos de projeto para incluir diferentes conjuntos de arquivos com base em qual estrutura está sendo direcionada. Os arquivos de projeto podem usar diferentes padrões de mascaramento, como `*.core.cs` , para incluir diferentes conjuntos de arquivos de origem, dependendo da estrutura que está sendo direcionada.

Essas técnicas permitem que uma única base de código comum seja mantida enquanto a nova funcionalidade é adicionada e (partes do) o aplicativo é portado para usar o .NET Core.

![Figura 3-5](media/Figure3-5.png)

**Figura 3-5.** O padrão Estrangulador ao longo do tempo.

Eventualmente, toda a camada de fachada corresponde à nova e moderna implementação. Neste ponto, o sistema herdado e a camada de face podem ser desativados.

## <a name="summary"></a>Resumo

Frequentemente, grandes ASP.NET MVC e aplicativos de API Web não serão portados para ASP.NET Core de uma só vez, mas serão migrados incrementalmente ao longo do tempo. Esta seção oferece várias estratégias para executar essa migração incremental. Escolha os um que funcionarão melhor para sua organização e aplicativo.

## <a name="references"></a>Referências

- [Microserviços .NET: arquitetura para aplicativos .NET em contêineres](https://aka.ms/microservicesebook)
- [Aplicativo de microserviços de referência do eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers)
- [Hospedar o ASP.NET Core no Windows com o IIS](https://docs.microsoft.com/aspnet/core/host-and-deploy/iis/)
- [Padrão do Estrangulador](https://docs.microsoft.com/azure/architecture/patterns/strangler)

>[!div class="step-by-step"]
>[Anterior](understand-update-dependencies.md) 
> [Avançar](example-migration-eshop.md)
