---
title: 'Aplicativos sem servidor: Arquitetura, padrões e implementação no Azure'
description: Guia para arquitetura sem servidor. Saiba quando, por que e como implementar uma arquitetura sem servidor [em vez de uma IaaS (infraestrutura como serviço) ou uma PaaS (plataforma como serviço)] em seus aplicativos empresariais.
author: JEREMYLIKNESS
ms.author: jeliknes
ms.date: 04/22/2020
ms.openlocfilehash: 867765d29a7c50694a5de7b1de56346d86600a83
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91171813"
---
# <a name="serverless-apps-architecture-patterns-and-azure-implementation"></a>Aplicativos sem servidor: Arquitetura, padrões e implementação no Azure

![Captura de tela que mostra a capa do livro eletrônico de aplicativos sem servidor.](./media/index/serverless-apps-cover-v3.png)

**Edição v 3.0** – atualizado para Azure Functions v3

> DOWNLOAD disponível em: <https://aka.ms/serverlessbookpdf>

PUBLICADO POR

Divisão de Desenvolvedores Microsoft, equipes dos produtos .NET e Visual Studio

Uma divisão da Microsoft Corporation

One Microsoft Way

Redmond, Washington 98052-6399

Copyright &copy; 2018-2020 da Microsoft Corporation

Todos os direitos reservados. Nenhuma parte do conteúdo deste guia pode ser reproduzida ou transmitida de nenhuma forma nem por nenhum meio sem a permissão por escrito do publicador.

Este livro é fornecido “no estado em que se encontra” e expressa os pontos de vista e as opiniões do autor. Os pontos de vista, as opiniões e as informações expressos neste guia, incluindo URLs e outras referências a sites da Internet, podem ser alteradas sem aviso prévio.

 Alguns exemplos aqui representados são fornecidos somente para fins de ilustração e são fictícios. Nenhuma associação ou conexão real é intencional ou deve ser inferida.

A Microsoft e as marcas listadas em <https://www.microsoft.com> na página da Web "Marcas" são marcas comerciais do grupo de empresas Microsoft.

Mac e macOS são marcas comerciais da Apple Inc.

Todas as outras marcas e logotipos são propriedade de seus respectivos proprietários.

Autor:

> **[Jeremy Likness](https://twitter.com/jeremylikness)**, gerente de programa de dados .net sênior, Microsoft Corp.

Colaborador:

> **[Cecil Phillip](https://twitter.com/cecilphillip)**, defensora da nuvem sênior, Microsoft Corp.

Editores:

> **[Bill Wagner](https://twitter.com/billwagner)**, desenvolvedor de conteúdo sênior, Microsoft Corp.

> **[Maira Wenzel](https://twitter.com/mairacw)**, desenvolvedor de conteúdo sênior, Microsoft Corp.

Participantes e revisores:

> **[Steve Smith](https://twitter.com/ardalis)**, Proprietário, Ardalis Services.

## <a name="introduction"></a>Introdução

Sem [servidor](https://azure.microsoft.com/solutions/serverless/) é a evolução das plataformas de nuvem na direção do código nativo de nuvem puro. Ela aproxima os desenvolvedores da lógica de negócios, isolando-os das questões de infraestrutura. É um padrão que não quer dizer "nenhum servidor", mas sim, "sem servidor". O código sem servidor é controlado por eventos. O código pode ser disparado por qualquer coisa, desde uma solicitação da Web HTTP tradicional até um temporizador ou o carregamento de um arquivo. A infraestrutura por trás da computação sem servidor permite dimensionar instantaneamente para atender a demandas elásticas e oferece a microcobrança, que realmente permite "pagar por aquilo que você usar". A computação sem servidor requer uma nova maneira de pensar e abordar a criação de aplicativos e não é a solução certa para todos os problemas. Como desenvolvedor, você precisa decidir:

- Quais são os prós e contras do uso da computação sem servidor?
- Por que você deve considerar a computação sem servidor para seus próprios aplicativos?
- Como pode você compilar, testar, implantar e manter seu código sem servidor?
- Em que caso é interessante migrar o código de aplicativos existentes para a computação sem servidor, e qual é a melhor maneira de realizar essa transformação?

## <a name="about-this-guide"></a>Sobre este guia

Este guia concentra-se no desenvolvimento de aplicativos nativos da nuvem que usam a computação sem servidor. O livro destaca os benefícios e expõe as possíveis desvantagens do desenvolvimento de aplicativos sem servidor e fornece uma pesquisa sobre arquiteturas sem servidor. São ilustrados vários exemplos de como a computação sem servidor pode ser usada, juntamente com vários padrões de design sem servidor.

Este guia explica os componentes da plataforma sem servidor do Azure e concentra-se especificamente na implementação da computação sem servidor usando o [Azure Functions](/azure/azure-functions/functions-overview). Você saberá mais sobre gatilhos e associações, e aprenderá a implementar aplicativos sem servidor que se baseiam em estado usando funções duráveis. Por fim, exemplos de negócios e estudos de caso o ajudarão a estabelecer um contexto e um quadro de referência para determinar se a computação sem servidor é a abordagem certa para seus projetos.

## <a name="evolution-of-cloud-platforms"></a>Evolução das plataformas de nuvem

A computação sem servidor é a culminação de várias iterações de plataformas de nuvem. A evolução começou com o computador físico sem sistema operacional no data center e progrediu para a IaaS (infraestrutura como serviço) e a PaaS (plataforma como serviço).

![Evolução de local para sem servidor](./media/serverless-evolution-iaas-paas.png)

Antes da nuvem, existia um limite perceptível entre desenvolvimento e operações. A implantação de um aplicativo significava responder a uma grande variedade de perguntas como:

- Qual hardware deve ser instalado?
- Como é o acesso físico ao computador protegido?
- O data center exige um no-break?
- Para onde os backups de armazenamento são enviados?
- É necessário que haja uma energia redundante?

A lista continua e a sobrecarga era enorme. Em muitas situações, os departamentos de TI eram obrigados a lidar com um enorme desperdício. O desperdício era devido à alocação excessiva de servidores como máquinas de backup para recuperação de desastres e servidores em espera para habilitar a expansão. Felizmente, a introdução da tecnologia de virtualização (como o [Hyper-V](/virtualization/hyper-v-on-windows/about/)) com máquinas virtuais (VMS) deu origem à IaaS (infraestrutura como serviço). A infraestrutura virtualizada permitiu que as operações estabelecessem um conjunto padrão de servidores como o backbone, levando a um ambiente flexível com a capacidade de provisionar de servidores exclusivos "sob demanda”. Ainda mais importante, a virtualização preparou o terreno para que a nuvem pudesse ser usada para fornecer máquinas virtuais "como serviço”. As empresas puderam realmente parar de se preocupar com computadores físicos ou com fonte de alimentação redundante. Com isso, elas passaram a se concentrar no ambiente virtual.

A IaaS ainda requer uma sobrecarga pesada porque as operações ainda são responsáveis por várias tarefas. Essas tarefas incluem:

- Aplicar patches e fazer backup de servidores.
- Instalar pacotes.
- Manter o sistema operacional atualizado.
- Monitorar o aplicativo.

A próxima evolução reduziu a sobrecarga ao fornecer a PaaS (plataforma como serviço). Com a PaaS, o provedor de nuvem lida com sistemas operacionais, patches de segurança e até mesmo com os pacotes necessários para dar suporte a uma plataforma específica. Em vez de criar uma VM e, em seguida, configurar o .NET e os servidores de Serviços de Informações da Internet (IIS), os desenvolvedores simplesmente escolhem um "destino de plataforma", como "aplicativo Web" ou "ponto de extremidade de API" e implantam o código diretamente. As perguntas de infraestrutura são reduzidas para:

- Qual o tamanho dos serviços necessários?
- Como os serviços podem ser expandidos (adicionar mais servidores ou nós)?
- Como os serviços podem ser escalados verticalmente (aumentar a capacidade de hospedar servidores ou nós)?

A computação sem servidor abstrai ainda mais os servidores, concentrando-se no código controlado por eventos. Em vez de se concentrarem em uma plataforma, os desenvolvedores podem se concentrar em um microsserviço que faz apenas uma coisa. As duas principais perguntas para compilar o código sem servidor são:

- O que dispara o código?
- O que o código faz?

Com a computação sem servidor, a infraestrutura é abstraída. Em alguns casos, o desenvolvedor nem precisa se preocupar mais com o host. Independentemente de haver uma instância do IIS, do Kestrel, do Apache ou de algum outro servidor Web em execução para gerenciar solicitações da Web, o desenvolvedor se concentrará em um gatilho HTTP. O gatilho fornece o conteúdo padrão e de plataforma cruzada para a solicitação. Além de simplificar o processo de desenvolvimento, o conteúdo também facilita os testes e, em alguns casos, torna o código facilmente portátil entre plataformas.

Outro recurso sem servidor é a microcobrança. É comum que aplicativos Web hospedem pontos de extremidade de API Web. No bare-metal tradicional, na IaaS e até mesmos nas implementações de PaaS, os recursos para hospedar as APIs são pagos continuamente. Isso significa que você paga para hospedar os pontos de extremidade, mesmo quando eles não estão sendo acessados. Geralmente você percebe que uma API é chamada mais do que outras, portanto, todo o sistema é dimensionado com base no suporte aos pontos de extremidade populares. A computação sem servidor permite que você dimensione cada ponto de extremidade de maneira independente e pague pelo uso, portanto, não há custos quando as APIs não são chamadas. A migração pode, em muitos casos, reduzir drasticamente o custo contínuo de suporte aos pontos de extremidade.

## <a name="what-this-guide-doesnt-cover"></a>O que este guia não aborda

Este guia enfatiza especificamente as abordagens de arquitetura e os padrões de design e não é uma visão aprofundada dos detalhes da implementação do Azure Functions, dos [Aplicativos Lógicos](/azure/logic-apps/logic-apps-what-are-logic-apps) ou de outras plataformas sem servidor. Este guia não aborda, por exemplo, fluxos de trabalho com Aplicativos Lógicos ou recursos do Azure Functions como a configuração do CORS (Compartilhamento de Recursos entre Origens), a aplicação de domínios personalizados ou o carregamento de certificados SSL. Esses detalhes estão disponíveis na [documentação online do Azure Functions](/azure/azure-functions/functions-reference).

### <a name="additional-resources"></a>Recursos adicionais

- [Centro de arquitetura do Azure](/azure/architecture/)
- [Práticas recomendadas para aplicativos em nuvem](/azure/architecture/best-practices/api-design)

## <a name="who-should-use-the-guide"></a>Quem deve usar o guia

Este guia foi escrito para desenvolvedores e arquitetos de solução que desejam criar aplicativos empresariais com o .NET que podem usar componentes sem servidor localmente ou na nuvem. Ele é útil para desenvolvedores, arquitetos e tomadores de decisões técnicas interessados em:

- Entender os prós e contras do desenvolvimento sem servidor
- Saber como abordar a arquitetura sem servidor
- Exemplos de implementações de aplicativos sem servidor

## <a name="how-to-use-the-guide"></a>Como usar o guia

A primeira parte deste guia examina por que a computação sem servidor é uma opção viável comparando várias abordagens de arquitetura diferentes. Ele examina a tecnologia e o ciclo de vida de desenvolvimento, porque todos os aspectos do desenvolvimento de software são afetados pelas decisões de arquitetura. Em seguida, ele examina os casos de uso e os padrões de design e inclui implementações de referência que usam o Azure Functions. Cada seção contém recursos adicionais para informar mais sobre uma área específica. O guia termina com recursos para instruções passo a passo e explorações práticas da implementação da computação sem servidor.

## <a name="send-your-feedback"></a>Envie seus comentários

O guia e os exemplos relacionados estão em constante desenvolvimento, portanto, seus comentários são bem-vindos! Se você tiver comentários de como este guia pode ser melhorado, use a seção de comentários na parte inferior de qualquer página baseada em [problemas do GitHub](https://github.com/dotnet/docs/issues).

>[!div class="step-by-step"]
>[Próximo](architecture-approaches.md)
