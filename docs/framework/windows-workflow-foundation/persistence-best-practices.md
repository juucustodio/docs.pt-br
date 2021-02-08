---
description: 'Saiba mais sobre: práticas recomendadas de persistência'
title: Práticas recomendadas de persistência
ms.date: 03/30/2017
ms.assetid: 6974c5a4-1af8-4732-ab53-7d694608a3a0
ms.openlocfilehash: 788c025d52e504e7a767a4aa0841ae01a7d3327c
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787871"
---
# <a name="persistence-best-practices"></a>Práticas recomendadas de persistência

Este documento aborda as práticas recomendadas para o design e a configuração de fluxo de trabalho relacionados à persistência de fluxo de trabalho.  
  
## <a name="design-and-implementation-of-durable-workflows"></a>Design e implementação de fluxos de trabalho duráveis  

 Geralmente, os fluxos de trabalho executam o trabalho em curtas períodos que são intercalados com horários durante o qual o fluxo de trabalho estiver ocioso porque está aguardando um evento. Esse evento pode ser itens como uma mensagem ou um timer expira. Para poder descarregar o fluxo de trabalho métodos como exemplo quando fica ocioso, o serviço que o host deve manter a instância de fluxo de trabalho. Isso é possível somente se a instância de fluxo de trabalho não está em uma zona sem persistir (por exemplo, aguardando uma transação para concluir, ou aguardando um retorno de chamada assíncrona). Para permitir que uma instância ocioso de fluxo de trabalho descarregar, o autor de fluxo de trabalho deve usar escopos de transação e atividades assíncronas para uma breve ações somente. Em particular, o autor deve manter atividades de atraso nesses sem para persistir as zonas tão curto como possível.  
  
 Um fluxo de trabalho só pode ser persistido se todos os tipos de dados usados pelo fluxo de trabalho são serializados. Além disso, os tipos personalizados usados em fluxos de trabalho persistentes devem ser serializáveis com <xref:System.Runtime.Serialization.NetDataContractSerializer> para ser persistido por <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>.  
  
 Uma instância de fluxo de trabalho não pode ser recuperada em caso de uma falha de host do computador ou se não foi persistente. Em geral, recomendamos que você persistir uma instância de fluxo de trabalho no início do ciclo de vida de fluxo de trabalho.  
  
 Se seu fluxo de trabalho é muito ocupado por tempo, recomendamos que você persistir a instância de fluxo de trabalho regularmente ao longo do seu período ocupado. Você pode fazer isso adicionando atividades de <xref:System.Activities.Statements.Persist> durante a sequência de atividades que mantém a instância de fluxo de trabalho ocupado. Assim, reciclagem do domínio de aplicativo, falhas host, ou falhas do computador não causam o sistema a ser rolado de volta para o início do período ocupado. Esteja ciente que adicionar atividades de <xref:System.Activities.Statements.Persist> ao fluxo de trabalho pode levar a uma degradação de desempenho.  
  
 A tela de aplicativo Windows Server simplifica bastante a configuração e uso de persistência. Para obter mais informações, consulte [persistência do Windows Server app Fabric](/previous-versions/appfabric/ee677272(v=azure.10))  
  
## <a name="configuration-of-scalability-parameters"></a>Configuração de parâmetros de escalabilidade  

 Os requisitos de escalabilidade e desempenho determinam as configurações dos seguintes parâmetros:  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A>  
  
- <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A>  
  
- <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior.InstanceLockedExceptionAction%2A>  
  
 Esses parâmetros devem ser definidos como segue, de acordo com o cenário atual.  
  
### <a name="scenario-a-small-number-of-workflow-instances-that-require-optimal-response-time"></a>Cenário: Um pequeno número de instâncias de fluxo de trabalho que exigem o tempo de resposta ótimo  

 Nesse cenário, todas as instâncias de fluxo de trabalho devem permanecer carregadas quando se tornam ociosos. Definir <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> para um valor grande. O uso dessa configuração impede que uma instância de fluxo de trabalho se mover entre computadores. Use essa configuração somente se um ou mais dos seguintes condições forem verdadeiras:  
  
- Uma instância de fluxo de trabalho recebe uma única mensagem em seu tempo de vida.  
  
- Todas as instâncias de fluxo de trabalho executadas em um único computador  
  
- Todas as mensagens que são recebidas por uma instância de fluxo de trabalho são recebidas pelo mesmo computador.  
  
 Use atividades de <xref:System.Activities.Statements.Persist> ou <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A> definido como 0 para ativar a recuperação de sua instância de fluxo de trabalho depois que falhas de host ou do computador de serviço.  
  
### <a name="scenario-workflow-instances-are-idle-for-long-periods-of-time"></a>Cenário: As instâncias de fluxo de trabalho são ociosos por longos períodos de tempo  

 Nesse cenário, defina <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> a 0 para liberar o mais rápido possível recursos.  
  
### <a name="scenario-workflow-instances-receive-multiple-messages-in-a-short-period-of-time"></a>Cenário: As instâncias de fluxo de trabalho vários recebem mensagens em um curto período de tempo  

 Nesse cenário, defina <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> como 60 segundos se essas mensagens são recebidas pelo mesmo computador. Isso evita uma sequência rápida de unload e carregar de uma instância de fluxo de trabalho. Isso também não mantém a instância na memória durante o suficiente tiempo.  
  
 Definir <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> a 0, e o conjunto <xref:System.ServiceModel.Activities.Description.SqlWorkflowInstanceStoreBehavior.InstanceLockedExceptionAction%2A> a BasicRetry ou a AggressiveRetry se essas mensagens podem ser recebidas por diferentes computadores. Isso permite que a instância de fluxo de trabalho é carregada por outro computador.  
  
### <a name="scenario-workflow-uses-delay-activities-with-short-durations"></a>Cenário: Atividades de atraso dos usos de fluxo de trabalho com durações curtas  

 Nesse cenário, <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> sonda regularmente o base de dados de persistência para as instâncias que devem ser carregadas devido a uma atividade expirada de <xref:System.Activities.Statements.Delay> . Se <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> encontrar um timer que expirou no intervalo de pesquisa seguir, a instância Store de fluxo de trabalho do SQL diminuirá o intervalo de pesquisa. A votação seguir ocorrerá em right após o timer expirou. Essa maneira, a instância Store de fluxo de trabalho do SQL obtém uma alta precisão de temporizadores que executam mais tempo do intervalo de pesquisa, que é definido por <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>. Para ativar o processamento hábil de um atrasos mais curtas, a instância de fluxo de trabalho deve permanecer na memória pelo menos um intervalo de pesquisa.  
  
 Definir <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToPersist%2A> a 0 para escrever o tempo de expiração a base de dados de persistência.  
  
 Definir <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior.TimeToUnload%2A> mais tempo que ou igual a <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> para manter no mínimo a instância na memória um intervalo de pesquisa.  
  
 Não recomendamos reduzir <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> porque isso resulta em uma carga na base de dados de persistência. Cada host serviço que usa <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> sonda o base de dados uma vez por período de detecção. A configuração <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> a um intervalo de tempo muito pequeno pode fazer com que o desempenho do sistema diminui se o número de host serviço é grande.  
  
## <a name="configuring-the-sql-workflow-instance-store"></a>Configurando a instância Store de fluxo de trabalho do SQL  

 A instância Store de fluxo de trabalho do SQL possui os seguintes parâmetros de configuração:  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceEncodingOption%2A>  
 Este parâmetro instrui <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> para compactar o estado da instância de fluxo de trabalho. A compactação reduz a quantidade de dados que são armazenados na base de dados de persistência e reduzir o tráfego de rede no caso do base de dados de persistência reside em um servidor de base de dados dedicado. Se a compactação é usado, requer recursos computacionais compactar e extrair o estado da instância. Na maioria dos casos, os passa de compactação aumentaram o desempenho.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceCompletionAction%2A>  
 Este parâmetro instrui <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> a mantém ou exclui instâncias concluídas. Manter instâncias concluídas aumenta os requisitos de armazenamento de base de dados de persistência e condu-los para tabelas maiores, o que aumenta tempo de pesquisa de tabela. A menos que as instâncias concluídas são necessárias depuração ou auditando, é melhor instruir <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> para excluir instâncias concluídas. As instâncias excluídas devem ser mantidas somente se o usuário estabelece um processo para eventualmente as remover. Observe que as chaves de correlação não podem ser reutilizadas como a instância concluída de fluxo de trabalho reside no armazenamento de instância.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>  
 Este parâmetro define o máximo intervalo com que <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> sonda o base de dados de persistência para as instâncias que devem ser carregadas quando uma atividade de <xref:System.Activities.Statements.Delay> expira. Se <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> encontrar um timer que expirou no intervalo de pesquisa seguir, diminuirá o intervalo de pesquisa de modo que a votação seguir ocorre direita após o timer expirou. Essa maneira, a instância Store de fluxo de trabalho do SQL obtém uma alta precisão de temporizadores que executam mais tempo de <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>.  
  
 Não recomendamos reduzir <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A>, porque isso resulta em uma carga na base de dados de persistência. Cada host serviço que usa <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> sonda o base de dados uma vez por período de detecção. A configuração <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.RunnableInstancesDetectionPeriod%2A> a um intervalo muito pequeno pode fazer com que o desempenho do sistema diminui se o número de host serviço é grande.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.HostLockRenewalPeriod%2A>  
 Este parâmetro define o intervalo com que o host renova o bloqueio na base de dados de persistência. Reduzir esse intervalo permitirá uma recuperação mais rápido de instâncias de fluxo de trabalho no caso de um host ou um computador falhará. Por outro lado, um período curta de renovação de bloqueio aumenta a carga na base de dados de persistência. Cada host serviço que usa <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> atualizará os bloqueios na base de dados uma vez por período de renovação. Se um computador executa muitos host serviço, certifique-se de que a carga causada pela renovação de bloqueio não reduz o desempenho do sistema. Se fizer isso, para ver aumentar <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.HostLockRenewalPeriod%2A>.  
  
 <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A>  
 Se ativado, <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> tentar de volta para carregar uma instância bloqueado para os próximos 30 segundos. Definir <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A> a BasicRetry ou a AggressiveRetry se o fluxo de trabalho recebe mais mensagens em um curto período de tempo, e essas mensagens são recebidas por diferentes computadores.  
  
 Porque o mecanismo do tentativa de carregamento não apresenta nenhuma sobrecarga de desempenho como novas tentativas de carregamento não são tentadas, <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore.InstanceLockedExceptionAction%2A> deve sempre ser ativado.
