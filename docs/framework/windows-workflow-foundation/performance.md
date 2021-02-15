---
title: Desempenho do Windows Workflow Foundation 4
description: Este artigo explica as características de desempenho da revisão principal do Windows Workflow Foundation, que faz parte do .NET Framework 4.
ms.date: 03/30/2017
ms.assetid: 67d2b3e8-3777-49f8-9084-abbb33b5a766
ms.openlocfilehash: f77ebaeb0b59dea1a75594c7425b960e3fe839cb
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96246544"
---
# <a name="windows-workflow-foundation-4-performance"></a>Desempenho do Windows Workflow Foundation 4

 O .NET Framework 4 inclui uma revisão principal do Windows Workflow Foundation (WF) com investimentos pesados em desempenho. Essa nova revisão apresenta alterações de design significativas das versões anteriores do [!INCLUDE[wf1](../../../includes/wf1-md.md)] que foram fornecidas como parte do .NET Framework 3,0 e .NET Framework 3,5. Foi re bem - principal do modelo, em runtime, e o trabalho feito com ferramentas de programação melhorar bastante o desempenho e a usabilidade. Este tópico mostra as características de desempenho importantes dessas revisões e compara-as com essas de versão anterior.

 O desempenho componente de fluxo de trabalho individual disparou por pedidos de magnitude entre WF3 e WF4.  Isso deixa a lacuna entre os serviços de Windows Communication Foundation em código (WCF) e os serviços de fluxo de trabalho do WCF serem bem pequenos.  A latência de fluxo de trabalho foi reduzida significativamente em WF4.  O desempenho de persistência gerado por um fator de 2,5 - 3,0.  Monitoramento da integridade por meio de acompanhamento de fluxo de trabalho tem significativamente menos sobrecarga.  Essas são razões de migrar ou peso a adotar WF4 em seus aplicativos.

## <a name="terminology"></a>Terminologia

 A versão do [!INCLUDE[wf1](../../../includes/wf1-md.md)] introduzida no .NET Framework 4 será chamada de WF4 para o restante deste tópico. [!INCLUDE[wf1](../../../includes/wf1-md.md)] foi introduzido no .NET Framework 3,0 e tinha algumas revisões secundárias por meio do .NET Framework 3,5 SP1. A versão .NET Framework 3,5 do Workflow Foundation será chamada de WF3 para o restante deste tópico. WF3 é fornecido no .NET Framework 4 lado a lado com WF4. Para obter mais informações sobre como migrar artefatos do WF3 para o WF4, consulte: [Guia de migração do Windows Workflow Foundation 4](migration-guidance.md).

 O Windows Communication Foundation (WCF) é o modelo de programação unificado da Microsoft para a criação de aplicativos orientados a serviços. Ele foi introduzido pela primeira vez como parte do .NET Framework 3,0 junto com WF3 e agora é um dos principais componentes do .NET Framework.

 Windows Server AppFabric é um conjunto de tecnologias integrados que tornam mais fácil criar, redimensionar e gerenciar Web e aplicativos compostos que executam no IIS. Fornece ferramentas para monitorar e gerenciar serviços e fluxos de trabalho. Para obter mais informações, consulte [Windows Server AppFabric 1,0](/previous-versions/appfabric/ff384253(v=azure.10)).

## <a name="goals"></a>Metas

 O objetivo deste tópico é mostrar as características de desempenho de WF4 com os dados medidas para diferentes cenários. Também fornece comparações detalhadas entre WF4 e WF3, e mostra o grandes aprimoramentos que foram feitas nessa nova revisão. Os cenários e os dados apresentados neste artigo determinam o custo subjacentes de diferentes aspectos de WF4 e de WF3. Esses dados são úteis para entender as características de desempenho de WF4 e podem ser úteis em migrações de planejamento de WF3 a WF4 ou WF4 de uso durante o desenvolvimento de aplicativos. No entanto, cuidado deve ser recolhido as conclusões desenhadas de dados apresentados neste artigo. O desempenho de um aplicativo de fluxo de trabalho composto é altamente dependente em como o fluxo de trabalho é implementado e como os diferentes componentes são integrados. Se deve abranger cada aplicativo para determinar as características de desempenho do aplicativo.

## <a name="overview-of-wf4-performance-enhancements"></a>Visão geral dos aprimoramentos de desempenho WF4

 WF4 cuidadosamente foi criado e implementado com alto desempenho e escalabilidade que são descritas nas seções.

### <a name="wf-runtime"></a>Runtime de WF

 O núcleo de runtime de [!INCLUDE[wf1](../../../includes/wf1-md.md)] é um agendador assíncrono que resulta a execução das atividades em um fluxo de trabalho. Fornece um ambiente performant, previsível de execução para atividades. O ambiente tem um contrato bem definido para execução, a seguir, a conclusão, cancelamento, as exceções, e um modelo de threads previsível.

 Em comparação com WF3, o runtime WF4 tem um agendador mais eficiente. Ele aproveita o mesmo pool de threads de e/s usado para o WCF, que é muito eficiente na execução de itens de trabalho em lote. A fila de agendador interna de item de trabalho é otimizado para a maioria de padrões comuns de uso. O tempo de execução do WF4 também gerencia os Estados de execução de forma muito leve com a lógica mínima de manipulação de eventos e de sincronização, enquanto o WF3 depende do registro e da invocação de eventos pesados para executar uma sincronização complexa para transições de estado.

### <a name="data-storage-and-flow"></a>Armazenamento de dados e fluxo

 Em WF3, os dados associados com uma atividade são modelados através das propriedades de dependência implementadas pelo tipo <xref:System.Windows.DependencyProperty>. O padrão de propriedade de dependência foi introduzido no Windows Presentation Foundation (WPF). Normalmente, esse padrão é muito flexível dar suporte à associação fácil de dados e outros recursos de interface do usuário. No entanto, o padrão requer as propriedades ser definido como campos estáticos na definição de fluxo de trabalho. Sempre que o runtime de [!INCLUDE[wf1](../../../includes/wf1-md.md)] obtém ou define os valores de propriedade, envolve a lógica pesado- tornada mais pesada de consulta.

 Lógica clara do escopo de dados dos usos WF4 para melhorar bastante como os dados são tratados em um fluxo de trabalho. Separa os dados armazenados em uma atividade dos dados que estão de fluxo através de limites de atividade usando dois conceitos distintos: variáveis e argumentos. Usando um escopo hierárquico claro para variáveis e argumentos "in/out/InOut", a complexidade do uso de dados para atividades é drasticamente reduzida e o tempo de vida dos dados também é automaticamente definido como escopo. As atividades tem uma assinatura bem definido descrita por seus argumentos. Simplesmente inspecionando uma atividade você pode determinar que espera dados e receber dados que serão gerados por eles como resultado da execução.

 Nas atividades WF3 foram inicializados quando um fluxo de trabalho foi criado. Em atividades de WF 4 são inicializados somente quando as atividades correspondentes estão executando. Isto permite um ciclo de vida mais simples de atividade sem executar operações inicializa/Uninitialize quando uma nova instância de fluxo de trabalho é criada, e assim obtido em mais eficiência

### <a name="control-flow"></a>Fluxo de Controle

 Assim como em qualquer linguagem de programação, [!INCLUDE[wf1](../../../includes/wf1-md.md)] fornece suporte para fluxos de controle para definições de fluxo de trabalho apresentando um conjunto de atividades de fluxo de controle para arranjar seqüencialmente, padrões loop, ramificar e outros. Em WF3, quando a mesma atividade precisa ser executada, novo <xref:System.Workflow.ComponentModel.ActivityExecutionContext> é criado e a atividade é clonada com uma lógica pesada de serialização e desserialização de baseada em <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>. Geralmente o desempenho para fluxos de controle iterativos é muito mais lento do que executando uma sequência de atividades.

 WF4 manipula esse bem diferente. Leva o modelo de atividade, cria um novo objeto de ActivityInstance, e adicioná-lo a fila de agendador. Todo esse processo envolve apenas a criação explícita de objetos e é muito leve.

### <a name="asynchronous-programming"></a>Programação assíncrona

 Os aplicativos geralmente têm um melhor desempenho e escalabilidade com programação assíncrona para operações longas de bloqueio como E/S ou operações distribuídos de computação. WF4 fornece suporte assíncrono por tipos de base <xref:System.Activities.AsyncCodeActivity>de atividade, <xref:System.Activities.AsyncCodeActivity%601>. O runtime entende nativo que as atividades assíncronos e portanto podem automaticamente colocar a instância em uma zona sem persistir quando o trabalho assíncrono está excelente. As atividades personalizados podem derivar desses tipos para executar o trabalho assíncrona sem armazenar o segmento de agendador de fluxo de trabalho e bloquear quaisquer atividades que podem ser capaz executar paralelamente.

### <a name="messaging"></a>Mensagens

 Inicialmente WF3 tinha muito suporte limitado de mensagem com as chamadas de eventos externos ou serviços da Web. No .NET Framework 3,5, os fluxos de trabalho podem ser implementados como clientes WCF ou expostos como serviços WCF por meio <xref:System.Workflow.Activities.SendActivity> de e <xref:System.Workflow.Activities.ReceiveActivity> . No WF4, o conceito de programação de mensagens baseada em fluxo de trabalho foi ainda mais reforçado por meio da forte integração da lógica de mensagens do WCF ao WF.

 O pipeline de processamento de mensagens unificadas fornecido no WCF no .NET 4 ajuda os serviços WF4s a ter desempenho e escalabilidade significativamente melhores que o WF3. WF4 também fornece um meio de programação mais sofisticado de mensagem que pode modelar padrão complexos (MEPs) de Exchange de mensagem. Os desenvolvedores podem usar contratos de serviço tipados obter programação fácil ou contratos de serviço un- tipados obter melhor desempenho sem pagar custo de serialização. Suporte do lado do cliente de cachê do canal por meio da classe <xref:System.ServiceModel.Activities.SendMessageChannelCache> em desenvolvedores de ajuda WF4 criar aplicativos rápidos com esforço mínimo. Para obter mais informações, consulte [alterando os níveis de compartilhamento de cache para atividades de envio](../wcf/feature-details/changing-the-cache-sharing-levels-for-send-activities.md).

### <a name="declarative-programming"></a>Programação declarativa

 WF4 fornece uma estrutura declarativamente limpa e de programação simples para modelar processos comerciais e serviços. O modelo de programação oferece suporte a composição totalmente declarativa de atividades, sem nenhum código ao lado de simplificando, bastante a criação de fluxo de trabalho. No .NET Framework 4, a estrutura de programação declarativa baseada em XAML foi unificada no único assembly System.Xaml.dll para dar suporte ao WPF e ao WF.

 Em WF4, XAML fornece uma experiência realmente declarativamente e permite-à definição inteira de fluxo de trabalho ser definida na marcação XML, referenciando atividades e digitar .NET de usar compilado. Isso foi difícil de fazer em WF3 com formato de XOML sem quebrar o personalizado code-behind de lógica. O novo XAML-Stack no .NET 4 tem um desempenho muito melhor na serialização/desserialização de artefatos de fluxo de trabalho e torna a programação declarativa mais atraente e sólida.

### <a name="workflow-designer"></a>Designer de Fluxo de Trabalho

 Suporte de programação completamente declarativo para WF4 aplicar explicitamente um mais altos requisitos para desempenho de tempo de design para grandes fluxos de trabalho. O designer de fluxo de trabalho em WF4 tem a escalabilidade muito melhor para grandes fluxos de trabalho do que aquela para WF3. Com suporte a virtualização de interface do usuário, o designer pode facilmente carregar um grande fluxo de trabalho 1000 atividades em alguns segundos, quando é quase impossível carregar um fluxo de trabalho algumas cem atividades com o designer WF3.

## <a name="component-level-performance-comparisons"></a>Comparações de desempenho de nível por componente

 Esta seção contém dados em comparações diretas entre atividades individuais em fluxos de trabalho WF3 e WF4.  Os pontos chave como a persistência tem um impacto no desempenho mais profundo dos componentes individuais de atividade.  As melhorias de desempenho em componentes individuais em WF4 são importantes embora porque os componentes são agora rápidos o suficiente para ser comparados com a lógica mão- valor de orquestração.  Um exemplo do que é abordado na próxima seção: "cenário de composição de serviço".

### <a name="environment-setup"></a>Configuração do ambiente

 ![Configuração do ambiente para medição de desempenho do fluxo de trabalho](./media/performance/performance-test-environment.gif)

 A figura anterior mostra a configuração de máquina usada para medidas de desempenho de nível por componente. Um único servidor e cinco clientes conectados sobre uma interface de rede Ethernet 1-Gbps. Para medidas fácil, o servidor é configurado para usar um único principal de um servidor dual de proc/principal executando Windows Server 2008 x. A utilização da CPU do sistema é mantida em quase 100%.

### <a name="test-details"></a>Detalhes do teste

 O WF3 <xref:System.Workflow.Activities.CodeActivity> é provável a atividade a mais simples que pode ser usada em um fluxo de trabalho WF3.  A atividade chama um método no code-behind que o programador de fluxo de trabalho pode colocar código em personalizado.  Em WF4, não há analógico direto ao WF3 <xref:System.Workflow.Activities.CodeActivity> que fornece a mesma funcionalidade.  Observe que há uma classe base de <xref:System.Activities.CodeActivity> em WF4 que não está relacionado ao WF3 <xref:System.Workflow.Activities.CodeActivity>.  Os autores de fluxo de trabalho são incentivados criar atividades personalizados e criar fluxos de trabalho XAML-only.  Nos testes abaixo, uma atividade chamada `Comment` é usada no lugar de <xref:System.Workflow.Activities.CodeActivity> vazia em fluxos de trabalho WF4.  O código na atividade de `Comment` é a seguinte:

```csharp
[ContentProperty("Body")]
    public sealed class Comment : CodeActivity
    {
        public Comment()
            : base()
        {
        }

        [DefaultValue(null)]
        public Activity Body
        {
            get;
            set;
        }

        protected override void Execute(CodeActivityContext context)
        {
        }
    }
```

### <a name="empty-workflow"></a>Fluxo de trabalho vazio

 Este teste usa um fluxo de trabalho da sequência sem atividades filhos.

### <a name="single-activity"></a>Única atividade

 O fluxo de trabalho é um fluxo de trabalho da sequência que contém uma atividade filho.  A atividade é <xref:System.Workflow.Activities.CodeActivity> sem código em casos WF3 e uma atividade de `Comment` em casos WF4.

### <a name="while-with-1000-iterations"></a>Quando com 1000 iterações

 O fluxo de trabalho da sequência contém uma atividade de <xref:System.Activities.Statements.While> com uma atividade filho no loop que não executa qualquer trabalho.

### <a name="replicator-compared-to-parallelforeach"></a>Replicator comparou a ParallelForEach

 <xref:System.Workflow.Activities.ReplicatorActivity> em WF3 tem modos de execução sequencial e paralela.  No modo sequencial, o desempenho da atividade é semelhante a <xref:System.Workflow.Activities.WhileActivity>.  <xref:System.Workflow.Activities.ReplicatorActivity> é mais útil para execução paralela.  O WF4 analógico para essa é a atividade de <xref:System.Activities.Statements.ParallelForEach%601> .

 O diagrama a seguir mostra os fluxos de trabalho usados para esse teste. O trabalho WF3 estão à esquerda e o trabalho WF4 estão à direita.

 ![WF3 ReplicatorActivity e WF4 ParallelForEach](./media/performance/replicator-parallel-wf3-wf4.gif)

### <a name="sequential-workflow-with-five-activities"></a>Fluxo de trabalho sequencial com cinco atividades

 Este teste serve mostrar o efeito de ter várias atividades executa em ordem.  Há cinco atividades na sequência.

### <a name="transaction-scope"></a>Escopo de transação

 O teste do escopo de transação diferem dos outros teste ligeiramente que uma nova instância de fluxo de trabalho não será criado para cada iteração.  Em vez disso, o fluxo de trabalho seja estruturada com um loop de quando que contém uma atividade de <xref:System.Activities.Statements.TransactionScope> que contém uma única atividade que não faz nenhum trabalho.  Cada um execução de um lote de 50 iterações através de loop de quando for contagem como uma única operação.

### <a name="compensation"></a>Compensação

 O fluxo de trabalho WF3 tem uma única atividade compensatable chamada `WorkScope`.  A atividade simplesmente implementa a interface de <xref:System.Workflow.ComponentModel.ICompensatableActivity> :

```csharp
class WorkScope :
        CompositeActivity, ICompensatableActivity
    {
        public WorkScope() : base() { }

        public WorkScope(string name)
        {
            this.Name = name;
        }

        public ActivityExecutionStatus Compensate(
            ActivityExecutionContext executionContext)
        {
            return ActivityExecutionStatus.Closed;
        }
    }
```

 O manipulador de falhas destina-se à `WorkScope` atividade. O fluxo de trabalho do WF4 é igualmente simplista.  <xref:System.Activities.Statements.CompensableActivity> tem um corpo e um manipulador de compensação.  Um explícito compensa é seguir na sequência.  A atividade de atividade de corpo e do manipulador de compensação é ambas são implementações:

```csharp
public sealed class CompensableActivityEmptyCompensation : CodeActivity
    {
        public CompensableActivityEmptyCompensation()
            : base() { }

        public Activity Body { get; set; }

        protected override void Execute(CodeActivityContext context) { }
    }
    public sealed class CompensableActivityEmptyBody : CodeActivity
    {
        public CompensableActivityEmptyBody()
            : base() { }

        public Activity Body { get; set; }

        protected override void Execute(CodeActivityContext context) { }
    }
```

O diagrama a seguir mostra o fluxo de trabalho de compensação básico. O trabalho WF3 estão à esquerda e o trabalho WF4 estão à direita.

![Fluxos de trabalho de compensação básica do WF3 e WF4](./media/performance/basic-compensation-workflows-wf3-wf4.gif)

### <a name="performance-test-results"></a>Resultados de testes de desempenho

 ![Tabela mostrando dados de resultados de teste de desempenho](./media/performance/performance-test-data.gif)

 ![Gráfico de colunas comparando dados de teste de desempenho WF3 e WF4](./media/performance/performance-test-chart.gif)

 Todos os testes são medidos em por segundo de fluxos de trabalho com exceção de teste do escopo de transação.  Como pode ser deduzido anterior, o desempenho de runtime de [!INCLUDE[wf1](../../../includes/wf1-md.md)] melhor em qualquer linha, especialmente em áreas que eles exigem mais execuções da mesma atividade como quando o loop do.

## <a name="service-composition-scenario"></a>Cenário de composição de serviço

 Como é mostrado na seção anterior, "comparações de desempenho no nível de componente", houve uma redução significativa na sobrecarga entre WF3 e WF4.  Os serviços de fluxo de trabalho do WCF agora podem praticamente corresponder ao desempenho dos serviços WCF codificados manualmente, mas ainda têm todos os benefícios do [!INCLUDE[wf1](../../../includes/wf1-md.md)] tempo de execução.  Esse cenário de teste compara um serviço WCF com um serviço de fluxo de trabalho WCF no WF4.

### <a name="online-store-service"></a>Serviço de Store online

 Um dos pontos fortes da Windows Workflow Foundation é a capacidade de compor processos usando vários serviços.  Para esse exemplo, há um serviço online de armazenamento que orquestre duas chamadas técnicos para comprar um pedido.  A primeira etapa é validar o pedido usando um ordem que valida o serviço.  A segunda etapa é preencher a ordem usando um serviço de depósito.

 Os dois serviços backend, a validação do serviço e o depósito os serviços de aplicativos, permanecem os mesmos para ambos os testes.  A parte que muda é o serviço online de Store que executa a orquestração.  Em um caso, o serviço é codificado manualmente como um serviço WCF.  Para o outro caso, o serviço é escrito como um serviço de fluxo de trabalho do WCF no WF4. os recursos específico de[!INCLUDE[wf1](../../../includes/wf1-md.md)]como o rastreamento e a persistência estão desativados para esse teste.

### <a name="environment"></a>Ambiente

![Configuração do ambiente para medição de desempenho](./media/performance/performance-test-environment.gif)

 As solicitações de cliente são feitas para o serviço online de Store por HTTP vários computadores.  Hosts únicos do computador todos os três serviços.  A camada de transporte entre o serviço online de Store e serviços backend é TCP ou HTTP.  A medida das operações/é baseada em dependendo do número de chamadas concluídos de `PurchaseOrder` feitas para o serviço online de Store.  Pool de canal é um novo recurso disponível em WF4.  Na parte WCF deste conjunto de pools de teste não é fornecida prontamente, portanto, uma implementação de código manual de uma técnica de Pooling simples foi usada no serviço de loja online.

### <a name="performance"></a>Desempenho

![Gráfico de colunas mostrando o desempenho do serviço de loja online](./media/performance/online-store-performance-graph.gif)

 Conectando para backend os serviços TCP sem canal que agrupam-se, o serviço de [!INCLUDE[wf1](../../../includes/wf1-md.md)] tem um impacto 17,2% em produção.  Com que o canal pool, a caneta é aproximadamente 23,8%.  Para HTTP, o impacto é muito menos: 4,3% sem agrupamento e 8,1% com agrupamento.  Também é importante observar que se agrupar do canal fornece muito pouco benefício ao usar HTTP.

 Embora haja sobrecarga do tempo de execução do WF4 em comparação com um serviço WCF codificado manualmente nesse teste, ele pode ser considerado um cenário de pior caso.  Os dois serviços backend neste teste torna muito pouco trabalho.  Em um cenário de ponta a ponta real, esses serviços efetuariam um operações mais faces como chamadas de base de dados, fazendo o impacto de desempenho da camada de transporte menos importante.  Isso mais os benefícios dos recursos disponíveis em WF4 faz a base de fluxo de trabalho uma alternativa viável para criar serviços de orquestração.

## <a name="key-performance-considerations"></a>Considerações sobre desempenho principal

 As áreas de recurso nesta seção, com exceção de interoperabilidade, bastante alterados entre WF3 e WF4.  Isso afeta o design de aplicativos de fluxo de trabalho assim como o desempenho.

#### <a name="workflow-activation-latency"></a>Latência de ativação de fluxo de trabalho

 Em um aplicativo de serviço de fluxo de trabalho do WCF, a latência para iniciar um novo fluxo de trabalho ou carregar um fluxo de trabalho existente é importante, pois ele pode ser bloqueado.  Essa situação de teste mede um host de WF3 XOML contra um host de WF4 XAMLX em um cenário típico.

##### <a name="environment-setup"></a>Configuração do ambiente

 ![Configuração do ambiente para latência e testes de rendimento](./media/performance/latency-throughput-environment-setup.gif)

##### <a name="test-setup"></a>Configuração de teste

 No cenário, um computador cliente entra em contato com um serviço de fluxo de trabalho WCF usando a correlação baseada em contexto.  Correlação de contexto requer uma associação especial de contexto e usa um cabeçalho de contexto ou o cookie para relacionar mensagens ao fluxo de trabalho correto instância.  Tem um benefício de desempenho que a identificação de correlação está localizada no cabeçalho de mensagem para que o corpo da mensagem não precisa ser analisado.

 O serviço criará um novo fluxo de trabalho com a solicitação e enviará uma resposta imediata de modo que a medida de latência não inclua o tempo gasto executando o fluxo de trabalho.  O trabalho WF3 são XOML com a code-behind e o trabalho WF4 são totalmente XAML.  Os aspectos de fluxo de trabalho WF4 como este:

 ![Fluxo de trabalho do escopo de correlação do WF4](./media/performance/wf4-correlationscope-workflow.gif)

 A atividade de <xref:System.ServiceModel.Activities.Receive> cria a instância de fluxo de trabalho.  Um valor passado a mensagem é recebida ecoado na mensagem de resposta.  Uma sequência após a resposta contém o resto de fluxo de trabalho.  Em casos anterior, somente uma atividade do comentário é mostrada.  O número de atividades de comentário é alterado para simular a complexidade de fluxo de trabalho.  Uma atividade do comentário é equivalente a um WF3 <xref:System.Workflow.Activities.CodeActivity> que não executa qualquer trabalho. Para obter mais informações sobre a atividade de comentário, consulte a seção "comparação de desempenho no nível de componente" anteriormente neste artigo.

##### <a name="test-results"></a>Resultados do teste

 Latência fria e passiva para os serviços de fluxo de trabalho do WCF:

 ![Gráfico de colunas mostrando latência fria e passiva para os serviços de fluxo de trabalho do WCF usando WF3 e WF4](./media/performance/latency-results-graph.gif)

 No gráfico anterior, frio se refere ao caso em que não há um existente <xref:System.ServiceModel.WorkflowServiceHost> para o fluxo de trabalho específico.  Ou seja a latência fria é quando o fluxo de trabalho está sendo usado pela primeira vez e o XOML ou o XAML precisam ser compilados.  A latência morna é o tempo de criação de uma nova instância de fluxo de trabalho quando o tipo de fluxo de trabalho já foi criado.  A complexidade de fluxo de trabalho faz a diferença muito pequena em casos WF4 mas tem uma progressão linear em casos WF3.

#### <a name="correlation-throughput"></a>Rendimento de correlação

 WF4 apresenta um novo recurso base de conteudo correlação.  WF3 de contexto fornecido com apenas correlação.  A correlação baseada em contexto só pode ser feita em associações de canal WCF específicas.  A identificação do fluxo de trabalho é inserida no cabeçalho de mensagem para usar essas associações.  O tempo de execução WF3 poderia identificar apenas um fluxo de trabalho por sua ID.  Com a correlação baseada em conteúdo, o autor do fluxo de trabalho pode criar uma chave de correlação fora de uma parte relevante dos dados, como um número de conta ou uma ID de cliente.

 Correlação de contexto base tem uma vantagem de desempenho que a chave de correlação está localizada no cabeçalho de mensagem.  A chave pode ser lido de mensagem sem de- serialização/mensagem- copiar.  Em correlação conteudo base, a chave de correlação é armazenada no corpo da mensagem.  Uma expressão XPath é usada para localizar a chave.  O custo desse processamento adicional depende do tamanho de mensagem, profundidade de chave no corpo, e o número de chaves.  Este teste compara contexto e correlação conteudo base e também mostra degradação de desempenho ao usar várias chaves.

#### <a name="environment-setup"></a>Configuração do ambiente

![Configuração de ambiente para teste de desempenho de fluxo de trabalho](./media/performance/performance-test-environment.gif)

#### <a name="test-setup"></a>Configuração de teste

![Teste de fluxo de trabalho de taxa de transferência de correlação](./media/performance/correlation-throughput-workflow.gif "Configuração do teste de fluxo de trabalho de produtividade de correlação")

 O fluxo de trabalho anterior é o mesmo usado na seção [persistência](#persistence) . Para os testes de correlação sem persistência, não há nenhum provedor de persistência instalado no tempo de execução. Correlação ocorre em dois locais: CreateOrder e CompleteOrder.

#### <a name="test-results"></a>Resultados do teste

![Rendimento de correlação](./media/performance/correlation-throughput-graph.gif "Grafo de taxa de transferência de correlação")

 Este gráfico a seguir mostra um decréscimo de desempenho como o número de chaves usadas em correlação conteudo base aumenta.  A semelhança em curvas entre o TCP e o HTTP indica a sobrecarga associada com esses protocolos.

#### <a name="correlation-with-persistence"></a>Correlação com persistência

 Com um fluxo de trabalho persistente, pressão CPU de conteudo correlação desloca com base em runtime de fluxo de trabalho a base de dados SQL.  Os procedimentos armazenados no provedor de persistência do SQL faça o trabalho de combinar as chaves para localizar o fluxo de trabalho apropriado.

 ![Gráfico de linhas mostrando os resultados de correlação e persistência](./media/performance/correlation-persistence-graph.gif)

 Correlação de contexto base ainda é mais rápido que correlação conteudo base.  No entanto, a diferença é pronunciada menos porque a persistência tem mais impacto no desempenho que correlação.

### <a name="complex-workflow-throughput"></a>Produção complexa de fluxo de trabalho

 A complexidade de um fluxo de trabalho não é medida somente pelo número de atividades.  As atividades compostas podem conter muitos filhos e os filhos podem também ser atividades compostas.  Como o número de níveis de aninhamento aumenta, o que faz o número de atividades que podem estar executando atualmente no estado e o número de variáveis que podem estar em estado.  Este teste compara a produção entre WF3 e WF4 ao executar fluxos de trabalho complexos.

### <a name="test-setup"></a>Configuração de teste

 Esses testes foram executados em um computador de maneira 2.66GHz 4 Intel Xeon X5355 @ com 4GB RAM executando Windows Server 2008 86.  O código de teste é executado em um único processo com um segmento pelo núcleo para atingir o uso da CPU 100%.

 Fluxos de trabalho gerados para esse teste têm duas variáveis principais: profundidade e número de atividades em cada sequência.  Cada nível de profundidade incluir uma atividade paralela, quando loop, decisões, atribuições, e sequências.  No designer WF4 representado abaixo, o fluxograma de nível superior é representado.  Cada atividade do fluxograma lembra o fluxograma principal.  Pode ser útil pensar em um fractal para representar este fluxo de trabalho, onde a profundidade é limitada aos parâmetros de teste.

 O número de atividades em um teste dado é determinado por profundidade e o número de atividades pela sequência.  A equação seguir calcula o número de atividades no teste WF4:

 ![Equação para calcular o número de atividades](./media/performance/number-activities-equation.gif)

 A contagem de atividade de teste WF3 pode ser computado com uma equação ligeiramente diferente devido a uma sequência extra:

 ![Equação para computar o número de atividades WF3](./media/performance/wf3-number-activities-equation.gif)

 De onde está o tamanho e a são o número de atividades pela sequência.  A lógica por trás dessas equações é que a primeira constante, multiplicada por, é o número de sequências e a segunda constante é o número de atividades estático no nível atual.  Há três atividades filhos do fluxograma em cada fluxograma.  A nível inferior de profundidade, esses fluxogramas estão vazios mas a outros níveis são cópias do fluxograma principal.  O número de atividades na definição de fluxo de trabalho de cada variação de teste é indicado na tabela a seguir:

 ![Uma tabela que mostra o número de atividades usadas em cada teste](./media/performance/workflow-variation-compare-table.gif)

 O número de atividades na definição de fluxo de trabalho aumenta com nitidez com cada nível de profundidade.  Mas somente um caminho pelo ponto de decisão é executado em uma determinada instância de fluxo de trabalho, portanto somente um subconjunto pequeno de atividades reais é executado.

 ![Fluxograma do fluxo de trabalho de produtividade complexa](./media/performance/complex-workflow-throughput-workflow.gif)

 Um fluxo de trabalho equivalente foi criado para WF3. O designer WF3 mostra o fluxo de trabalho inteiro na área de design em vez de aninhamento, portanto é muito grande exibir neste tópico. Um snippet de fluxo de trabalho é mostrado abaixo.

 ![Trecho de fluxograma do fluxo de trabalho do WF3](./media/performance/wf3-workflow-snippet.gif)

 Para exercitar aninhamento em casos, extremos outro fluxo de trabalho que seja parte dos usos 100 deste teste tivesse sequências.  Na sequência interno são único `Comment` ou <xref:System.Workflow.Activities.CodeActivity>.

 ![Fluxograma de uma sequência aninhada](./media/performance/nested-sequence-workflow.gif)

 O rastreamento e a persistência não são usados como parte deste teste.

### <a name="test-results"></a>Resultados do teste

 ![Gráfico de colunas mostrando resultados de desempenho de produtividade](./media/performance/throughput-performance-results.gif)

 Mesmo com fluxos de trabalho complexos com muitos de profundida e um número alto de atividades, os resultados de desempenho são consistentes com outros números de produção mostradas anteriormente neste artigo.  A taxa de WF4 é pedidos de magnitude mais rapidamente e tem que ser comparadas em uma escala logarítmica.

### <a name="memory"></a>Memória

 A sobrecarga de memória do Windows Workflow Foundation é medida em dois pontos chave: complexidade de fluxo de trabalho e número de definições de fluxo de trabalho.  As medidas de memória foram executadas em uma estação de trabalho de 64 bits do Windows 7.  Há várias maneiras de obter a medição do tamanho do conjunto de trabalho, como o monitoramento de contadores de desempenho, o ambiente de sondagem. conjunto de trabalho ou o uso de uma ferramenta como VMMap disponível em [VMMap](/sysinternals/downloads/vmmap). Uma combinação de métodos foi usada para obter e verificar os resultados de cada teste.

### <a name="workflow-complexity-test"></a>Teste a complexidade de fluxo de trabalho

 O teste de complexidade de fluxo de trabalho mede a diferença de conjunto de trabalho baseado em complexidade de fluxo de trabalho.  Além dos fluxos de trabalho complexo usados na seção anterior, as novas variações são adicionados para cobrir dois casos básicos: um único fluxo de trabalho de atividade e uma sequência com 1000 atividades.  Para esses testes fluxos de trabalho são inicializados e executados para a conclusão em um único loop serial por um período de um minuto.  Cada variação de teste é executada três vezes e os dados são gravados a média dessas três é executado.

 Os dois novos teste básicos têm fluxos de trabalho que são como aqueles mostrados abaixo:

 ![Fluxo de trabalho complexo para WF3 e WF4](./media/performance/complex-workflow-wf3-wf4.gif)

 No fluxo de trabalho WF3 mostrado acima, as atividades vazios de <xref:System.Workflow.Activities.CodeActivity> são usadas.  As atividades acima de `Comment` usos de fluxo de trabalho WF4.  A atividade de `Comment` foi descrito na seção comparações de desempenho de nível por componente anteriormente neste artigo.

 ![Gráfico de colunas mostrando o uso de memória de fluxo de trabalho complexo para fluxos de trabalho WF3 e WF4](./media/performance/complex-memory-usage-wf3-wf4.gif)

 Uma das tendências claras observar no gráfico é que se aninhar relativamente tem impacto mínimo sobre o uso de memória em WF3 e em WF4.  O impacto o mais significativa de memória do número de atividades em um determinado fluxo de trabalho.  Dado os dados da sequência 1000, a sequência complexa 5 profundidade 5, e profundidade complexa 7 variações da sequência 1, é claro como o número de atividades inserir milhares, increase de uso de memória ficar mais visível.  Em casos extremos sequência 1 (profundidade 7) onde há atividades de ~29K, WF4 estiver usando quase 79% menos memória que WF3.

### <a name="multiple-workflow-definitions-test"></a>Vários teste das definições de fluxo de trabalho

 Medir a memória pela definição de fluxo de trabalho é dividido em dois diferentes teste devido às opções disponíveis para hospedar fluxos de trabalho em WF3 e em WF4.  Os testes são rodados de maneira diferente do teste de complexidade de fluxo de trabalho que um fluxo de trabalho já está citado como exemplo e executado somente uma vez por definição.  Isso ocorre porque a definição de fluxo de trabalho e seu host permanecem em memória para o tempo de vida de Appdomain.  A memória usado executando uma determinada instância de fluxo de trabalho deve ser removida durante a coleta de lixo.  A orientação de migração para WF4 contém informações mais detalhadas sobre as opções de hospedagem. Para obter mais informações, consulte [WF Migration Cookbook: Hospedagem de fluxo de trabalho](migration-guidance.md).

 Criar várias definições de fluxo de trabalho para um teste de definição de fluxo de trabalho pode ser feita em várias maneiras.  Por exemplo, um pode usar a geração de código para criar um conjunto de 1000 fluxos de trabalho que são idênticos exceto no nome e para salvar cada um desses fluxos de trabalho em arquivos separados.  Essa abordagem foi tirada para teste console- hospedado.  Em WF3, a classe de <xref:System.Workflow.Runtime.WorkflowRuntime> foi usada para executar as definições de fluxo de trabalho.  WF4 pode usar <xref:System.Activities.WorkflowApplication> para criar uma instância única de fluxo de trabalho ou usar diretamente <xref:System.Activities.WorkflowInvoker> para executar a atividade como se fosse um chamada de método.  <xref:System.Activities.WorkflowApplication> é um host de uma única instância de fluxo de trabalho e tem mais próximo uma paridade recurso a <xref:System.Workflow.Runtime.WorkflowRuntime> de modo que é usado neste teste.

 Para hospedar fluxos de trabalho no IIS é possível usar <xref:System.Web.Hosting.VirtualPathProvider> para criar um novo <xref:System.ServiceModel.WorkflowServiceHost> em vez de gerar todos os arquivos de XAMLX ou de XOML.  O <xref:System.Web.Hosting.VirtualPathProvider> manipula a solicitação de entrada e responde com um "arquivo virtual" que pode ser carregado de um banco de dados ou, nesse caso, gerado de forma dinâmica.  Portanto é desnecessário criar arquivos 1000 físico.

 As definições de fluxo de trabalho usadas no teste de console foram fluxos de trabalho sequenciais simples com uma única atividade.  A única atividade foi <xref:System.Workflow.Activities.CodeActivity> vazio para as caixas WF3 e uma atividade de `Comment` para casos WF4.  Configuração dos casos hospedados usaram fluxos de trabalho que começam em receber uma mensagem e terminam em enviar uma resposta:

A imagem a seguir mostra um fluxo de trabalho do WF3 com ReceiveActivity e um fluxo de trabalho do WF4 com o padrão de solicitação/resposta:

 ![Serviços de fluxo de trabalho em WF3 e WF4](./media/performance/workflow-receive-activity.gif)

 A tabela a seguir mostra o Delta no conjunto de trabalho entre uma única definição de fluxo de trabalhos e as definições de 1001:

|Hospedando opções|Delta do conjunto de trabalho WF3|Delta do conjunto de trabalho WF4|
|---------------------|---------------------------|---------------------------|
|Fluxos de trabalho hospedados do aplicativo de console|18 MB|9 MB|
|O IIS hospedou serviços de fluxo de trabalho|446 MB|364 MB|

 Hospedar definições de fluxo de trabalho no IIS consome muito mais memória devido aos <xref:System.ServiceModel.WorkflowServiceHost> artefatos de serviço WCF detalhados e à lógica de processamento de mensagens associada ao host.

 Para o console que hospeda em WF3 fluxos de trabalho foram implementados no código em vez de XOML.  Em WF4 a opção é usar XAML.  O XAML livre é armazenado como um recurso inserido no assembly compilado e durante o runtime para fornecer a implementação de fluxo de trabalho.  Há uma sobrecarga associada a este processo.  Para fazer uma comparação entre justa WF3 e WF4, os fluxos de trabalho codificados foram usados em vez de XAML.  Um exemplo de um dos fluxos de trabalho WF4 é mostrado abaixo:

```csharp
public class Workflow1 : Activity
{
    protected override Func<Activity> Implementation
    {
        get
        {
            return new Func<Activity>(() =>
            {
                return new Sequence
                {
                    Activities = {
                        new Comment()
                    }
                };
            });
        }
        set
        {
            base.Implementation = value;
        }
    }
}
```

 Há muitos outros fatores que podem afetar o consumo de memória. Conselhos o mesmo para todos os programas gerenciados ainda se aplica.  A configuração em ambientes hospedados, o objeto de <xref:System.ServiceModel.WorkflowServiceHost> criado para uma definição de fluxo de trabalho permanece na memória até que o pool de aplicativos é reciclado.  Isso deve ser mantido em mente ao escrever extensões.  Além disso, é melhor evitar variáveis "globais" (variáveis com escopo para todo o fluxo de trabalho) e limitar o escopo de variáveis sempre que possível.

## <a name="workflow-runtime-services"></a>Serviços de runtime de fluxo de trabalho

### <a name="persistence"></a>Persistência

 WF3 e WF4 ambos são fornecidas com um provedor de persistência SQL.  O provedor de persistência WF3 SQL é uma implementação simples que serialize a instância de fluxo de trabalho e o armazena em uma operação.  Por esse motivo, o desempenho desse provedor intensamente depende do tamanho de instância de fluxo de trabalho.  Em WF3, o tamanho da instância pode aumentar por muitas razões, como é discutido anteriormente neste documento.  Vários clientes escolha para não usar o provedor de persistência padrão de SQL como armazenar uma instância serializado em uma base de dados não fornece nenhuma visibilidade no estado de fluxo de trabalho.  Para localizar um trabalho específicos sem conhecer a identificação de trabalho, uma teria que desserializar cada instância armazenado e examinar o conteúdo.  Muitos desenvolvedores preferem escrever seus próprios provedores de persistência para superar essa obstáculo.

 O provedor de persistência WF4 SQL tenta resolver alguns desses interesses.  As tabelas de persistência expõe determinada informações como os indicadores ativos e as propriedades promotable.  O novo recurso de conteudo baseado em WF4 correlação não deseja executar bem usando a abordagem de persistência WF3 SQL, que fez alterações na organização de instância persistentes de fluxo de trabalho.  Isso torna o provedor de persistência mais complexos e coloca o esforço extra na base de dados.

### <a name="environment-setup"></a>Configuração do ambiente

![Configuração de ambiente para teste de desempenho de fluxo de trabalho](./media/performance/performance-test-environment.gif)

### <a name="test-setup"></a>Configuração de teste

 Mesmo com um conjunto aprimorado de recurso e uma melhor manipulação de concorrência, o provedor de persistência SQL em WF4 é mais rápido do que o provedor em WF3.  Para apresentar isso, dois fluxos de trabalho executando essencialmente as mesmas operações em WF3 e em WF4 são comparados abaixo.

 ![Fluxo de trabalho de persistência em WF3 à esquerda e WF4 à direita](./media/performance/persist-workflow-wf3-wf4.gif)

 Os dois fluxos de trabalho ambos são criados por uma mensagem recebida.  Após enviar uma resposta inicial, o fluxo de trabalho é mantido.  Em casos WF3, <xref:System.Workflow.ComponentModel.TransactionScopeActivity> vazia é usado para iniciar a persistência.  O mesmo pode ser obtido em WF3, marcando uma atividade como "persistir no fechamento".  Um segundo, a mensagem correlacionada conclui o fluxo de trabalho.  Fluxos de trabalho são persistidos mas não descarregados.

### <a name="test-results"></a>Resultados do teste

 ![Gráfico de colunas mostrando persistência de produtividade](./media/performance/throughput-persistence-graph.gif)

 Quando o transporte entre o cliente e a camada intermediária é HTTP, a persistência em WF4 mostra uma melhoria de 2,6 vezes.  O transporte TCP aumenta o fator a 3,0 vezes.  Em todos os casos, a utilização da CPU na camada intermediária é 98% ou maior.  A razão para a produção WF4 é maior realiza-se devido ao runtime mais rápido de fluxo de trabalho.  O tamanho da instância é serializado baixo para ambos os casos e não é um elemento de contribuição principal nesta situação.

 WF3 e fluxos de trabalho WF4 neste teste usam uma atividade para indicar explicitamente quando a persistência deve ocorrer.  Isso tem a vantagem de persistir o fluxo de trabalho sem descarregá-lo.  Em WF3, também é possível persistir usando o recurso de <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> , mas este descarrega a instância de fluxo de trabalho de memória.  Se um desenvolvedor que usa WF3 deseja verificar se um fluxo de trabalho persiste em determinados pontos, tem que alterar a definição de fluxo de trabalho ou pagar o custo descarregar e recarregar a instância de fluxo de trabalho.  Um novo recurso em WF4 possibilita persistir sem descarregar: <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A>.  Esse recurso permite que a instância de fluxo de trabalho está armazenado em ociosa mas é na memória até que o limite de <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> está localizado ou a execução é continuada.

 Observe que o provedor de persistência WF4 SQL executa mais trabalho na camada de base de dados.  O base de dados SQL pode se tornar um gargalo portanto é importante monitorar existem o uso da CPU e o disco.  Certifique-se de incluir os seguintes contadores de desempenho de base de dados SQL quando aplicativos de fluxo de trabalho de teste de desempenho:

- PhysicalDisk \\ % de tempo de leitura do disco

- PhysicalDisk \\ % tempo de disco

- PhysicalDisk \\ % de tempo de gravação de disco

- PhysicalDisk \\ % Méd. comprimento da fila de disco

- Comprimento da fila de leitura de disco disco físico \

- Comprimento da fila de gravação de disco disco físico \

- PhysicalDisk \ comprimento atual da fila de disco

- Informações do processador- \\ % tempo do processador

- SQLServer: Travas \ tempo de espera trava de média (ms)

- SQLServer: Travas \ espera por de trava/s

### <a name="tracking"></a>Acompanhamento

 O rastreamento de fluxo de trabalho pode ser usado para acompanhar o progresso de um fluxo de trabalho.  Informações que está incluída em eventos de rastreamento é determinada por um perfil de rastreamento.  Mais complexo o perfil de rastreamento, mais caro o rastreamento fica.

 WF3 enviados com um serviço SQL- base de rastreamento.  Esse serviço pode trabalhar nos modos processados em lotes e não processados em lotes.  No modo não processado em lotes, controlando eventos são gravados diretamente a base de dados.  No modo processado em lotes, controlando eventos são coletados em lotes mesmo que o estado da instância de fluxo de trabalho.  O modo processado em lotes tem um desempenho melhor para o intervalo o maior de projetos de fluxo de trabalho.  No entanto, em lotes pode ter um impacto de desempenho negativo se o fluxo de trabalho executa muitos atividades sem persistir e as atividades são rastreadas.  Isso geralmente aconteceria em loop e a melhor maneira para evitar esse cenário é criar grandes loop para conter um ponto de persistência.  Introduzir um ponto de persistência em um loop pode afetar negativamente o desempenho também portanto é importante medir o custo de cada e vir anterior com um balanço.

 WF4 não é enviado com um serviço de rastreamento SQL.  A gravação de informações de rastreamento em um banco de dados SQL pode ser tratada melhor de um servidor de aplicativos em vez de ser integrada ao .NET Framework. Portanto o rastreamento SQL é tratado agora por AppFabric.  O provedor pronto para uso de rastreamento em WF4 é baseado no rastreamento de evento para o Windows (ETW).

 ETW é um kernel- nível, o sistema de evento de baixo latência compilado no Windows.  Usa um modelo de provedor/consumidor que execute possível incorrer somente a caneta para o rastreamento de evento quando há realmente um consumidor.  Além de eventos kernel como o processador, o disco, a memória, e o uso de rede, muitos aplicativos aproveitam ETW também.  Os eventos de ETW são mais avançados de contadores de desempenho que os eventos podem ser personalizados para o aplicativo.  Um evento pode conter texto como uma identificação de fluxo de trabalho ou uma mensagem informativa.  Além disso, os eventos são categorizados com máscaras de bits de modo que consumir um certo subconjunto de eventos menos tenha impacto de desempenho de tratar todos os eventos.

 As vantagens de usar a abordagem ETW para controlar em vez do SQL incluem:

- A coleção de eventos de rastreamento pode ser separada para outro processo.  Isso proporciona maior flexibilidade de como os eventos são gravados.

- Os eventos de rastreamento do ETW são facilmente combinados com os eventos ETW do WCF ou outros provedores de ETW, como um SQL Server ou um provedor de kernel.

- Os autores de fluxo de trabalho não precisam modificar um fluxo de trabalho melhor para trabalhar com uma implementação específica de rastreamento, como o modo em lotes de serviço de rastreamento de WF3 SQL.

- Um administrador pode girar de acompanhar ou sem reciclar o processo host.

 Os benefícios de desempenho ao rastreamento de ETW vêm com um desvantagem.  Os eventos de ETW podem ser perdidas se o sistema está sob a pressão intensa de recurso.  O processamento de eventos não serve bloquear a execução do programa normal e portanto não se garante que todos os eventos de ETW serão passados para seus assinantes.  Isso torna acompanhar de ETW grande para o monitoramento da integridade mas não para fazer auditoria em apropriado.

 Quando WF4 não possui um provedor de rastreamento SQL, AppFabric faz.  A abordagem de rastreamento SQL de AppFabric é assinar eventos de ETW com um serviço do Windows que processa em lotes os eventos e os escrevam a uma tabela SQL criada para inserções rápido possível.  Um trabalho separados sai os dados da tabela e reformam-nos nas tabelas de relatório que podem ser exibidas no painel de AppFabric.  Isso significa que um lote de eventos de rastreamento é tratado independente de fluxo de trabalho proveniente de e portanto não tenha que aguardar um ponto de persistência antes de ser gravado.

 Os eventos de ETW podem ser gravados com ferramentas como o logman ou o xperf.  O arquivo de compacto ETL pode ser exibido com uma ferramenta como o xperfview ou ser convertido em um formato mais legível, como XML, com tracerpt.  Em WF3, a única opção para obter eventos de rastreamento sem um base de dados SQL é criar um serviço personalizado de rastreamento. Para obter mais informações sobre o ETW, consulte [Serviços WCF e rastreamento de eventos para Windows](../wcf/samples/wcf-services-and-event-tracing-for-windows.md) e [rastreamento de eventos-aplicativos do Windows](/windows/desktop/etw/event-tracing-portal).

 Ativar o rastreamento de fluxo de trabalho irá afetar o desempenho em vários níveis.  A marca de nível abaixo usar a ferramenta de logman para consumir eventos de rastreamento de ETW e para gravar-los a um arquivo de ETL.  O custo de rastreamento SQL em AppFabric não está no escopo deste artigo.  O perfil básico de rastreamento, também usado em AppFabric, é mostrada nessa marca de nível.  Também estão incluídos o custo de acompanhar somente eventos de monitoramento de integridade.  Esses eventos são úteis para solucionar problemas e determinar a taxa média do sistema.

### <a name="environment-setup"></a>Configuração do ambiente

 ![Configuração de ambiente para teste de desempenho de fluxo de trabalho](./media/performance/performance-test-environment.gif)

### <a name="test-results"></a>Resultados do teste

 ![Gráfico de colunas mostrando custos de rastreamento de fluxo de trabalho](./media/performance/workflow-tracking-costs.gif)

 Monitoramento da integridade tem um impacto de aproximadamente 3% em produção.  Os custos de perfil básico são aproximadamente 8%.

## <a name="interop"></a>Interoperabilidade

 WF4 é quase uma reescrita completo de [!INCLUDE[wf1](../../../includes/wf1-md.md)] e portanto fluxos de trabalho WF3 e as atividades não são diretamente compatíveis com WF4.  Muitos clientes que adotaram Windows Workflow Foundation antecipadamente terão definições de fluxo de trabalho internas ou de terceiros e atividades personalizadas para WF3.  Uma maneira de fazer a transição para WF4 é usar a atividade de Interoperabilidade, que pode executar as atividades WF3 de dentro de um fluxo de trabalho WF4.  É recomendável que a atividade de <xref:System.Activities.Statements.Interop> seja usada somente quando necessário. Para obter mais informações sobre como migrar para o WF4, Confira as [diretrizes de migração do WF4](migration-guidance.md).

### <a name="environment-setup"></a>Configuração do ambiente

 ![Configuração de ambiente para teste de desempenho de fluxo de trabalho](./media/performance/performance-test-environment.gif)

### <a name="test-results"></a>Resultados do teste

A tabela a seguir mostra os resultados da execução de um fluxo de trabalho que contém cinco atividades em uma sequência em várias configurações.

|Teste|Produção (fluxos de trabalho/s)|
|----------|-----------------------------------|
|Sequência WF3 em runtime WF3|1.576|
|Sequência WF3 em runtime WF4 usando Interoperabilidade|2.745|
|Sequência WF4|153.582|

 Há um aumento notável de desempenho ao uso de Interoperabilidade sobre WF3 reto.  No entanto, quando comparado com as atividades WF4, increase é irrisória.

## <a name="summary"></a>Resumo

 Os sejam investimentos no desempenho para WF4 pagaram fora em muitas áreas cruciais.  O desempenho componente de fluxo de trabalho individual é em alguns casos centenas de vezes em WF4 mais rápido comparado a WF3 devido a um runtime mais magro de [!INCLUDE[wf1](../../../includes/wf1-md.md)] .  Números de latência é significativamente melhor também.  Isso significa que a penalidade de desempenho para uso em [!INCLUDE[wf1](../../../includes/wf1-md.md)] oposição à codificação manual dos serviços de orquestração do WCF é muito pequena considerando os benefícios adicionais do uso do [!INCLUDE[wf1](../../../includes/wf1-md.md)] .  O desempenho de persistência gerado por um fator de 2,5 - 3,0.  Monitoramento da integridade por meio de fluxo de trabalho que acompanha agora tem a sobrecarga muito pequena.  Um conjunto abrangente de guias de migração está disponível para aqueles que estão considerando mover de WF3 a WF4.  Qualquer esta deve fazer o WF4 uma opção atrativas para escrever aplicativos complexos.
