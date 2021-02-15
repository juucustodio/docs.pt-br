---
title: Específicos de recurso do Windows Workflow Foundation
description: Este artigo descreve os novos recursos que .NET Framework 4 adiciona a Windows Workflow Foundation e cenários nos quais os recursos podem ser úteis.
ms.date: 03/30/2017
ms.assetid: e84d12da-a055-45f6-b4d1-878d127b46b6
ms.openlocfilehash: 6c508e184aee0e4aa0634d128de94ac45ef78f45
ms.sourcegitcommit: d8020797a6657d0fbbdff362b80300815f682f94
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/24/2020
ms.locfileid: "95716285"
---
# <a name="windows-workflow-foundation-feature-specifics"></a>Específicos de recurso do Windows Workflow Foundation

.NET Framework 4 adiciona uma série de recursos para Windows Workflow Foundation. Este documento descreve um número de recursos novos, e fornece detalhes sobre cenários em que podem ser úteis.

## <a name="messaging-activities"></a>Atividades de mensagem

As atividades de mensagens ( <xref:System.ServiceModel.Activities.Receive> , <xref:System.ServiceModel.Activities.SendReply> , <xref:System.ServiceModel.Activities.Send> , <xref:System.ServiceModel.Activities.ReceiveReply> ) são usadas para enviar e receber mensagens do WCF de seu fluxo de trabalho. <xref:System.ServiceModel.Activities.Receive> e <xref:System.ServiceModel.Activities.SendReply> as atividades são usadas para formar uma operação de serviço Windows Communication Foundation (WCF) que é exposta por meio do WSDL, assim como os serviços Web WCF padrão. <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.ReceiveReply> são usados para consumir um serviço Web semelhante a um WCF <xref:System.ServiceModel.ChannelFactory> ; uma experiência de **Adicionar referência de serviço** também existe para o Workflow Foundation que gera atividades pré-configuradas.

### <a name="getting-started-with-messaging-activities"></a>Guia de introdução com atividades de mensagem

- No Visual Studio 2012, crie um projeto de aplicativo do serviço de fluxo de trabalho WCF. Um par de <xref:System.ServiceModel.Activities.Receive> e de <xref:System.ServiceModel.Activities.SendReply> será colocado na tela.

- Clique com o botão direito do mouse no projeto e selecione **Adicionar referência de serviço**. Aponte para um Web Service WSDL existente e clique em **OK**. Crie seu projeto para mostrar as atividades geradas (implementadas usando <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.ReceiveReply> ) em sua caixa de ferramentas.

- [Documentação dos serviços de fluxo de trabalho](../wcf/feature-details/workflow-services.md)

### <a name="messaging-activities-example-scenario"></a>Cenário exemplo de atividades de mensagem

Um `BestPriceFinder` serviço chama vários serviços de companhia aérea para encontrar o melhor preço de tíquete para uma rota específica. A implementação desse cenário exige que você use as atividades de mensagem para receber a solicitação de preço, recuperar os preços dos serviços de back-end e responder à solicitação de preço com o melhor preço. Ele também exigiria que você usa outras atividades prontas para criar a lógica de negócios para calcular o melhor preço.

## <a name="workflowservicehost"></a>WorkflowServiceHost

O <xref:System.ServiceModel.WorkflowServiceHost> é o host de fluxo de trabalho pronto para uso que dá suporte a várias instâncias, configurações e mensagens do WCF (embora os fluxos de trabalho não sejam obrigados a usar o sistema de mensagens para serem hospedados). Ele também se integra com persistência, controle e controle de instância por meio de um conjunto de comportamentos de serviço. Assim como o WCF <xref:System.ServiceModel.ServiceHost> , o <xref:System.ServiceModel.WorkflowServiceHost> pode ser hospedado internamente em um aplicativo do console/WinForms/WPF ou serviço do Windows, ou hospedado na Web (como um arquivo. xamlx) no IIS ou no was.

### <a name="getting-started-with-workflow-service-host"></a>Guia de introdução com host de Serviço de Fluxo de Trabalho

- No Visual Studio 2010, crie um projeto de aplicativo do serviço de fluxo de trabalho WCF: este projeto será configurado para ser usado <xref:System.ServiceModel.WorkflowServiceHost> em um ambiente de host da Web.

- Para hospedar um fluxo de trabalho de não mensagem, adicione <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint> personalizado que criará a instância com base em uma mensagem.

- As instâncias de fluxo de trabalho podem ser controladas (por exemplo, suspensas ou encerradas) adicionando um <xref:System.ServiceModel.Activities.WorkflowControlEndpoint> ao <xref:System.ServiceModel.WorkflowServiceHost> e usando um <xref:System.ServiceModel.Activities.WorkflowControlClient> .

- Para Exemplos <xref:System.ServiceModel.WorkflowServiceHost> pode ser encontrado nas seções a seguir:

  - [Execução](./samples/execution.md)

  - Aplicativo: [Gerenciamento de instância suspenso](./samples/suspended-instance-management.md)

- [Visão geral de hospedar serviços de fluxo de trabalho](../wcf/feature-details/hosting-workflow-services-overview.md)

### <a name="workflowservicehost-scenario"></a>Cenário de WorkflowServiceHost

Um serviço BestPriceFinder chama vários serviços de companhia aérea para encontrar o melhor preço de tíquete para uma rota específica. A implementação desse cenário exigiria que você hospede o fluxo de trabalho no <xref:System.ServiceModel.WorkflowServiceHost> . Ele também usaria as atividades da mensagem para receber a solicitação de preço, recuperar os preços dos serviços de back-end e responder à solicitação de preço com o melhor preço.

## <a name="correlation"></a>Correlação

Uma correlação é uma das duas coisas:

- Uma maneira de mensagens de agrupamento juntos; ou seja, a relação entre uma mensagem de solicitação e sua resposta.

- Uma maneira para mapear uma parte de dados a uma instância de serviço

### <a name="getting-started"></a>Introdução

- Para começar com correlação, crie um novo projeto no Visual Studio. Crie uma variável do tipo <xref:System.ServiceModel.Activities.CorrelationHandle>.

- Um exemplo de correlação usado para agrupar mensagens seja adjacente uma correlação de solicitação de resposta que agrupe mensagens juntos.

  - Em uma <xref:System.ServiceModel.Activities.Receive> atividade, clique na <xref:System.ServiceModel.Activities.Receive.CorrelationInitializers%2A> propriedade e adicione uma <xref:System.ServiceModel.Activities.RequestReplyCorrelationInitializer> usando o CorrelationHandle criado na primeira etapa acima.

  - Crie uma <xref:System.ServiceModel.Activities.SendReply> atividade clicando com o botão direito do mouse no <xref:System.ServiceModel.Activities.Receive> e clicando em "criar SendReply". Cole-o no fluxo de trabalho após a atividade de <xref:System.ServiceModel.Activities.Receive> .

- Um exemplo de mapear uma parte de dados a uma instância do serviço é correlação conteudo base que mapeia um conjunto de dados (por exemplo, um ID de ordem) para uma determinada instância de fluxo de trabalho.

  - Em quaisquer atividades de mensagem, clique na propriedade de `CorrelationInitializers` e adicione <xref:System.ServiceModel.Activities.QueryCorrelationInitializer> usando a variável de <xref:System.ServiceModel.Activities.CorrelationHandle> criado anterior. Clique duas vezes na propriedade desejada na mensagem (por exemplo, OrderID) no menu suspenso. Defina a propriedade de `CorrelatesWith` à variável de <xref:System.ServiceModel.Activities.CorrelationHandle> usado anterior.

- [Documentação conceitual de correlação](../wcf/feature-details/correlation.md)

### <a name="correlation-scenario"></a>Cenário de correlação

Um fluxo de trabalho de processamento de pedidos é usado para lidar com a criação de novos pedidos e a atualização de pedidos existentes que estão em processo. A implementação desse cenário exigiria que você hospede o fluxo de trabalho no <xref:System.ServiceModel.WorkflowServiceHost> e use as atividades de mensagens. Ele também exigiria a correlação com base no `orderId` para garantir que as atualizações sejam feitas no fluxo de trabalho correto.

## <a name="simplified-configuration"></a>Configuração simplificada

O esquema de configuração do WCF é complexo e fornece aos usuários muitos recursos difíceis de encontrar. No [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] , nos concentramos em ajudar os usuários do WCF a configurar seus serviços com os seguintes recursos:

- Eliminando a necessidade para a configuração explícita por serviço. Se você não configurar nenhum \<service> elemento para o serviço e seu serviço não definir nenhum ponto de extremidade programaticamente, um conjunto de pontos de extremidade será adicionado automaticamente ao seu serviço, um por endereço base de serviço e por contrato implementado pelo seu serviço.

- Permite que o usuário para definir valores padrão para associações e comportamentos de WCF, que serão aplicados aos serviços sem a configuração explícita.

- Os pontos de extremidade padrão definem pontos de extremidade pré-configurados reutilizáveis, que têm valores fixos para uma ou mais propriedades de ponto de extremidade (endereço, associação e contrato), e reservam-nos definir propriedades personalizadas.

- Por fim, o <xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601> permite que você faça o gerenciamento central da configuração do cliente WCF, útil em cenários em que a configuração é selecionada ou alterada após o tempo de carregamento do domínio do aplicativo.

### <a name="getting-started"></a>Introdução

- [O guia de um desenvolvedor a WCF 4,0](/previous-versions/dotnet/articles/ee354381(v=msdn.10))

- [Factory do canal de configuração](xref:System.ServiceModel.Configuration.ConfigurationChannelFactory%601)

- [Elemento padrão de ponto de extremidade](xref:System.ServiceModel.Configuration.StandardEndpointElement)

- [Aprimoramentos de configuração de serviço no .NET Framework 4](/archive/blogs/endpoint/service-configuration-improvements-in-net-4)

- [Erro comum de usuário em .NET 4: Mistyping o nome da configuração de serviço de WF/WCF](/archive/blogs/endpoint/common-user-mistake-in-net-4-mistyping-the-wfwcf-service-configuration-name)

### <a name="simplified-configuration-scenarios"></a>Cenários simplificados de configuração

- Um desenvolvedor ASMX experiente deseja começar a usar o WCF. No entanto, o WCF parece muito complicado! Que é todas essas informações que eu preciso de gravar em um arquivo de configuração? Em .NET 4, você ainda pode decidir não ter um arquivo de configuração de qualquer.

- Um conjunto existente de serviços WCF é muito difícil de configurar e manter. O arquivo de configuração possui milhares de linhas de código XML que são bastante perigosas para tocar. Ajuda é necessária para reduzir a quantidade de código para algo manejável.

## <a name="data-contract-resolver"></a>Resolução do contrato de dados

No .NET Framework 3,5, havia algumas limitações no design de tipos conhecidos:

- Adicionar tipos conhecidos dinamicamente, durante a serialização desserialização, ou não foi possível.

- Os serializadores não pode manipular informações desconhecida de xsi:type .

- Não foi possível que usuários especificar que xsi:type de deseja ou não ter aparecer no fio, por exemplo, faça o tamanho de uma instância de serialização no fio menor.

O [DataContractResolver](../wcf/samples/datacontractresolver.md) resolve esses problemas no .NET Framework 4,5.

### <a name="getting-started"></a>Introdução

- [Documentação da API de resolução do contrato de dados](xref:System.Runtime.Serialization.DataContractResolver)

- [Introdução ao resolvedor do contrato de dados](/archive/blogs/youssefm/configuring-known-types-dynamically-introducing-the-datacontractresolver)

- Exemplos:

  - [DataContractResolver](../wcf/samples/datacontractresolver.md)

  - [KnownAssemblyAttribute](../wcf/samples/knownassemblyattribute.md)

### <a name="data-contract-resolver-scenarios"></a>Cenários de resolução do contrato de dados

- Evitar ter que declarar <xref:System.Runtime.Serialization.KnownTypeAttribute> de dez objetos em um serviço.

- Reduzindo o tamanho da operação XML.

## <a name="flowchart"></a>Fluxograma

O fluxograma é um paradigma conhecido para representar visualmente problemas de domínio. É um novo estilo de fluxo de controle que estamos introduzindo no .NET Framework 4. Uma característica principal do fluxograma é que apenas uma atividade é executada em um determinado momento. Os fluxogramas podem expressar loop e resultados alternativos, mas não podem expressar nativo a execução simultânea de vários nós.

### <a name="getting-started"></a>Introdução

- No Visual Studio 2012, crie um aplicativo de console de fluxo de trabalho. Adicione um fluxograma no designer de fluxo de trabalho.

- O recurso de fluxograma usa as seguintes classes:

  - <xref:System.Activities.Statements.Flowchart>

  - <xref:System.Activities.Statements.FlowNode>

  - <xref:System.Activities.Statements.FlowDecision>

  - <xref:System.Activities.Statements.FlowStep>

  - <xref:System.Activities.Statements.FlowSwitch%601>

- Exemplos:

  - [Tratamento de falha em uma atividade do fluxograma usando TryCatch](./samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)

  - [Processo de aluguer](./samples/hiring-process.md)

- Documentação do designer:

  - [Designers de atividade de fluxograma](/visualstudio/workflow-designer/flowchart-activity-designers)

### <a name="flowchart-scenarios"></a>Cenários do fluxograma

Uma atividade do fluxograma pode ser usada para implementar um jogo de estimativa. O jogo de estimativa é muito simples: o computador seleciona um número aleatório e o jogador tem que descobrir esse número. Quando o jogador envia cada estimativa, o computador mostra uma dica (ou seja, "Experimente um número mais baixo"). Se o Player encontrar o número em menos de 7 tentativas, ele receberá uma congratulação especial do computador. Esse kit pode ser implementado com uma combinação das seguintes atividades procedurais:

- <xref:System.Activities.Statements.Sequence>

- <xref:System.Activities.Statements.While>

- <xref:System.Activities.Statements.Switch%601>

- <xref:System.Activities.Statements.TryCatch>

- <xref:System.Activities.Statements.Assign%601>

- <xref:System.Activities.Statements.If>

## <a name="procedural-activities-sequence-if-foreach-switch-assign-dowhile-while"></a>Atividades procedurais (sequência, se, ForEach, alterne, atribui, DoWhile, quando)

As atividades procedurais fornecem um mecanismo para o fluxo de controle em um modelo usando os conceitos que são familiares para programadores. Essas atividades permitem construções de linguagem de programação tradicionalmente estruturadas e, quando apropriado, fornecem paridade de linguagem com linguagens de procedimento comuns, como C# e Visual Basic.

### <a name="getting-started"></a>Introdução

- No Visual Studio 2012, crie um aplicativo de console de fluxo de trabalho. Adicione atividades procedurais no designer de fluxo de trabalho.

- Exemplos:

  - [Processo de aluguer](./samples/hiring-process.md)

  - [Processo de compra corporativo](./samples/corporate-purchase-process.md)

- Documentação do designer:

  - [Designer de atividade Parallel](/visualstudio/workflow-designer/parallel-activity-designer)

  - [Designer de atividade\<T> ParallelForEach](/visualstudio/workflow-designer/parallelforeach-t-activity-designer)

### <a name="procedural-activity-scenarios"></a>Cenários procedurais de atividades

- <xref:System.Activities.Statements.Parallel>: Um sistema de gerenciamento de documentos de intranet tem um fluxo de trabalho de aprovação de documentos. Documentos precisam ser aprovados por pessoas em vários departamentos antes que eles sejam publicado a intranet. Não há uma ordem estabelecida para as aprovações; Eles podem ocorrer a qualquer momento enquanto o documento estiver na fase de "aprovação pendente". Quando um usuário envia um documento para revisão, ele deve ser aprovado pelo gerente direto, pelo administrador da intranet e pelo Gerenciador de comunicações interno.

- <xref:System.Activities.Statements.ParallelForEach%601>: Um aplicativo de WF gerencia compras corporativos dentro de uma grande empresa. As regras corporativos determina que planejando antes que qualquer operação de compras, as avaliações de três fornecedores diferentes são necessárias. Um funcionário do departamento de compras seleciona três fornecedores da lista de fornecedores da empresa. Depois que esses fornecedores foram selecionados e notificados, a empresa esperará suas propostas econômicas. As propostas podem vie em qualquer ordem. Para implementar esse cenário em WF, usamos <xref:System.Activities.Statements.ParallelForEach%601> que iterará através da coleção de fornecedores e solicitará suas propostas econômicas. As oferece são coletadas completos, melhor é selecionado e exibido.

## <a name="invokemethod"></a>InvokeMethod

A atividade de <xref:System.Activities.Statements.InvokeMethod> reserva chamar métodos públicos em objetos ou no escopo. Suporta chamar métodos de instância e estática com ou sem parâmetros (que incluem matrizes de parâmetros), e métodos genéricos. Também permite executar o método forma síncrona e de forma assíncrona.

### <a name="getting-started"></a>Introdução

- No Visual Studio 2012, crie um aplicativo de console de fluxo de trabalho. Adicione uma atividade de <xref:System.Activities.Statements.InvokeMethod> no designer de fluxo de trabalho, e configurar métodos estáticos e de instância nele.

- Documentação do designer: [Designer de atividade InvokeMethod](/visualstudio/workflow-designer/invokemethod-activity-designer)

### <a name="invokemethod-scenarios"></a>Cenários de InvokeMethod

- Um método em um objeto no escopo precisa ser chamado. Por exemplo, um valor precisa ser adicionado a um dicionário. Adicione o método de instância do dicionário é invocado, e a chave e o valor é fornecido.

- Um método precisa ser chamado em um objeto CLR herdado. Em vez de criar uma atividade personalizado para envolver a chamada à classe herdado, se estiver no escopo durante a execução de fluxo de trabalho, <xref:System.Activities.Statements.InvokeMethod> pode ser usado.

## <a name="error-handling-activities"></a>Atividades de tratamento de erro

A <xref:System.Activities.Statements.TryCatch> atividade fornece um mecanismo para capturar exceções que ocorrem durante a execução de um conjunto de atividades contidas (semelhante à construção try/catch em C# e Visual Basic). <xref:System.Activities.Statements.TryCatch> fornece tratamento de exceção a nível de fluxo de trabalho. Quando uma exceção sem tratamento é gerada, o fluxo de trabalho é anulado e o bloco finally não será executado. Esse comportamento é consistente com o C#.

### <a name="getting-started"></a>Introdução

- No Visual Studio 2012, crie um aplicativo de console de fluxo de trabalho. Adicione uma atividade de <xref:System.Activities.Statements.TryCatch> no designer de fluxo de trabalho.

- Exemplo: [tratamento de falhas em uma atividade de fluxograma usando TryCatch](./samples/fault-handling-in-a-flowchart-activity-using-trycatch.md)

- Documentação do designer: [erro ao manipular designers de atividade](/visualstudio/workflow-designer/error-handling-activity-designers)

### <a name="error-handling-scenarios"></a>Cenários de manipulação de erro

Um conjunto de atividades precisa ser executado, e a lógica específica precisa ser executada quando ocorre um erro. Se durante essa lógica de tratamento de erros que se encontra o erro é não recuperável, a exceção será rethrown, e a atividade pai (ou o host) manipulará o problema.

## <a name="pick-activity"></a>Atividade de picareta

A atividade de <xref:System.Activities.Statements.Pick> fornece o fluxo de controle baseado em que modela WF. <xref:System.Activities.Statements.Pick> contém várias ramificações onde cada ramificação espera um determinado evento ocorra antes de executar. Nessa configuração, <xref:System.Activities.Statements.Pick> se comporta semelhante a <xref:System.Activities.Statements.Switch%601> que a atividade será executado somente de um conjunto de eventos que está escuta. Cada ramificação é causado evento e o evento que ocorre executa a ramificação correspondente primeiro. Quaisquer outras ramificações cancelarem e param de ouvir eventos.

### <a name="getting-started"></a>Introdução

- No Visual Studio 2012, crie um aplicativo de console de fluxo de trabalho. Adicione uma atividade de <xref:System.Activities.Statements.Pick> no designer de fluxo de trabalho.

- Exemplo: [usando a atividade de seleção](./samples/using-the-pick-activity.md)

- Documentação do designer: [escolher designer de atividade](/visualstudio/workflow-designer/pick-activity-designer)

### <a name="pick-scenario"></a>Cenário de picareta

Um usuário precisa ser solicitado para a entrada. Em circunstâncias normais, o desenvolvedor usaria uma chamada de método como <xref:System.Console.ReadLine%2A> para solicitar uma entrada de usuário. O problema com essa configuração é que o programa espera até que o usuário digite algo. Nesse cenário, um tempo limite é necessário desbloquear uma atividade de bloqueio. Um cenário comum é um que requer uma tarefa ser concluído em uma determinada duração de tempo. Tempo para fora uma atividade de bloqueio é um cenário onde a picareta adicionar muito valor.

## <a name="wcf-routing-service"></a>WCF que requer o serviço

O serviço de roteamento foi projetado para ser um roteador de software genérico que permite controlar como as mensagens do WCF fluem entre seus clientes e serviços. O serviço de roteamento permite dissociar seus clientes de seus serviços, o que oferece muito mais liberdade em termos das configurações às quais você pode dar suporte e a flexibilidade que você tem ao considerar como hospedar seus serviços. No .NET Framework 3,5, os clientes e os serviços foram rigidamente acoplados; um cliente tinha que saber sobre todos os serviços necessários para falar e onde eles estavam localizados. Além disso, o WCF no .NET Framework 3,5 tinha as seguintes limitações:

- Manipulação de erro foi complexo, como essa lógica tinha que ser embutido no cliente.

- Os clientes e serviços tinham que sempre usar as mesmas associações.

- Os serviços foram raramente bom acrescentado: é mais fácil ter a conversa de cliente a um serviço que implementa todos, em vez de precisando de escolher entre vários serviços.

O serviço de roteamento no .NET 4 foi projetado para facilitar a solução desses problemas. O novo serviço de roteamento possui os seguintes recursos:

1. O conteúdo do roteamento (os objetos de<xref:System.ServiceModel.Dispatcher.MessageFilter> examinar uma mensagem para determinar onde deve ser enviada.)

2. Ponte de protocolo (mensagem de & de transporte)

3. Tratamento de erros (o roteador captura exceções de comunicação e efetua o failover para pontos de extremidade alternativos)

4. (Na memória) atualização dinâmica de <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601> e configuração de roteamento.

### <a name="getting-started"></a>Introdução

1. Documentação: [Roteamento](../wcf/feature-details/routing.md)

2. Exemplos: [serviços de roteamento &#91;exemplos do WCF&#93;](../wcf/samples/routing-services.md)

3. Blog: [regras de roteamento!](/archive/blogs/RoutingRules/)

### <a name="routing-scenarios"></a>Cenários de roteamento

O serviço de roteamento é útil nas seguintes situações:

- Os clientes podem falar a vários serviços sem ter que evitá-los diretamente todos.

- Os clientes podem executar lógica adicional em uma solicitação de cliente determinar onde rotear-la

- Decompor as operações que um cliente é executado em várias implementações de serviço sem refatoração o cliente.

- Os clientes e serviços podem falar associações diferentes com as configurações de segurança diferentes.

- Os clientes podem ser ativados para ser mais robustos contra a falhar ou a indisponibilidade de serviços.

## <a name="wcf-discovery"></a>Descoberta de WCF

A descoberta do WCF é uma tecnologia de estrutura que permite incorporar um mecanismo de descoberta à sua infraestrutura de aplicativo. Você pode usar esse para fazer o serviço para descobrir, e configurar seus clientes para procurar pelos serviços. Os clientes não precisam ser codificados difícil com ponto final, fazendo seu aplicativo mais robusta e tolerante falha. A descoberta é a plataforma perfeita para compilar recursos de uma configuração em seu aplicativo.

O produto é construído sobre o padrão de WS- descoberta. Ele foi projetado para ser interoperável, extensível e genérico. O modo de apoios ao produto dois de operação:

1. Gerenciado: onde há uma entidade na rede conhecedoa sobre serviços existentes, os clientes consultar-la diretamente para informações. Isso é análogo a Ative Directory.

2. Ad hoc: onde mensagens multicast de clientes usam localizar serviços.

Além disso, as mensagens de descoberta são protocolo de rede desconhecido; você pode usá-los em superior qualquer protocolo que oferecer suporte aos requisitos de modo. Por exemplo, as mensagens de multicast de descoberta podem ser enviadas pelo canal UDP ou qualquer outra rede que dê suporte a mensagens multicast. Esses pontos de design, combinados com flexibilidade de recursos, permitem que você adapte a descoberta especificamente para sua solução.

### <a name="getting-started"></a>Introdução

- Documentação: [descoberta do WCF](../wcf/feature-details/wcf-discovery.md)

- Exemplos: [descoberta (amostras)](../wcf/samples/discovery-samples.md)

### <a name="discovery-scenarios"></a>Cenários de descoberta

Um desenvolvedor não deseja para pontos de extremidade difícil de código, desde que é conhecido quando serviço my estão disponíveis. Em vez disso, o desenvolvedor deseja escolha um serviço em runtime. Mais desacoplar, vigor, e uma configuração são necessários entre os componentes no aplicativo.

## <a name="tracking"></a>Acompanhamento

O rastreamento de fluxo de trabalho fornece informações sobre a execução de uma instância de fluxo de trabalho. Os eventos de rastreamento são emitidos de um fluxo de trabalho no nível da instância do fluxo de trabalho e quando as atividades no fluxo de trabalho são executadas. Um participante de acompanhamento de fluxo de trabalho precisa ser adicionado ao host de fluxo de trabalho para assinar a acompanhar registros. Os registros de rastreamento são filtrados utilizando um perfil de rastreamento. O .NET Framework fornece um participante de acompanhamento de ETW (rastreamento de eventos para Windows) e um perfil básico é instalado no arquivo de machine.config.

### <a name="getting-started"></a>Introdução

1. No Visual Studio 2010, crie um projeto de aplicativo do serviço de fluxo de trabalho WCF. Um par de <xref:System.ServiceModel.Activities.Receive> e de <xref:System.ServiceModel.Activities.SendReply> será colocado na tela para o início.

2. Abra o web.config e adicionar um comportamento de rastreamento de ETW sem o perfil.

    1. O perfil padrão é usado.

    2. Abra o Visualizador de eventos e habilite o canal analítico no seguinte nó: **Visualizador de eventos**, **logs de aplicativos e serviços**, **Microsoft**, **Windows**, **servidor de aplicativos-aplicativos**. Clique com o botão direito do mouse em **analítica** e selecione **habilitar log**.

    3. Execute o serviço de fluxo de trabalho.

    4. Observe os eventos de rastreamento de fluxo de trabalho no visualizador de eventos.

3. Exemplos: [acompanhamento](./samples/tracking.md)

4. Documentação conceitual: rastreamento [e acompanhamento de fluxo de trabalho](workflow-tracking-and-tracing.md)

## <a name="sql-workflow-instance-store"></a>Store instância de fluxo de trabalho do SQL

<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> é uma implementação com base no servidor SQL de um armazenamento de instância. Um armazenamento de instância armazena o estado de uma instância em execução junto com todos os dados necessários carregar e continuar essa instância. O host serviço instrui o armazenamento de instância para salvar o estado da instância se o fluxo de trabalho persistir, e instrui o armazenamento de instância para carregar o estado da instância quando uma mensagem chega para essa instância ou uma atividade do atraso expira.

### <a name="getting-started"></a>Introdução

1. No Visual Studio 2012, crie um fluxo de trabalho que contenha uma atividade implícita ou explícita <xref:System.Activities.Statements.Persist> . Adicionar o comportamento de <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> ao seu host serviço de fluxo de trabalho. Isso pode ser feito no código ou no arquivo de configuração do aplicativo.

2. Exemplos: [persistência](/previous-versions/dotnet/netframework-4.0/dd699769(v%3dvs.100))

3. Documentação conceitual: [repositório de instância do fluxo de trabalho SQL](sql-workflow-instance-store.md).
