---
title: Persistência de fluxo de trabalho
description: .NET Framework 4.6.1 inclui a classe SqlWorkflowInstanceStore, que permite a persistência de dados de fluxo de trabalho e metadados em um banco de SQL Server.
ms.date: 03/30/2017
helpviewer_keywords:
- programming [WF], persistence
ms.assetid: 39e69d1f-b771-4c16-9e18-696fa43b65b2
ms.openlocfilehash: 2184a159423a611a8936e900591a480ce7ef6ec8
ms.sourcegitcommit: bc293b14af795e0e999e3304dd40c0222cf2ffe4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "96293800"
---
# <a name="workflow-persistence"></a>Persistência de fluxo de trabalho

Persistência de fluxo de trabalho é a captura durável do estado de uma instância de fluxo de trabalho, independente de processo ou de informações do computador. Isso é feito para fornecer um ponto conhecido de recuperação para a instância de fluxo de trabalho no caso de falha do sistema, ou para preservar a memória descarregando as instâncias de fluxo de trabalho que não estão fazendo ativamente o trabalho, ou para mover o estado da instância de fluxo de trabalho de um nó para outro nó em um farm de servidores.  
  
 Persistência permite a agilidade do processo, a escalabilidade, a recuperação face falhar, e a capacidade gerenciar mais eficientemente a memória. O processo de persistência inclui a identificação de um ponto de persistência, a coleta de dados a ser salvos, e finalmente a delegação de armazenamento real de dados a um provedor de persistência.  
  
 Para habilitar a persistência de um fluxo de trabalho, você precisa associar um repositório de instância com **WorkflowApplication** ou **WorkflowServiceHost** , conforme mencionado em [como habilitar a persistência para fluxos de trabalho e serviços de fluxo de trabalho](how-to-enable-persistence-for-workflows-and-workflow-services.md). O **WorkflowApplication** e o **WorkflowServiceHost** usam o repositório de instância associado a eles para permitir a persistência de instâncias de fluxo de trabalho em um repositório de persistência e o carregamento de instâncias de fluxo de trabalho na memória com base nos dados de instância de fluxo de trabalho armazenados no repositório de persistência.  
  
 O [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] é fornecido com a classe **SqlWorkflowInstanceStore** , que permite a persistência de dados e metadados sobre instâncias de fluxo de trabalho em um SQL Server 2005 ou SQL Server 2008. Consulte [repositório de instância de fluxo de trabalho SQL](sql-workflow-instance-store.md) para obter mais detalhes.  
  
 Para armazenar e carregar os dados específicos do aplicativo junto com informações relacionadas instância de fluxo de trabalho, você pode criar os participantes de persistência que estendem a classe de <xref:System.Activities.Persistence.PersistenceParticipant> . Um participante de persistência participa no processo de persistência para salvar dados serializados personalizados no armazenamento de persistência, para carregar os dados da instância na memória, e executar qualquer lógica adicional em uma transação de persistência. Para obter mais informações, consulte [participantes da persistência](persistence-participants.md).  
  
 A tela de aplicativo Windows Server simplifica o processo de configurar a persistência. Para obter mais informações, consulte [conceitos de persistência com o Windows Server app Fabric](/previous-versions/appfabric/ee677272(v=azure.10))  
  
## <a name="implicit-persistence-points"></a>Pontos implícitos de persistência  

 A lista a seguir contém exemplos das circunstâncias na qual um fluxo de trabalho é mantido quando um armazenamento de instância é associado com um fluxo de trabalho.  
  
- Quando uma atividade **TransactionScope** é concluída ou uma atividade **TransactedReceiveScope** é concluída.  
  
- Quando uma instância de fluxo de trabalho se torna ociosa e o **WorkflowIdleBehavior** é definido no host do fluxo de trabalho. Isso ocorre, por exemplo, quando você usa atividades de mensagens ou uma atividade de **atraso** .  
  
- Quando um WorkflowApplication se torna ocioso e a propriedade **PersistableIdle** do aplicativo é definida como **PersistableIdleAction. Persist**.  
  
- Quando um aplicativo host seja instruído para persistir ou descarregar uma instância de fluxo de trabalho.  
  
- Quando uma instância de fluxo de trabalho seja finalizada ou termina.  
  
- Quando uma atividade de **persistência** é executada.  
  
- Quando uma instância de um fluxo de trabalho desenvolvido usando uma versão anterior do Windows Workflow Foundation localizar um ponto de persistência durante a execução interoperável.  
  
## <a name="in-this-section"></a>Nesta seção  
  
- [Store instância de fluxo de trabalho do SQL](sql-workflow-instance-store.md)  
  
- [Armazenamentos de instância](instance-stores.md)  
  
- [Participantes de persistência](persistence-participants.md)  
  
- [Práticas recomendadas de persistência](persistence-best-practices.md)  
  
- [Instâncias são persistentes de fluxo de trabalho](non-persisted-workflow-instances.md)  
  
- [Pausando e continuando um fluxo de trabalho](pausing-and-resuming-a-workflow.md)
