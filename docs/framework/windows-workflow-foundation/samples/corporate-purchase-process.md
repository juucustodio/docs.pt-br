---
description: 'Saiba mais sobre: processo de compra corporativa'
title: Processo de compra corporativo
ms.date: 03/30/2017
ms.assetid: a5e57336-4290-41ea-936d-435593d97055
ms.openlocfilehash: c26b1f46f29b7a6ec06acf5d19381b5c8f460433
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787858"
---
# <a name="corporate-purchase-process"></a>Processo de compra corporativo

Este exemplo mostra como criar uma solicitação bem básico para o processo com base (RFP) de compra de propostas com a melhor seleção automático de proposta. Combina <xref:System.Activities.Statements.Parallel>, <xref:System.Activities.Statements.ParallelForEach%601>, e <xref:System.Activities.Statements.ForEach%601> e uma atividade personalizado para criar um fluxo de trabalho que representa o processo.

 Este exemplo contém um aplicativo cliente ASP.NET que permite interagir com o processo como participantes diferentes (como o solicitante original ou um fornecedor específico).

## <a name="requirements"></a>Requisitos

- Visual Studio 2012.

- [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].

## <a name="demonstrates"></a>Demonstra

- Atividades personalizados.

- Composição de atividades.

- Indicadores.

- Persistência.

- Persistência esquematizada.

- Rastreamento.

- Controlar.

- Hospedagem [!INCLUDE[wf1](../../../../includes/wf1-md.md)] em clientes diferentes (aplicativos Web ASP.net e aplicativos WinForms).

> [!IMPORTANT]
> Os exemplos podem já estar instalados no seu computador. Verifique o seguinte diretório (padrão) antes de continuar.  
>
> `<InstallDrive>:\WF_WCF_Samples`  
>
> Se esse diretório não existir, vá para [Windows Communication Foundation (WCF) e exemplos de Windows Workflow Foundation (WF) para .NET Framework 4](https://www.microsoft.com/download/details.aspx?id=21459) para baixar todos os Windows Communication Foundation (WCF) e [!INCLUDE[wf1](../../../../includes/wf1-md.md)] exemplos. Este exemplo está localizado no seguinte diretório.  
>
> `<InstallDrive>:\WF_WCF_Samples\WF\Application\PurchaseProcess`  
  
## <a name="description-of-the-process"></a>Descrição do processo  

 Este exemplo mostra uma implementação de um programa Windows Workflow Foundation (WF) para reunir propostas de fornecedores para uma empresa genérica.  
  
1. Um funcionário da empresa X cria um aplicativo de propostas (RFP).  
  
    1. O funcionário no título e a descrição de RFP.  
  
    2. O funcionário seleciona os fornecedores que desejam convidar para enviar propostas.  
  
2. O funcionário envia a proposta.  
  
    1. Uma instância de fluxo de trabalho é criada.  
  
    2. O fluxo de trabalho está aguardando todos os editores para enviar suas propostas.  
  
3. As propostas são recebidas completos, o fluxo de trabalho itera com todas as propostas recebidas e selecione melhor.  
  
    1. Cada fornecedor tem uma reputação (este exemplo armazena a lista de reputação em VendorRepository.cs).  
  
    2. Total de valor proposta é determinado por (o valor tipado no fornecedor) (*) escrita de reputação de fornecedor/100.  
  
4. O solicitador original pode ver todas as propostas enviadas. A melhor proposta é apresentada em uma seção especial no relatório.  
  
## <a name="process-definition"></a>Definição de processo  

 A lógica de núcleo de exemplo usa uma atividade de <xref:System.Activities.Statements.ParallelForEach%601> que espera as oferece de cada fornecedor (usando uma atividade personalizado que cria um indexador), e registra a proposta de fornecedor como um RFP (usando uma atividade de <xref:System.Activities.Statements.InvokeMethod> ).  
  
 O exemplo efetua iterações em com todas as propostas recebidas armazenadas em `RfpRepository`, calculando o valor definido (usando uma atividade de <xref:System.Activities.Statements.Assign> e atividades de <xref:System.Activities.Expressions> ), e se o valor definido é melhor do que a melhor oferecem anterior, atribui o novo valor como melhor oferecem (usando <xref:System.Activities.Statements.If> e atividades de <xref:System.Activities.Statements.Assign> ).  
  
## <a name="projects-in-this-sample"></a>Projetos nisso exemplo  

 Este exemplo contém os seguintes projetos.  
  
|Projeto|Descrição|  
|-------------|-----------------|  
|Comum|Os objetos de entidade usados dentro do processo (aplicativo de propostas, fornecedor, e proposta de provedor).|  
|WfDefinition|A definição de processo (como um programa de [!INCLUDE[wf1](../../../../includes/wf1-md.md)] ) e o host (`PurchaseProcessHost`) usado por aplicativos cliente para criar e usar as instâncias de compra processam o fluxo de trabalho.|  
|Clientes web|Um aplicativo cliente ASP.NET que permite que os usuários criem e participem de instâncias do processo de compra. Usa um host de criado para interagir com o mecanismo de fluxo de trabalho.|  
|WinFormsClient|Um aplicativo cliente Windows Forms que permite aos usuários criarem e participem nas instâncias do processo de compras. Usa um host de criado para interagir com o mecanismo de fluxo de trabalho.|  
  
### <a name="wfdefinition"></a>WfDefinition  

 A tabela a seguir contém uma descrição dos arquivos mais importantes no projeto de WfDefinition.  
  
|Arquivo|Descrição|  
|----------|-----------------|  
|IPurchaseProcessHost.cs|Interface para o host de fluxo de trabalho.|  
|PurchaseProcessHost.cs|Implementação de um host para o fluxo de trabalho. O host abstrai os detalhes do runtime de fluxo de trabalho e é usado em todos os aplicativos cliente carregar, executar, e interagir com as instâncias de fluxo de trabalho de `PurchaseProcess` .|  
|PurchaseProcessWorkflow.cs|Uma atividade que contém a definição de fluxo de trabalho do processo de compra (deriva de <xref:System.Activities.Activity>).<br /><br /> As atividades que derivam de <xref:System.Activities.Activity> compor a funcionalidade montando atividades personalizados existentes e atividades de biblioteca de atividade de [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] . Montar as atividades é a maneira mais básica de criar a funcionalidade personalizada.|  
|WaitForVendorProposal.cs|Esta atividade personalizado é derivado de <xref:System.Activities.NativeActivity> e cria-se um indexador que deve ser nomeado que posteriormente por um fornecedor para enviar a proposta.<br /><br /> As atividades que derivam de <xref:System.Activities.NativeActivity>, como aqueles que derivam de <xref:System.Activities.CodeActivity>, criam a funcionalidade imperativa substituindo <xref:System.Activities.NativeActivity.Execute%2A>, mas também têm acesso a qualquer funcionalidade de runtime de fluxo de trabalho com <xref:System.Activities.ActivityContext> que é passado para o método de `Execute` . Esse contexto tem suporte para agendamento e cancelamento de atividades filhas, configuração de zonas sem persistência (blocos de execução durante os quais o tempo de execução não mantém os dados do fluxo de trabalho, como em transações atômicas) e <xref:System.Activities.Bookmark> objetos (identificadores para retomar fluxos de trabalho pausados).|  
|TrackingParticipant.cs|<xref:System.Activities.Tracking.TrackingParticipant> que recebe todos os eventos de rastreamento e o salva em um arquivo de texto.<br /><br /> Os participantes de rastreamento são adicionados à instância do fluxo de trabalho como extensões.|  
|XmlWorkflowInstanceStore.cs|Um personalizado <xref:System.Runtime.DurableInstancing.InstanceStore> que salva aplicativos de fluxo de trabalho para arquivos XML.|  
|XmlPersistenceParticipant.cs|Um personalizado <xref:System.Activities.Persistence.PersistenceParticipant> que salva uma instância do aplicativo de propostas para um arquivo XML.|  
|AsyncResult.cs/CompletedAsyncResult.cs|O auxiliar classe implementando o padrão assíncrono para componentes de persistência.|  
  
### <a name="common"></a>Comum  

 A tabela a seguir contém uma descrição das classes mais importantes no projeto comuns.  
  
|Class|Descrição|  
|-----------|-----------------|  
|Fornecedor|Um fornecedor que envia propostas em uma solicitação para propostas.|  
|RequestForProposal|Uma solicitação para propostas (RFP) é um convite para que fornecedores enviem propostas em uma mercadorias ou em um determinado serviço.|  
|VendorProposal|Uma proposta enviada por um fornecedor a um RFP concrete.|  
|VendorRepository|O armazenamento de fornecedores. Essa implementação contém uma coleção de memória das instâncias de fornecedor e métodos para expor essas instâncias.|  
|RfpRepository|O armazenamento de solicitações para propostas. Essa implementação contém usa Linq para XML consulte o arquivo XML de aplicativos de propostas gerados pela persistência esquematizada. |  
|IOHelper|Essa classe trata todos os problemas de I/O-related (pastas, os caminhos, e assim por diante).|  
  
### <a name="web-client"></a>Clientes web  

 A tabela a seguir contém uma descrição de páginas da Web as mais importantes no projeto do cliente web.  
  
|Arquivo|Descrição|  
|-|-|  
|CreateRfp.aspx|Cria e envia uma nova solicitação para propostas.|  
|Default.aspx|Mostra todas as solicitações ativos e concluídas para propostas.|  
|GetVendorProposal.aspx|Obtém uma proposta de um fornecedor em uma solicitação concreta para propostas. Esta página é usada por fornecedores.|  
|ShowRfp.aspx|Mostrar todas as informações sobre uma solicitação para propostas (propostas recebidas, datas, valores, e outras informações.) Esta página é usada somente pelo criador do aplicativo de propostas.|  
  
### <a name="winforms-client"></a>Cliente de WinForms  

 A tabela a seguir contém uma descrição de formulários os mais importantes no projeto formulários de vitória.  
  
|Formulário|Descrição|  
|-|-|  
|NewRfp|Cria e envia uma nova solicitação para propostas.|  
|ShowProposals|Mostrar todas as solicitações ativos e concluídas para propostas. **Observação:**  Talvez seja necessário clicar no botão **Atualizar** na interface do usuário para ver as alterações nessa tela depois de criar ou modificar uma solicitação de proposta.|  
|SubmitProposal|Obter uma proposta de um fornecedor em uma solicitação concreta para propostas. Essa janela é usada por fornecedores.|  
|ViewRfp|Mostrar todas as informações sobre uma solicitação para propostas (propostas recebidas, datas, valores, e outras informações.) Essa janela é usada somente pelo criador de solicitação para propostas.|  
  
### <a name="persistence-files"></a>Arquivos de persistência  

 A tabela a seguir mostra os arquivos gerados pelo provedor de persistência (`XmlPersistenceProvider`) está localizada no caminho da pasta temporária do sistema atual (usando <xref:System.IO.Path.GetTempPath%2A>). O arquivo de rastreamento é criado no caminho atual de execução.  
  
|Nome do Arquivo|Descrição|Caminho|  
|-|-|-|  
|rfps.xml|O arquivo XML com todas as solicitações ativos e concluídas para propostas.|<xref:System.IO.Path.GetTempPath%2A>|  
|[instanceid]|Este arquivo contém todas informações sobre uma instância de fluxo de trabalho.<br /><br /> Este arquivo é gerado pela implementação esquematizada de persistência (PersistenceParticipant em XmlPersistenceProvider).|<xref:System.IO.Path.GetTempPath%2A>|  
|[instanceId] .tracking|Um arquivo de texto com todos os eventos que ocorreram em uma instância concreta.<br /><br /> Este arquivo é gerado por TrackingParticipant.|<xref:System.IO.Path.GetTempPath%2A>|  
|PurchaseProcess.Tracing.TraceLog.txt|O arquivo de rastreamento gerado pelo fluxo de trabalho com base nas definições de configuração no App.config ou nos arquivos web.config.|Caminho de execução atual|  
  
#### <a name="to-use-this-sample"></a>Para usar este exemplo  
  
1. Usando o Visual Studio 2010, abra o arquivo de solução PurchaseProcess. sln.  
  
2. Para executar o projeto do cliente Web, abra **Gerenciador de soluções** e clique com o botão direito do mouse no projeto do **cliente Web** . Selecione **definir como projeto de inicialização**.  
  
3. Para executar o projeto cliente WinForms, abra **Gerenciador de soluções** e clique com o botão direito do mouse no projeto **cliente WinForms** . Selecione **definir como projeto de inicialização**.  
  
4. Para criar a solução, pressione CTRL+SHIFT+B.  
  
5. Para executar a solução, pressione CTRL+F5.  
  
### <a name="web-client-options"></a>Opções de cliente web  
  
- **Criar uma nova RFP**: cria uma nova solicitação de propostas (RFP) e inicia um fluxo de trabalho de processo de compra.  
  
- **Atualizar**: atualiza a lista de RFPs ativas e concluídas na janela principal.  
  
- **Exibir**: mostra o conteúdo de uma RFP existente. Fornecedores podem enviar suas propostas (ou convidado se o RFP não for concluído.)  
  
- Exibir como: o usuário pode acessar a RFP usando identidades diferentes selecionando o participante desejado na caixa de combinação **Exibir como** na grade de RFPs ativa.  
  
### <a name="winforms-client-options"></a>Opções de cliente de WinForms  
  
- **Criar RFP**: cria uma nova solicitação de propostas (RFP) e inicia um fluxo de trabalho de processo de compra.  
  
- **Atualizar**: atualiza a lista de RFPs ativas e concluídas na janela principal.  
  
- **Exibir RFP**: mostra o conteúdo de uma RFP existente. Fornecedores podem enviar suas propostas (ou convidado se o RFP não é concluído)  
  
- **Conectar como**: o usuário pode acessar a RFP usando identidades diferentes selecionando o participante desejado na caixa de combinação **Exibir como** na grade de RFPs ativa.
