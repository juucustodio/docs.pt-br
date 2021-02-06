---
description: 'Saiba mais sobre: ativação de instância'
title: Ativação de instância
ms.date: 03/30/2017
ms.assetid: 134c3f70-5d4e-46d0-9d49-469a6643edd8
ms.openlocfilehash: a301f49fb79e7c74cd3a64e891526e5b89fdd1c6
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99631197"
---
# <a name="instance-activation"></a>Ativação de instância

A instância Store de fluxo de trabalho do SQL executa uma tarefa periodicamente interna que acorde e detecte instâncias praticáveis ou activatable de fluxo de trabalho na base de dados de persistência. Se encontra uma instância viável de fluxo de trabalho, notifica o host de fluxo de trabalho que é capaz de ativar a instância. Se o armazenamento de instância encontra uma instância activatable de fluxo de trabalho, notifica um host genérico que ative um host de fluxo de trabalho, que executa por sua vez a instância de fluxo de trabalho. As seções neste tópico explica o processo de ativação de instância em detalhes.  
  
## <a name="detecting-and-activating-runnable-workflow-instances"></a><a name="RunnableSection"></a> Detectando e ativando instâncias de fluxo de trabalho executáveis  

 O armazenamento da instância do fluxo de trabalho SQL considera uma instância de fluxo de trabalho *executável* se a instância não estiver no estado suspenso ou no estado concluído e atender às seguintes condições:  
  
- A instância é desbloqueada e tem um timer pendente que expirou.  
  
- A instância tem um bloqueio expirado nele.  
  
- A instância está desbloqueada e seu status é em **execução**.  
  
 A instância Store de fluxo de trabalho do SQL aumenta <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> quando encontra uma instância viável. Após isso, o SqlWorkflowInstanceStore para monitorar de <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand> até que seja chamado uma vez no armazenamento.  
  
 Um host de fluxo de trabalho que assine para <xref:System.Activities.DurableInstancing.HasRunnableWorkflowEvent> e capaz de carregar a instância executa <xref:System.Activities.DurableInstancing.TryLoadRunnableWorkflowCommand> contra o armazenamento de instância para carregar a instância na memória. Um host de fluxo de trabalho é considerado capaz de carregar uma instância de fluxo de trabalho se o host e a instância têm a propriedade de metadados **WorkflowServiceType** definida com o mesmo valor.  
  
## <a name="detecting-and-activating-activatable-workflow-instances"></a>Detectando e ativando instâncias de fluxo de trabalho de Activatable  

 Uma instância de fluxo de trabalho será considerada *ativável* se a instância for executável e não houver nenhum host de fluxo de trabalho capaz de carregar a instância está em execução no computador. Consulte detectar e ativar instâncias praticáveis de fluxo de trabalho anterior para a definição de uma instância viável de fluxo de trabalho.  
  
 A instância Store de fluxo de trabalho do SQL aumenta <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent> quando encontra uma instância activatable de fluxo de trabalho na base de dados. Após isso, o SqlWorkflowInstanceStore para monitorar de <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand> até que seja chamado uma vez no armazenamento.  
  
 Quando um host genérico que assine para <xref:System.Activities.DurableInstancing.HasActivatableWorkflowEvent> recebe o evento, executa <xref:System.Activities.DurableInstancing.QueryActivatableWorkflowsCommand> contra o armazenamento de instância para obter os parâmetros de ativação necessários para criar um host de fluxo de trabalho. O host genérico usa esses parâmetros de ativação para criar um host de fluxo de trabalho, que por sua vez as carrega e as executa o serviço viável ouvinte como um exemplo.  
  
## <a name="generic-hosts"></a>Hosts genéricos  

 Um host genérico é um host com o valor da propriedade de metadados **WorkflowServiceType** para hosts genéricos é definido como **WorkflowServiceType. any** para indicar que ele pode lidar com qualquer tipo de fluxo de trabalho. Um host genérico tem um parâmetro XName chamado **ActivationType**.  
  
 Atualmente, o armazenamento da instância do fluxo de trabalho SQL oferece suporte a hosts genéricos com o valor do parâmetro ActivationType definido como **was**. Se o ActivationType não é definido como WAS, a instância de fluxo de trabalho do SQL gerencie <xref:System.Runtime.DurableInstancing.InstancePersistenceException>Store. O serviço de gerenciamento de fluxo de trabalho fornecido com os recursos de hospedagem do Windows Server AppFabric é um host genérico que tem o tipo de ativação definido como **was**.  
  
 Para WAS ativação, um host genérico requer um conjunto de parâmetros de ativação derivar o endereço do ponto de extremidade em que os novos host podem ser ativados. Os parâmetros de ativação para ativação do WAS são nome do site, caminho relativo para o aplicativo ao site, e caminho para o serviço relativo para o aplicativo. A instância Store de fluxo de trabalho do SQL armazena esses parâmetros de ativação durante a execução de <xref:System.Activities.DurableInstancing.SaveWorkflowCommand>.  
  
## <a name="runnable-instances-detection-period"></a>Período viável de detecção de instâncias  

 A propriedade **período de detecção de instâncias executáveis** do repositório da instância do fluxo de trabalho SQL especifica o período após o qual o armazenamento da instância do fluxo de trabalho SQL executa uma tarefa de detecção para detectar qualquer instância de fluxo de trabalho executável ou ativável no banco de dados de persistência após o ciclo de detecção anterior. Consulte [período de detecção de instâncias executáveis](runnable-instances-detection-period.md) para obter mais detalhes sobre essa propriedade.
