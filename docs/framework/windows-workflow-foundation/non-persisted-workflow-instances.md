---
description: 'Saiba mais sobre: instâncias de fluxo de trabalho não persistentes'
title: Instâncias são persistentes de fluxo de trabalho
ms.date: 03/30/2017
ms.assetid: 5e01af77-6b14-4964-91a5-7dfd143449c0
ms.openlocfilehash: 0ee5968426a6bb800b9e70ac592c6da191c22511
ms.sourcegitcommit: ddf7edb67715a5b9a45e3dd44536dabc153c1de0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/06/2021
ms.locfileid: "99787897"
---
# <a name="non-persisted-workflow-instances"></a>Instâncias são persistentes de fluxo de trabalho

Quando uma nova instância de um fluxo de trabalho é criada que persiste seu estado em <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore>, o host serviço cria uma entrada para o serviço no armazenamento de instância. Posteriormente, quando a instância do fluxo de trabalho é mantida pela primeira vez, <xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> armazena o estado atual da instância. Se o fluxo de trabalho é hospedado no serviço de ativação de processo do Windows, os dados de implantação de serviço são gravados também para o armazenamento de instância quando a instância é mantida pela primeira vez.

Desde que a instância do fluxo de trabalho não tenha sido persistida, ela está em um estado **não persistente** . Quando nesse estado, a instância de fluxo de trabalho não pode ser recuperada após um domínio de aplicativo se recicla, falha do host, ou falha do computador.

## <a name="the-non-persisted-state"></a>O estado não persistente

As instâncias duráveis de fluxo de trabalho que não foram persistentes permanecem em um estado não mantido nos seguintes casos:

- Falhas de host serviço antes de instância de fluxo de trabalho são mantidas pela primeira vez. O de instância de fluxo de trabalho na instância armazenam e não são recuperadas. Se uma mensagem correlacionada chega, a instância de fluxo de trabalho se torna ativa novamente.

- A instância de fluxo de trabalho apresenta uma exceção antes de ser mantidas pela primeira vez. Como <xref:System.Activities.UnhandledExceptionAction> retornado, os seguintes cenários ocorrem:

  - <xref:System.Activities.UnhandledExceptionAction> é definido como <xref:System.Activities.UnhandledExceptionAction.Abort>: Quando ocorre uma exceção, informações de implantação de serviço é escrita para o armazenamento de instância, e a instância de fluxo de trabalho é descarregada de memória. O de instância de fluxo de trabalho em um estado não persistido e não podem ser recarregadas.

  - <xref:System.Activities.UnhandledExceptionAction> é definido como <xref:System.Activities.UnhandledExceptionAction.Cancel> ou a <xref:System.Activities.UnhandledExceptionAction.Terminate>: Quando ocorre uma exceção, informações de implantação de serviço é escrita para o armazenamento de instância, e o estado da instância da atividade é definido como <xref:System.Activities.ActivityInstanceState.Closed>.

Para minimizar o risco de localizar instâncias são persistentes descarregadas de fluxo de trabalho, recomendamos persistir o fluxo de trabalho no início em seu ciclo de vida.

## <a name="detection-and-removal-of-non-persisted-instances"></a>Detecção e remoção de instâncias são persistentes

<xref:System.Activities.DurableInstancing.SqlWorkflowInstanceStore> não remove quaisquer instâncias são mantidas de fluxo de trabalho da instância. Também não remove quaisquer proprietários expiradas de bloqueio que não persistiram as instâncias de fluxo de trabalho associados com eles.

Recomendamos que o administrador verifica periodicamente o armazenamento de instância para instâncias são persistentes. Os administradores podem remover essas instâncias da instância como sabem que esse fluxo de trabalho não receberá mensagens correlacionadas. Por exemplo, se a instância foi na base de dados por vários meses e se souber que o fluxo de trabalho normalmente tem um tempo de vida de vários dias, seria seguro suponha que isso foi inicializada uma instância que falhasse.

Para localizar ocorrências são mantidas na instância Store de fluxo de trabalho do SQL você pode usar as seguintes consultas SQL:

- Esta consulta localiza todas as instâncias que não foram persistentes, e retorna a hora de identificação e de criação (armazenados na hora UTC) para eles.

  ```sql
  select InstanceId, CreationTime
      from [System.Activities.DurableInstancing].[Instances]
      where IsInitialized = 0
  ```

- Esta consulta localiza todas as instâncias que não foram persistentes, e não é carregado, e retorna a hora de identificação e de criação (armazenados na hora UTC) para eles.

  ```sql
  select InstanceId, CreationTime
      from [System.Activities.DurableInstancing].[Instances]
      where IsInitialized = 0
          and CurrentMachine is NULL
  ```

- Esta consulta localiza todas as instâncias suspensas que não foram persistentes, e retorna a identificação, o tempo de criação (armazenados na hora UTC), a razão de suspensão, e o nome da exceção para eles.

  ```sql
  select InstanceId, CreationTime, SuspensionReason, SuspensionExceptionName
      from [System.Activities.DurableInstancing].[Instances]
      where IsInitialized = 0
          and IsSuspended = 1
  ```

Use cuidado quando você estiver excluindo instâncias são persistentes. Geralmente, é seguro remover instâncias são persistentes criadas por <xref:System.ServiceModel.Activities.WorkflowServiceHost> que são suspensas ou não carregadas. Essas instâncias específicas podem ser excluídas de armazenamento excluindo os do modo de `[System.Activities.DurableInstancing].[Instances]` usando o seguinte comando SQL, substituindo a identificação correta de instância

```sql
delete [System.Activities.DurableInstancing].[Instances]
    where InstanceId=’078a9bc4-ada5-4f9e-8cce-b0eb0009995f’
```

> [!WARNING]
> Não recomendamos remover todas as instâncias são persistentes porque isso inclui instâncias que foram criados e apenas para ter sido persistente ainda não.
