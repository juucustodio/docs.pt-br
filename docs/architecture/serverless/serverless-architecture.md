---
title: Arquitetura sem servidor-aplicativos sem servidor
description: Exploração de várias arquiteturas e aplicativos que têm suporte de arquiteturas sem servidor, incluindo aplicativos Web, dispositivos móveis e IoT.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: f7d80ce3957c2ad90a67ae6ba1fc2786af30fcc1
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171709"
---
# <a name="serverless-architecture"></a>Arquitetura sem servidor

Há muitas abordagens ao uso de arquiteturas sem [servidor](https://azure.com/serverless) . Este capítulo explora exemplos de arquiteturas comuns que se integram sem servidor. Ele também aborda preocupações que podem apresentar desafios adicionais ou exigir uma consideração extra ao implementar sem servidor. Por fim, são fornecidos vários exemplos de design que ilustram vários casos de uso sem servidor.

Os hosts sem servidor geralmente usam uma camada de PaaS ou baseada em contêiner existente para gerenciar as instâncias sem servidor. Por exemplo, Azure Functions se baseia no [serviço Azure app](/azure/app-service/). O serviço de aplicativo é usado para expandir instâncias e gerenciar o tempo de execução que executa Azure Functions código. Para funções baseadas no Windows, o host é executado como PaaS e dimensiona o tempo de execução do .NET. Para funções baseadas em Linux, o host aproveita contêineres.

![Arquitetura de Azure Functions](./media/azure-functions-architecture.png)

O núcleo de trabalhos Web fornece um contexto de execução para a função. O Language Runtime executa scripts, executa bibliotecas e hospeda a estrutura para o idioma de destino. Por exemplo, Node.js é usado para executar funções JavaScript e o .NET Framework é usado para executar funções C#. Você aprenderá mais sobre as opções de linguagem e plataforma mais adiante neste capítulo.

Alguns projetos podem se beneficiar com a criação de uma abordagem "tudo" para servidor. Os aplicativos que dependem muito de microservices podem implementar todos os microserviços usando a tecnologia sem servidor. A maioria dos aplicativos é híbrida, seguindo um projeto de N camadas e usando servidores para os componentes que fazem sentido, pois os componentes são modulares e escalonáveis de forma independente. Para ajudar a entender esses cenários, esta seção descreve alguns exemplos comuns de arquitetura que usam sem servidor.

## <a name="full-serverless-back-end"></a>Back-end completo sem servidor

O back-end completo sem servidor é ideal para vários tipos de cenários, especialmente ao criar aplicativos novos ou "de campo verde". Um aplicativo com uma grande área de superfície de APIs pode se beneficiar da implementação de cada API como uma função sem servidor. Aplicativos baseados na arquitetura de microserviços são outro exemplo que podem ser implementados como um back-end completo sem servidor. Os microserviços se comunicam por vários protocolos entre si. Os cenários específicos incluem:

- Produtos SaaS baseados em API (exemplo: processador de pagamentos financeiros).
- Aplicativos orientados a mensagens (exemplo: solução de monitoramento de dispositivo).
- Aplicativos focados na integração entre serviços (exemplo: aplicativo de reservas de viagens).
- Processos que são executados periodicamente (exemplo: limpeza de banco de dados baseada em temporizador).
- Aplicativos focados na transformação de dados (exemplo: importação disparada por upload de arquivo).
- Extrair processos de ETL (transformação e carregamento).

Há outros casos de uso mais específicos que são abordados posteriormente neste documento.

## <a name="monoliths-and-starving-the-beast"></a>Monolítico e "privando o fera"

Um desafio comum é migrar um aplicativo monolítico existente para a nuvem. A abordagem menos arriscada é "mover e deslocar" totalmente para máquinas virtuais. Muitas lojas preferem usar a migração como uma oportunidade de modernizar sua base de código. Uma abordagem prática para a migração é chamada de "privar o fera". Nesse cenário, o monolítico é migrado "no estado em que se encontra" para começar. Em seguida, os serviços selecionados são modernizados. Em alguns casos, a assinatura do serviço é idêntica à original: ela simplesmente é hospedada como uma função. Os clientes são atualizados para usar o novo serviço em vez do ponto de extremidade monolítico. No ínterim, as etapas como replicação de banco de dados permitem que os microserviços hospedem seu próprio armazenamento mesmo quando as transações ainda são tratadas pelo monolítico. Eventualmente, todos os clientes são migrados para os novos serviços. O monolítico é "privado" (seus serviços não são mais chamados) até que toda a funcionalidade tenha sido substituída. A combinação de proxies e sem servidor pode facilitar grande parte dessa migração.

![Migração monolítica sem servidor](./media/serverless-monolith-migration.png)

Para saber mais sobre essa abordagem, Assista ao vídeo: [traga seu aplicativo para a nuvem com Azure Functions sem servidor](https://channel9.msdn.com/Events/Connect/2017/E102).

## <a name="web-apps"></a>Aplicativos Web

Os aplicativos Web são excelentes candidatos para aplicativos sem servidor. Atualmente, há duas abordagens comuns para aplicativos Web: orientado por servidor e controlado por cliente (como um aplicativo de página única ou SPA). Aplicativos Web baseados em servidor normalmente usam uma camada de middleware para emitir chamadas de API para renderizar a interface do usuário da Web. Os aplicativos SPA fazem chamadas à API REST diretamente do navegador. Em ambos os cenários, o servidor pode acomodar o middleware ou a solicitação da API REST fornecendo a lógica comercial necessária. Uma arquitetura comum é criar um servidor Web estático leve. O aplicativo de página única (SPA) serve HTML, CSS, JavaScript e outros ativos de navegador. O aplicativo Web então se conecta a um back-end de microserviço.

## <a name="mobile-back-ends"></a>Back-ends móveis

O paradigma controlado por eventos de aplicativos sem servidor os torna ideal como back-ends móveis. O dispositivo móvel dispara os eventos e o código sem servidor é executado para atender a solicitações. Tirar proveito de um modelo sem servidor permite que os desenvolvedores aprimorem a lógica de negócios sem precisar implantar uma atualização completa do aplicativo. A abordagem sem servidor também permite que as equipes compartilhem pontos de extremidade e trabalhem em paralelo.

Os desenvolvedores móveis podem criar lógica de negócios sem se tornar especialistas no lado do servidor. Tradicionalmente, os aplicativos móveis conectados a serviços locais. Criar a camada de serviço exigida entendendo a plataforma do servidor e o paradigma de programação. Os desenvolvedores trabalharam com operações para provisionar servidores e configurá-los adequadamente. Às vezes, dias ou até mesmo semanas foram gastos na criação de um pipeline de implantação. Todos esses desafios são abordados por servidor.

Sem servidor abstrai as dependências do lado do servidor e permite que o desenvolvedor se concentre na lógica de negócios. Por exemplo, um desenvolvedor móvel que cria aplicativos usando uma estrutura JavaScript também pode criar funções sem servidor com JavaScript. O host sem servidor gerencia o sistema operacional, uma instância de Node.js para hospedar o código, as dependências de pacote e muito mais. O desenvolvedor recebe um conjunto simples de entradas e um modelo padrão para saídas. Em seguida, eles podem se concentrar na criação e no teste da lógica de negócios. Portanto, eles são capazes de usar habilidades existentes para criar a lógica de back-end para o aplicativo móvel sem precisar aprender novas plataformas ou se tornar um "desenvolvedor do lado do servidor".

![Back-end móvel sem servidor](./media/serverless-mobile-backend.png)

A maioria dos provedores de nuvem oferece produtos sem servidor baseados em móveis que simplificam todo o ciclo de vida do desenvolvimento móvel. Os produtos podem automatizar o provisionamento de bancos de dados para persistirem, lidar com preocupações DevOpss, fornecer compilações baseadas em nuvem e estruturas de teste e a capacidade de gerar scripts de processos comerciais usando a linguagem preferencial do desenvolvedor. Seguir uma abordagem sem servidor voltada para dispositivos móveis pode simplificar o processo. Sem servidor remove a enorme sobrecarga de provisionamento, configuração e manutenção de servidores para o back-end móvel.

## <a name="internet-of-things-iot"></a>Internet das coisas (IoT)

A IoT refere-se a objetos físicos que estão em rede. Às vezes, eles são chamados de "dispositivos conectados" ou "dispositivos inteligentes". Tudo, desde carros e máquinas de vendas, pode estar conectado e enviar informações que vão desde o inventário até dados de sensor, como temperatura e umidade. Na empresa, a IoT fornece melhorias de processos de negócios por meio de monitoramento e automação. Os dados de IoT podem ser usados para regulamentar o clima em um grande depósito ou acompanhar o inventário por meio da cadeia de suprimentos. A IoT pode detectar derramamentos químicos e chamar o departamento de incêndio quando a fumaça for detectada.

O enorme volume de dispositivos e informações geralmente determina uma arquitetura orientada por eventos para rotear e processar mensagens. Sem servidor é uma solução ideal por vários motivos:

- Habilita o dimensionamento conforme o volume de dispositivos e dados aumenta.
- Acomoda a adição de novos pontos de extremidade para dar suporte a novos dispositivos e sensores.
- Facilita o controle de versão independente para que os desenvolvedores possam atualizar a lógica de negócios de um dispositivo específico sem precisar implantar o sistema inteiro.
- Resiliência e menos tempo de inatividade.

A disseminação da IoT resultou em vários produtos sem servidor que se concentram especificamente em preocupações com a IoT, como o [Hub IOT do Azure](/azure/iot-hub). O servidor automatiza tarefas como registro de dispositivos, imposição de políticas, acompanhamento e até mesmo implantação de código para dispositivos na *borda*. A borda se refere a dispositivos como sensores e atuadores que estão conectados a, mas não a uma parte ativa do, à Internet.

>[!div class="step-by-step"]
>[Anterior](architecture-approaches.md) 
> [Avançar](serverless-architecture-considerations.md)
