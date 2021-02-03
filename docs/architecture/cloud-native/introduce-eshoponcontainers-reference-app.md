---
title: Introdução ao aplicativo de referência do eShopOnContainers
description: Apresentando o aplicativo de referência de microserviços nativos do eShopOnContainers Cloud para ASP.NET Core e o Azure.
ms.date: 01/19/2021
ms.openlocfilehash: 35aa92794d8488c3de60f42af52654c4c26aad82
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99505668"
---
# <a name="introducing-eshoponcontainers-reference-app"></a>Introdução ao aplicativo de referência do eShopOnContainers

A Microsoft, em parceria com especialistas líderes da Comunidade, produziu um aplicativo de referência de microserviços nativos de nuvem com recursos completos, eShopOnContainers. Esse aplicativo foi criado para demonstrar o uso do .NET e do Docker e, opcionalmente, do Azure, do kubernetes e do Visual Studio, para criar uma vitrine online.

![Captura de tela do aplicativo de exemplo eShopOnContainers.](./media/eshoponcontainers-sample-app-screenshot.png)

**Figura 2-1**. Captura de tela do aplicativo de exemplo eShopOnContainers.

Antes de iniciar este capítulo, recomendamos que você baixe o [aplicativo de referência eShopOnContainers](https://github.com/dotnet-architecture/eShopOnContainers). Se você fizer isso, deverá ser mais fácil acompanhar as informações apresentadas.

## <a name="features-and-requirements"></a>Recursos e requisitos

Vamos começar com uma análise dos recursos e requisitos do aplicativo. O aplicativo eShopOnContainers representa uma loja online que vende vários produtos físicos, como camisetas e café Mugs. Se você comprou algo online antes, a experiência de usar a loja deve ser relativamente familiar. Aqui estão alguns dos recursos básicos que o armazenamento implementa:

- Listar itens do catálogo
- Filtrar itens por tipo
- Filtrar itens por marca
- Adicionar itens à cesta de compras
- Editar ou remover itens da cesta
- Check-out
- Registrar uma conta
- Entrar
- Sair
- Revisar pedidos

O aplicativo também tem os seguintes requisitos não funcionais:

- Ele precisa ser altamente disponível e deve ser dimensionado automaticamente para atender ao maior tráfego (e reduzir verticalmente depois que o tráfego é sublado).
- Ele deve fornecer monitoramento fácil de usar de seus logs de integridade e diagnóstico para ajudar a solucionar quaisquer problemas encontrados.
- Ele deve dar suporte a um processo de desenvolvimento ágil, incluindo suporte para integração e implantação contínuas (CI/CD).
- Além dos dois front-ends da Web (aplicativo tradicional e de página única), o aplicativo também deve oferecer suporte a aplicativos cliente móveis que executam diferentes tipos de sistemas operacionais.
- Ele deve dar suporte a hospedagem de plataforma cruzada e desenvolvimento de plataforma cruzada.

![eShopOnContainers referência arquitetura de desenvolvimento de aplicativos.](./media/eshoponcontainers-development-architecture.png)

**Figura 2-2**. eShopOnContainers referência arquitetura de desenvolvimento de aplicativos.

O aplicativo eShopOnContainers pode ser acessado de clientes Web ou móveis que acessam o aplicativo via HTTPS direcionando o aplicativo do servidor MVC ASP.NET Core ou um gateway de API apropriado. Os gateways de API oferecem várias vantagens, como desacoplar serviços de back-end de clientes front-end individuais e fornecer maior segurança. O aplicativo também usa um padrão relacionado conhecido como back-ends-para-Fronts (BFF), que recomenda a criação de gateways de API separados para cada cliente front-end. A arquitetura de referência demonstra a divisão dos gateways de API com base em se a solicitação é proveniente de um cliente Web ou móvel.

A funcionalidade do aplicativo é dividida em muitos microserviços distintos. Há serviços responsáveis por autenticação e identidade, listando itens do catálogo de produtos, gerenciando cestas de compras de usuários e colocando pedidos. Cada um desses serviços separados tem seu próprio armazenamento persistente. Não há um só armazenamento de dados mestre com o qual todos os serviços interagem. Em vez disso, a coordenação e a comunicação entre os serviços são feitas de acordo com a necessidade e por meio de um barramento de mensagem.

Cada um dos diferentes microservices é projetado de forma diferente, com base em seus requisitos individuais. Esse aspecto significa que sua pilha de tecnologia pode diferir, embora todas sejam compiladas usando o .NET e projetadas para a nuvem. Os serviços mais simples fornecem acesso básico de criação-leitura-atualização-exclusão (CRUD) aos armazenamentos de dados subjacentes, enquanto os serviços mais avançados usam Domain-Driven abordagens e padrões de design para gerenciar a complexidade dos negócios.

![Diferentes tipos de microserviços](./media/different-kinds-of-microservices.png)

**Figura 2-3**. Tipos diferentes de microserviços.

## <a name="overview-of-the-code"></a>Visão geral do código

Como ele usa microservices, o aplicativo eShopOnContainers inclui alguns projetos e soluções separados em seu repositório GitHub. Além de soluções separadas e arquivos executáveis, os vários serviços são projetados para serem executados dentro de seus próprios contêineres, durante o desenvolvimento local e em tempo de execução em produção. A Figura 2-4 mostra a solução completa do Visual Studio, na qual os vários projetos diferentes são organizados.

![Projetos na solução do Visual Studio.](./media/projects-in-visual-studio-solution.png)

**Figura 2-4**. Projetos na solução do Visual Studio.

O código é organizado para dar suporte aos diferentes microserviços e, em cada microserviço, o código é dividido na lógica do domínio, em questões de infraestrutura e na interface do usuário ou ponto de extremidade de serviço. Em muitos casos, as dependências de cada serviço podem ser atendidas pelos serviços do Azure em produção e opções alternativas para o desenvolvimento local. Vamos examinar como os requisitos do aplicativo são mapeados para os serviços do Azure.

## <a name="understanding-microservices"></a>Noções básicas sobre microsserviços

Este livro se concentra em aplicativos nativos de nuvem criados usando a tecnologia do Azure. Para saber mais sobre as práticas recomendadas de microserviço e como arquitetar aplicativos baseados em microserviço, leia o livro complementar, [microservices .net: arquitetura para aplicativos .net em contêineres](https://dotnet.microsoft.com/download/thank-you/microservices-architecture-ebook).

>[!div class="step-by-step"]
>[Anterior](candidate-apps.md) 
> [Avançar](map-eshoponcontainers-azure-services.md)
