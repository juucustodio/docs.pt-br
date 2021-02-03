---
title: DevOps
description: Considerações sobre o DevOps para aplicativos nativos de nuvem
ms.date: 01/19/2021
ms.openlocfilehash: 089f6ac82f3ce0613c7b8e0b9527f3fa9cf7b50c
ms.sourcegitcommit: f2ab02d9a780819ca2e5310bbcf5cfe5b7993041
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2021
ms.locfileid: "99506195"
---
# <a name="devops"></a>DevOps

A mantra favorita dos consultores de software é responder "depende" de qualquer pergunta apresentada. Não é porque os consultores de software estão boass de não tomar uma posição. É porque não há uma resposta verdadeira para qualquer pergunta no software. Não há nenhum direito absoluto e errado, mas sim um equilíbrio entre os opostos.

Considere, por exemplo, as duas principais escolas do desenvolvimento de aplicativos Web: SPAs (aplicativos de página única) versus aplicativos do lado do servidor. Por um lado, a experiência do usuário tende a ser melhor com o SPAs e a quantidade de tráfego para o servidor Web pode ser minimizada, tornando possível hospedá-los em algo tão simples quanto a hospedagem estática. Por outro lado, SPAs tendem a ser mais lentos de desenvolver e mais difíceis de testar. Qual é a escolha certa? Bem, depende de sua situação.

Os aplicativos nativos de nuvem não estão imunes ao mesmo dicotomia. Eles têm vantagens claras em termos de velocidade de desenvolvimento, estabilidade e escalabilidade, mas gerenciá-los pode ser um pouco mais difícil.

Há anos, não era incomum o processo de mover um aplicativo de desenvolvimento para produção para levar um mês ou ainda mais. As empresas lançaram software em uma cadência de 6 meses ou até mesmo a cada ano. Uma delas não precisa olhar além do Microsoft Windows para ter uma ideia da cadência das versões que eram aceitáveis antes dos dias do Windows 10 em verde. Cinco anos passados entre o Windows XP e o vista, mais 3 entre o Vista e o Windows 7.

Agora, é bem estabelecido que ser capaz de lançar o software rapidamente dá às empresas de movimentação rápida uma enorme vantagem do mercado em relação a seus concorrentes mais sloths. É por esse motivo que as principais atualizações do Windows 10 agora são aproximadamente a cada seis meses.

Os padrões e as práticas que permitem uma liberação mais rápida e confiável para agregar valor aos negócios são coletivamente conhecidos como DevOps. Eles consistem em uma ampla gama de ideias que abrangem todo o ciclo de vida do desenvolvimento de software, desde a especificação de um aplicativo até a entrega e operação desse aplicativo.

DevOps surgiu antes dos microserviços e é provável que o movimento em direção ao menor, mais se ajuste aos serviços de finalidade não teria sido possível sem DevOps para fazer o lançamento e operar não apenas um, mas muitos aplicativos na produção.

![Figura 10-1 as tendências de pesquisa mostram que o crescimento em microserviços não começa até que DevOps seja uma ideia bem estabelecida.](./media/microservices-vs-devops.png)

**Figura 10-1** -DevOps e microservices.

Por meio de boas práticas de DevOps, é possível perceber as vantagens dos aplicativos nativos de nuvem sem Suffocating em uma montanha de trabalho que realmente opera os aplicativos.

Não há um martelo de ouro quando se trata de DevOps. Ninguém pode vender uma solução completa e totalmente abrangente para liberar e operar aplicativos de alta qualidade. Isso ocorre porque cada aplicativo é muito diferente de todos os outros. No entanto, há ferramentas que podem tornar o DevOps uma proposta muito menos assustadora. Uma dessas ferramentas é conhecida como Azure DevOps.

## <a name="azure-devops"></a>Azure DevOps

O Azure DevOps tem um longo pedigree. Ele pode rastrear suas raízes de volta para quando Team Foundation Server movidos pela primeira vez online e pelas várias alterações de nome: Visual Studio online e Visual Studio Team Services. Ao longo dos anos, no entanto, ele se tornou muito mais do que seus antecessores.

O Azure DevOps é dividido em cinco componentes principais:

![Figura 10-2 as cinco áreas principais do Azure DevOps](./media/devops-components.png)

**Figura 10-2** – Azure DevOps.

**Azure Repos** -gerenciamento de código-fonte que dá suporte ao TFVC (respeitável controle de versão do Team Foundation) e ao [git](https://en.wikipedia.org/wiki/Git)favorito do setor. As solicitações de pull fornecem uma maneira de habilitar a codificação social, estimulando a discussão sobre alterações à medida que elas são feitas.

**Azure boards** -fornece um problema e uma ferramenta de acompanhamento de itens de trabalho que se esforça para permitir que os usuários escolham os fluxos que funcionam melhor para eles. Ele vem com vários modelos pré-configurados, incluindo aqueles para oferecer suporte a estilos de desenvolvimento e do SCRUM.

**Azure pipelines** -um sistema de gerenciamento de versão e compilação que dá suporte à integração rígida com o Azure. As compilações podem ser executadas em várias plataformas do Windows para Linux para macOS. Os agentes de compilação podem ser provisionados na nuvem ou localmente.

**Azure Test Plans** -nenhuma pessoa de QA será deixada com o suporte de teste de gerenciamento de teste e exploratório oferecido pelo recurso de Test Plans.

**Azure Artifacts** -um feed de artefatos que permite que as empresas criem suas próprias versões internas do NuGet, NPM e outras. Ele atende a uma dupla finalidade de atuar como um cache de pacotes upstream, se houver uma falha de um repositório centralizado.

A unidade organizacional de nível superior no Azure DevOps é conhecida como um projeto. Dentro de cada projeto, os vários componentes, como Azure Artifacts, podem ser ativados e desativados. Cada um desses componentes fornece diferentes vantagens para aplicativos nativos de nuvem. Os três mais úteis são repositórios, placas e pipelines. Se os usuários desejarem gerenciar seu código-fonte em outra pilha de repositórios, como o GitHub, mas ainda se beneficiarem da Azure Pipelines e de outros componentes, isso é perfeitamente possível.

Felizmente, as equipes de desenvolvimento têm muitas opções ao selecionar um repositório. Um deles é o GitHub.

## <a name="github-actions"></a>GitHub Actions

Fundada em 2009, o GitHub é um repositório baseado na Web amplamente popular para hospedagem de projetos, documentação e código. Muitas empresas de tecnologia de grande porte, como Apple, Amazon, Google e corporações convencionais, usam o GitHub. O GitHub usa o sistema de controle de versão distribuído e de software livre chamado Git como base. Na parte superior, ele adiciona seu próprio conjunto de recursos, incluindo acompanhamento de defeito, solicitações de recurso e pull, gerenciamento de tarefas e wikis para cada base de código.

À medida que o GitHub evolui, ele também está adicionando recursos de DevOps. Por exemplo, o GitHub tem seu próprio pipeline de CI/CD (integração contínua/entrega contínua), chamado `GitHub Actions` . As ações do GitHub são uma ferramenta de automação de fluxo de trabalho habilitada pela Comunidade. Ele permite que as equipes do DevOps se integrem com suas ferramentas existentes, combinem e combinem novos produtos e se conectem ao ciclo de vida do software, incluindo parceiros de CI/CD existentes. "

O GitHub tem mais de 40 milhões usuários, tornando-o o maior host do código-fonte do mundo. Em outubro de 2018, a Microsoft comprou o GitHub. A Microsoft penhorou que o GitHub permanecerá em uma [plataforma aberta](https://techcrunch.com/2018/06/04/microsoft-promises-to-keep-github-independent-and-open/) que qualquer desenvolvedor possa conectar e estender. Ele continua a operar como uma empresa independente. O GitHub oferece planos para contas corporativas, de equipe, profissionais e gratuitas.

## <a name="source-control"></a>Controle do código-fonte

Organizar o código para um aplicativo nativo de nuvem pode ser desafiador. Em vez de um único aplicativo gigante, os aplicativos nativos de nuvem tendem a ser compostos por uma Web de aplicativos menores que se comunicam entre si. Assim como acontece com tudo em computação, a melhor disposição do código continua sendo uma pergunta aberta. Há exemplos de aplicativos bem-sucedidos usando diferentes tipos de layouts, mas duas variantes parecem ter a maior popularidade.

Antes de entrar no controle do código-fonte propriamente dito, provavelmente vale a pena decidir quantos projetos são apropriados. Em um único projeto, há suporte para vários repositórios e pipelines de compilação. As placas são um pouco mais complicadas, mas sim, as tarefas podem ser facilmente atribuídas a várias equipes dentro de um único projeto. É possível dar suporte a centenas, até milhares de desenvolvedores, de um único projeto DevOps do Azure. Isso é provavelmente a melhor abordagem, pois fornece um único local para que todo o desenvolvedor possa trabalhar e reduz a confusão de encontrar um aplicativo quando os desenvolvedores não têm certeza de qual projeto no qual ele reside.

Dividir o código para os microserviços no projeto DevOps do Azure pode ser um pouco mais desafiador.

![Figura 10-3 único versus vários repositórios](./media/single-repository-vs-multiple.png)

**Figura 10-3** – um versus muitos repositórios.

### <a name="repository-per-microservice"></a>Repositório por microserviço

À primeira vista, essa abordagem parece a abordagem mais lógica para dividir o código-fonte para os microserviços. Cada repositório pode conter o código necessário para criar um microserviço. As vantagens dessa abordagem estão prontamente visíveis:

1. As instruções para criar e manter o aplicativo podem ser adicionadas a um arquivo LEIAme na raiz de cada repositório. Ao inverter os repositórios, é fácil encontrar essas instruções, reduzindo o tempo de rotação para os desenvolvedores.
2. Cada serviço está localizado em um local lógico, facilmente encontrado sabendo o nome do serviço.
3. As compilações podem ser facilmente configuradas de forma que sejam disparadas apenas quando uma alteração é feita no repositório proprietário.
4. O número de alterações que entram em um repositório é limitado ao pequeno número de desenvolvedores que trabalham no projeto.
5. A segurança é fácil de configurar restringindo os repositórios aos quais os desenvolvedores têm permissões de leitura e gravação.
6. As configurações de nível de repositório podem ser alteradas pela equipe proprietária com um mínimo de discussão com outras pessoas.

Uma das principais ideias por trás de microserviços é que os serviços devem ser silodos e separados uns dos outros. Ao usar o design controlado por domínio para decidir sobre os limites dos serviços, os serviços atuam como limites transacionais. As atualizações de banco de dados não devem abranger vários serviços. Essa coleção de dados relacionados é conhecida como um contexto limitado.  Essa ideia é refletida pelo isolamento de dados de microserviço para um banco de dado separado e autônomo do restante dos serviços. Isso faz muito sentido para levar essa ideia até o código-fonte do.

No entanto, essa abordagem não está sem seus problemas. Um dos mais gnarly problemas de desenvolvimento do nosso tempo é o gerenciamento de dependências. Considere o número de arquivos que compõem o `node_modules` diretório médio. Uma nova instalação de algo parecido `create-react-app` com o provavelmente trará milhares de pacotes. A questão de como gerenciar essas dependências é uma tarefa difícil.

Se uma dependência for atualizada, os pacotes downstream também deverão atualizar essa dependência. Infelizmente, isso leva o trabalho de desenvolvimento, portanto, invariavelmente, o `node_modules` diretório termina com várias versões de um único pacote, cada um com uma dependência de algum outro pacote com controle de versão em uma cadência um pouco diferente. Ao implantar um aplicativo, qual versão de uma dependência deve ser usada? A versão que está em produção no momento? A versão atualmente em beta, mas é provável que esteja em produção no momento em que o consumidor faz isso para produção? Problemas difíceis que não são resolvidos apenas com o uso de microservices.

Há bibliotecas que dependem de uma ampla variedade de projetos. Dividindo os microserviços por um em cada repositório, as dependências internas podem ser melhor resolvidas usando o repositório interno, Azure Artifacts. As compilações para bibliotecas enviarão suas versões mais recentes para Azure Artifacts para consumo interno. O projeto downstream ainda deve ser atualizado manualmente para assumir uma dependência dos pacotes recentemente atualizados.

Outra desvantagem se apresenta ao mover o código entre os serviços. Embora seja interessante acreditar que a primeira divisão de um aplicativo em microserviços é 100% correta, a realidade é que raramente estamos tão prescients quanto não fazer nenhum erro de divisão de serviço. Portanto, a funcionalidade e o código que os conduz deverão mudar de serviço para serviço: repositório para repositório. Ao saltar de um repositório para outro, o código perde seu histórico. Há muitos casos, especialmente no caso de uma auditoria, em que o histórico completo de uma parte do código é inestimável.

A desvantagem final e mais importante é coordenar alterações. Em um aplicativo de microserviços verdadeiro, não deve haver nenhuma dependência de implantação entre os serviços. Deve ser possível implantar os serviços A, B e C em qualquer ordem, pois eles têm acoplamento flexível. Na realidade, no entanto, há ocasiões em que é desejável fazer uma alteração que cruze vários repositórios ao mesmo tempo. Alguns exemplos incluem a atualização de uma biblioteca para fechar uma brecha de segurança ou alterar um protocolo de comunicação usado por todos os serviços.

Para fazer uma alteração entre repositórios, é necessário que uma confirmação para cada repositório seja feita sucessivamente. Cada alteração em cada repositório precisará ser solicitada por pull e revisada separadamente. Essa atividade pode ser difícil de coordenar.

Uma alternativa ao uso de muitos repositórios é colocar todo o código-fonte em um gigante, sabendo, único repositório.

### <a name="single-repository"></a>Repositório único

Nessa abordagem, às vezes conhecida como um [monorepository](https://danluu.com/monorepo/), todo o código-fonte de cada serviço é colocado no mesmo repositório. A princípio, essa abordagem parece ser uma boa ideia, o que provavelmente tornaria o difícil de lidar com o código-fonte. No entanto, há algumas vantagens marcadas para trabalhar dessa forma.

A primeira vantagem é que é mais fácil gerenciar dependências entre projetos. Em vez de contar com um feed de artefatos externo, os projetos podem importar diretamente um do outro. Isso significa que as atualizações são instantâneas e as versões conflitantes provavelmente serão encontradas no momento da compilação na estação de trabalho do desenvolvedor. Em vigor, deslocar parte do teste de integração para a esquerda.

Ao mover o código entre projetos, agora é mais fácil preservar o histórico à medida que os arquivos forem detectados como tendo sido movidos em vez de serem reescritos.

Outra vantagem é que a ampla gama de alterações que cruzam limites de serviço pode ser feita em uma única confirmação. Essa atividade reduz a sobrecarga de ter potencialmente dezenas de alterações a serem examinadas individualmente.

Há muitas ferramentas que podem executar a análise estática de código para detectar práticas de programação inseguras ou uso problemático de APIs. Em um mundo de vários repositórios, cada repositório precisará ser iterado para localizar os problemas neles. O repositório único permite executar a análise em um só lugar.

Também há muitas desvantagens para a abordagem de repositório único. Uma das mais importantes preocupações é que ter um único repositório gera preocupações de segurança. Se o conteúdo de um repositório estiver vazado em um repositório por modelo de serviço, a quantidade de código perdido será mínima. Com um único repositório, tudo o que a empresa possui pode ser perdido. Houve muitos exemplos no passado sobre isso acontecendo e degradendo trabalhos inteiros de desenvolvimento de jogos. Ter vários repositórios expõe menos área de superfície, que é uma característica desejável na maioria das práticas de segurança.

O tamanho do único repositório provavelmente se tornará não gerenciável rapidamente. Isso apresenta algumas implicações de desempenho interessantes. Pode ser necessário usar ferramentas especializadas, como o [sistema de arquivos virtual para git](https://github.com/Microsoft/VFSForGit), que foi originalmente projetado para melhorar a experiência dos desenvolvedores na equipe do Windows.

Frequentemente, o argumento para usar um único repositório se resume a um argumento que o Facebook ou o Google usam esse método para a organização do código-fonte. Se a abordagem for boa o suficiente para essas empresas, certamente, essa será a abordagem correta para todas as empresas. A verdade da questão é que poucas empresas operam em qualquer coisa como a escala do Facebook ou do Google. Os problemas que ocorrem nessas escalas são diferentes daqueles que a maioria dos desenvolvedores enfrentarão. O que é bom para o ganso pode não ser bom para o analisar.

No final, qualquer uma das soluções pode ser usada para hospedar o código-fonte para os microservices. No entanto, na maioria dos casos, a sobrecarga de gerenciamento e de engenharia da operação em um único repositório não vale as vantagens meagers. Dividir o código em vários repositórios incentiva a melhor separação de preocupações e incentiva a autonomia entre as equipes de desenvolvimento.

### <a name="standard-directory-structure"></a>Estrutura de diretório padrão

Independentemente do único versus de vários repositórios, cada serviço terá seu próprio diretório. Uma das melhores otimizações para permitir que os desenvolvedores entrem em projetos rapidamente é manter uma estrutura de diretório padrão.

![Figura 10-4 uma estrutura de diretório padrão para os serviços de email e de entrada](./media/dir-struct.png)

**Figura 10-4** -estrutura de diretório padrão.

Sempre que um novo projeto é criado, um modelo que coloca a estrutura correta deve ser usado. Esse modelo também pode incluir itens úteis como um arquivo LEIAme de esqueleto e um `azure-pipelines.yml` . Em qualquer arquitetura de microserviço, um alto grau de variação entre projetos torna as operações em massa em relação aos serviços mais difíceis.

Há muitas ferramentas que podem fornecer Templating para um diretório inteiro, contendo vários diretórios de código-fonte. O [Yeoman](https://yeoman.io/) é popular no mundo do JavaScript e o GitHub lançou recentemente [modelos de repositório](https://github.blog/2019-06-06-generate-new-repositories-with-repository-templates/), que fornecem grande parte da mesma funcionalidade.

## <a name="task-management"></a>Gerenciamento de tarefas

O gerenciamento de tarefas em qualquer projeto pode ser difícil. Na frente, há inúmeras perguntas a serem respondidas sobre o tipo de fluxos de trabalho a serem configurados para garantir a produtividade ideal do desenvolvedor.

Os aplicativos nativos de nuvem tendem a ser menores do que os produtos de software tradicionais ou pelo menos eles são divididos em serviços menores. O rastreamento de problemas ou tarefas relacionadas a esses serviços permanece tão importante quanto qualquer outro projeto de software. Ninguém deseja perder o controle de algum item de trabalho ou explicar a um cliente que seu problema não foi registrado corretamente. As placas são configuradas no nível do projeto, mas dentro de cada projeto, as áreas podem ser definidas. Eles permitem a interrupção de problemas em vários componentes. A vantagem de manter todo o trabalho para todo o aplicativo em um só lugar é que é fácil mover itens de trabalho de uma equipe para outra, já que eles são bem compreendidos.

O DevOps do Azure vem com vários modelos populares pré-configurados. Na configuração mais básica, tudo o que é necessário saber é o que há na lista de pendências, em que as pessoas estão trabalhando e o que é feito. É importante ter essa visibilidade no processo de criação de software, para que o trabalho possa ser priorizado e tarefas concluídas relatadas ao cliente. É claro que alguns projetos de software se encontram em um processo tão simples quanto `to do` , `doing` e `done` . Não demora muito para que as pessoas comecem a adicionar etapas como `QA` ou `Detailed Specification` ao processo.

Uma das partes mais importantes das metodologias Agile é a auto-introspecção em intervalos regulares. Essas revisões destinam-se a fornecer informações sobre quais problemas a equipe está enfrentando e como eles podem ser aprimorados. Frequentemente, isso significa alterar o fluxo de problemas e recursos por meio do processo de desenvolvimento. Portanto, é perfeitamente saudável expandir os layouts das placas com estágios adicionais.

Os estágios nas placas não são a única ferramenta organizacional. Dependendo da configuração do quadro, há uma hierarquia de itens de trabalho. O item mais granular que pode aparecer em um quadro é uma tarefa. Uma tarefa que contém campos para um título, uma descrição, uma prioridade, uma estimativa da quantidade de trabalho restante e a capacidade de vincular a outros itens de trabalho ou itens de desenvolvimento (branches, confirmações, solicitações de pull, compilações e assim por diante). Os itens de trabalho podem ser classificados em diferentes áreas do aplicativo e em diferentes iterações (sprints) para facilitar sua localização.

![Figura 10-5 um exemplo de tarefa no Azure DevOps](./media/task-details.png)

**Figura 10-5** -tarefa no Azure DevOps.

O campo Descrição dá suporte aos estilos normais esperados (negrito, sublinhado e tachado) e a capacidade de inserir imagens. Isso o torna uma ferramenta poderosa para uso ao especificar trabalho ou bugs.

As tarefas podem ser acumuladas em recursos, que definem uma unidade maior de trabalho. Os recursos, por sua vez, podem ser [acumulados em Epics](/azure/devops/boards/backlogs/define-features-epics?view=azure-devops). A classificação de tarefas nessa hierarquia facilita muito a compreensão de como um recurso grande é para ser implantado.

![Figura 10-6 tipos de item de trabalho configurados por padrão no modelo de processo básico](./media/board-issue-types.png)

**Figura 10-6** -item de trabalho no Azure DevOps.

Há diferentes tipos de exibições nos problemas no Azure Boards. Os itens que ainda não estão agendados aparecem na pendência. A partir daí, eles podem ser atribuídos a um Sprint. Um Sprint é uma caixa de tempo durante a qual é esperada alguma quantidade de trabalho será concluída. Esse trabalho pode incluir tarefas, mas também a resolução de tíquetes. Uma vez lá, o Sprint inteiro pode ser gerenciado na seção de painel do Sprint. Esta exibição mostra como o trabalho está progredindo e inclui um gráfico de gravação para fornecer uma estimativa sempre atualizada de se o Sprint será bem-sucedido.

![Figura 10-7 um quadro com um Sprint definido](./media/sprint-board.png)

**Figura 10-7** -placa no Azure DevOps.

Agora, deve ser aparente que há uma grande quantidade de energia nas placas no Azure DevOps. Para os desenvolvedores, há exibições fáceis do que está sendo trabalhado. Para os gerentes de projeto exibições no futuro trabalho, bem como uma visão geral do trabalho existente. Para os gerentes, há muitos relatórios sobre a capacidade e a insourcing. Infelizmente, não há nada mágico sobre aplicativos nativos de nuvem que eliminam a necessidade de controlar o trabalho. Mas se você precisar acompanhar o trabalho, há alguns lugares onde a experiência é melhor do que no Azure DevOps.

## <a name="cicd-pipelines"></a>Pipelines de CI/CD

Quase nenhuma alteração no ciclo de vida de desenvolvimento de software foi tão revolucionária quanto o advento da CI (integração contínua) e do CD (entrega contínua). A criação e execução de testes automatizados em relação ao código-fonte de um projeto assim que uma alteração é verificada em captura de erros antecipadamente. Antes do advento das compilações de integração contínua, não seria incomum efetuar pull do código do repositório e descobrir que ele não passou em testes nem sequer foi criado. Isso resultou no rastreamento da origem da quebra.

Tradicionalmente, o fornecimento de software para o ambiente de produção exigia documentação extensiva e uma lista de etapas. Cada uma dessas etapas precisava ser concluída manualmente em um processo muito propenso a erros.

![Figura 10-8 uma lista de verificação](./media/checklist.png)

**Figura 10-8** -lista de verificação.

A irmã da integração contínua é a entrega contínua na qual os pacotes compilados recentemente são implantados em um ambiente. O processo manual não pode ser dimensionado para corresponder à velocidade de desenvolvimento para que a automação se torne mais importante. As listas de verificação são substituídas por scripts que podem executar as mesmas tarefas com mais rapidez e precisão do que qualquer humano.

O ambiente no qual a entrega contínua é entregue pode ser um ambiente de teste ou, como está sendo feito por muitas empresas de tecnologia de grande porte, pode ser o ambiente de produção. O último exige um investimento em testes de alta qualidade que podem dar confiança de que uma alteração não irá interromper a produção para os usuários. Da mesma forma que a integração contínua capturou problemas no código, a entrega contínua inicial captura problemas no início do processo de implantação.

A importância de automatizar o processo de criação e entrega é acentuada por aplicativos nativos de nuvem. As implantações acontecem com mais frequência e para mais ambientes, Implantando manualmente as bordas em impossível.

### <a name="azure-builds"></a>Compilações do Azure

O Azure DevOps fornece um conjunto de ferramentas para tornar a integração e a implantação contínuas mais fáceis do que nunca. Essas ferramentas estão localizadas em Azure Pipelines. O primeiro deles é o Azure builds, que é uma ferramenta para executar definições de compilação baseadas em YAML em escala. Os usuários podem trazer seus próprios computadores de compilação (ótimo para se a compilação exigir um ambiente de configuração meticulosa) ou usar um computador de um pool atualizado constantemente de máquinas virtuais hospedadas do Azure. Esses agentes de compilação hospedados vêm pré-instalados com uma ampla gama de ferramentas de desenvolvimento, não apenas para o desenvolvimento do .NET, mas para tudo, desde Java até Python até o desenvolvimento do iPhone.

O DevOps inclui uma ampla gama de definições de compilação prontas para uso que podem ser personalizadas para qualquer compilação. As definições de compilação são definidas em um arquivo chamado `azure-pipelines.yml` e verificadas no repositório para que possam ter controle de versão junto com o código-fonte. Isso torna muito mais fácil fazer alterações no pipeline de compilação em uma ramificação, pois as alterações podem ser verificadas apenas nessa ramificação. Um exemplo `azure-pipelines.yml` para criar um aplicativo web ASP.net na estrutura completa é mostrado na figura 10-9.

```yml
name: $(rev:r)

variables:
  version: 9.2.0.$(Build.BuildNumber)
  solution: Portals.sln
  artifactName: drop
  buildPlatform: any cpu
  buildConfiguration: release

pool:
  name: Hosted VS2017
  demands:
  - msbuild
  - visualstudio
  - vstest

steps:
- task: NuGetToolInstaller@0
  displayName: 'Use NuGet 4.4.1'
  inputs:
    versionSpec: 4.4.1

- task: NuGetCommand@2
  displayName: 'NuGet restore'
  inputs:
    restoreSolution: '$(solution)'

- task: VSBuild@1
  displayName: 'Build solution'
  inputs:
    solution: '$(solution)'
    msbuildArgs: '-p:DeployOnBuild=true -p:WebPublishMethod=Package -p:PackageAsSingleFile=true -p:SkipInvalidConfigurations=true -p:PackageLocation="$(build.artifactstagingdirectory)\\"'
    platform: '$(buildPlatform)'
    configuration: '$(buildConfiguration)'

- task: VSTest@2
  displayName: 'Test Assemblies'
  inputs:
    testAssemblyVer2: |
     **\$(buildConfiguration)\**\*test*.dll
     !**\obj\**
     !**\*testadapter.dll
    platform: '$(buildPlatform)'
    configuration: '$(buildConfiguration)'

- task: CopyFiles@2
  displayName: 'Copy UI Test Files to: $(build.artifactstagingdirectory)'
  inputs:
    SourceFolder: UITests
    TargetFolder: '$(build.artifactstagingdirectory)/uitests'

- task: PublishBuildArtifacts@1
  displayName: 'Publish Artifact'
  inputs:
    PathtoPublish: '$(build.artifactstagingdirectory)'
    ArtifactName: '$(artifactName)'
  condition: succeededOrFailed()
```

**Figura 10-9** -um exemplo de Azure-pipelines. yml

Essa definição de compilação usa várias tarefas internas que tornam a criação de compilações tão simples quanto a criação de um conjunto de Lego (mais simples do que o Giant Millennium Falcon). Por exemplo, a tarefa do NuGet restaura os pacotes NuGet, enquanto a tarefa VSBuild chama as ferramentas de Build do Visual Studio para executar a compilação real. Há centenas de tarefas diferentes disponíveis no Azure DevOps, com milhares de outras que são mantidas pela Comunidade. É provável que, independentemente das tarefas de compilação que você pretende executar, alguém tenha criado um já.

As compilações podem ser disparadas manualmente, por um check-in, em um agendamento ou pela conclusão de outra compilação. Na maioria dos casos, a criação de cada check-in é desejável. As compilações podem ser filtradas para que diferentes compilações sejam executadas em diferentes partes do repositório ou em diferentes ramificações. Isso permite cenários como a execução de compilações rápidas com testes reduzidos em solicitações pull e execução de um pacote de regressão completo no tronco em uma base noturna.

O resultado final de uma compilação é uma coleção de arquivos conhecidos como artefatos de compilação. Esses artefatos podem ser passados para a próxima etapa no processo de compilação ou adicionados a um feed de artefatos do Azure, para que possam ser consumidos por outras compilações.

### <a name="azure-devops-releases"></a>Versões do Azure DevOps

As compilações cuidam da compilação do software em um pacote freqüentemente, mas os artefatos ainda precisam ser enviados para um ambiente de teste para concluir a entrega contínua. Para isso, o Azure DevOps usa uma ferramenta separada chamada releases. A ferramenta de versões usa a biblioteca das mesmas tarefas que estava disponível para a compilação, mas introduziu um conceito de "estágios". Um estágio é um ambiente isolado no qual o pacote está instalado. Por exemplo, um produto pode fazer uso de um ambiente de desenvolvimento, QA e de produção. O código é entregue continuamente no ambiente de desenvolvimento em que os testes automatizados podem ser executados em relação a ele. Depois que esses testes passarem pela versão, o ambiente de QA será movido para teste manual. Por fim, o código é enviado para a produção, onde está visível para todos.

![Figura 10-10 um pipeline de lançamento de exemplo com fases de desenvolvimento, QA e produção](./media/release-pipeline.png)

**Figura 10-10** – pipeline de liberação

Cada estágio na compilação pode ser disparado automaticamente pela conclusão da fase anterior. Em muitos casos, no entanto, isso não é desejável. Mover o código para produção pode exigir aprovação de alguém. A ferramenta releases dá suporte a isso permitindo que os aprovadores em cada etapa do pipeline de lançamento. As regras podem ser configuradas de forma que uma pessoa ou grupo de pessoas específico deva se desconectar em uma versão antes de fazer a produção. Esses Gates permitem verificações manuais de qualidade e também para conformidade com quaisquer requisitos regulatórios relacionados ao controle do que entra em produção.

### <a name="everybody-gets-a-build-pipeline"></a>Todo mundo Obtém um pipeline de compilação

Não há nenhum custo para configurar muitos pipelines de Build, portanto, é vantajoso ter pelo menos um pipeline de compilação por microserviço. O ideal é que os microserviços sejam implantados independentemente em qualquer ambiente, de modo que cada um deles possa ser liberado por meio de seu próprio pipeline sem liberar uma massa de código não relacionado é perfeito. Cada pipeline pode ter seu próprio conjunto de aprovações, permitindo variações no processo de compilação para cada serviço.

### <a name="versioning-releases"></a>Versões de controle de versão

Uma desvantagem de usar a funcionalidade de versões é que ela não pode ser definida em um arquivo com check-in `azure-pipelines.yml` . Há muitas razões pelas quais você pode querer fazer isso de ter definições de versão por ramificação para incluir um esqueleto de versão em seu modelo de projeto. Felizmente, o trabalho é contínuo para mudar alguns dos estágios com suporte para o componente de compilação. Isso será conhecido como compilação de vários estágios e a [primeira versão estará disponível agora](https://devblogs.microsoft.com/devops/whats-new-with-azure-pipelines/)!

>[!div class="step-by-step"]
>[Anterior](azure-security.md) 
> [Avançar](feature-flags.md)
