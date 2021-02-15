---
title: Modernizar os aplicativos existentes do .NET com a nuvem do Azure e Contêineres do Windows
description: Aprenda a migrar aplicativos usando o método lift-and-shift e modernizar os existentes para a nuvem e contêineres do Azure com este livro eletrônico.
ms.date: 01/07/2021
ms.openlocfilehash: bf6e6dff75c939508947aabeda14955b880f5a89
ms.sourcegitcommit: 5d9cee27d9ffe8f5670e5f663434511e81b8ac38
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2021
ms.locfileid: "98025460"
---
# <a name="modernize-existing-net-applications-with-azure-cloud-and-windows-containers"></a>Modernizar aplicativos .NET existentes com contêineres do Windows e nuvem do Azure

![Imagem da capa do guia Modernizar aplicativos .NET.](./media/index/web-application-guide-cover-image.png)

**Edição v 5.0**

Consulte o [changelog](https://aka.ms/modernize-ebook-changelog) para obter as atualizações do livro e as contribuições da Comunidade.

PUBLICADO pelas divisões da Microsoft Press e do Microsoft representante da Microsoft Corporation, One Microsoft Way Redmond, Washington 98052-6399

Copyright © 2021 da Microsoft Corporation

Todos os direitos reservados. Nenhuma parte do conteúdo deste guia pode ser reproduzida de nenhuma forma, nem por nenhum meio, sem a permissão por escrito do distribuidor.

Este livro está disponível gratuitamente na forma de um livro eletrônico (e-book) por meio de diversos canais da Microsoft, como <https://dot.net/architecture>.

Se você tiver dúvidas relacionadas a este livro, envie um email para [dotnet-architecture-ebooks-feedback@service.microsoft.com](mailto:dotnet-architecture-ebooks-feedback@service.microsoft.com?subject=Feedback%20for%20.NET%20Container%20&%20Microservices%20Architecture%20book) .

Este livro é fornecido “no estado em que se encontra” e expressa os pontos de vista e as opiniões do autor. Os pontos de vista, as opiniões e as informações expressos neste livro, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.

 Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios. Nenhuma associação ou conexão real é intencional ou deve ser inferida.

A Microsoft e as marcas listadas em <https://www.microsoft.com> na página da Web "Marcas" são marcas comerciais do grupo de empresas Microsoft. Todas as outras marcas são propriedade de seus respectivos proprietários.

Autor:
> **Cesar de la Torre**, Sr. pm, equipe de produtos .net, Microsoft Corp.

Participantes e revisores:
> **Scott Hunter**, diretor de parceiros, equipe do .net, Microsoft **Paul Yuknewicz**, gerente principal de PM, equipe de ferramentas do Visual Studio, Microsoft **Lisa Guthrie**, Sr. pm, equipe de ferramentas do Visual Studio, Microsoft **ankit** as, gerente principal PM, equipe do .net, Microsoft **Unai Zorrilla**, líder de desenvolvedor, conceitos simples **Javier Valero**, diretor de operações no grupo Solutio

## <a name="introduction"></a>Introdução

Quando você decidir modernizar seus serviços ou aplicativos Web e movê-los para a nuvem, você não precisará necessariamente recriar totalmente a arquitetura de seus aplicativos. Recriar a arquitetura de um aplicativo usando uma abordagem avançada como microsserviços nem sempre é uma opção devido a restrições de custo e tempo. Dependendo do tipo de aplicativo, recriar a arquitetura dele também pode não ser necessário. Para otimizar o custo-benefício da estratégia de migração na nuvem de sua organização, é importante considerar as necessidades de seus negócios e os requisitos de seus aplicativos. Você precisará determinar:

- Quais aplicativos exigem uma transformação ou recriação da arquitetura.

- Quais aplicativos precisam ser modernizado apenas parcialmente.

- Quais aplicativos podem usar a “migração lift-and-shift” diretamente para a nuvem.

## <a name="about-this-guide"></a>Sobre este guia

Este guia se concentra principalmente na modernização inicial de aplicativos Web ou orientados a serviços existentes da estrutura de Microsoft .NET, o que significa a ação de mover uma carga de trabalho para um ambiente mais novo ou moderno sem alterar significativamente o código do aplicativo e a arquitetura básica.

Este guia também destaca os benefícios de mover seus aplicativos para a nuvem e modernizar parcialmente os aplicativos usando um conjunto específico de novas tecnologias e abordagens, como Contêineres do Windows e plataformas de computação relacionadas nos Contêineres do Windows que dão suporte ao Azure.

## <a name="path-to-the-cloud-for-existing-net-applications"></a>Caminho para a nuvem para aplicativos .NET existentes

As organizações normalmente optam por mover para a nuvem devido à agilidade e à velocidade oferecida aos seus aplicativos. Você pode configurar milhares de servidores (VMs) na nuvem em questão de minutos, em comparação com as semanas de configuração de servidores locais normais.

Não há uma estratégia única e padronizada para migrar aplicativos para a nuvem. A estratégia de migração certa para você depende das necessidades e prioridades da sua organização, bem como o tipo de aplicativos que você está migrando. Nem todos os aplicativos valem o investimento de mudar para um modelo de [PaaS](https://azure.microsoft.com/overview/what-is-paas/) (plataforma como serviço) ou de desenvolver um modelo de aplicativo [nativo de nuvem](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications). Em muitos casos, você pode adotar uma abordagem em fases ou incremental para investir na movimentação de seus ativos para a nuvem, dependendo das suas necessidades de negócios.

Para aplicativos modernos com a melhor agilidade e valor a longo prazo para a organização, você pode se beneficiar de investir em arquiteturas de aplicativos *nativos da nuvem*. No entanto, para aplicativos que são ativos existentes ou herdados, é essencial gastar o mínimo possível de tempo e dinheiro (sem recriação da arquitetura ou alterações de código) ao movê-los para a nuvem, para perceber benefícios significativos.

A Figura 1-1 mostra os caminhos possíveis que podem ser escolhidos ao mover os aplicativos .NET existente para a nuvem em fases incrementais.

 ![Caminhos de modernização para aplicativos e serviços .NET existentes](./media/image1-1.png)

**Figura 1-1**. Caminhos de modernização para aplicativos e serviços .NET existentes

Cada abordagem de migração traz diferentes vantagens e motivos para usá-la. Você pode escolher uma abordagem única ao migrar aplicativos para a nuvem ou escolher certos componentes de várias abordagens. Aplicativos individuais não estão limitados a uma única abordagem ou estado de maturidade. Por exemplo, uma abordagem híbrida comum teria determinados componentes locais e outros componentes na nuvem.

A definição e a breve explicação de cada nível de maturidade do aplicativo são as seguintes:

**Nível 1: aplicativos prontos para a infraestrutura de nuvem** : nesta abordagem de migração, você apenas migra ou rehospeda seus aplicativos locais atuais para uma plataforma [IaaS](https://azure.microsoft.com/overview/what-is-iaas/)(infraestrutura como serviço). Os aplicativos têm quase a mesma composição de antes, mas agora você os implanta em VMs na nuvem.
Esse tipo simples de migração é normalmente conhecido no setor como "lift-and-shift".

**Nível 2: aplicativos otimizados na nuvem** : nesse nível e ainda sem rearquitetar ou alterar código significativo, você pode obter benefícios adicionais na execução de seu aplicativo na nuvem com tecnologias modernas, como contêineres e serviços adicionais gerenciados na nuvem. Melhore a agilidade dos seus aplicativos para distribuição mais rápida refinando seus processos de DevOps (operações de desenvolvimento) corporativas. Você obtém essa funcionalidade usando tecnologias como contêineres do Windows, que se baseiam no mecanismo do Docker. Contêineres removem a fricção que é causada pelas dependências de aplicativo ao implantar em vários estágios. Nesse modelo de maturidade, você pode implantar contêineres ou IaaS ou PaaS ao usar serviços gerenciados por nuvem adicionais relacionados a bancos de dados, cache como serviço, monitoramento e pipelines de CI/CD (integração contínua/implantação contínua).

O terceiro nível de maturidade é a meta final na nuvem, mas é opcional para muitos aplicativos e não é o foco principal deste guia:

**Nível 3: aplicativos nativos de nuvem** : essa abordagem de migração normalmente é orientada pela necessidade de negócios e tem como alvo a modernização de seus aplicativos críticos. Nesse nível, você pode usar os serviços de PaaS para mover seus aplicativos para plataformas de computação de PaaS. Implemente aplicativos [nativos da nuvem](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications) e arquitetura de microsserviços para desenvolver aplicativos com agilidade de longo prazo e dimensionar para novos limites. Esse tipo de modernização normalmente requer arquitetura específica para a nuvem. Geralmente é necessário escrever novo código, especialmente ao mover aplicativos nativos de nuvem e modelos baseados em microsserviços. Essa abordagem pode ajudar a obter os benefícios que são difíceis de obter no seu ambiente de aplicativo local e monolítico.

A Tabela 1-1 descreve as principais vantagens e motivos para escolher cada abordagem de migração ou modernização.

| **Pronto para infraestrutura de nuvem** <br /> *Lift-and-shift* | **Otimizado para a nuvem** <br /> *Modernizar* | **Nativo de nuvem** <br /> *Modernizar, rearquitetar e reescrever* |
|---|---|---|
| **Destino de computação do aplicativo** |
| Aplicativos implantados em VMs no Azure | Aplicativos monolíticos ou de N camadas implantados no Serviço de Aplicativo do Azure, ACI (Instância de Contêiner do Azure), VMs com contêineres ou AKS (Serviço de Kubernetes do Azure) | Os microsserviços em contêineres no AKS (Serviço de Kubernetes do Azure) e/ou microsserviços sem servidor com base no Azure Functions. |
| **Destino de dados** |
| SQL ou qualquer banco de dados relacional em uma VM | Instância Gerenciada do Banco de Dados SQL do Azure ou outro banco de dados gerenciado na nuvem. | Bancos de dados refinados por microsserviço, com base no Banco de Dados SQL do Azure, Azure Cosmos DB ou outro banco de dados gerenciado na nuvem |
| **Vantagens**|
| <li>Sem recriação da arquitetura, sem novo código <li> Mínimo de esforço para migração rápida <li> Mínimo denominador comum com suporte no Azure <li> Garantias básicas de disponibilidade <li> Depois de mudar para a nuvem, é mais fácil modernizar ainda mais | <li> Sem recriação da arquitetura <li> Alterações mínimas de código/configuração <li> Melhoria na implantação e agilidade de DevOps para liberação devido a contêineres <li> Aumento da densidade e redução dos custos de implantação <li> Portabilidade de aplicativos e dependências <li> Flexibilidade de destinos de host: abordagens de PaaS ou IaaS | <li> Arquiteto da nuvem, você obtém os melhores benefícios da nuvem, mas é necessário um novo código <li> Abordagens de microsserviços nativos de nuvem <li> Aplicativos críticos modernos, hiperescalonáveis e resilientes de nuvem <li> Serviços totalmente gerenciados <li> Otimizado para escala <li> Otimizado para agilidade autônoma por subsistema <li> Baseado em implantação e DevOps |
| **Desafios** |
| <li> Menor valor de nuvem, diferente da mudança em despesas operacionais ou data centers de fechamento <li> O pouco é gerenciado: sem aplicação de patch de so ou middleware; pode usar soluções de infraestrutura, como Terraform, Spinnaker ou Puppet | <li> O desenvolvimento de contêineres é uma etapa adicional na curva de aprendizado para desenvolvedores e Operações de TI <li> Os pipelines de DevOps e CI/CD geralmente são ' a ' a ' a para essa abordagem. Se não estiver presente no momento na cultura da organização, poderá ser um desafio adicional| <li> Requer a rearquitetura de aplicativos nativos de nuvem e arquiteturas de microserviço e geralmente requer refatoração significativa de código ou regravação ao modernizar (aumento de tempo e orçamento)|
> **Tabela 1-1.** Benefícios e desafios de caminhos de modernização para serviços e aplicativos .NET existentes

### <a name="key-technologies-and-architectures-by-maturity-level"></a>Principais tecnologias e arquiteturas por nível de maturidade

Aplicativos do .NET Framework inicialmente começavam com o .NET Framework versão 1.0, que foi lançado no final de 2001. Em seguida, as empresas foram movidas para versões mais recentes (como 2,0, 3,5 e .NET Framework 4. x). A maioria dos aplicativos era executada no Windows Server e no IIS (Servidor de Informações da Internet) e usava um banco de dados relacional, como o SQL Server, Oracle, MySQL ou qualquer outro RDBMS.

A maioria dos aplicativos .NET existentes hoje em dia se baseia no .NET Framework 4.x ou até mesmo no .NET Framework 3.5 e usa estruturas da Web como o ASP.NET MVC, Web Forms do ASP.NET, ASP.NET Web API, WCF (Windows Communication Foundation), ASP.NET SignalR e Páginas da Web ASP.NET. Esses tecnologias estabelecidas do .NET Framework dependem do Windows. É importante considerar essa dependência se você estiver migrando simplesmente migrando aplicativos herdados e deseja realizar o mínimo de alterações na sua infraestrutura de aplicativo.

A Figura 1-2 mostra as principais tecnologias e estilos de arquitetura usados em cada um dos três níveis de maturidade de nuvem:

![Principais tecnologias para cada nível de maturidade para modernizar aplicativos Web .NET existentes](./media/image1-2.png)

**Figura 1-2.** Principais tecnologias para cada nível de maturidade para modernizar aplicativos Web .NET existentes

A Figura 1-2 realça os cenários mais comuns, mas muitas variações híbridas e mistas são possíveis quando se trata de arquitetura. Por exemplo, os modelos de maturidade se aplicam não apenas a arquiteturas monolíticas em aplicativos Web existentes, mas também a arquiteturas com orientação de serviço, de N camadas e outras variações de estilo de arquiteturas. O foco maior ou o percentual em um ou outro tipo de arquitetura e em tecnologias relacionadas determinam o nível de maturidade geral de seus aplicativos.

Cada nível de maturidade no processo de modernização está associado às seguintes tecnologias e abordagens principais:

- **Infraestrutura de nuvem-pronta** (Rehost ou comparação básica & Shift): como uma primeira etapa, muitas organizações desejam apenas executar uma estratégia de migração de nuvem rapidamente. Nesse caso, os aplicativos são hospedados novamente. A maioria da nova hospedagem pode ser automatizada usando as [Migrações para Azure](https://aka.ms/azuremigrate), um serviço que fornece as diretrizes, os insights e os mecanismos necessários para ajudar você a migrar para o Azure com base em ferramentas de nuvem como o [Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/) e o [Serviço de Migração do Banco de Dados do Azure](https://azure.microsoft.com/campaigns/database-migration/). Você também pode definir a nova hospedagem manualmente, para que seja possível conhecer os detalhes da infraestrutura sobre seus ativos ao mover aplicativos herdados para a nuvem. Por exemplo, você pode mover seus aplicativos para VMs no Azure com poucas modificações, provavelmente com apenas alterações simples de configuração. Nesse caso, a rede é semelhante a um ambiente local, especialmente se você criar redes virtuais no Azure.

- **Otimizado para a nuvem** (contêineres de serviços gerenciados e do Windows): esse modelo trata de fazer algumas otimizações de implantação importantes para obter alguns benefícios significativos da nuvem, sem alterar a arquitetura principal do aplicativo. A etapa fundamental aqui é adicionar suporte a [Contêineres do Windows](/virtualization/windowscontainers/about/) aos seus aplicativos .NET Framework existentes. Essa importante etapa (transporte em contêineres) não requer alteração no código, portanto, o esforço de lift-and-shift geral é baixo. Você pode usar ferramentas como [Image2Docker](https://github.com/docker/communitytools-image2docker-win) ou o Visual Studio, com as suas ferramentas para [Docker](https://www.docker.com/). O Visual Studio escolhe automaticamente padrões inteligentes para aplicativos ASP.NET e imagens de Contêineres do Windows. Essas ferramentas oferecem um loop interno ágil e um caminho rápido para levar os contêineres para o Azure. A agilidade é melhorada ao implantar em vários ambientes.
Em seguida, passando para a produção, você poderá implantar seus Contêineres do Windows no [Aplicativo Web para Contêineres do Azure](https://azure.microsoft.com/services/app-service/containers/), no [ACI (Instâncias de Contêiner do Azure)](https://azure.microsoft.com/services/container-instances/) e em VMs do Azure com o Windows Server 2016 e contêineres, se preferir uma abordagem IaaS. Para aplicativos de vários contêineres mais complexos, considere usar orquestradores como [ACS/AKS (Serviço de Kubernetes do Azure)](https://azure.microsoft.com/services/container-service/).

Durante essa modernização inicial, também é possível adicionar ativos da nuvem, como monitoramento com ferramentas como o [Azure Application Insights](/azure/application-insights/app-insights-overview); pipelines de CI/CD para os ciclos de vida de aplicativos com o [Azure DevOps Services](https://azure.microsoft.com/services/devops/) e muitos outros serviços de recurso de dados que estão disponíveis no Azure. Por exemplo, é possível modificar um aplicativo Web monolítico que foi originalmente desenvolvido usando [Web Forms do ASP.NET](https://www.asp.net/web-forms) ou [ASP.NET MVC](https://www.asp.net/mvc) tradicionais, mas agora ele é implantado usando os Contêineres do Windows. Se você usar Contêineres do Windows, também deverá migrar os dados para um banco de dados em uma [Instância Gerenciada do Banco de Dados SQL do Azure](/azure/sql-database/), tudo sem alterar a arquitetura principal do seu aplicativo.

- **Nativo de nuvem**: como introduzido, você deve pensar na arquitetura [de aplicativos nativos de nuvem](https://www.gartner.com/doc/3181919/architect-design-cloudnative-applications) quando estiver visando aplicativos grandes e complexos com várias equipes de desenvolvimento independentes trabalhando em diferentes microservices que podem ser desenvolvidos e implantados de forma autônoma. Além disso, devido à escalabilidade granular e independente por microsserviço. Essas abordagens de arquitetura enfrentam desafios e complexidades muito importantes, mas podem ser bastante simplificadas com o uso de orquestradores e PaaS de nuvem como o [ACS/AKS (Serviço de Kubernetes do Azure)](https://azure.microsoft.com/services/container-service/) (Kubernetes gerenciado) e o [Azure Functions](https://azure.microsoft.com/services/functions/) para uma abordagem sem servidor. Todas essas abordagens (como microsserviços e sem servidor) geralmente requerem que você crie para a nuvem e escreva um novo código, adaptado a plataformas específicas do PaaS ou alinhado a arquiteturas específicas, como microsserviços.

A Figura 1-3 mostra as tecnologias internas que você pode usar para cada nível de maturidade:

![Tecnologias internas para cada nível de maturidade de modernização](./media/image1-3.png)

**Figura 1-3.** Tecnologias internas para cada nível de maturidade de modernização

## <a name="lift-and-shift-scenario"></a>Cenário de lift-and-shift

Para usar migrações lift-and-shift, lembre-se que é possível usar muitas variações diferentes de migração lift-and-shift nos seus cenários de aplicativo. Se você é apenas o novo host do seu aplicativo, você pode ter um cenário semelhante ao mostrado na Figura 1-4, em que as VMs na nuvem são usadas apenas para seu aplicativo e para o servidor de banco de dados.

![Exemplo de um cenário de IaaS puro na nuvem](./media/image1-4.png)

**Figura 1-4**. Exemplo de um cenário de IaaS puro na nuvem

## <a name="modernization-scenarios"></a>Cenários de modernização

Para cenários de modernização, você pode ter um aplicativo otimizado para a nuvem puro que usa elementos apenas desse nível de maturidade. Ou talvez você tenha um aplicativo de estado intermediário com alguns elementos Prontos para Infraestrutura de Nuvem e outros elementos Otimizados para a Nuvem (uma modelo misto de “escolha”), como na Figura 1-5.

![Cenário de exemplo de "Escolha", com o banco de dados no IaaS, DevOps e ativos em contêineres](./media/image1-5.png)

**Figura 1-5.** Cenário de exemplo de "Escolha", com o banco de dados no IaaS, DevOps e ativos em contêineres

Em seguida, como o cenário ideal para migração de muitos aplicativos .NET Framework existentes, você poderia migrar para um aplicativo Otimizado para a Nuvem para obter vantagens significativas com pouco trabalho. Essa abordagem também prepara você para o modelo Nativo da Nuvem como uma possível evolução futura. A Figura 1-6 mostra um exemplo.

![Cenário de exemplo de aplicativos Otimizados para Nuvem, com Contêineres do Windows e serviços gerenciados](./media/image1-6.png)

**Figura 1-6.** Cenário de exemplo de aplicativos Otimizados para Nuvem, com Contêineres do Windows e serviços gerenciados

Indo ainda mais além, você poderia estender o seu aplicativo Otimizado para a Nuvem existente adicionando alguns microsserviços para cenários específicos. Essa abordagem o moveria parcialmente para o nível de Cloud-Native modelo, que não é o foco principal das diretrizes presentes.

## <a name="what-this-guide-does-not-cover"></a>O que este guia não cobre

Este guia abrange um subconjunto específico de cenários de exemplo, conforme mostrado na Figura 1-7. Este guia se concentra apenas nos cenários de comparação de precisão e de deslocamento e, por fim, no modelo de Cloud-Optimized. No modelo Otimizado para a Nuvem, um aplicativo .NET Framework é modernizado usando os Contêineres do Windows, além de componentes adicionais como o monitoramento e pipelines de CI/CD. Cada componente é fundamental para implantar aplicativos na nuvem de maneira mais rápida e ágil.

![O modelo Nativo da Nuvem não é abordado neste guia](./media/image1-7.png)

**Figura 1-7.** O modelo Nativo da Nuvem não é abordado neste guia

O foco deste guia é específico. Ele mostra o caminho que você pode tomar para realizar uma migração lift-and-shift dos seus aplicativos .NET existentes, sem precisar recriar a arquitetura e sem alterar o código. Por fim, ele mostra como tornar seu aplicativo Otimizado para a Nuvem.

Este guia não mostra como criar aplicativos Nativos para a Nuvem, por exemplo, como evoluir para uma arquitetura de microsserviços. Para rearquitetar seus aplicativos ou criar aplicativos novos que se baseiam em microserviços, consulte os [microserviços .net do livro eletrônico: arquitetura para aplicativos .net em contêineres](https://aka.ms/microservicesebook).

### <a name="additional-resources"></a>Recursos adicionais

- **Ciclo de vida do aplicativo Docker em contêiner com a plataforma e as ferramentas da Microsoft** (livro eletrônico baixável) \
  <https://aka.ms/dockerlifecycleebook>

- **Microserviços .net: arquitetura para aplicativos .net em contêineres** (livro eletrônico baixável) \
  <https://aka.ms/microservicesebook>

- **Arquitetura de aplicativos Web modernos com o ASP.NET Core e o Azure** (livro eletrônico para download) \
  <https://aka.ms/webappebook>

## <a name="who-should-use-this-guide"></a>Quem deve usar este guia

Este guia foi escrito para desenvolvedores e arquitetos de solução que desejam modernizar aplicativos Web ASP.NET existentes ou serviços WCF baseados no .NET Framework, para aumentar a agilidade na distribuição e liberação de aplicativos.

Você também pode achar este guia útil se for um tomador de decisões técnicas, como um arquiteto corporativo ou um líder de desenvolvimento/diretor que deseja ter apenas uma visão geral dos benefícios que podem ser alcançados usando Contêineres do Windows e implantando na nuvem ao usar o Microsoft Azure.

## <a name="how-to-use-this-guide"></a>Como usar este guia

Este guia aborda “o porquê”, isto é, por que modernizar seus aplicativos existentes e os benefícios específicos obtidos ao usar os Contêineres do Windows ao mover seus aplicativos para a nuvem. O conteúdo dos primeiros capítulos do guia destina-se a arquitetos e tomadores de decisões técnicas que desejam obter uma visão geral, mas que não precisam se concentrar nos detalhes técnicos passo a passo nem na implementação.

O último capítulo deste guia apresenta vários tutoriais passo a passo que se concentram em cenários de implantação específicos. Este guia oferece versões mais breves dos tutoriais passo a passo para resumir os cenários e realçar seus benefícios. Os tutoriais passo a passo completos detalham a configuração e a implementação e são publicados como um conjunto de [postagens de wiki](https://github.com/dotnet-architecture/eShopModernizing/wiki) no mesmo [repositório do GitHub](https://github.com/dotnet-architecture/eShopModernizing) público em que residem os aplicativos de exemplo relacionados (discutido na próxima seção). O último capítulo e os tutoriais da wiki passo a passo no GitHub serão mais interessantes para desenvolvedores e arquitetos que desejam se concentrar nos detalhes de implementação.

## <a name="sample-apps-for-modernizing-legacy-apps-eshopmodernizing"></a>Aplicativos de exemplo para modernização de aplicativos herdados: eShopModernizing

O repositório [eShopModernizing](https://github.com/dotnet-architecture/eShopModernizing) no GitHub oferece dois aplicativos de exemplo que simulam aplicativos Web monolíticos herdados. Um aplicativo Web é desenvolvido usando o ASP.NET MVC; o segundo aplicativo Web é desenvolvido usando o ASP.NET Web Forms e o terceiro aplicativo é um aplicativo de N camadas com um aplicativo da área de trabalho cliente do WinForms que consome um back-end do serviço WCF. Todos esses aplicativos são baseados no .NET Framework tradicional. Esses aplicativos de exemplo não usam o .NET Core ou o .NET 5,0 ou ASP.NET Core, pois eles devem ser aplicativos .NET Framework existentes/herdados para serem modernizados.

Esses aplicativos de exemplo têm uma segunda versão, com o código modernizado, e são bastante simples. A diferença mais importante entre as versões do aplicativo é que as segundas versões usam Contêineres do Windows como a opção de implantação. Também há algumas adições para as segundas versões, como Blobs de Armazenamento do Microsoft Azure para gerenciar imagens, Azure Active Directory para gerenciar a segurança e o Azure Application Insights para monitorar e auditar os aplicativos.

## <a name="send-your-feedback"></a>Envie seus comentários

Este guia foi escrito para ajudar você a entender suas opções para melhorar e modernizar aplicativos Web .NET existentes. O guia e os aplicativos de exemplo relacionados estão em evolução. Agradecemos seus comentários! Se você tiver comentários sobre como esse guia pode ser mais útil, envie-o para [dotnet-architecture-ebooks-feedback@service.microsoft.com](mailto:dotnet-architecture-ebooks-feedback@service.microsoft.com?subject=Feedback%20for%20.NET%20Container%20&%20Microservices%20Architecture%20book) .

>[!div class="step-by-step"]
>[Próximo](lift-and-shift-existing-apps-azure-iaas.md) <!-- Next Chapter -->
