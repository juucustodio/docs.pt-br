---
title: Abordagens de implantação de arquitetura-aplicativos sem servidor
description: Um guia para diferentes maneiras como as arquiteturas empresariais são implantadas na nuvem, com comparação entre IaaS, PaaS, contêineres e sem servidor.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 06/26/2018
ms.openlocfilehash: 89a8e6a52331b563be334a867f563e9ded8d8cc4
ms.sourcegitcommit: 7e42488c2f8f63f6d499b5f8fb1dec5bac9ad254
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/28/2021
ms.locfileid: "98957956"
---
# <a name="architecture-deployment-approaches"></a>Abordagens de implantação de arquitetura

Independentemente da abordagem de arquitetura usada para criar um aplicativo de negócios, a implementação ou a implantação desses aplicativos pode variar. Os negócios hospedam aplicativos em tudo, desde hardware físico até funções sem servidor.

## <a name="n-tier-applications"></a>Aplicativos de N camadas

O [padrão de arquitetura de N camadas](/azure/architecture/guide/architecture-styles/n-tier) é uma arquitetura madura e simplesmente se refere a aplicativos que separam várias camadas lógicas em camadas físicas separadas. A arquitetura de n camadas é uma implementação física da arquitetura de N camadas. A implementação mais comum dessa arquitetura inclui:

- Uma camada de apresentação, por exemplo, um aplicativo Web.
- Uma API ou uma camada de acesso a dados, como uma API REST.
- Uma camada de dados, como um banco de dado SQL.

![Arquitetura de N camadas](./media/n-tier-architecture.png)

As soluções de N camadas têm as seguintes características:

- Normalmente, os projetos são alinhados com camadas.
- O teste pode ser abordado de forma diferente por camada.
- As camadas fornecem camadas de abstração, por exemplo, a camada de apresentação normalmente é que desconhecem dos detalhes de implementação da camada de dados.
- Normalmente, as camadas só interagem com camadas adjacentes.
- As versões geralmente são gerenciadas no projeto e, portanto, camada, nível. Uma simples alteração de API pode exigir uma nova versão de uma camada intermediária inteira.

Essa abordagem fornece vários benefícios, incluindo:

- Isolamento do banco de dados (geralmente o front-end não tem acesso direto ao back-end do banco de dados).
- A reutilização da API (por exemplo, clientes móveis, de área de trabalho e de aplicativos Web pode reutilizar as mesmas APIs).
- Capacidade de escalar horizontalmente camadas de forma independente.
- Isolamento de refatoração: uma camada pode ser Refatorada sem afetar outras camadas.

## <a name="on-premises-and-infrastructure-as-a-service-iaas"></a>Local e infraestrutura como serviço (IaaS)

A abordagem tradicional para hospedar aplicativos requer a compra de hardware e o gerenciamento de todas as instalações de software, incluindo o sistema operacional. Originalmente, isso envolvia data centers caros e hardware físico. Os desafios que acompanham o hardware físico operacional são muitos, incluindo:

- A necessidade de comprar em excesso para cenários de demanda "apenas no caso" ou de pico.
- Proteção do acesso físico ao hardware.
- Responsabilidade por falha de hardware (como falha de disco).
- Cool.
- Configurando roteadores e balanceadores de carga.
- Redundância de energia.
- Proteção do acesso ao software.

![Abordagem de IaaS](./media/iaas-approach.png)

A virtualização de hardware, por meio de "máquinas virtuais", permite a infraestrutura como um serviço (IaaS). As máquinas host são efetivamente particionadas para fornecer recursos a instâncias com alocações para sua própria memória, CPU e armazenamento. A equipe provisiona as VMs necessárias e configura as redes associadas e o acesso ao armazenamento.

Para obter mais informações, consulte [arquitetura de referência de N camadas da máquina virtual](/azure/architecture/reference-architectures/virtual-machines-windows/n-tier).

Embora a virtualização e a infraestrutura como serviço (IaaS) resolvam muitas preocupações, ela ainda deixa muita responsabilidade nas mãos da equipe de infraestrutura. A equipe mantém versões do sistema operacional, aplica patches de segurança e instala dependências de terceiros nos computadores de destino. Os aplicativos geralmente se comportam de modo diferente em máquinas de produção em comparação com o ambiente de teste Problemas surgem devido a diferentes versões de dependência e/ou níveis de SKU do sistema operacional. Embora muitas organizações implantem aplicativos de N camadas para esses destinos, muitas empresas se beneficiam da implantação em um modelo nativo de nuvem, como [a plataforma como um serviço](#platform-as-a-service-paas). As arquiteturas com microserviços são mais desafiadoras devido aos requisitos de expansão para elasticidade e resiliência.

Para obter mais informações, consulte [máquinas virtuais](/azure/virtual-machines/).

## <a name="platform-as-a-service-paas"></a>PaaS (plataforma como serviço)

A PaaS (plataforma como serviço) oferece soluções configuradas que os desenvolvedores podem conectar diretamente. PaaS é outro termo para hospedagem gerenciada. Ele elimina a necessidade de gerenciar o sistema operacional base, os patches de segurança e, em muitos casos, qualquer dependência de terceiros. Exemplos de plataformas incluem aplicativos Web, bancos de dados e back-ends móveis.

A PaaS aborda os desafios comuns ao IaaS. A PaaS permite que o desenvolvedor se concentre no esquema de banco de dados ou código em vez de como ele é implantado. Os benefícios do PaaS incluem:

- Pague por modelos de uso que eliminem a sobrecarga de investir em computadores ociosos.
- Implantação direta e pipelines aprimorados de DevOps, integração contínua (CI) e entrega contínua (CD).
- Atualizações automáticas, atualizações e patches de segurança.
- Expansão e escala vertical do botão de ação (escala elástica).

A principal desvantagem do PaaS tradicionalmente foi o bloqueio do fornecedor. Por exemplo, alguns provedores de PaaS oferecem suporte apenas a ASP.NET, Node.js ou outras linguagens e plataformas específicas. Produtos como Azure App serviço evoluíram para abordar várias plataformas e dar suporte a uma variedade de linguagens e estruturas para hospedar aplicativos Web.

![Arquitetura de plataforma como serviço](./media/paas-architecture.png)

## <a name="software-as-a-service-saas"></a>SaaS (software como serviço)

Software como serviço ou SaaS é centralmente hospedado e disponível sem instalação ou provisionamento local. O SaaS geralmente é hospedado em cima da PaaS como uma plataforma para a implantação de software. O SaaS fornece serviços para execução e conexão com o software existente. Em geral, o SaaS é específico do setor e da vertical. O SaaS geralmente é licenciado e geralmente fornece um modelo de cliente/servidor. A maioria das ofertas de SaaS modernas usam aplicativos baseados na Web para o cliente. As empresas normalmente consideram o SaaS como uma solução de negócios para ofertas de licença. Geralmente, ele não é implementado como consideração de arquitetura para escalabilidade e capacidade de manutenção de um aplicativo. Na verdade, a maioria das soluções de SaaS baseia-se em IaaS, PaaS e/ou back-ends sem servidor.

Saiba mais sobre o SaaS por meio de um [aplicativo de exemplo](/azure/sql-database/saas-tenancy-welcome-wingtip-tickets-app).

## <a name="containers-and-functions-as-a-service-faas"></a>Contêineres e funções como serviço (FaaS)

Contêineres são uma solução interessante que permite benefícios semelhantes a PaaS sem a sobrecarga de IaaS. Um contêiner é, essencialmente, um tempo de execução que contém o básico, que é necessário para executar um aplicativo exclusivo. O kernel ou a parte principal do sistema operacional do host e serviços como armazenamento são compartilhados em um host. O kernel compartilhado permite que os contêineres sejam leves (alguns são meros megabytes de tamanho, em comparação com o tamanho de Gigabyte de máquinas virtuais típicas). Com os hosts já em execução, os contêineres podem ser iniciados rapidamente, facilitando a alta disponibilidade. A capacidade de criar contêineres rapidamente também fornece camadas extras de resiliência. O Docker é uma das implementações mais populares de contêineres.

Os benefícios dos contêineres incluem:

- Leve e portátil
- Independente, portanto, não é necessário instalar dependências
- Fornecer um ambiente consistente independentemente do host (executado exatamente igual em um laptop, como em um servidor de nuvem)
- Pode ser provisionado rapidamente para expansão
- Pode ser reiniciado rapidamente para se recuperar de uma falha

Um contêiner é executado em um host de contêiner (que, por sua vez, pode ser executado em um computador bare-metal ou uma máquina virtual). Vários contêineres ou instâncias dos mesmos contêineres podem ser executados em um único host. Para failover e resiliência reais, os contêineres devem ser dimensionados entre os hosts.

Para obter mais informações sobre contêineres do Docker, consulte [o que é o Docker](../microservices/container-docker-introduction/docker-defined.md).

O gerenciamento de contêineres em hosts normalmente requer uma ferramenta de orquestração como kubernetes. Configurar e gerenciar soluções de orquestração pode adicionar sobrecarga e complexidade adicionais aos projetos. Felizmente, muitos provedores de nuvem fornecem serviços de orquestração por meio de soluções PaaS para simplificar o gerenciamento de contêineres.

A imagem a seguir ilustra um exemplo de instalação do kubernetes. Nós no endereço de instalação scale out and failover. Eles executam instâncias de contêiner do Docker que são gerenciadas pelo servidor primário. O *kubelet* é o cliente que retransmite comandos do kubernetes para o Docker.

![Kubernetes](./media/kubernetes-example.png)

Para obter mais informações sobre orquestração, consulte [kubernetes no Azure](/azure/aks/intro-kubernetes).

O FaaS (funções como serviço) é um serviço de contêiner especializado que é semelhante a sem servidor. Uma implementação específica do FaaS, chamada [OpenFaaS](https://github.com/openfaas/faas), se encontra na parte superior dos contêineres para fornecer recursos sem servidor. O OpenFaaS fornece modelos que empacotam todas as dependências de contêiner necessárias para executar um trecho de código. O uso de modelos simplifica o processo de implantação de código como uma unidade funcional. O OpenFaaS visa arquiteturas que já incluem contêineres e orquestradores porque ele pode usar a infraestrutura existente. Embora ele forneça funcionalidade sem servidor, ele exige especificamente que você use o Docker e um Orchestrator.

## <a name="serverless"></a>Sem servidor

Uma arquitetura sem servidor fornece uma clara separação entre o código e seu ambiente de hospedagem. Você implementa o código em uma *função* que é invocada por um *gatilho*. Depois que a função é encerrada, todos os recursos necessários podem ser liberados. O gatilho pode ser manual, um processo cronometrado, uma solicitação HTTP ou um upload de arquivo. O resultado do gatilho é a execução do código. Embora as plataformas sem servidor variem, a maioria fornece acesso a APIs e associações predefinidas para simplificar tarefas como gravar em um banco de dados ou enfileirar resultados.

Sem servidor é uma arquitetura que depende muito da abstração do ambiente de host para se concentrar no código. Pode ser considerado *menos servidor*.

As soluções de contêiner fornecem aos desenvolvedores scripts de Build existentes para publicar código em imagens prontas para servidor. Outras implementações usam soluções PaaS existentes para fornecer uma arquitetura escalonável.

A abstração significa que a equipe de DevOps não precisa provisionar ou gerenciar servidores nem contêineres específicos. A plataforma sem servidor hospeda o código, como um script ou executáveis empacotados criados com um SDK relacionado, e aloca os recursos necessários para que o código seja dimensionado.

Os diagramas de ilustração a seguir têm quatro componentes sem servidor. Uma solicitação HTTP faz com que o código da API de check-out seja executado. A API de check-out insere o código em um banco de dados, e a inserção dispara várias outras funções para executar tarefas como tarefas de computação e cumprir o pedido.

![Implementação sem servidor](./media/serverless-implementation.png)

As vantagens da inclusão sem servidor:

- **Alta densidade.** Muitas instâncias do mesmo código sem servidor podem ser executadas no mesmo host em comparação com contêineres ou máquinas virtuais. A escala de instâncias em vários hosts aumenta e resiliência.
- **Microcobrança.** A maioria dos provedores sem servidor cobra com base nas execuções sem servidor, permitindo uma economia de custos massiva em determinados cenários.
- **Escala instantânea.** O servidor não pode ser dimensionado para corresponder cargas de trabalho de forma automática e rápida.
- **Tempo de colocação no mercado mais rápido.** Os desenvolvedores se concentram no código e implantam diretamente na plataforma sem servidor. Os componentes podem ser liberados independentemente um do outro.

O servidor não é mais frequentemente discutido no contexto de computação, mas também pode se aplicar aos dados. Por exemplo, o [Azure SQL](/azure/sql-database) e o [Cosmos DB](/azure/cosmos-db) fornecem bancos de dados de nuvem que não exigem a configuração de máquinas host ou clusters. Este livro se concentra na computação sem servidor.

## <a name="summary"></a>Resumo

Há um amplo espectro de opções disponíveis para arquitetura, incluindo uma abordagem híbrida. O servidor simplifica a abordagem, o gerenciamento e o custo dos recursos do aplicativo às custas de controle e portabilidade. No entanto, muitas plataformas sem servidor expõem a configuração para ajudar a ajustar a solução. Boas práticas de programação também podem levar a um código mais portátil e menos o bloqueio de plataforma sem servidor. A tabela a seguir ilustra as abordagens de arquitetura lado a lado. Escolha sem servidor com base nas suas necessidades de dimensionamento, se você deseja ou não gerenciar o tempo de execução e como você pode dividir suas cargas de trabalho em pequenos componentes. Você aprenderá sobre possíveis desafios com pontos de decisão sem servidor e outros no próximo capítulo.

|         |IaaS     |PaaS     |Contêiner|Sem servidor|
|---------|---------|---------|---------|----------|
|**Escala**|VM       |Instância |Aplicativo      |Função  |
|**Abstrai**|Hardware|Plataforma|Host do sistema operacional|Runtime   |
|**Unidade** |VM       |Project  |Imagem    |Código      |
|**Tempo de vida**|Months|Dias para meses|Minutos a dias|Milissegundos a minutos|
|**Responsabilidade**|Aplicativos, dependências, tempo de execução e sistema operacional|Aplicativos e dependências|Aplicativos, dependências e tempo de execução|Função

- A **escala** se refere à unidade usada para dimensionar o aplicativo
- Os **resumos** referem-se à camada que é abstrata pela implementação
- **Unidade** refere-se ao escopo do que está implantado
- Tempo de **vida** refere-se ao tempo de execução típico de uma instância específica
- **Responsabilidade** refere-se à sobrecarga para criar, implantar e manter o aplicativo

O próximo capítulo se concentrará em arquitetura sem servidor, casos de uso e padrões de design.

## <a name="recommended-resources"></a>Recursos recomendados

- [Guia de arquitetura do aplicativo do Azure](/azure/architecture/guide/)
- [Azure Cosmos DB](/azure/cosmos-db)
- [SQL do Azure](/azure/sql-database)
- [Padrão de arquitetura de N camadas](/azure/architecture/guide/architecture-styles/n-tier)
- [Kubernetes no Azure](/azure/aks/intro-kubernetes)
- [Microsserviços](/azure/architecture/guide/architecture-styles/microservices)
- [Arquitetura de referência de N camadas da máquina virtual](/azure/architecture/reference-architectures/virtual-machines-windows/n-tier)
- [Máquinas virtuais](/azure/virtual-machines/)
- [O que é o Docker?](../microservices/container-docker-introduction/docker-defined.md)
- [Aplicativo SaaS Wingtip tickets](/azure/sql-database/saas-tenancy-welcome-wingtip-tickets-app)

>[!div class="step-by-step"]
>[Anterior](architecture-approaches.md) 
> [Avançar](serverless-architecture.md)
